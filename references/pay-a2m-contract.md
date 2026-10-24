# 夜秣PPT工坊 · 按量付费（A2M 402）调用契约

> 本文件是「调用方（Agent / 客户端）」视角的契约说明。
> 协议依据：本机安装的支付宝官方技能 `alipay-aipay`
> （`references/integration/modules/interface-contract/aipay-interface-contract.md`）。
> 本文件只做本地化转写，**不改动协议本身**；协议以官方文档为准。

## 1. 三个角色

| 角色 | 是谁 | 干什么 |
|---|---|---|
| 商家服务端 | `https://api.yemo.xyz`（FastAPI + uvicorn） | 出 402 账单、验付、出品 PPTX、履约确认 |
| 支付宝 | `alipay.aipay.agent.payment.verify` / `fulfillment.confirm` | 验凭证、记履约 |
| 调用方 | 本技能 `scripts/pay_generate.py` | 发请求、读账单、带凭证重试、校验交付 |

**职责分工**：账单签名、验付（payment.verify）与商家履约确认（fulfillment.confirm）由商家服务端完成；
调用方只做客户端编排（发请求、读账单、状态持久化、携凭证重试），付款由支付宝官方收银流程完成。

## 2. 资源与价格

| 项 | 值 |
|---|---|
| 资源 URL | `https://api.yemo.xyz/api/ppt/generate` |
| 请求方式 | `GET`（参数拼 query）或 `POST`（JSON body），服务端合并两者 |
| 单价 | **9.90 元 / 次**（一册 = 一次，与服务市场登记单价一致） |
| 商品名 | 夜秣PPT工坊 · 单套演示文稿出品 |
| service_id | `API_XXXXXXXXXXXXXXXX（PPT 服务号）` |
| seller_id | `2088XXXXXXXXXXXX（你的商户 PID）` |
| seller_app_id | `2021XXXXXXXXXXXX（你的 AppID）` |
| 币种 | CNY |
| 支付截止 | 账单 `pay_before`，出单后 30 分钟 |

## 3. 请求参数

服务端把 GET query 与 POST JSON body 合并成一个 `params` 字典，交给出品引擎。已支持字段：

| 字段 | 类型 | 说明 | 默认 |
|---|---|---|---|
| `topic` | string | 演示文稿标题 / 主题（必填） | 无，必填 |
| `style` | string | 风格名，见 `references/style_gallery.md` 与 `/api/ppt/styles` | `儿童手绘` |
| `pages` | int | 目标页数（含封面结尾） | 由内容决定，5–30 |
| `outline` | string 或 array | 自带大纲 / 稿件，走「客户自带稿件」路径 | 无 |
| `audience` | string | 听众 / 场景（投资人 / 学生 / 家长…） | 通用听众 |

未知字段服务端忽略，**不会报错**。

请求头：

- 首次请求：**不带** `Payment-Proof`。
- 重试请求：带 `Payment-Proof: <base64url JSON>`（值与官方脚本生成的完全一致）。

## 4. 响应一：HTTP 402（需要付款）

响应头：

```
Payment-Needed: <base64url(JSON)>
```

解码后结构（字段与官方契约一致）：

```json
{
  "protocol": {
    "out_trade_no": "YEMO...",
    "amount": "9.90",
    "currency": "CNY",
    "resource_id": "/api/ppt/generate",
    "pay_before": "2026-09-23T20:30:00+08:00",
    "seller_signature": "...",
    "seller_sign_type": "RSA2",
    "seller_unique_id": "2088XXXXXXXXXXXX（你的商户 PID）"
  },
  "method": {
    "seller_name": "夜秣PPT工坊",
    "seller_id": "2088XXXXXXXXXXXX（你的商户 PID）",
    "seller_app_id": "2021XXXXXXXXXXXX（你的 AppID）",
    "goods_name": "夜秣PPT工坊 · 单套演示文稿出品",
    "seller_unique_id_key": "seller_id",
    "service_id": "API_XXXXXXXXXXXXXXXX（PPT 服务号）"
  }
}
```

响应体（**只用于调试，支付依据是响应头**）：

```json
{ "code": "Payment-Needed", "out_trade_no": "YEMO...", "amount": "9.9", "currency": "CNY", "goods_name": "..." }
```

## 5. 付款（不做自研）

- **沙箱**：调用官方技能自带脚本
  `references/integration/modules/scripts/local_402_sandbox_pay.py`（`run --auto-complete`），
  它负责收银下单、生成 `payScheme`、构造 `Payment-Proof` 头、带凭证重试。
  沙箱要求服务端 `method.service_id == api_mock_service_id`（由服务端配置切换，不由调用方改）。
- **生产**：调用方**只停在付款确认前**，把账单摘要与付款链接交给人确认；
  未经明确确认，不得发起真实付款。

## 6. 响应二：HTTP 200（交付成功）

响应头：

```
Payment-Validation: <base64url(JSON)>
```

```json
{ "trade_no": "...", "out_trade_no": "YEMO...", "validated": true, "resource_id": "/api/ppt/generate" }
```

响应体：

```json
{
  "resource_id": "/api/ppt/generate",
  "content": {
    "title": "开学第一课",
    "style": "儿童手绘",
    "slide_count": 12,
    "file_name": "YEMO....pptx",
    "file_path": "/opt/yemo-ppt-api/outputs/YEMO....pptx",
    "size_bytes": 123456,
    "sha256": "...",
    "out_trade_no": "YEMO...",
    "download_path": "/api/ppt/download/YEMO...",
    "resource_id": "/api/ppt/generate",
    "goods_name": "夜秣PPT工坊 · 单套演示文稿出品",
    "brand": "夜秣PPT工坊",
    "generated_at": "2026-09-23T20:05:00+08:00"
  },
  "trade_no": "...",
  "out_trade_no": "YEMO...",
  "already_fulfilled": false,
  "fulfillment_confirmed": true
}
```

**展示字段**（给用户看的就这六项）：标题、风格、页数、文件名、下载链接 `download_path`、
订单号 `out_trade_no`。`sha256` / `size_bytes` 作为交付凭证一并展示。

调用方必须校验：

1. HTTP 200；
2. 响应体 `content` 非空且含 `resource_id`；
3. `Payment-Validation.validated == true`；
4. `Payment-Validation.resource_id` 与响应体 `resource_id` 一致；
5. 响应体 `out_trade_no` 与本次账单的 `out_trade_no` 一致（防串单）。

**成功路径不追加独立回执**——履约确认由服务端完成，调用方不再调 `fulfillment.confirm`。

## 7. 失败与异常

| 场景 | 表现 | 调用方动作 |
|---|---|---|
| 验付未通过 | 再次 402（message 含「验付未通过」） | 视为需重新付款，不交付 |
| 验付接口异常 | 500 `VERIFY_FAILED` | 状态不明 → 先查单，再决定是否重试 |
| 履约确认失败 | 502 `FULFILLMENT_CONFIRM_FAILED` | **用同一 Payment-Proof 重试**，不重新付款 |
| 网络中断 / 5xx | 无响应 | 状态不明 → 先查单 |
| 已履约再来同一凭证 | 200 + `already_fulfilled=true` | 直接复用上次结果，**不重复出品** |

### 状态不明时先查单

两条查单路径，按顺序用：

1. **资源查单**：`GET /api/ppt/download/{out_trade_no}` —— 200 说明已出品，直接下载；
   404 说明还没交付。
2. **同凭证重试**：带**同一个** `Payment-Proof` 再请求一次资源接口。
   服务端幂等：已 `FULFILLED` 会返回 `already_fulfilled=true` 与上次结果，不会二次扣费、不会重复出品。

只有在查单确认「未支付 / 未履约」时，才回到 402 让用户重新付款。

## 8. 幂等与复用同一订单

- 一次出品 = 一个 `out_trade_no`，从 402 账单里拿，之后全程复用，**不重新生成订单号**；
- 付款后重试的是**同一个 URL、同一份业务参数**，只多带一个 `Payment-Proof` 头；
- 重试只换凭证，不换订单、不换参数；
- 服务端以 `trade_no` 防重复履约。
