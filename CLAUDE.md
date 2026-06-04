# AnalysisSKILLS

这个仓库收录竞品分析相关的 Skill 和报告，供 Claude Code 使用时参考。

GitHub Pages 地址：`https://schihhsin.github.io/AnalysisSKILLS/`

## 目录结构

```
AnalysisSKILLS/
├── original_report/              # 最早的竞品分析报告（AI CLI 工具，手工产出）
├── original_skill/               # 基于 original_report 提炼的第一版 Skill（时昕昱）
│   └── SKILL-competitive-analysis.md
├── skill_used_report/            # 使用 original_skill 生成的报告示例
│   └── 芯片算子领域竞品分析Skill.md  # 领域特定的触点框架扩展
├── competitive-analysis-bufan/   # 另一位同学（卜凡）独立开发的 Skill
│   ├── SKILL.md
│   └── references/               # 方法论拆分存放（搜集/分析/可视化/核查）
├── competitive-analysis-merged/  # 融合优化后的版本（主要使用这个）
│   ├── SKILL.md
│   └── references/
│       └── guizang-ppt-skill/    # 内置的横向翻页 PPT skill（Stage 4 形态 B 调用）
├── SKILL_guide.md                # original_skill 的使用说明
├── skill-improvement-report.html # 两版 Skill 的融合分析报告（深色蓝紫渐变主题）
└── skill-usage-guide.html        # 融合版 Skill 的使用指南（GitHub Pages 对外可访问）
```

## 主要使用版本

**`competitive-analysis-merged/`** 是融合后的主版本，融合了两个版本的优点：

- **流程结构**：来自 competitive-analysis-bufan 的 4 阶段管道（规划→搜集→分析→可视化），有完整的 Human-in-the-Loop 检查点
- **视角选择**：Stage 1 显性确认分析视角（UX/PM/UI/Tech/Strategy），贯穿全程
- **信息搜集**：competitive-analysis-bufan 的图文采集协议、视频工作流、失败处理策略
- **可视化骨架**：在 original_skill 单一 UX 骨架基础上扩展为 5 种视角骨架（S1-S5）+ 10 种表达模式（P1-P10）
- **开发规格**：original_skill 的 TypeScript 接口 + 状态机格式
- **设计系统**：浅色主题默认（暖白），深色为显式可选

使用时将 `SKILL.md` + `references/` 下所有文件一起上传到知识库（含 `references/guizang-ppt-skill/`，PPT 模板要一起传）。

### Stage 4 可视化的两种交付形态

可视化阶段进入时先让用户选交付物：

- **形态 A — 楼层滚动深度报告（HTML）**：多页楼层 + Snap Scroll + 两层导航，适合深读 / 评审 / 长期资产。走原有 Step 4.1～4.4。
- **形态 B — 横向翻页演讲 PPT（单文件 HTML）**：适合分享 / 路演 / 发布，委派内置的 `references/guizang-ppt-skill/` 生成（电子杂志风 / 瑞士国际主义风）。走 Step 4.PPT。
- **形态 C — 两者都要**：先 A 后 B，PPT 内容取自楼层报告核心结论。

PPT 路径不自己手写，直接调 guizang-ppt-skill 的模板（`assets/template.html` / `assets/template-swiss.html`）与风格规范。guizang 的来源标识只用于确认 skill 来源，不写进生成的 PPT 页面。

## 两个源版本

### original_skill（时昕昱）
- 5 阶段线性流程，专注 UX 视角
- 强项：HTML 报告视觉规格（Mockup、配色、导航）、TypeScript 开发规格
- 适合：已知要做 UX 分析、需要高质量 HTML 报告

### competitive-analysis-bufan（卜凡）
- 4 阶段模块化，多视角（PM/UX/UI/Tech/Strategy）
- **原版**仅支持 Markdown/对话流输出，无 HTML 可视化；当前文件夹内已融入 original_skill 的可视化能力
- 强项：交互流程控制、信息搜集方法论、长期跟踪支持
- 适合：需要过程可控、分析视角多样的场景

## 扩展示例

`skill_used_report/芯片算子领域竞品分析Skill.md` 是一个领域特定扩展，展示了如何基于通用 Skill 定义行业特有的触点框架（芯片/算子领域的 16 个触点）。可以参考这个思路为其他垂直领域做类似扩展。

## 使用指南 HTML（skill-usage-guide.html）

对外展示用的使用说明页面，部署在 GitHub Pages。覆盖内容：

- **三种使用方式**：方式 A（Claude Code CLI）、方式 B（VS Code / JetBrains IDE 插件）、方式 C（Claude.ai 网页版，个人用）
- **三种分析模式**：快速摸底（15–30 min）、标准分析（1–3 h）、完整可视化（3–6 h）
- **四个阶段**：Stage 1 规划 → Stage 2 搜集 → Stage 3 分析 → Stage 4 可视化，含全部 10 个 Human-in-the-Loop 检查点
- **五种分析视角**：UX / PM / UI / Tech / Strategy，各自对应的分析维度和报告骨架类型

**维护规则**：对 `competitive-analysis-merged/` 下的 Skill 内容有任何变动，必须同步更新 `skill-usage-guide.html`。

## 融合分析报告（skill-improvement-report.html）

记录两版 Skill 的差异对比、融合策略、改动前后流程对比，供内部参考。深色蓝紫渐变主题（`#0a0a0a` 底色，`linear-gradient(135deg, #818cf8, #d946ef)` 主色调）。
