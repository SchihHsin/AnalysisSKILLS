# Stage 4 — 可视化报告框架

本文档定义了竞品分析可视化报告的骨架类型、表达模式库、设计系统和技术规格。

> **职责边界**：可视化阶段只负责把 Stage 3 的结构化产物渲染为多页 HTML 报告。**不做新的分析、不补漏数据**。数据不全先回 Stage 3 补齐，不要在可视化阶段编造内容凑页面。

## 1. 何时进入可视化阶段

需要可视化报告的典型场景：
- 设计评审 / 跨团队对齐 / 高管汇报
- 对外分享（行业沙龙、客户展示）
- 长期参考资产（团队 wiki、设计系统知识库）

不需要可视化报告的场景：
- 内部快速决策 / 开发自用 / 研究笔记 → Markdown 报告已足够
- 数据不全、还在持续搜集中 → 等数据稳定再生成

## 2. 报告骨架类型（进入前先选型）

**用户旅程图不是所有报告的默认主脊。** 进入 Stage 4 的第一步是根据 Stage 3 的主导分析角色，选择对应的报告骨架类型。骨架决定：index.html 的组织逻辑、内容页的分组方式、导航的标签命名。

| 骨架类型 | 主导角色 | index.html 主脊 | 内容页分组单元 | 综合页 |
|---------|---------|----------------|--------------|-------|
| **S1 体验旅程型** | UX | 用户旅程地图（情绪曲线主线） | 旅程阶段 → 交互触点 | 设计洞察 |
| **S2 功能全景型** | PM | 产品概要对比矩阵（定位/用户/价值主张） | 功能域/能力类别 | 决策要点 |
| **S3 设计语言型** | UI | 视觉身份总览（第一印象并排） | 设计层级（视觉/信息/交互/动效） | 设计决策洞察 |
| **S4 能力架构型** | Tech | 能力雷达总览（多维评分主脊） | 技术能力域 | 技术决策要点 |
| **S5 竞争格局型** | Strategy | 市场定位图谱（竞争格局主脊） | 分析视角（市场/产品/用户/增长） | 战略机会点 |

### 骨架组合

骨架可以有机组合，不必强选一种。**组合规则**：

- **主骨架**：决定 `index.html` 的主脊内容和一级导航的组织逻辑
- **次骨架**（可多个）：贡献特定内容页或内容页内的分析视角，不改变主脊

**常见组合及适用场景**：

| 主骨架 | 次骨架 | 次骨架贡献内容 | 典型场景 |
|-------|-------|-------------|---------|
| S2 功能全景型 | + S1 | 关键流程触点对比页（`tp-*.html`） | PM 主导但分析体验差异 |
| S1 体验旅程型 | + S3 | 视觉/组件层对比页（`layer-*.html`） | UX 报告附设计系统基础 |
| S5 竞争格局型 | + S2 | 功能域深度对比页（`cat-*.html`） | 战略分析需功能层佐证 |
| S5 竞争格局型 | + S1 | 关键产品触点作为案例（`tp-*.html`） | 对外汇报需要具体案例支撑 |
| S4 能力架构型 | + S1 | 核心开发者流程体验对比（`tp-*.html`） | 技术分析同时关注开发者旅程 |
| S4 能力架构型 | + S2 | 功能覆盖对比页（`cat-*.html`） | 技术评估需横向功能对比 |

**组合时的导航设计**：
- 主骨架的分组单元做一级 Tab
- 次骨架贡献的页面归入相关一级 Tab 下（作为二级条目），或作为独立的综合 Tab
- 一级 Tab ≤ 5 个；次骨架内容宁可合并为 1 个 Tab，不要无限扩张

**组合时的文件命名**：主骨架命名约定优先，次骨架贡献的页面保留各自命名约定（如 `cat-*.html` 和 `tp-*.html` 可在同一目录共存）。

### S1 — 体验旅程型（UX 主导）

**组织逻辑**：以用户完成核心任务的旅程为主线，触点是最小分析单元。  
**需要来自 Stage 3 的产物**：用户旅程地图（阶段/行为/触点/情绪曲线/摩擦+机会）+ 触点级分析 + 设计洞察  
**index.html 主脊**：用户旅程地图，4行结构（用户行为 / 关键触点 chip / 情绪曲线 / 摩擦+机会），触点 chip 可点击跳转  

```
index.html          # 封面 + 旅程地图
tp-{stage}.html     # 每个旅程阶段，含该阶段下各触点（P1/P2/P5）
highlights.html     # 跨触点设计洞察（P8）+ 推荐方向（P9，如需）
```

### S2 — 功能全景型（PM 主导）

**组织逻辑**：以产品能力版图为主线，功能域是分析单元；关注覆盖广度、定价结构、商业模式差异。  
**需要来自 Stage 3 的产物**：产品定位/用户画像对比 + 功能覆盖分析（按域分类）+ 定价/商业模式分析 + 决策洞察  
**index.html 主脊**：产品概要对比矩阵（各产品一列，行 = 定位/目标用户/核心价值/商业模式/定价层级）

```
index.html            # 封面 + 产品概要对比矩阵
cat-{category}.html   # 每个功能域（如：内容创作/协作/集成/管理），含 P4 覆盖矩阵 + P1 深度对比
highlights.html       # 关键决策洞察（P8）+ 功能差距机会（P9）
```

### S3 — 设计语言型（UI 主导）

**组织逻辑**：以设计系统层级为主线，从视觉基础到交互细节逐层对比。  
**需要来自 Stage 3 的产物**：设计语言描述（色彩/字体/间距）+ 组件/模式对比 + 交互行为分析 + 设计洞察  
**index.html 主脊**：视觉身份总览（各产品第一印象并排，含色彩系统/字体/整体风格关键词）

```
index.html            # 封面 + 视觉身份总览（P6 设计语言图板）
layer-visual.html     # 视觉基础层：色彩系统 / 字体 / 图标 / 插图风格（P6/P2）
layer-component.html  # 组件层：核心 UI 组件对比（P2 并排 Mockup）
layer-motion.html     # 交互/动效层：反馈时机 / 过渡方式 / 微交互（P2/P5，如有数据）
highlights.html       # 设计决策洞察（P8）
```

### S4 — 能力架构型（Tech 主导）

**组织逻辑**：以技术能力域为主线，API/集成点是分析单元；关注能力边界、开发者体验、性能差异。  
**需要来自 Stage 3 的产物**：能力评分（可量化）+ API/集成分析（按域分类）+ 性能/限制对比 + 技术洞察  
**index.html 主脊**：能力雷达总览（P10 雷达图，各维度评分可视化）

```
index.html          # 封面 + 能力雷达总览（P10）
cap-{domain}.html   # 每个技术域（如：认证/数据/集成/性能），含 P4 覆盖矩阵 + P1 深度对比
highlights.html     # 技术决策洞察（P8）+ 选型建议（P9，如需）
```

### S5 — 竞争格局型（Strategy 主导）

**组织逻辑**：以市场格局为主线，从宏观定位到微观差异化逐层展开。  
**需要来自 Stage 3 的产物**：定位分析（可量化为坐标）+ 竞争策略对比 + 用户声音/市场反馈 + 战略洞察  
**index.html 主脊**：市场定位图谱（P3 定位图，以最有价值的两个维度做主轴）

```
index.html            # 封面 + 市场定位图谱（P3）
lens-market.html      # 市场/增长视角：TAM/定价策略/增长路径（P1/P3）
lens-product.html     # 产品/功能视角：差异化特性/护城河（P4/P1）
lens-user.html        # 用户视角：用户声音/情感分布/NPS 等（P7/P10）
highlights.html       # 战略机会点洞察（P8）+ 差异化建议（P9）
```

## 3. 输出物理结构

文件结构由骨架类型决定，上方 §2 已给出每种骨架的文件命名约定。通用结构：

```
reports/{project}-{date}-visual/
├── index.html          # 封面 + 主脊页（内容由骨架类型决定）
├── shared.css          # 共享样式（颜色变量、字体、楼层、组件类）
├── nav.js              # 全局导航逻辑（两层 Tab、hash 同步、键盘）
├── {content}.html      # 内容页 × N（命名约定由骨架类型决定）
├── highlights.html     # 综合洞察页（所有骨架类型均有）
├── dev-spec.html       # 开发规格（可选）
├── sharing-slides.html # 经验分享版（可选）
└── assets/
    ├── img/            # 产品截图、对比图
    └── icons/          # SVG 图标库
```

**何时拆多文件 vs 单文件**：
- 内容页 ≤ 3 个 + 不需要分发 → **单文件 HTML**（所有内容塞进 index.html，CSS/JS 内联）
- 内容页 4 个以上 → **按骨架类型的分组单元拆文件**
- 内容页 > 10 个 → 考虑是否需要三层导航或拆子项目

## 4. 表达模式库（内容驱动）

**核心原则：格式服务内容，不是内容填充格式。** 每个洞察/触点，先问「最清晰的表达方式是什么」，再从模式库里选工具。同一份报告中不同页面可以用不同模式——这是优点，不是不一致。

### 4.0 骨架选型 + 封面（必做）

**第一步永远是骨架选型**，对应 §2 的五种骨架类型（S1–S5）。骨架决定 index.html 的主脊内容、所有内容页的分组方式、导航 Tab 的标签命名。

**封面页（所有骨架通用，index.html 第一屏）**：项目名 + 一句话副标题 · 分析日期/版本号 badge · 竞品 logo 列阵 · 「开始阅读 ↓」CTA。不要堆指标卡片，封面就该让人立刻知道这是什么报告。

**主脊页（index.html 第二屏起，由骨架类型决定）**：

| 骨架 | 主脊内容 | 链接单元 → 目标文件 |
|------|---------|-------------------|
| S1 UX | 用户旅程地图（行为 / 触点 chip / 情绪曲线 / 摩擦+机会） | 触点 chip → `tp-*.html#tp-id` |
| S2 PM | 产品概要对比矩阵（定位 / 目标用户 / 核心价值 / 商业模式 / 定价层级） | 功能域 chip → `cat-*.html` |
| S3 UI | 视觉身份总览（各产品第一印象并排 + 关键词） | 设计层级 tab → `layer-*.html` |
| S4 Tech | 能力雷达总览（P10 雷达图，各维度评分） | 技术域 chip → `cap-*.html` |
| S5 Strategy | 市场定位图谱（P3 定位图，两轴展开） | 分析视角 tab → `lens-*.html` |

**关键交互**：主脊页的链接单元必须 100% 跳得通，这是整个报告的主导航入口。

---

其余内容页从下方模式库（§4.3）中选取最合适的表达形式。

### 4.1 角色视角 → 分析维度

骨架确定后，再用下表确定各模式内部的具体分析维度。不同角色使用同一模式（如 P1 对比表），写的行维度和 P10 雷达图的轴完全不同：

| 角色视角 | 优先模式 | P1 对比表的典型行维度 | P10 雷达图的典型轴 |
|---------|---------|-------------------|--------------------|
| **PM** | P4 覆盖矩阵、P3 定位图谱、P1 | 价格档位 · 免费配额 · 付费转化门槛 · 团队协作 · 企业级功能 | 功能完整度 · 定价竞争力 · 扩展性 · 生态丰富度 · 上手门槛 |
| **UX** | P5 任务流对比、P2 并排 Mockup、P1 | 步骤数 · 错误恢复路径 · 空态设计 · 帮助引导 · 操作反馈时机 | 任务完成效率 · 错误容忍度 · 新手友好度 · 一致性 · 情感质量 |
| **UI** | P6 设计语言图板、P2 并排 Mockup、P8 | 视觉密度 · 颜色语义 · 组件风格 · 动效哲学 · 信息层级策略 | 视觉一致性 · 品牌辨识度 · 信息密度 · 交互精致度 · 可访问性 |
| **Tech** | P4 覆盖矩阵（API 维度）、P1、P10 | 认证方式 · API 速率限制 · SDK 覆盖语言 · Webhook 支持 · 文档完整度 | 能力广度 · 性能/延迟 · 可靠性 · 开发者体验 · 集成生态 |
| **Strategy** | P3 定位图谱、P7 用户声音墙、P10 | 目标用户段 · 增长策略 · 商业模式 · 定价杠杆 · 社区/生态 | 市场覆盖度 · 品牌认知度 · 护城河强度 · 增长潜力 · 差异化程度 |

**多角色混合时**：次要角色的维度可作为内容页的补充行，但不要让一张对比表同时承载 PM + Tech + UX 的所有维度——那是三张表的内容，不是一张。

### 4.2 洞察类型 → 模式选择

每个触点/洞察，先判断核心信息是什么，再选模式：

| 洞察类型 | 最需要回答的问题 | 推荐模式 |
|---------|--------------|---------|
| 多产品在同一维度有不同解法 | 各家具体怎么做？优劣是什么？ | **P1** 多产品对比表 |
| 视觉/界面差异本身是洞察 | 这两种界面长什么样？取舍是什么？ | **P2** 并排 Mockup + 标注 |
| 产品在某轴上各有哲学取舍 | 各家处于什么定位？ | **P3** 定位图谱 |
| 关注功能覆盖的广度 | 谁有谁没有？覆盖度多少？ | **P4** 功能覆盖矩阵 |
| 完成同一任务的路径步骤不同 | 流程长度/断点/聚合点在哪里？ | **P5** 任务流对比 |
| 设计语言/视觉系统本身是主题 | 色彩/字体/间距/组件风格有什么取舍？ | **P6** 设计语言图板 |
| 用户反馈/情感分布是证据 | 真实用户怎么说？正负集中点在哪？ | **P7** 用户声音墙 |
| 某条洞察是跨触点综合结论 | 背后的 why + 如何复用？ | **P8** 洞察卡片 |
| 需要形成设计决策/行动建议 | 我们应该怎么做？ | **P9** 推荐方向页 |
| 多维度综合评分对比 | 各家在多个维度上的相对强弱？ | **P10** 雷达图 |

**不要**因为「上一个触点用了对比表」就把所有触点都塞进对比表——每次都从洞察本身出发选模式。

### 4.3 模式规格

---

#### P1 多产品对比表

**适用**：多产品在同一触点的做法需要逐维度对齐比较；各家解法差异在「机制和取舍」层面，而非视觉层面。  
**约束**：单楼层行数 ≤ 6（含表头）；超出则拆为两屏。

```html
<section class="floor" id="{tp-id}">
  <header class="floor-head">
    <span class="tp-id">{tp-id}</span>
    <h2>{触点名}</h2>
    <p class="tp-context">阶段：{阶段} · 维度：{维度}</p>
  </header>
  <div class="floor-body">
    <table class="cmp">
      <thead>
        <tr>
          <th class="row-label"></th>
          <th><span class="ph-name">{产品A}</span><span class="ph-sub">{做法一句话}</span></th>
          <!-- 每个产品一列 -->
        </tr>
      </thead>
      <tbody>
        <!-- 行维度来自 Stage 3 的分析角度，不要硬套固定集合 -->
        <!-- 示例维度：可以是「错误处理/空态/帮助引导」，也可以是「定价策略/用户门槛」 -->
        <tr><th>{分析维度1}</th><td><!-- mockup 或文字 --></td><td>...</td></tr>
        <tr><th>{分析维度2}</th><td>...</td><td>...</td></tr>
        <tr class="pros"><th>优势</th><td>+ ...<br>+ ...</td><td>...</td></tr>
        <tr class="cons"><th>劣势</th><td>− ...<br>− ...</td><td>...</td></tr>
        <tr class="summary"><th>一句话总结</th><td>...</td><td>...</td></tr>
      </tbody>
    </table>
  </div>
  <footer class="tension">
    <strong>核心张力：</strong>{设计矛盾} · <strong>推荐：</strong>{方向}
  </footer>
</section>
```

> 维度行由 Stage 3 的分析决定，不强制「界面形态/核心机制/优势/劣势/一句话总结」这五行。同一张表内所有产品使用相同的维度集合；「无此功能」是合法值，必须显式写出。

---

#### P2 并排 Mockup + 标注

**适用**：视觉差异本身是洞察——对比表的文字无法替代视觉证据；各产品界面形态明显不同且背后取舍明确。  
**约束**：最多 3 个产品并排；超过 3 个改用 P1 对比表。

```html
<section class="floor cmp-visual" id="{tp-id}">
  <header class="floor-head">
    <h2>{触点名} — 视觉对比</h2>
  </header>
  <div class="floor-body cols-{N}">
    <div class="col">
      <div class="label-top">{产品A}</div>
      <!-- mockup 变体（见 §7）-->
      <p class="annotation"><strong>{做法核心}</strong> — {取舍说明，一句话}</p>
    </div>
    <!-- 每个产品一列 -->
  </div>
  <footer class="tension">
    <strong>核心张力：</strong>{设计矛盾} · <strong>推荐：</strong>{方向}
  </footer>
</section>
```

---

#### P3 定位图谱

**适用**：产品之间存在明显的哲学/市场/体验取向差异，可以用两条轴描述（Strategy/PM 视角常见）。  
**例**：X 轴「自动化←→可控性」，Y 轴「面向个人←→面向团队」。

```html
<section class="floor" id="positioning">
  <header class="floor-head">
    <h2>{维度1} × {维度2} 定位图谱</h2>
    <p class="tp-context">{说明两轴的含义及评判依据}</p>
  </header>
  <div class="floor-body positioning-layout">
    <svg class="positioning-map" viewBox="0 0 600 400">
      <line x1="40" y1="200" x2="560" y2="200" class="axis"/>
      <line x1="300" y1="20" x2="300" y2="380" class="axis"/>
      <text x="560" y="195" class="axis-label axis-right">{X正向}</text>
      <text x="40"  y="195" class="axis-label axis-left">{X负向}</text>
      <text x="300" y="18"  class="axis-label axis-top">{Y正向}</text>
      <text x="300" y="395" class="axis-label axis-bottom">{Y负向}</text>
      <g class="product-dot">
        <circle cx="{x}" cy="{y}" r="10"/>
        <text dx="14" dy="4">{产品A}</text>
      </g>
      <!-- 每个产品一个点 -->
    </svg>
    <p class="map-insight">{一句话说明图谱的核心发现}</p>
  </div>
</section>
```

---

#### P4 功能覆盖矩阵

**适用**：PM 视角，关注功能覆盖广度（谁有谁没有）而非各家做法深度。  
**符号**：✓ 有 / △ 部分/有限 / — 无。

```html
<section class="floor" id="coverage-{domain}">
  <header class="floor-head">
    <h2>{功能域} 覆盖矩阵</h2>
  </header>
  <div class="floor-body">
    <table class="coverage-matrix">
      <thead>
        <tr>
          <th>功能</th>
          <th>{产品A}</th><th>{产品B}</th><th>{产品C}</th>
        </tr>
      </thead>
      <tbody>
        <!-- 功能点分组时用 <tr class="group-header"><td colspan="N">{分组名}</td></tr> -->
        <tr>
          <td class="feat-name">{功能点}</td>
          <td class="yes">✓</td><td class="partial">△</td><td class="no">—</td>
        </tr>
      </tbody>
    </table>
  </div>
</section>
```

---

#### P5 任务流对比

**适用**：UX 视角，核心洞察是「完成同一任务，各家步骤数/路径/断点差异显著」。  
**布局**：每个产品一行，横向铺步骤气泡；断点用红色，聚合/简化点用绿色标出。

```html
<section class="floor" id="flow-{task}">
  <header class="floor-head">
    <h2>{任务名} — 路径对比</h2>
    <p class="tp-context">{说明起点与终点的定义}</p>
  </header>
  <div class="floor-body flow-rows">
    <div class="flow-row">
      <span class="flow-label">{产品A}</span>
      <div class="steps">
        <div class="step">{步骤1}</div>
        <div class="step friction">{摩擦点}</div>
        <div class="step">{步骤N}</div>
      </div>
    </div>
    <!-- 每个产品一行 -->
  </div>
  <p class="flow-summary">{结论：步骤数对比 + 关键断点位置}</p>
</section>
```

---

#### P6 设计语言图板

**适用**：UI 视角，对比对象是「设计系统/视觉语言」本身（色系、字体、间距、组件风格、动效哲学）。  
**布局**：每个产品一列，每行一个设计维度。

```html
<section class="floor" id="design-language">
  <header class="floor-head">
    <h2>设计语言对比</h2>
  </header>
  <div class="floor-body lang-grid cols-{N}">
    <div class="lang-col">
      <div class="brand-label">{产品A}</div>
      <div class="color-swatches">
        <span class="swatch" style="background:{hex}" title="{色彩语义}"></span>
      </div>
      <div class="type-sample" style="font-family:{font}">{字体样本文字}</div>
      <div class="comp-sample"><!-- 核心组件 CSS 实现 --></div>
      <div class="keywords">{关键词标签，如「极简/严肃/工具感」}</div>
    </div>
  </div>
</section>
```

---

#### P7 用户声音墙

**适用**：关键洞察来自用户反馈（评论/评测/社区讨论），情感分布本身是分析证据。  
**布局**：引言卡片网格，按情感（正向/负向）或主题分组。

```html
<section class="floor" id="user-voice-{product}">
  <header class="floor-head">
    <h2>{产品} 用户声音 — {主题}</h2>
  </header>
  <div class="floor-body quotes-grid">
    <div class="quote-card positive">
      <p class="q-text">"{引文}"</p>
      <span class="q-source">{来源平台} · {日期}</span>
    </div>
    <div class="quote-card negative">
      <p class="q-text">"{引文}"</p>
      <span class="q-source">{来源平台} · {日期}</span>
    </div>
  </div>
  <p class="voice-summary">{一句话总结情感分布的核心发现}</p>
</section>
```

---

#### P8 洞察卡片（Highlight）

**适用**：跨触点综合洞察，一条洞察本身就是一屏的主角；区别于触点对比页（那是「这个触点各家怎么做」，这是「有一条规律贯穿多个触点」）。

```html
<section class="floor highlight" id="hl-{N}">
  <div class="hl-num">0{N}</div>
  <div class="hl-body">
    <h2>{亮点标题：一句话说清价值}</h2>
    <p class="why">{为什么重要——设计原理或用户价值，不是描述「是什么」}</p>
    <div class="evidence">
      <!-- 视觉证据：mockup 变体 / 截图 / 对比图 -->
    </div>
  </div>
</section>
```

**入选标准**（同时满足三条）：
1. 解决了旅程中的关键摩擦点（呼应情绪曲线低谷）
2. 与竞品有明显差异化（不是行业人均都做的事）
3. 背后有可解释的设计原理（不是「碰巧好看」）

---

#### P9 推荐方向页

**适用**：基于洞察形成设计决策建议，让报告回答「我们应该怎么做」。内部研究/纯学习目的可省略；需要推动落地时必须有。  
**布局**：左栏核心理念 + 建议列表（因为/所以结构），右栏推荐方案 mockup。

```html
<section class="floor proposal" id="proposal-{scope}">
  <header class="floor-head">
    <h2>{触点/场景} — 推荐方向</h2>
  </header>
  <div class="floor-body two-col">
    <div class="col-left">
      <p class="principle">{核心理念，一句话定调}</p>
      <ol class="suggestions">
        <li><strong>{建议1}</strong>——因为 {理由}，所以 {预期效果}</li>
        <!-- 3 条具体建议 -->
      </ol>
    </div>
    <div class="col-right">
      <!-- 推荐方案的多状态 mockup（idle / active / done / failed 等） -->
    </div>
  </div>
</section>
```

---

#### P10 雷达图

**适用**：多维度综合评分比较（5-8 个维度），每个维度可量化或可评级。  
**警告**：只在维度间确实可以用统一量级评分时用；否则对比表更诚实。

```html
<section class="floor" id="radar-{scope}">
  <header class="floor-head">
    <h2>{分析域} 综合评分</h2>
    <p class="tp-context">{评分维度说明及1-5分标准}</p>
  </header>
  <div class="floor-body radar-layout">
    <svg class="radar" viewBox="0 0 400 400">
      <!-- 网格线、轴线（N条）、标签、polygon per product -->
    </svg>
    <div class="radar-legend">
      <!-- 每个产品色块 + 名称 + 总分 -->
    </div>
  </div>
</section>
```

---

### 4.6 开发规格页（可选）

为前端可直接落地的关键组件提供规格：

```typescript
interface {ComponentName} {
  // Props
  prop1: Type;       // 默认值，含义
  prop2?: Type;      // 可选

  // Events
  onChange?: (value: Type) => void;
}

// 状态机
type Status = 'idle' | 'active' | 'done' | 'failed';

// 状态转移表
// 事件         | 触发条件        | 转移到     | 副作用
// submit       | input ≠ ''      | active     | 调用 API
// success      | API 200         | done       | 显示结果
// error        | API !2xx        | failed     | 显示错误 + 重试按钮
```

**必含部分**：
- Props 列表（类型 + 默认值 + 说明）
- 事件签名
- 状态机（所有状态 + 转移条件 + 副作用）
- 边界条件（空态、加载中、错误、超长输入、网络断开等）

### 4.7 经验分享页（可选）

只在需要对外分享时做。结构通常是：
1. 一张图说清核心发现
2. 3 个最反直觉的洞察
3. 一句话行动呼吁

不要塞太多——分享版本是「最浓缩 5 分钟」，不是完整报告的复刻。

## 5. 设计系统

### 5.1 配色（CSS 变量统一管理）

### 默认主题改为「浅色」

**默认**：暖白背景 + 深色文字 + 符合分析主题的单一点缀色

### 仅在以下情况选用暗色

- 用户**显式**要求"深色 / dark theme"
- 单页着重视觉冲击（如发布会预览图）

### 浅色 token 示例
```css
:root {
  /* 背景层 */
  --bg:        #f7f5ef;   /* 主背景：暖白偏奶油，避免纯白刺眼 */
  --bg-soft:   #efece4;   /* 次级背景：用于行标签、信号区 */
  --bg-card:   #ffffff;   /* 卡片纯白：拉开层级 */
  --bg-mockup: #1a1a1d;   /* 终端 mockup 保持深色：唯一的暗区，制造质感对比 */

  /* 文字层（4 级层次） */
  --ink:    #14141a;       /* 标题、强调文字 */
  --ink-2:  #4a4a55;       /* 正文 */
  --ink-3:  #7a7a85;       /* 辅助说明 */
  --ink-4:  #a8a8b0;       /* 占位、最弱信息 */

  /* 边线（3 级） */
  --line:        #e0ddd2;  /* 标准边线 */
  --line-soft:   #ebe8de;  /* 软边线（次级分隔） */
  --line-strong: #1a1a1d;  /* 强边线（顶部装饰线） */

  /* 唯一点缀色：单一暖色或单一冷色，不混用 */
  --primary:      #b8412c;        /* 推荐：deep terra-cotta 编辑感强 */
  --primary-soft: rgba(184, 65, 44, 0.08);
}
```

### 关键反模式（要避免的）

❌ **不要**：浅色页面里散布多种亮色点缀（紫+蓝+绿+红+橙），会显廉价
✅ **要**：浅色 + 1 个暖色点缀 + 状态色（仅在需要时用），保持编辑性
❌ **不要**：浅色背景 + 浅色卡片（无层次）
✅ **要**：浅色页面背景 + 纯白卡片 + 深色 mockup，三层对比清晰


### 5.2 字体

```css
:root {
  --font-sans: 'Inter', -apple-system, 'Segoe UI', sans-serif;
  --font-mono: 'JetBrains Mono', 'SF Mono', Menlo, monospace;
  --font-cn: 'PingFang SC', 'Microsoft YaHei', sans-serif;

  /* 字号阶梯 */
  --t-1: 12px;        /* 元数据、tag */
  --t-2: 14px;        /* 正文、表格 */
  --t-3: 16px;        /* 强调正文 */
  --t-4: 20px;        /* 小标题 */
  --t-5: 28px;        /* 楼层标题 */
  --t-6: 40px;        /* 主标题 */
  --t-7: 64px;        /* 数字标号（亮点页） */
}
```

最小可读正文 **12px**，不要再小。

### 5.3 图标系统（无 emoji）

**全部使用 SVG 线性图标**：
- viewBox: `0 0 24 24`
- stroke-width: `1.5`
- stroke-linecap: `round`
- stroke-linejoin: `round`
- fill: `none`

**唯一例外**：终端 Mockup 内部保留 ASCII 字符（`❯ ✔ ✗ ⠿ ⠋`）作为终端美学的一部分——这些不是 emoji，是 Unicode 字符，与终端实际行为吻合。

不要在正文里堆 🚀 ✨ 🎯 这类装饰性 emoji——会让报告显得不专业。

## 6. 技术规格

### 6.1 楼层（Snap Scroll）

**核心原则**：每楼层 = 一屏视口
**反模式**：不要让任何楼层超过 100vh。如果内容溢出，要么拆成两屏，要么压缩内容——可视化报告的阅读节奏靠 snap 维持，溢出会破坏节奏。


### 楼层布局规范:
```css
.floor {
  min-height: calc(100vh - 88px);  /* 减去 sticky topnav 高度 */
  max-width: 1480px;
  margin: 0 auto;
  padding: 48px 32px;
  display: flex;
  flex-direction: column;
}
.floor-head { flex-shrink: 0; }     /* 标题区不压缩 */
.floor-body { flex: 1; display: flex; flex-direction: column; min-height: 0; }
```

### 内容密度的硬约束

每楼层在 **1440 × 900** 视口下应可一屏显示，不需要垂直滚动。这要求：

| 内容类型 | 单楼层最大量 |
|---|---|
| 文字段落 | 不超过 4 段，每段 ≤ 3 行 |
| 表格行数 | 不超过 8 行（含表头） |
| 卡片数量 | 4 列时 ≤ 8 个，3 列时 ≤ 6 个，2 列时 ≤ 4 个 |
| Mockup 数量 | 单楼层最多 1 个大 mockup + 1-2 个小 mockup |

**违反约束 = 拆分到下一楼**。不要硬塞。

### 视口适配的 3 个常见错误

❌ **错误 1**：用 `height: 100vh` 而非 `min-height` —— 会强制截断长内容
✅ **正确**：`min-height: 100vh`，允许长内容自然溢出但提示用户继续滚动

❌ **错误 2**：内部容器无 `min-height: 0` —— Flex 子元素会撑破父容器
✅ **正确**：`.floor-body { flex: 1; min-height: 0; }`

❌ **错误 3**：固定字体大小 + 太多内容 —— 1280px 屏幕直接溢出
✅ **正确**：用 `clamp()` 或在媒体查询中调整字号

---


### 6.2 两层导航 Tab

```
┌─────────────────────────────────────────────────┐
│ [阶段1]  [阶段2]  [阶段3]  [阶段4]  [阶段5]      │  ← 第一层（旅程阶段）
├─────────────────────────────────────────────────┤
│  [触点A] [触点B] [触点C] [触点D]                  │  ← 第二层（当前阶段下的触点）
└─────────────────────────────────────────────────┘
```

**行为规格**：
- 阶段 Tab 切换 → 跳转到对应 `tp-{stage-id}.html` 文件
- 触点 Tab 跟随**滚动位置自动高亮**当前可见触点
- 点击触点 Tab → 平滑滚动到该触点页
- 当前位置同步到 URL hash（`#tp-03-a`），刷新和分享链接稳定

### 顶部 sticky 双行 tab

```html
<nav class="topnav">
  <div class="topnav-inner">
    <!-- 第一行：页面级 tab -->
    <div class="topnav-row phase">
      <span class="topnav-meta">project · date</span>
      <a class="topnav-tab" data-page="index.html" href="index.html">00 · 概览</a>
      <a class="topnav-tab" data-page="tp-overview.html" href="tp-overview.html">01 · 全景对比</a>
      <!-- ... -->
    </div>
    <!-- 第二行：楼层级 tab（hash 锚点） -->
    <div class="topnav-row sub">
      <span class="topnav-meta">本页</span>
      <a class="topnav-tab" href="#f1">f1 · 标题</a>
      <a class="topnav-tab" href="#f2">f2 · 标题</a>
    </div>
  </div>
</nav>
```

### nav.js 
1. 自动高亮当前页 phase tab（基于 `data-page` 与 `location.pathname`）
2. 自动同步 sub tab 与 hash（hashchange + IntersectionObserver）
3. 平滑滚动到楼层（点击 sub tab）
4. 方向键支持（↑↓/jk/PgUp/PgDn）切换楼层
5. 输入框聚焦时禁用方向键劫持

**Anti-pattern**:   
❌ **不要**：把所有内容塞在一个长滚动页面里靠右侧浮动小圆点导航
✅ **要**：编辑性报告用顶部双行 tab，可点击、可键盘、可分享 hash

### 6.4 跨文件状态保持

- 全局 nav state 写入 `sessionStorage`，跨文件跳转时恢复
- 页面加载时读取 `?from=` 参数，自动滚动到来源触点对应位置（用于「返回上一级」）


## 7. Mockup 变体库

界面形态行的视觉证据可用以下任一变体：

### 7.2 Browser Mockup（Web 应用）

```html
<div class="mw">
  <div class="mwbar">
    <div class="mdt r"></div><div class="mdt y"></div><div class="mdt g"></div>
    <div class="mwurl">https://{domain}/{path}</div>
  </div>
  <div class="mwb">
    <!-- 页面截面，可用 CSS 网格/flex 布局还原 -->
  </div>
</div>
```

### 7.3 Mobile Mockup（移动 App）

```html
<div class="mm">
  <div class="mmnotch"></div>
  <div class="mmscreen">
    <div class="mmstatus">9:41 ●●● 100%</div>
    <!-- App 内容 -->
    <div class="mmbar"></div>
  </div>
</div>
```

宽度通常 280-320px，aspect-ratio 9:19.5。

### 7.4 Component Mockup（裸组件）

只展示组件本身，不带任何 chrome/frame。适用于：按钮、表单、卡片、Toast、Modal 等纯组件级对比。

```html
<div class="mc">
  <!-- 组件 HTML，加 box-shadow 凸显 -->
</div>
```

### 7.5 Mockup 内容原则

1. **展示该产品该触点的最典型状态**——不要展示边缘场景
2. **文字要具体**——不要写「输入框」，要写实际可能出现的文本（如 `❯ 重构 @src/auth.ts` 而非 `❯ 输入指令`）
3. **颜色符合该产品的实际风格**——不要为了好看统一改色
4. **数据要合理**——金额、数量、时间戳要符合实际产品的量级，不要写 `$999999`
5. **展示多状态时用 small multiples**——不要把 idle / loading / error 横着拉一长条

## 8. 质量检查清单（提交前自审）

### 结构完整性
- [ ] 已按 §2 确认骨架类型（S1–S5），封面页就绪
- [ ] 主脊页内容符合骨架类型要求（§4.0 表格对应项）
- [ ] 主脊页的所有链接单元 100% 跳得通（chip / tab → 对应内容页）
- [ ] 每个内容页都有「核心张力 + 推荐方向」（可嵌在页脚或独立推荐页）
- [ ] 所有产品在每个分析单元上都有覆盖——没有「A 页比了 3 家、B 页只比 2 家」
- [ ] 综合洞察（P8 洞察卡片）数量合理（3-10 条，质重于量）

### 模式使用合理性
- [ ] 每个页面的模式选择与洞察类型匹配（回查 §4.2 的选择逻辑）
- [ ] 使用了 P1 对比表的页面：同一表内所有产品使用相同维度行，「无此功能」显式写出
- [ ] 使用了 P2 并排 Mockup 的页面：≤ 3 个产品，标注说明取舍而非只描述外观
- [ ] 使用了 P3/P10 的页面：评分/定位标准在 tp-context 或图注中有说明
- [ ] 如有 P9 推荐方向页：建议有「因为/所以」结构，不只是「推荐 A 方案」一句空话

### 内容质量
- [ ] 每个触点/洞察有视觉证据（mockup 变体、截图或 CSS 实现的组件示意）
- [ ] 洞察卡片（P8）说的是「为什么重要」，而非「是什么」的描述
- [ ] 定位图谱/雷达图（P3/P10）维度有明确的两端定义，不是模糊形容词

### 视觉呈现
- [ ] 全局无装饰性 emoji（终端 Mockup 内的 ASCII 字符除外）
- [ ] 所有楼层 ≤ 100vh，snap scroll 生效（没有内容溢出）
- [ ] 两层导航 Tab 在所有页面正确显示并可交互
- [ ] 若为组合骨架，次骨架贡献的页面已归入合理的导航结构，一级 Tab 总数 ≤ 5 个
- [ ] 字号阶梯一致，最小正文 ≥ 12px

### 一致性
- [ ] 配色使用 CSS 变量，没有硬编码 hex 散落各处
- [ ] 同一模式在不同页面的 CSS class 命名一致（如 `.cmp`、`.highlight`）
- [ ] 优势/劣势格式一致（`+` 绿色 / `−` 红色，单条不超过 20 字）

## 9. 常见问题处理

### Q: 某个产品的某个触点信息搜不到怎么办？
优先重新搜索：官方文档 / GitHub README / 深度评测 / YouTube demo。仍找不到的话，**在该格子写「无公开信息」**，不要猜测——猜测会让整张对比表的可信度归零。

### Q: 某个产品没有这个功能？
这本身就是分析结论。在格子里写「**无此功能**」，在劣势行加一条「缺失该功能，需第三方补充」，在一句话总结里写「该产品不覆盖此触点」。**不要**留空。

### Q: 触点维度划分不确定，怎么判断？
回到 analysis-frameworks.md §1.4 的判断标准：「**不同竞品在这个维度上是否做了不同的设计决策？**」如果答案是否，维度太细（合并）；如果不同竞品的答案无法用同一句话描述，需要拆分。

### Q: 多少个触点合适？
- 极简扫描：3-5 个
- 快速调研：5-8 个
- 完整 UX 研究：15-25 个
- 大规模研究：> 25 个建议拆子项目

### Q: 必须做「推荐方向页」吗？
- 内部研究参考、纯学习 → 可省，只保留对比
- 要形成设计决策依据 → 必须做，否则报告只回答「别人怎么做」，没回答「我们应该怎么做」

### Q: 数据不全能否进入 Stage 4？
**不能**。可视化阶段是渲染层，不补数据。回 Stage 3 补齐再来。硬上的后果是「漂亮但空洞」的报告，比 Markdown 报告还糟。

### Q: 多人协作时如何避免冲突？
按触点拆 `tp-*.html` 文件，每人维护各自的触点页；`shared.css` 由一人统筹（避免样式漂移）；`index.html` 的旅程图最后整合。

### Q: 暗色模式要做吗？
默认不做。除非分享场景特别要求。做了反而要维护两套配色，得不偿失。如要做，全部走 CSS 变量 + `prefers-color-scheme` 媒体查询，不要 JS 切换。

### Q: 移动端要适配吗？
**不强制**。可视化报告默认是桌面阅读场景（>= 1280px）。如果业务上确实需要移动端，最低要做到：
- 楼层在窄屏取消 snap，改为常规滚动
- 触点对比表在窄屏改为垂直堆叠（每个产品一段，而不是横向并列）
- 两层导航 Tab 在窄屏折叠为汉堡菜单
但通常报告类内容在手机上阅读体验差，建议直接提示「请在桌面打开」。
