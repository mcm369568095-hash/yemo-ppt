# 风格画廊 · 夜秣PPT工坊

> 给客户挑风格用的一页纸。技术定义在 `scripts/styles.json`，brief 里写 `"style": "<key>"` 即可整册套用。
> 本文件由配色库自动生成，改配色请改 `styles.json` 后重新生成，不要手改本表。

## 速查表

| key | 风格 | 气质 | 最适合 | 主题 |
|---|---|---|---|---|
| `kids_hand` | 儿童手绘（原厂） | 明亮童趣、夸张表情、蜡笔质感 | 主题班会 / 幼小教育 / 校园活动 / 安全科普 | 浅色 |
| `swiss` | 瑞士国际主义 | 理性克制、严格网格、一抹红 | 咨询报告 / 金融分析 / 董事汇报 / 数据陈述 | 浅色 |
| `navy_gold` | 深海蓝金 | 高端、稳重、金色点缀 | 融资计划书 / 年度总结 / 高管汇报 / 品牌发布 | 暗色 |
| `mono_min` | 极简黑白 | 克制、留白、字即是图 | 个人 IP / 高端品牌 / 作品集 / 理念宣讲 | 浅色 |
| `editorial` | 编辑杂志风 | 纸媒质感、衬线大标题、栏式排版 | 年度报告 / 品牌故事 / 文化分享 / 深度长文 | 浅色 |
| `bento` | Bento 网格 | 模块化、信息密度高、Apple 风 | 产品 overview / 数据看板 / 功能介绍 / 投资更新 | 浅色 |
| `glass` | 玻璃拟态 | 通透、层次、轻奢科技 | SaaS 产品 / AI 工具介绍 / 官网风演示 | 浅色 |
| `dark_tech` | 暗色科技 | 深色底、霓虹点缀、硬核未来 | AI 产品发布 / 技术分享 / 开发者大会 / 安全主题 | 暗色 |
| `aurora` | 极光霓虹 | 梦幻、流动光带、未来感 | 前沿科技 / 概念发布 / 创意提案 / 青年文化 | 暗色 |
| `blueprint` | 建筑蓝图 | 精确、工程感、线稿标注 | 技术方案 / 系统架构 / 工程规划 / 流程规范 | 浅色 |
| `academic` | 学术深蓝 | 严谨、规范、框架清晰 | 论文答辩 / 课题汇报 / 医疗科研 / 培训讲义 | 浅色 |
| `clay` | 黏土 3D | 柔软、亲和、手工质感 | 产品介绍 / 教育课件 / 生活方式 / 团队建设 | 浅色 |
| `riso` | 复古波普 | 网点印刷、撞色、复古俏皮 | 创意营销 / 独立出版 / 音乐活动 / 品牌联名 | 浅色 |
| `memphis` | 孟菲斯几何 | 撞色、几何铺陈、年轻张扬 | 校园活动 / 年轻品牌 / 节日营销 / 创意提案 | 浅色 |
| `guochao` | 国潮 | 中国红金、传统纹样、庄重喜庆 | 政务汇报 / 节庆活动 / 文化品牌 / 年度报告 | 浅色 |
| `organic` | 有机自然 | 温润、植物、手作质感 | 生态环保 / 健康养生 / 食品农业 / 民宿文旅 | 浅色 |
| `typo_bold` | 大字报 | 超大标题、极简底、强观点 | 观点演讲 / 发布会 / 口号墙 / 金句页 | 浅色 |
| `custom` | 自定义风格 | 客户自填 | 任何预设之外的风格 | 浅色 |

## 逐风格详解

### `kids_hand` · 儿童手绘（原厂）（Kids Hand-drawn）

**长什么样**：明亮的蜡笔涂鸦感，圆滚滚的造型、夸张表情，孩子一眼就被抓住。

**什么场合用**：学校 / 教育类客户首选；配 scene 五档（A活跃/B严肃/C应急/K温柔/R红色）调气质。

- 气质关键词：明亮童趣、夸张表情、蜡笔质感
- 适用：主题班会 / 幼小教育 / 校园活动 / 安全科普
- 主题：浅色底 + 深色字（脚本会自动切换背景死命令与亮度哨兵）
- 字体：正文 汉仪跳跳体简 / 标题 站酷高端黑
- ⚠️ 不覆盖画风与配色，完全沿用 scene 五档（A活跃/B严肃/C应急/K温柔/R红色）

### `swiss` · 瑞士国际主义（Swiss International）

**长什么样**：白底、严格网格、大量留白，只用一抹正红做强调。理性到骨子里。

**什么场合用**：咨询、金融、董事汇报。客户要是说『别花哨，要专业』，选它。

- 气质关键词：理性克制、严格网格、一抹红
- 适用：咨询报告 / 金融分析 / 董事汇报 / 数据陈述
- 主题：浅色底 + 深色字（脚本会自动切换背景死命令与亮度哨兵）
- 配色：`paper` #F5F5F2 · `field` #D61E1E · `support` #EEEEEB · `pop` #1E1E1E · `ink` #191919
- 字体：正文 微软雅黑 / 标题 站酷高端黑
- 背景提示词要点：`flat light grey paper, hairline grid, one small red block, huge clean center`
- 插图提示词要点：`flat geometric icon-like subject, precise edges, no gradients`

### `navy_gold` · 深海蓝金（Corporate Navy）

**长什么样**：深海蓝底 + 香槟金描边，像高级酒店大堂的灯光。

**什么场合用**：融资 BP、年度总结、高端发布会。暗色主题，字是浅色。

- 气质关键词：高端、稳重、金色点缀
- 适用：融资计划书 / 年度总结 / 高管汇报 / 品牌发布
- 主题：暗色底 + 浅色字（脚本会自动切换背景死命令与亮度哨兵）
- 配色：`paper` #101C34 · `field` #C6A05A · `support` #182C4E · `pop` #E8D6AA · `ink` #EEF0F6
- 字体：正文 微软雅黑 / 标题 站酷高端黑
- 背景提示词要点：`deep navy wash, gold hairline frame, soft vignette, clean center for title`
- 插图提示词要点：`elegant subject with gold rim light, deep navy ambient, flat premium look`

### `mono_min` · 极简黑白（Monochrome Minimal）

**长什么样**：纯黑白灰，字本身就是图。极致留白，安静但有压迫感。

**什么场合用**：个人 IP、作品集、理念宣讲。内容少而重时效果最好。

- 气质关键词：克制、留白、字即是图
- 适用：个人 IP / 高端品牌 / 作品集 / 理念宣讲
- 主题：浅色底 + 深色字（脚本会自动切换背景死命令与亮度哨兵）
- 配色：`paper` #FAFAFA · `field` #111111 · `support` #F2F2F2 · `pop` #787878 · `ink` #161616
- 字体：正文 微软雅黑 / 标题 站酷高端黑
- 背景提示词要点：`near-white paper, single hairline, vast empty copy space`
- 插图提示词要点：`single minimal subject, thin line, no color, quiet`

### `editorial` · 编辑杂志风（Editorial Magazine）

**长什么样**：米白纸张、衬线大标题、分栏排版，像一本杂志摊开。

**什么场合用**：年度报告、品牌故事、文化分享。文字量大的稿子配它最舒服。

- 气质关键词：纸媒质感、衬线大标题、栏式排版
- 适用：年度报告 / 品牌故事 / 文化分享 / 深度长文
- 主题：浅色底 + 深色字（脚本会自动切换背景死命令与亮度哨兵）
- 配色：`paper` #FAF7F2 · `field` #1A1A1A · `support` #EEE8DE · `pop` #A62723 · `ink` #201D1A
- 字体：正文 微软雅黑 / 标题 站酷高端黑
- 背景提示词要点：`cream paper grain, faint column rules, warm and literate`
- 插图提示词要点：`ink-drawn subject with print texture, editorial and refined`

### `bento` · Bento 网格（Bento Grid）

**长什么样**：圆角模块拼成的信息墙，一块一块很清楚，Apple 发布会那味。

**什么场合用**：产品 overview、数据看板、功能介绍。信息多但要有条理时首选。

- 气质关键词：模块化、信息密度高、Apple 风
- 适用：产品 overview / 数据看板 / 功能介绍 / 投资更新
- 主题：浅色底 + 深色字（脚本会自动切换背景死命令与亮度哨兵）
- 配色：`paper` #F6F7F9 · `field` #2563EB · `support` #EBEEF5 · `pop` #10B981 · `ink` #181C24
- 字体：正文 微软雅黑 / 标题 站酷高端黑
- 背景提示词要点：`soft neutral wash, faint rounded tile rhythm, airy`
- 插图提示词要点：`clean flat subject, rounded friendly geometry, product-like`

### `glass` · 玻璃拟态（Glassmorphism）

**长什么样**：毛玻璃质感的半透明卡片浮在柔和渐变上，轻奢、通透。

**什么场合用**：SaaS / AI 工具介绍、官网风演示。科技但不硬。

- 气质关键词：通透、层次、轻奢科技
- 适用：SaaS 产品 / AI 工具介绍 / 官网风演示
- 主题：浅色底 + 深色字（脚本会自动切换背景死命令与亮度哨兵）
- 配色：`paper` #EEF4FF · `field` #5865F2 · `support` #E1E8FA · `pop` #22D3EE · `ink` #1E233C
- 字体：正文 微软雅黑 / 标题 站酷高端黑
- 背景提示词要点：`soft gradient with blurred colour blobs, frosted veil, airy`
- 插图提示词要点：`subject with frosted glass edges, soft bloom, translucent`

### `dark_tech` · 暗色科技（Dark Tech）

**长什么样**：深炭底 + 霓虹青描边，像科幻片里的控制台。

**什么场合用**：AI 产品发布、技术分享、安全主题。暗色主题，字是浅色。

- 气质关键词：深色底、霓虹点缀、硬核未来
- 适用：AI 产品发布 / 技术分享 / 开发者大会 / 安全主题
- 主题：暗色底 + 浅色字（脚本会自动切换背景死命令与亮度哨兵）
- 配色：`paper` #12141C · `field` #22E2D8 · `support` #1E222E · `pop` #C6FF3D · `ink` #E8EEF8
- 字体：正文 微软雅黑 / 标题 站酷高端黑
- 背景提示词要点：`deep charcoal wash, faint neon hairline, vignette, clean center`
- 插图提示词要点：`subject with thin neon outline on dark field, crisp flat`

### `aurora` · 极光霓虹（Aurora Neon）

**长什么样**：深靛蓝底上流动的极光带，紫青渐变，梦幻未来感。

**什么场合用**：概念发布、前沿科技、创意提案。偏艺术，商务汇报慎用。

- 气质关键词：梦幻、流动光带、未来感
- 适用：前沿科技 / 概念发布 / 创意提案 / 青年文化
- 主题：暗色底 + 浅色字（脚本会自动切换背景死命令与亮度哨兵）
- 配色：`paper` #0C0E20 · `field` #7C5CFF · `support` #1A183A · `pop` #56F0DC · `ink` #ECEEFF
- 字体：正文 微软雅黑 / 标题 站酷高端黑
- 背景提示词要点：`deep indigo with flowing aurora light bands, soft glow`
- 插图提示词要点：`subject lit by violet-cyan rim light, ethereal`

### `blueprint` · 建筑蓝图（Architectural Blueprint）

**长什么样**：浅蓝图纸 + 精确线稿 + 标注，工程师的浪漫。

**什么场合用**：系统架构、工程规划、流程规范。讲『怎么搭起来』时最对。

- 气质关键词：精确、工程感、线稿标注
- 适用：技术方案 / 系统架构 / 工程规划 / 流程规范
- 主题：浅色底 + 深色字（脚本会自动切换背景死命令与亮度哨兵）
- 配色：`paper` #F0F5FC · `field` #18468C · `support` #E4EEFA · `pop` #5A78A0 · `ink` #122034
- 字体：正文 微软雅黑 / 标题 站酷高端黑
- 背景提示词要点：`pale blue technical paper, faint measurement grid, thin rules`
- 插图提示词要点：`precise line-art subject, drafting aesthetic, measured strokes`

### `academic` · 学术深蓝（Academic Blue）

**长什么样**：干净白底 + 深蓝框架 + 一点强调红，严谨可信。

**什么场合用**：论文答辩、课题汇报、医疗科研、培训讲义。

- 气质关键词：严谨、规范、框架清晰
- 适用：论文答辩 / 课题汇报 / 医疗科研 / 培训讲义
- 主题：浅色底 + 深色字（脚本会自动切换背景死命令与亮度哨兵）
- 配色：`paper` #FAFAFC · `field` #1A366E · `support` #ECF0F8 · `pop` #B02020 · `ink` #1E2228
- 字体：正文 微软雅黑 / 标题 站酷高端黑
- 背景提示词要点：`near-white paper, faint navy frame line, tidy and formal`
- 插图提示词要点：`clear diagram-like subject, precise and credible`

### `clay` · 黏土 3D（Claymorphism）

**长什么样**：软软的黏土造型，哑光质感，暖色打光，想捏一把。

**什么场合用**：产品介绍、教育课件、生活方式。亲和力要求高时选它。

- 气质关键词：柔软、亲和、手工质感
- 适用：产品介绍 / 教育课件 / 生活方式 / 团队建设
- 主题：浅色底 + 深色字（脚本会自动切换背景死命令与亮度哨兵）
- 配色：`paper` #FAF6F2 · `field` #FF8A65 · `support` #F6E8E0 · `pop` #7EC8B4 · `ink` #3C302C
- 字体：正文 微软雅黑 / 标题 站酷高端黑
- 背景提示词要点：`soft pastel wash with puffy rounded light shapes, matte`
- 插图提示词要点：`soft clay subject, matte finish, warm studio light`

### `riso` · 复古波普（Risograph Print）

**长什么样**：粗网点、撞色块、套印错位，复古 zine 的俏皮。

**什么场合用**：创意营销、独立出版、音乐活动。年轻、有态度的品牌。

- 气质关键词：网点印刷、撞色、复古俏皮
- 适用：创意营销 / 独立出版 / 音乐活动 / 品牌联名
- 主题：浅色底 + 深色字（脚本会自动切换背景死命令与亮度哨兵）
- 配色：`paper` #F7F2E8 · `field` #E84A4A · `support` #FADEB4 · `pop` #3A78BE · `ink` #201C18
- 字体：正文 微软雅黑 / 标题 站酷高端黑
- 背景提示词要点：`warm paper tint, coarse halftone dots, flat colour wash`
- 插图提示词要点：`bold flat subject with halftone texture, ink misregistration`

### `memphis` · 孟菲斯几何（Memphis Pop）

**长什么样**：波点、锯齿、几何碎片满地撒，80 年代的快乐。

**什么场合用**：校园活动、节日营销、年轻品牌。热闹场合专用。

- 气质关键词：撞色、几何铺陈、年轻张扬
- 适用：校园活动 / 年轻品牌 / 节日营销 / 创意提案
- 主题：浅色底 + 深色字（脚本会自动切换背景死命令与亮度哨兵）
- 配色：`paper` #FAF8FC · `field` #FF5A8C · `support` #F0EBFF · `pop` #FFC83C · `ink` #282030
- 字体：正文 微软雅黑 / 标题 站酷高端黑
- 背景提示词要点：`pale ground with small flat geometric confetti, playful`
- 插图提示词要点：`bold flat subject with geometric accents, energetic`

### `guochao` · 国潮（Chinese Chic）

**长什么样**：中国红 + 暖金，传统纹样现代化，庄重又喜庆。

**什么场合用**：政务汇报、节庆活动、文化品牌、年度报告。

- 气质关键词：中国红金、传统纹样、庄重喜庆
- 适用：政务汇报 / 节庆活动 / 文化品牌 / 年度报告
- 主题：浅色底 + 深色字（脚本会自动切换背景死命令与亮度哨兵）
- 配色：`paper` #FAF4EB · `field` #B22020 · `support` #F6E8D6 · `pop` #C6A05A · `ink` #2C201C
- 字体：正文 微软雅黑 / 标题 站酷高端黑
- 背景提示词要点：`warm rice-paper wash, subtle traditional ornament at edges`
- 插图提示词要点：`subject with red-gold palette and modern flat ornament`

### `organic` · 有机自然（Hand-crafted Organic）

**长什么样**：大地色、水彩颗粒、植物手作感，看得见纤维。

**什么场合用**：生态环保、健康养生、食品农业、民宿文旅。

- 气质关键词：温润、植物、手作质感
- 适用：生态环保 / 健康养生 / 食品农业 / 民宿文旅
- 主题：浅色底 + 深色字（脚本会自动切换背景死命令与亮度哨兵）
- 配色：`paper` #F7F8F2 · `field` #6A945A · `support` #EAF0E2 · `pop` #D6A860 · `ink` #2C3028
- 字体：正文 微软雅黑 / 标题 站酷高端黑
- 背景提示词要点：`soft earthy wash, pressed-paper grain, faint botanical traces`
- 插图提示词要点：`botanical handmade subject, watercolour grain, calm`

### `typo_bold` · 大字报（Typographic Bold）

**长什么样**：超大标题占半页，一句话就是一页，观点砸出来。

**什么场合用**：观点演讲、发布会、金句墙。内容越少越有力。

- 气质关键词：超大标题、极简底、强观点
- 适用：观点演讲 / 发布会 / 口号墙 / 金句页
- 主题：浅色底 + 深色字（脚本会自动切换背景死命令与亮度哨兵）
- 配色：`paper` #F8F8F6 · `field` #111111 · `support` #F0F0EC · `pop` #FFD600 · `ink` #141414
- 字体：正文 微软雅黑 / 标题 站酷高端黑
- 背景提示词要点：`flat pale ground with a single bold colour band, vast empty`
- 插图提示词要点：`minimal high-contrast subject, poster-like`

### `custom` · 自定义风格（Custom）

**长什么样**：客户说什么风格，就是什么风格（需要把描述翻译成英文母前缀 + 配色）。

**什么场合用**：预设都不满意时用。必须由 Agent 补齐 style_override，否则会回落默认模板。

- 气质关键词：客户自填
- 适用：任何预设之外的风格
- 主题：浅色底 + 深色字（脚本会自动切换背景死命令与亮度哨兵）
- ⚠️ 写 "style": "custom" 时，必须在 brief 顶层同时写 style_override.prefix / prefix_bg / colors（由 Agent 按客户描述生成）；或用 style_custom 字段写中文描述，脚本会据此要求 Agent 补齐

## 给客户的选择建议（Agent 话术）

客户拿不准时，按这个顺序推：

1. **看场合**：正式汇报 → `swiss` / `navy_gold` / `academic`；对外营销 → `riso` / `memphis` / `typo_bold`；
   科技产品 → `dark_tech` / `glass` / `bento`；文化政务 → `guochao` / `editorial`；教育孩子 → `kids_hand` / `clay`。
2. **看内容量**：文字多 → `editorial` / `academic`；要点多且散 → `bento` / `cards` 版式；
   一句话观点 → `typo_bold`。
3. **看投放环境**：投屏会议室偏暗 → 暗色风格（`dark_tech` / `navy_gold`）更抓眼；
   要打印出来发 → 一律浅色风格。
4. **客户有品牌色** → 直接用 `custom`，把品牌色填进 `colors.field`，其余沿用最接近的预设。

> 推荐时**一次给三个**：一个最稳的、一个最有记忆点的、一个最贴客户行业的，让客户挑。别甩 17 个选项给他。
