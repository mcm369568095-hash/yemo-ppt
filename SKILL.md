---
name: 夜秣PPT工坊
description: >
  商业化 AI 演示文稿定制：给一个标题，服务端出品可编辑 PPTX（17 种设计风格、20 种版式、配图全包）。
  付费方式：支付宝 AI 付按次结算，9.90 元/册，首次需在支付宝开通一次「AI 付」钱包授权（以后自动扣）；
  调用本技能前必须跑 `scripts/pay_generate.py quote → pay → prove`，**未经确认不发起真实付款**。
  当用户说「做个PPT」「把这份材料做成PPT」「某某主题的演示文稿」「夜秣PPT工坊」「按风格出一套PPT」时触发。
description_zh: "商业化 AI 演示文稿定制工坊，输入标题即可出品可编辑 PPTX（17 种设计风格，9.90 元按次计费，首用需在支付宝开通一次 AI 付）"
description_en: "Commercial AI presentation studio - one title in, an editable PPTX out, billed per deck. Alipay AI Pay one-time wallet authorization required for first use."
version: 1.2.10
slug: yemo-ppt
displayName: 夜秣PPT工坊（可编辑PPT生成）
author: 夜秣
---

# 夜秣PPT工坊 · 商业化 AI 演示文稿定制

> 输入一个标题（可选：自带内容 / 指定风格 / 听众 / 大纲），**服务端**完成生图、抠图、组装，返回可编辑 `.pptx`。
> 出图走作者服务端代持网关，费用已含在单次出品价里，每套最多 13 页。客户端零密钥、零本地生图脚本。

---

## 🧾 产品定位与计费（先看这里）

| 项目 | 说明 |
|---|---|
| **出品方** | 夜秣（作者） |
| **客户需要准备** | 一个标题（+ 可选：自带内容 / 指定风格 / 听众 / 大纲） |
| **生图费用** | **作者承担**（服务端内置网关 Key，客户无需自备任何 API） |
| **客户付费方式** | **按出品次数付费**：跑 `scripts/pay_generate.py`，经支付宝 AI 付结算，**9.90 元 / 册** |
| **交付物** | 可编辑 `.pptx`（背景可换、插图可编辑、文字全可改）+ 可选 交付清单图 |
| **付费前必做** | 先 `quote` 拿账单、再 `pay` 生成支付入口、付款后 `prove` 取回成品 |

> **没有「本地免费自产」路径**：本技能发布的只有付费客户端，生图 / 抠图 / 组装全部在作者服务端完成，
> 客户端不携带任何生图脚本或密钥，无法离线白嫖。要拿到成品，必须走付费链路。

---

## 💳 付费出品（A2M 402）· 调用线上接口

| 项 | 值 |
|---|---|
| 资源 URL | `https://api.yemo.xyz/api/ppt/generate` |
| 请求方式 | `GET`（参数拼 query）或 `POST`（JSON body） |
| 输入 | `topic`（必填）、`style`、`pages`、`audience`、`outline` |
| 单价 | **9.90 元 / 册**（与服务市场登记单价一致） |
| 依赖 | 仅 Python 标准库；无需 SDK、无需密钥 |
| 付款入口依赖 | 买家侧官方支付 CLI `alipay-bot`（装法见下） |
| 协议依据 | 支付宝官方 A2M 402 契约 |

> **服务端是谁的、能不能换**：`api.yemo.xyz` 是作者已部署的商家服务端（出账单、验付、出品、交付），
> 装完即用，无需自建。

完整字段与响应结构见 `references/pay-a2m-contract.md`。

### 四步调用（脚本：`scripts/pay_generate.py`）

```bash
PY="python"          # 你环境中的 Python 3 解释器
SKILL="."            # 技能根目录（在技能目录内运行即可）

# ① 出账：拿 402 账单，停在你付款确认前（默认动作，绝不自动付款）
"$PY" "$SKILL/scripts/pay_generate.py" quote --topic "开学第一课" --style "儿童手绘" --pages 12

# ② 生成支付入口（二维码 + 付款链接），交给用户扫码
"$PY" "$SKILL/scripts/pay_generate.py" pay --state-file .pay-state.json

# ③ 付款后带凭证取回成品（同一个订单号，不重新下单）
"$PY" "$SKILL/scripts/pay_generate.py" prove --proof "<Payment-Proof>"

# ④ 状态不明时先查单（先查资源，再用同一凭证幂等重试）
"$PY" "$SKILL/scripts/pay_generate.py" status --proof "<Payment-Proof>"
```

> 🔴 **402 账单里没有付款链接，也没有二维码。** 账单只是「报价单」，
> 支付入口必须用买家侧官方 CLI 生成（`pay` 子命令已封装该步骤）：
> ```bash
> npx -y @alipay/agent-payment@latest install   # 装出 alipay-bot
> ```
> 装完若 `alipay-bot` 不在 PATH，脚本会自动去找；找不到就用 `--bot <完整路径>` 指定。

> 🔴🔴 **第 0 步（一次性）：先开通钱包，再谈付款。**
> 支付宝 AI 付是**一个智能体环境绑一个支付宝账号**。没开通就跑 `pay`，
> 扫出来的不是收银台而是「开通/绑定页」；拿一个已经在别处开通过 AI 付的账号去扫，
> 支付宝 App 会提示**「请勿重复绑定」**。
> ```bash
> "$PY" "$SKILL/scripts/pay_generate.py" wallet check          # 看状态：ready / pending / none
> "$PY" "$SKILL/scripts/pay_generate.py" wallet apply          # none 时：出开通码，扫码拿 6 位授权码
> "$PY" "$SKILL/scripts/pay_generate.py" wallet bind --code 123456
> ```
> **谁扫 apply 的码，谁就是这台机器以后的固定付款账号**（换人要先 `wallet close` 解绑）。
> `pay` 默认自带这道门禁，确认已绑好时可加 `--skip-wallet-check` 跳过。

> 🔴 **作者自测限制：买家和卖家不能是同一个支付宝账号。**
> 收款账号（商家 PID）与付款账号是同一个时，支付宝直接拒绝出支付入口。
> 这不是故障：**作者自己在本机永远付不了自己的商品**。真实客户不受影响——客户用自己的号买，与商家收款号天然不同。

### 铁律（照做，别自创）

**职责分工**：账单签名、服务端验付（`payment.verify`）、商家履约确认（`fulfillment.confirm`）
由商家服务端（api.yemo.xyz）实现；本技能脚本只做客户端编排——发请求、解析 402 账单、
状态持久化、携凭证重试；付款始终走支付宝官方收银流程。

1. **复用同一订单。** `out_trade_no` 从 402 账单里拿，之后全程复用；付款后重试的是**同一个 URL + 同一份参数**，只多带一个 `Payment-Proof` 头。
2. **状态不明先查单。** 5xx/超时/履约确认失败 → 先 `status` 查单，再用**同一凭证**重试，不重新付款、不重复出品。
3. **成功路径不追加独立回执。** 商家履约确认由服务端在返回资源时完成，买家回执由官方支付能力发送。
4. **未确认不付款。** 生产环境脚本只停在付款确认前；没有明确的人工确认，不发起真实付款。

### 支付链路自查项

| 自查项 | 本技能实现 |
|---|---|
| **402 账单** | 未付款时服务端返回 HTTP **402** + `Payment-Needed` 响应头（Base64URL 账单） |
| **支付入口** | `pay` 子命令调买家侧官方 CLI `alipay-bot 402-buyer-pay`，生成付款链接与二维码；账单本身不含任何链接 |
| **钱包开通** | `wallet` 子命令封装 check/apply/bind/close 三步；`pay` 前自动门禁，未开通不出付款码 |
| **凭证重试** | 付款后携 `Payment-Proof` 请求头重试；原始请求参数由状态文件保存，**原样重放、保持一致**，不重新下单 |
| **服务端验付** | 商家服务端验付（payment.verify）凭证与订单；无效或过期凭证不交付资源，返回 402 |
| **商家履约** | 服务端返回资源时同步发送履约确认（fulfillment.confirm）；确认失败可重试，同凭证重试不重新扣费 |
| **订单与幂等** | 订单状态持久化于 `.pay-state.json`，全程复用同一 `out_trade_no`；服务端按订单幂等，**不重复扣费、不重复出品** |

### 交付后展示给客户的六项

标题 / 风格 / 页数 / 文件名 / 下载链接 `download_path` / 订单号 `out_trade_no`
（`sha256` 与 `size_bytes` 作为交付凭证一并给出）。

---

### 🖼 配图：9.90 元已包含，客户不需要任何账号

| 项 | 说明 |
|---|---|
| **谁出图** | 商家服务端代出图并写入 PPT，客户全程不接触生图网关与密钥 |
| **客户要准备什么** | 什么都不用。不需要申请网关、不需要填 key、不需要装 Pillow / python-pptx |
| **页数上限** | **每套最多 13 页**（含封面与结尾页）。客户要 30 页也按 13 页出，成本锁死不失控 |
| **交付节奏** | 付款后**秒级**先返回一份完整可编辑的 PPT；配图在后台并发生成，完成后自动覆盖同一文件 |
| **查配图进度** | `GET https://api.yemo.xyz/api/ppt/images/<out_trade_no>` → `state: running / done / failed`，附 `done/total` |
| **出图失败** | 不影响交付：客户至少拿到一份完整可用的 PPT，不会空手，也不会重复扣费 |

命令行取进度：

```bash
"$PY" "$SKILL/scripts/pay_generate.py" images --out-trade-no "<out_trade_no>"
# 或加 --wait 阻塞等到配图完成（默认每 10 秒查一次，最多等 10 分钟）
"$PY" "$SKILL/scripts/pay_generate.py" images --out-trade-no "<out_trade_no>" --wait
```

配图完成后再下载，拿到的就是带图成品：
`GET https://api.yemo.xyz/api/ppt/download/<out_trade_no>`

---

## 🎨 17 种设计风格

瑞士国际主义 / 深海蓝金 / 极简黑白 / 编辑杂志 / Bento 网格 / 玻璃拟态 /
暗色科技 / 极光霓虹 / 建筑蓝图 / 学术深蓝 / 黏土3D / 复古波普 / 孟菲斯 / 国潮 / 有机自然 /
大字报 / 儿童手绘，外加 1 个「自定义风格」填空位。各风格示例见 `references/style_gallery.md`。

---

## 🧩 安装 · 运行 · 打包

| 动作 | 怎么做 |
|---|---|
| **安装** | 把本目录整个放进 `~/.workbuddy/skills/夜秣PPT工坊`（用户级）或 `<项目>/.workbuddy/skills/`（项目级）；无需 pip 安装任何包 |
| **本地加载** | WorkBuddy 重启后自动加载；触发词写在 SKILL.md 的 `description` 里，命中即启用 |
| **付款入口前置** | 首次付款前装一次买家侧官方 CLI：`npx -y @alipay/agent-payment@latest install`（装出 `alipay-bot`）。没装则 `pay` 命令会明确报错并给出安装命令 |
| **运行（付费）** | `python scripts/pay_generate.py quote --topic "..."` → `... pay` 生成支付入口 → `... prove`（标准库即可） |
| **打包** | `python scripts/package_skill.py` → `dist/夜秣PPT工坊-<version>.zip`（仅含付费客户端，自动排除本地自产脚本） |

> ✅ **出图密钥由商家服务端代持**（落盘权限 600，永不下发给调用方），技能包内不含任何密钥。
> 买家**无需申请生图网关、无需填写任何 key** —— 装完即用，9.90 元已包含全部配图费用。
> 本技能**不含任何本地生图 / 组装脚本**，成品一律由服务端出品。

---

## ❓ 常见问题

- **Q：能不能在自己电脑上免费生成？** A：不能。发布包只含付费客户端，生图 / 抠图 / 组装都在服务端完成，客户端无相关脚本与密钥，必须走付费链路。
- **Q：作者能自己付钱测试吗？** A：不能。买家与卖家不能是同一支付宝账号，作者自测需用第三方账号绑钱包。真实客户用自己的号买，天然无此限制。
- **Q：付了钱一直不出图怎么办？** A：先 `images --out-trade-no <单号> --wait` 查进度；仍失败用 `status --proof <凭证>` 查单，再用同一凭证重试，不会重复扣费。
- **Q：要 30 页能出吗？** A：单套硬上限 13 页。超出请分多套下单。

> 服务端内部生产规范、版式铁律、文案纯净度流程等作者内部文档见 `LOCAL_DEV.md`（不随技能发布）。
