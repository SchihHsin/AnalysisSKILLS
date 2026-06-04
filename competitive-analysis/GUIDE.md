# 竞品分析 Skill · 使用指南

## 这是什么

一个帮你做竞品分析的 AI Skill——从搜集资料、生成洞察，到输出可交付的报告。你负责告诉它分析什么、目标是什么，它负责搜集、分析、输出。

支持两种使用方式：**Claude Code**（斜杠命令）和 **Claude.ai 网页版**（上传文件 + 口令触发）。

---

## 方式 A · Claude Code（斜杠命令）

### 第一步：放入命令文件

在你的项目根目录创建如下结构：

```
.claude/
└── commands/
    └── competitive-analysis.md    ← 把 SKILL.md 的内容复制到这里
```

references 文件放在项目里任意位置均可（Claude Code 可以直接读取项目内的文件）：

```
competitive-analysis/
├── references/
│   ├── research-methodology.md
│   ├── analysis-frameworks.md
│   ├── visualization-framework.md
│   ├── verification-protocol.md
│   └── assets/
│       ├── report-template.md
│       └── tracking-template.md
```

### 第二步：用斜杠触发

在 Claude Code 对话框输入：

```
/competitive-analysis
```
不带参数 → 进入完整 Interactive Mode，AI 会引导你一步步来。

```
/competitive-analysis fast Figma vs Sketch
```
`fast` → 快速模式，直接开始；后面的内容是初始目标。

```
/competitive-analysis continue figma-d2c
```
`continue` → 恢复历史分析，读取 `tracking/figma-d2c.md` 里的进度。

```
/competitive-analysis visualize notion-linear
```
`visualize` → 直接进入 Stage 4，把已有报告做成 HTML。

```
/competitive-analysis query Figma 和 Sketch 的定价差异
```
`query` → 快查，不创建任何文件，直接给结论。

---

## 方式 B · Claude.ai 网页版（Project 知识库）

### 第一步：上传文件到 Project 知识库

在 Claude.ai 创建一个 Project，把以下文件全部上传到知识库：

```
SKILL.md                               ← 必须，主文件
references/research-methodology.md    ← 必须，搜集方法论
references/analysis-frameworks.md     ← 必须，分析框架
references/visualization-framework.md ← 做 HTML 报告时需要
references/verification-protocol.md   ← 建议上传
references/assets/report-template.md  ← 建议上传
references/demo-conversations.md      ← 建议上传（帮 AI 理解交互节奏）
```

> **最简上传**：只上传 `SKILL.md` 也能用，但 Stage 4 HTML 报告的输出质量会降低。

### 第二步：用自然语言触发

在 Project 对话框里直接说需求：

```
帮我对比 Figma、Sketch、Framer 的组件管理体验
```

网页版没有斜杠命令，用以下**口令**替代斜杠参数：

| 对应 Claude Code 斜杠参数 | 网页版等价口令 |
|---|---|
| `/competitive-analysis fast ...` | 在需求前加「快速」：`快速帮我看看 ...` |
| `/competitive-analysis continue X` | `继续 X 的分析` |
| `/competitive-analysis visualize X` | `把 X 的报告做成可视化网页版` |
| `/competitive-analysis query ...` | `快查：...` |

---

## 触发示例（两种方式通用）

不需要特定格式，直接说你想做什么：

```
帮我对比 Figma、Sketch、Framer 的组件管理体验
```
```
调研一下 Notion、Linear、Jira 的功能和定价
```
```
做一份 AI CLI 工具的竞品分析，重点看交互设计
```
```
快速摸底一下国内几款设计工具的现状
```

Skill 会自动识别你的意图，推断分析视角，然后开始引导你。

---

## 三种使用模式

根据你的时间和需求选择：

### 模式 A · 快速摸底（15-30 分钟）

**适合**：初步了解某个领域、快速准备会议素材

**说法**：在需求前加「快速」或「快查」

```
快速帮我看看 Claude Code、Cursor、Copilot 各自的定位
```

**流程**：规划 → 搜集 → 直接给结论，不写完整报告，不做 HTML

**输出**：一段结构化的分析文字，带关键发现和推荐方向

---

### 模式 B · 标准分析（1-3 小时）

**适合**：做设计决策、给团队汇报、产品规划参考

**说法**：正常描述需求

```
帮我做一份 Figma vs Sketch vs Adobe XD 的完整竞品分析，UX 视角
```

**流程**：Stage 1 规划（3 次确认）→ Stage 2 搜集 → Stage 3 Markdown 报告

**输出**：完整的 Markdown 分析报告，含用户旅程、触点对比、洞察和建议

---

### 模式 C · 完整可视化（3-6 小时）

**适合**：对外分享、高管评审、长期参考资产

**说法**：说明需要 HTML 报告

```
帮我做一份竞品分析报告，最后要做成可以演示的网页版
```

**流程**：Stage 1-3 完整流程 → Stage 4 生成多页 HTML 报告

**输出**：Markdown 报告 + 可在浏览器打开的 HTML 报告（Snap Scroll、两层导航）

---

## 每个阶段你需要做什么

Skill 会在关键节点停下来等你回复，你不需要主动推进。

| 阶段 | AI 在做 | 你需要做 |
|------|--------|--------|
| Stage 1 · 规划 | 推断视角、建议竞品和维度 | 确认或调整（说「对」或指出要改的地方） |
| Stage 2 · 搜集 | 搜集资料、截图、整理素材 | 等待；遇到信息缺口时做决策 |
| Stage 3 · 分析 | 写报告、提炼洞察 | 审阅报告摘要，决定是否要调整方向 |
| Stage 4 · 可视化 | 生成 HTML 文件 | 确认页面方案；最后审阅输出 |

> **随时可以打断**：在任何阶段说「等一下」「换个方向」都可以，Skill 会停下来处理你的反馈。

---

## 最常用的口令

```
对，继续                    ← 确认当前方案，进入下一步
不对，[说明要改什么]        ← 纠正方向
先暂停，我有个问题          ← 中途打断
这个竞品不需要，去掉 X      ← 调整竞品名单
重点放在 [某个维度]         ← 调整分析重心
不用做 HTML，Markdown 就够  ← 跳过 Stage 4
帮我继续之前的 [项目名] 分析 ← 恢复历史进度
```

---

## 常见问题

**Q：Skill 推断的视角不对怎么办？**
在 Stage 1.1 的确认环节直接纠正：「不对，我想要的是 PM 视角，重点看功能和定价。」

**Q：某个竞品搜不到信息怎么办？**
Skill 会主动告知并给你三个选项（跳过/换来源/你来提供）。如果你有账号或截图，直接发给它。

**Q：报告太长/太短怎么调？**
在 Stage 3 报告审阅环节说：「触点太多了，只保留最重要的 5 个」或「这个部分太浅，帮我深挖一下定价策略」。

**Q：能继续上次没做完的分析吗？**
说「继续 [项目名] 的分析」，Skill 会读取 `tracking/` 里的进度记录，从上次中断的地方恢复。

**Q：只想快速问一个问题，不需要完整分析怎么办？**
说「快查：[你的问题]」，Skill 会直接回答，不启动完整流程，不创建任何文件。

---

## 输出文件在哪里

```
tracking/{项目名}.md          ← 分析规划和进度记录
materials/{项目名}/           ← 搜集的截图和素材
reports/{项目名}-{日期}-v1.md ← Markdown 分析报告
reports/{项目名}-{日期}-visual/ ← HTML 可视化报告（如有）
```

打开 HTML 报告目录里的 `index.html` 即可在浏览器查看。
