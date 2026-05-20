# AnalysisSKILLS

这个仓库收录竞品分析相关的 Skill 和报告，供 Claude Code 使用时参考。

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
└── SKILL_guide.md                # original_skill 的使用说明
```

## 主要使用版本

**`competitive-analysis-merged/`** 是融合后的主版本，融合了两个版本的优点：

- **流程结构**：来自 competitive-analysis-bufan 的 4 阶段管道（规划→搜集→分析→可视化），有完整的 Human-in-the-Loop 检查点
- **视角选择**：Stage 1 显性确认分析视角（UX/PM/UI/Tech/Strategy），贯穿全程
- **信息搜集**：competitive-analysis-bufan 的图文采集协议、视频工作流、失败处理策略
- **可视化骨架**：在 original_skill 单一 UX 骨架基础上扩展为 5 种视角骨架（S1-S5）+ 10 种表达模式（P1-P10）
- **开发规格**：original_skill 的 TypeScript 接口 + 状态机格式
- **设计系统**：浅色主题默认（暖白），深色为显式可选

使用时将 `SKILL.md` + `references/` 下所有文件一起上传到知识库。

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
