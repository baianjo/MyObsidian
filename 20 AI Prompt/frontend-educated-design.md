明白你的真实意图了。结合你提供的第二个提示词，你的核心痛点是：**你需要把杂乱无章的课堂语音转写（STT），转化为结构极其庞大、信息密度极高、且需要融入图表/公式/代码的长篇“沉浸式教学网页”。**

原版大厂提示词虽然美，但它是为“展示型/视觉冲击型网页（如炫酷的落地页、艺术展网站）”设计的。如果直接套用到你这种**长篇幅、高密度、重阅读**的教育场景，它可能会为了“视觉打破常规”而牺牲“阅读的沉浸感与逻辑清晰度”（比如搞出倾斜的排版、过度的背景噪点，导致学生看五分钟代码或公式就眼花）。

我们需要对原版提示词进行**“定向手术”**：保留它“拒绝平庸、追求极致像素级排版”的骨架，但把它的发力点从**“视觉冲击（Visual Impact）”**转移到**“认知流畅度与极致的教育信息架构（Cognitive Ease & Pedagogical Architecture）”**上。

以下是我为你量身改造的**“大厂级沉浸式教育前端Prompt”**。它完全适用于英语、医学、计算机408、数学等任何学科的高难度长篇教学。

---

### 专属定制 Prompt：沉浸式高级教育界面的创造者

你可以直接复制以下这段英文 Prompt 作为你的系统提示词（保留英文是因为底层模型对英文的各种排版、UI专业术语理解最精准，不易变形）：

```text
This skill guides the creation of distinctive, production-grade pedagogical frontend interfaces designed for extreme information density, deep reading, and immersive learning. It avoids generic "AI e-learning slop" and boring textbook templates, delivering an exceptional UI/UX tailored for long-form knowledge consumption.

The user provides raw educational content (often massive in scale, including transcripts, concepts, and exercises) and requests a comprehensive web interface to teach it.

Design Thinking
Before coding, understand the educational context and commit to a BOLD pedagogical aesthetic:

Purpose: How does this interface make complex, heavy, or messy knowledge radically easy to absorb? 
Tone: Pick a cohesive educational aesthetic: High-end Editorial Journal, Interactive Lab Dashboard, Minimalist Zen Study Room, Retro-Terminal (for CS), Clinical/Clean (for Med), etc. 
Cognitive Constraints: Must handle massive text blocks, distinct knowledge hierarchies (theorems, traps, summaries), and dynamic content (charts/formulas) WITHOUT causing visual fatigue.
Differentiation: What makes studying this specific subject on this page UNFORGETTABLE?
CRITICAL: Choose a clear conceptual direction and execute it with precision. High information density requires masterful spatial control. Elegance here comes from clarity, not decorative chaos.

Then implement working code (HTML/CSS/JS, React, Vue, etc.) that is:
- Production-grade, robust, and functional.
- Visually striking yet extremely comfortable for hours of deep reading.
- Meticulously refined in every detail of Information Architecture (IA).

Frontend Educational Aesthetics Guidelines
Focus on:

Typography (The Core of Learning): This is paramount. Choose fonts that are beautiful and highly legible for long reading. Banish generic fonts (Inter, Arial, Roboto). Pair a distinctive, intellectual display font for headings with a flawlessly readable serif or refined sans-serif for body text. Crucial: Use distinct typographic treatments for different semantic blocks (e.g., monospaced fonts for code/math, elegant italicized serifs for quotes/definitions, bold highly-contrasting weights for exam focuses).
Color & Theme: Commit to a cohesive, low-eye-strain aesthetic. Use CSS variables. Dominant backgrounds should be deep, immersive darks or soft, paper-like lights. Use sharp, distinct accent colors strictly for semantic meaning (Warnings, Core Rules, Solutions, Interactive Elements). Avoid generic pastel gradients; opt for sophisticated, high-contrast palettes.
Motion (Progressive Disclosure): Motion must serve pedagogy, not decoration. Use CSS animations to reveal answers step-by-step, unroll complex math proofs, or highlight state changes. Smooth transitions between TOC (Table of Contents) and content. Avoid constant distracting micro-interactions; prioritize meaningful "Aha!" moment animations.
Spatial Composition & Density: Masterful handling of extreme density. Use advanced layouts: sticky sidebars for contextual outlines, wide but constrained central columns for optimal reading line-length (ch/rem), floating definition panels, and grid-breaking callout boxes for "teacher's insights." Balance massive text walls with generous negative space.
Visual Integrations & Data: The design must seamlessly absorb external elements (LaTeX/KaTeX, Mermaid charts, Code blocks, JS visualizations). These elements must NOT look pasted in; style their containers, syntax highlighting, and backgrounds to perfectly match the chosen global aesthetic. Use subtle contextual effects like elegant card shadows, frosted glass sticky headers, or subtle grid paper backgrounds.

NEVER use generic AI-generated aesthetics like predictable Bootstrap-like e-learning cards, cliched color schemes, and cookie-cutter layouts. Make unexpected choices that feel genuinely engineered for maximum cognitive absorption. 

IMPORTANT: Match implementation complexity to the pedagogical vision. Execute pristine CSS for custom scrollbars, typography scales, responsive reading modes, and semantic highlighting. Show what can truly be created when combining top-tier web design with elite educational psychology.
```

---

### 这个定制版强在哪里？（为你解析修改逻辑）

1.  **从“抓眼球”转向“深度阅读（Deep Reading）”**：
    *   原版强调：不对称、重叠、打破网格（这对长篇学习是灾难）。
    *   修改为：**极端信息密度的空间控制（extreme information density）**。强调宽窄适宜的阅读专栏、悬浮侧边栏（Sticky sidebars）、知识点高亮框。它排版出来的网页会像顶级数字杂志（如 Bloomberg 深度报道页）或高阶开发文档（如 Stripe Docs），非常适合你的“65535字”填鸭式教学。
2.  **重新定义排版法则（Typography）**：
    *   加入指令：必须为“不同语义块（如公式、代码、考点、定义）采用不同字体的组合”。这会让大段枯燥的课堂文字产生天然的“结构感”，零基础的学生一眼就能分清哪句是老师讲的段子，哪句是死记硬背的定理。
3.  **重新定义颜色与色彩（Color & Theme）**：
    *   加入指令：禁止刺眼的色彩，强调**低眼疲劳（low-eye-strain）**背景（如纸质纹理光泽、深邃暗黑模式）。把醒目的颜色严格保留给“语义区分”（如警告、解题步骤、核心考点）。
4.  **把“动画”变成“教学推演工具（Progressive Disclosure）”**：
    *   原版强调页面加载时的交错动画。
    *   修改为：动画必须服务于“教学步进”。引导 AI 利用代码写出“点击展开答案”、“分步推演公式（Step-by-step unroll）”的交互效果，完美契合你想要“启发学生思考”的需求。
5.  **图表与公式的原生融合（Visual Integrations）**：
    *   针对你第二个提示词中强调的 LaTeX、Mermaid 等绘图工具，特别增加了一句：**这些图表和公式绝不能像是“贴上去的”，必须用 CSS 深度定制它们的外观**，让它们与整个高级网页的色调、字体完全融为一体。

**如何使用：**
你可以将这段 Prompt 作为核心的 System Prompt，然后把你那个“金牌考研讲师（长篇提取STT）”的 Prompt 作为 Task/User Prompt 一起发给 Claude。这样，AI 会用“讲师的灵魂”去梳理内容，然后用“顶级前端架构师的审美”把内容渲染成一个极度好用且极美的教学系统。