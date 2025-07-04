# lovers-match 产品功能迭代计划 (基于现有 HTML 架构)

## 核心原则

在保持当前单一 `index.html` 技术架构不变的前提下，通过增强客户端 JavaScript 能力，为网站注入新的活力和深度。所有功能将聚焦于提升用户体验、分析深度和分享传播能力。

---

## V2.0 功能规划

### 1. 功能一：引入"时辰"输入，实现完整"八字"分析 (核心升级)

-   **用户界面 (UI)**:
    -   在"您的生日"和"您伴侣的生日"输入区域，各增加一个"出生时辰"的下拉选择框。
    -   该选项可设为"可选"，如果用户不清楚时辰，可以选择"时辰不详"，系统则回退到当前仅基于"年月日"的分析模式。
-   **计算逻辑 (JavaScript)**:
    -   升级 `calculateCompatibility` 函数，使其能够处理包含"时辰"的完整四柱八字。
    -   引入"日主"（出生日的天干）作为分析核心，这将是命理分析准确性的质的飞跃。
    -   基于完整的八字，分析日主之间的五行生克关系，以及地支的"刑、冲、合、害"等更复杂的关系。
-   **价值**:
    -   **专业性**: 从"生肖配对"升级为真正的"八字合婚"，分析结果更精准、更具深度。
    -   **个性化**: "日主"代表最核心的自我，分析将更贴近用户个体，大大提升说服力。

### 2. 功能二：结果分享与保存 (增强传播力)

-   **功能实现**:
    -   **生成分享链接**: 当用户点击"揭示你们的宇宙连接"后，在结果页面生成一个可复制的URL。这个URL将包含两位用户的生日信息作为查询参数 (e.g., `.../index.html?y1=1990&m1=5&d1=10&h1=8&y2=1992&m2=8&d2=15&h2=20`)。
    -   **通过链接恢复结果**: 当有人打开这个特殊链接时，页面上的JavaScript会自动读取URL中的参数，填充日期选择器，并直接执行计算、展示结果。
    -   **本地保存**: (可选) 提供一个"保存本次记录"按钮，将输入的生日信息存储在浏览器的 `localStorage` 中。用户下次访问时，可以一键"读取上次记录"。
-   **价值**:
    -   **病毒式传播**: 用户可以方便地将自己的配对结果分享给伴侣或朋友，每个用户都可能成为网站的推广者。
    -   **提升用户粘性**: 保存功能方便了用户的重复使用。

### 3. 功能三：结果呈现可视化 (提升体验)

-   **功能实现**:
    -   **八字命盘**: 为双方生成一个简洁的八字命盘图，清晰地展示出年、月、日、时四柱的天干地支。
    -   **五行雷达图**: 使用雷达图 (Radar Chart) 来展示双方五行（金、木、水、火、土）的强弱分布，让互补或相似之处一目了然。
    -   **关系快照**: 除了总分，用标签或小图标的形式快速展示几个关键关系，如"天作之合"、"相冲相克"、"互为贵人"等。
-   **技术选型**: 可以使用轻量级的图表库（如 `Chart.js`）或纯 `CSS/SVG` 来实现，避免引入过重的依赖。
-   **价值**:
    -   **直观易懂**: 图形化展示比纯文字描述更有吸引力，信息传递效率更高。
    -   **美观与分享欲**: 精美的结果页面更能激发用户的分享欲望。

### 4. 功能四：深化分析内容 (增加付费潜力)

-   **功能实现**:
    -   **神煞(Shensha)分析**: 在现有分析基础上，加入对婚恋关系影响较大的几个关键"神煞"，如"桃花"、"红鸾"、"天喜"（正面）以及"孤辰"、"寡宿"（负面），并提供简短的解读。
    -   **关系建议细化**: `getLoveAdvice` 函数可以根据更详细的八字信息（例如，谁的食伤更旺，代表更懂浪漫；谁的比劫更重，代表性格更强）给出更有针对性的建议。
-   **价值**:
    -   **内容为王**: 提供比竞品更深入、更专业的免费内容，建立用户信任。
    -   **未来变现**: 这些更深入的分析可以作为未来推出"专业版报告"或付费解锁内容的基础。

### 5. 功能五：引入 MBTI 匹配度分析 (MVP + 详细功能)

此功能旨在通过引入流行的 MBTI (Myers-Briggs Type Indicator) 匹配分析，拓展产品受众并提供多元化的关系探索视角。

#### 5.1 MVP 功能

-   **用户界面 (UI)**:
    -   在 `index.html` 页面中增加一个"MBTI 匹配度分析"的入口（例如按钮或链接）入口要醒目，可以加入一下动画效果。
    -   用户点击后，通过 JavaScript 切换视图，显示 MBTI 分析界面，隐藏八字分析界面。
    -   MBTI 分析界面包含：
        -   为双方（用户和伴侣）各提供一个 MBTI 类型选择器（下拉菜单或单选）。
        -   一个"计算 MBTI 匹配度"按钮。
        -   一个用于显示匹配结果和简要分析的区域。
-   **计算逻辑 (JavaScript)**:
    -   新增 `calculateMbtiCompatibility(type1: string, type2: string)` 函数。
    -   **匹配算法 (基于简化维度匹配)**:
        -   对比双方 MBTI 类型的四个维度 (E/I, S/N, T/F, J/P)。
        -   每个维度相同（例如，都是 E，都是 S）则视为兼容度加分项。
        -   每个维度相反（例如，一个是 E，一个是 I）则视为中立或轻微减分项，但会强调互补性。
        -   根据匹配结果，给出"兼容"、"中等兼容"、"需要磨合"等简要评语。
        -   不提供具体分数，而是侧重于描述性的兼容性分析。
-   **价值**:
    -   **快速上线**: 以最小开发量验证市场对 MBTI 功能的兴趣。
    -   **拓宽受众**: 吸引对 MBTI 感兴趣的用户群体。

#### 5.2 详细功能

-   **用户界面 (UI)**:
    -   优化 MBTI 类型选择器，可以考虑更直观的卡片选择或分步引导。
    -   结果展示区域增加可视化元素，例如简单的图示或颜色编码来表示不同维度的兼容性。
    -   增加"分享 MBTI 匹配结果"功能，生成包含 MBTI 类型信息的 URL 参数。
    -   (可选) 增加"保存本次 MBTI 记录"功能到 `localStorage`。
-   **计算逻辑 (JavaScript)**:
    -   **匹配算法 (结合现有兼容性图表或更细致的理论)**:
        -   研究并整合网上流传的、更详细的 MBTI 兼容性理论或图表（例如，BrainManager 或 MyPersonality 提供的图表）。
        -   根据这些资料，实现更精细的匹配度评分（例如 0-100 分），或更具体、多层次的兼容性描述。
        -   为每种 MBTI 类型组合提供更详细的解读，包括优点、潜在挑战和关系建议。
    -   **个性化建议**: 针对不同 MBTI 组合，提供更深入的、可操作的关系建议，例如沟通技巧、冲突解决策略等。
-   **价值**:
    -   **深度体验**: 提供更专业、有深度的 MBTI 匹配分析。
    -   **提升分享欲**: 丰富的可视化和详细解读能促进用户分享。
    -   **数据积累**: 为未来可能的付费高级分析奠定基础。 