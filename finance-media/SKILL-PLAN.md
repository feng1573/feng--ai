# 财经自媒体 · 技能规划清单

> 生成日期：2026-09-16
> 适用对象：财经自媒体创作者（本机 DSH 环境）
> 平台范围：**抖音 / 视频号（短视频）· 小红书（图文笔记）· 公众号（长文）**
> 垂直方向：**待定**（见 §6，这一项会改变数据源与合规规则，需你先拍板）

---

## 一、现状基线：本机已有什么、没有什么

### 1.1 已有：277 个「人设型」技能

来源 `jnMetaCode/agency-agents-zh v1.4.0`（MIT），部署于 `~/.dsh/skills/`，部署记录见 `../agency-deploy/README.md`（22 项校验通过）。

它们的本质是**角色定义（prompt persona）**——规定「谁来做、按什么原则做、交付什么」，**不包含任何可执行能力**：不能抓行情、不能画图、不能配音、不能发布。

命名规律：全部带部门前缀（`finance-` / `marketing-` / `design-` …），**没有任何一个非人设的「能力型」skill**（已实测确认）。

### 1.2 没有：数据源、生成、发布、存证能力

| 缺口类别 | 具体缺失 | 后果 |
|---|---|---|
| 数据源 | 无行情/财报/宏观抓取 skill | 财经内容无数据支撑，只能"讲观点" |
| 图表生成 | 无 K 线/净值曲线/对比图生成 skill | 视频与图文缺视觉证据 |
| 音视频生成 | 无 TTS/字幕/合成/封面 skill | 短视频无法标准化量产 |
| 发布对接 | 无平台接口 skill | 一稿多投靠手工 |
| 存证追溯 | 无信源台账/事实核查 skill | 被投诉时无法自证 |

**结论**：人设技能解决"怎么写"，真正决定产能和生死的是下面要新建的**能力型 skill**。

---

## 二、财经自媒体的 4 层技能架构

```
L0 风控底座   ← 最该先建，财经赛道封号成本最高
   ├─ 财经合规预审官
   ├─ 事实核查与信源台账
   └─ 市场数据管道
L1 内容生产
   ├─ 选题情报（已有可复用）
   ├─ 投研分析（已有可复用）
   ├─ 数据可视化 / K线图生成
   └─ 财经文案（已有可复用）
L2 平台适配   ← 三平台各一套
   ├─ 抖音/视频号 脚本导演 + 短视频流水线
   ├─ 小红书 图文笔记工厂
   └─ 公众号 深度长文 + 排版
L3 分发与复盘
   ├─ 跨平台发布器
   ├─ 私域沉淀
   └─ 效果复盘
```

---

## 三、技能清单

图例：**已有**＝现成可 `/slug` 点名；**新建**＝需写入 `~/.dsh/skills/`；P0＝必须最先做，P1＝第二梯队，P2＝规模化后再做。

### L0 风控底座（P0 全部）

| # | 技能名（建议 slug） | 类型 | 优先级 | 核心能力 | 关键交付物 |
|---|---|---|---|---|---|
| 1 | `finance-content-compliance-review` | 新建 | **P0** | 发布前自动过审：荐股嫌疑、收益承诺、内幕信息暗示、绝对化用语、免责声明缺失、平台敏感词 | 风险分级报告（放行/改写/禁止）+ 逐条修改建议 + 免责声明模板 |
| 2 | `finance-fact-ledger` | 新建 | **P0** | 每条数据留痕：数值、来源、URL、抓取时间、口径 | 可追溯 `ledger.json` / 表格，供事后自证 |
| 3 | `finance-market-data-pipeline` | 新建 | **P0** | 行情/财报/宏观数据的定时抓取、清洗、缓存、校验 | 标准化数据集 + 数据新鲜度告警 |
| — | `support-legal-compliance-checker` | 已有 | P1 | 通用法律合规兜底（广告法、知识产权） | 可与 #1 叠加使用 |

**为什么 1、2、3 是 P0**：财经自媒体的三条命门是「荐股违规」「数据造谣」「信源不可溯」，全部落在 L0。少建一个，前面产能越高风险越大。

### L1 内容生产

| # | 技能名 | 类型 | 优先级 | 核心能力 | 关键交付物 |
|---|---|---|---|---|---|
| 4 | `finance-data-visualizer` | 新建 | **P1** | K 线图、净值曲线、板块热力、同比对比、宏观走势图，统一视觉模板 | PNG/SVG 图表 + 可复用样式规范 |
| 5 | `marketing-daily-news-briefing` | 已有 | P1 | 多源新闻实时采集、交叉验证、结构化简报 | 每日选题简报 |
| 6 | `finance-investment-researcher` | 已有 | P1 | 深度投研分析框架 | 研究分析稿 |
| 7 | `finance-financial-analyst` | 已有 | P1 | 财务建模、假设显性化、敏感性分析 | 财务拆解内容 |
| 8 | `marketing-content-creator` | 已有 | P1 | 多渠道同一故事的多形态表达 | 初稿 |
| 9 | `specialized-document-generator` | 已有 | P2 | 程序化生成 PDF/PPTX/XLSX（含图表） | 研报式成品、付费内容 |
| 10 | `finance-hk-stock-compliance-reviewer` | 已有 | P2 | 港美股披露规则（**仅垂直方向含港股时启用**） | 披露合规意见 |

### L2 平台适配（三平台各一套）

| # | 技能名 | 类型 | 优先级 | 核心能力 | 关键交付物 |
|---|---|---|---|---|---|
| 11 | `finance-short-video-pipeline` | 新建 | **P1** | 口播稿 → TTS 配音 → 字幕 → 时间轴 → 成片 → 封面；含竖屏版式与图表动效 | 可直接发布的竖屏成片 + 封面图 |
| 12 | `marketing-douyin-strategist` | 已有 | P1 | 抖音算法机制、爆款结构、完播率优化 | 脚本 + 发布策略 |
| 13 | `marketing-weixin-channels-strategist` | 已有 | P1 | 视频号社交推荐逻辑 | 视频号适配策略 |
| 14 | `marketing-short-video-editing-coach` | 已有 | P2 | 剪映/PR/达芬奇/调色/音频工程方法 | 剪辑技术指导 |
| 15 | `finance-xiaohongshu-note-factory` | 新建 | **P1** | 首图模板、笔记结构、标签策略的**财经特化**版本 | 图文笔记包（首图+正文+标签） |
| 16 | `marketing-xiaohongshu-operator` | 已有 | P1 | 小红书种草逻辑、爆款公式 | 笔记策略 |
| 17 | `finance-wechat-longform` | 新建 | **P1** | 公众号深度长文结构 + Markdown 转微信排版（样式内联） | 可粘贴入公众号后台的 HTML |
| 18 | `marketing-wechat-operator` | 已有 | P1 | 公众号内容策略、社群、私域 | 选题与运营策略 |
| 19 | `marketing-zhihu-strategist` | 已有 | P2 | 知乎深度问答（复用作为公众号长文素材源） | 问答稿 |
| 20 | `marketing-weibo-strategist` | 已有 | P2 | 微博热点跟进（若后续扩平台） | 热点内容 |

### L3 分发与复盘

| # | 技能名 | 类型 | 优先级 | 核心能力 | 关键交付物 |
|---|---|---|---|---|---|
| 21 | `finance-multiplatform-publisher` | 新建 | P2 | 一稿多投：各平台标题/标签/封面差异化、发布队列、失败重试 | 发布任务单 + 各平台差异版 |
| 22 | `marketing-private-domain-operator` | 已有 | P2 | 私域沉淀、社群运营 | 私域承接方案 |
| 23 | `finance-content-performance-review` | 新建 | P2 | 各平台数据回流、选题效果归因、下轮选题建议 | 复盘报告 + 选题优先级 |
| 24 | `marketing-search-growth-orchestrator` | 已有 | P2 | 搜索流量增长（公众号/知乎/小红书搜索） | 搜索词布局 |

---

## 四、落地路线图

### 第一期 · 风控底座（建议立即做，3 个新建）
1. `finance-content-compliance-review`（**先做这个**，单点验证效果）
2. `finance-fact-ledger`
3. `finance-market-data-pipeline`
> 验收：拿你最近 3 篇已有内容跑一遍 #1，看能否准确指出风险点。准了再往下走。

### 第二期 · 生产闭环（4 个新建 + 复用已有）
4. `finance-data-visualizer`
5. `finance-short-video-pipeline`
6. `finance-xiaohongshu-note-factory`
7. `finance-wechat-longform`
> 验收：同一份选题素材，能一次产出竖屏成片 + 小红书图文 + 公众号长文三种形态。

### 第三期 · 规模化（2 个新建）
8. `finance-multiplatform-publisher`
9. `finance-content-performance-review`

---

## 五、必装 vs 可选速查

**核心必装（7 个新建）**
`finance-content-compliance-review` · `finance-fact-ledger` · `finance-market-data-pipeline` · `finance-data-visualizer` · `finance-short-video-pipeline` · `finance-xiaohongshu-note-factory` · `finance-wechat-longform`

**规模起来再加（2 个）**
`finance-multiplatform-publisher` · `finance-content-performance-review`

**已有可直接点名（按环节）**

| 环节 | `/slug` |
|---|---|
| 选题情报 | `marketing-daily-news-briefing` |
| 投研分析 | `finance-investment-researcher`、`finance-financial-analyst`、`finance-financial-forecaster` |
| 通用合规兜底 | `support-legal-compliance-checker` |
| 文案 | `marketing-content-creator` |
| 抖音 | `marketing-douyin-strategist` |
| 视频号 | `marketing-weixin-channels-strategist` |
| 小红书 | `marketing-xiaohongshu-operator`、`marketing-xiaohongshu-specialist` |
| 公众号 | `marketing-wechat-operator`、`marketing-wechat-official-account` |
| 剪辑方法 | `marketing-short-video-editing-coach` |
| 播客 | `marketing-podcast-strategist` |
| 成品文件 | `specialized-document-generator` |
| 私域 | `marketing-private-domain-operator` |

---

## 六、待你拍板的关键项

### 6.1 垂直方向（**必须先定**，直接决定上面技能怎么建）

| 选项 | 数据源 | 合规红线强度 | 对清单的影响 |
|---|---|---|---|
| A. A股/基金/宏观 | AkShare、Tushare | **最强**（荐股、内幕、收益承诺） | #1 规则最严；#3 需接 A 股接口 |
| B. 美股/港股/全球资产 | yfinance、SEC EDGAR、HKEX | 中（另需关注外汇合规话题） | 可启用 #10 港美股合规 |
| C. 个人理财/财商科普 | 公开统计、央行/统计局 | 最弱 | #1 可大幅简化；#3 需求下降 |
| D. 加密/大宗商品 | 交易所公开 API | 平台限流风险高 | #3 需多交易所聚合 |

### 6.2 其他确认项
- 更新频率（日更 / 周更？决定 #3 调度与 #11 量产强度）
- 是否真人出镜（决定 #11 是纯合成还是素材剪辑）
- 变现方式（广告 / 知识付费 / 引流？影响 CTA 与私域设计）
- 是否有合规审查的人力预算（无则 #1 必须自动化且从严）

---

## 七、下一步

告诉我**垂直方向**（A/B/C/D）+ 是否按第一期开建，我会：
1. 先给出 `finance-content-compliance-review` 的完整 skill 规格（frontmatter + 正文）供你确认；
2. 确认后写入 `~/.dsh/skills/`，并用你的一篇真实内容做验收测试。

### 附：skill 文件标准格式（供参考）

```markdown
---
name: finance-content-compliance-review
description: "财经内容合规预审官 — 发布前自动审查荐股嫌疑、收益承诺、内幕信息、绝对化用语与免责声明，输出风险分级与改写建议。"
---

# 财经内容合规预审官

## 你的身份与记忆
## 你的核心使命
## 你必须遵循的关键规则
## 你的工作流程
## 交付物
```

> 注意：`disable-model-invocation: true` 表示该技能**只能手动 `/slug` 点名**，不会被模型自动匹配。风控类技能**不建议**加这一行（希望每次都被自动触发）；人设类（如现有剪辑教练）则适合加上，避免误触发。
