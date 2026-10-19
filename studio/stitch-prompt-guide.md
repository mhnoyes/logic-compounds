# The Master Guide to Stitch Prompts: Deterministic UI/UX Design via Advanced Prompt Engineering

## 1. Executive Vision: Syntax Decays, Design Invariants Compound

In modern AI-native interface design, manual coding and pixel-pushing are rapidly giving way to semantic direction. Google’s **Stitch** platform enables creators to generate, iterate, and refine complete application frontends using natural language. However, as documented in user experiences across the Google AI Developers Forum, naive conversational prompting frequently leads to layout resets, component omission, visual regression, and contextual drift. 

The fundamental axiom governing high-fidelity AI design is simple: **Syntax decays, logic compounds**. While specific UI frameworks and styling syntax continuously evolve, the core principles of structured mental models, spatial hierarchies, and attention-steering frameworks remain permanent engineering assets. 

By synthesizing the foundational **Stitch Prompt Guide** created by Vincent Nallatamby and refined by community practitioners with the **5-Tier Invariant Prompt Engineering Framework**, this guide provides a compiler-grade methodology for Stitch. It transforms probabilistic natural language queries into deterministic, state-preserving UI/UX generation runtimes.

---

## 2. Core Principles of Stitch Prompting

Stitch operates best when prompts clearly separate **macro-architectural structure** from **micro-aesthetic styling**. According to the official Stitch guidelines, effective prompting requires mastering two distinct modes of engagement:

### High-Level vs. Detailed Prompting
*   **High-Level Prompts (Brainstorming & Concept Discovery)**: Ideal for early-stage exploration and high-level layout scaffolding. High-level prompts establish the broad application domain and core value proposition (e.g., *"An app for marathon runners to engage with a community, find partners, get training advice, and find races near them"*).
*   **Detailed Prompts (Production-Grade Screen Generation)**: Required when targeted, specific UI outcomes are needed. Detailed prompts explicitly enumerate core functionalities, layout regions, interactive components, and precise brand aesthetics up front (e.g., *"A Japandi-styled tea store product detail page featuring neutral minimalist colors, black CTA buttons, soft elegant serif typography, and herbal tea brewing specifications"*).

### Setting the Visual Vibe via Attribute Clamping
To prevent the model from defaulting to generic, center-of-the-distribution boilerplate designs, prompt engineers must clamp the visual "vibe" using explicit, non-overlapping design descriptors:
*   **Aesthetic Adjectives**: Use precise adjectives that directly condition color palettes, font pairings, and spatial density (e.g., *"minimalist and focused"*, *"vibrant and encouraging"*, *"industrial and high-density"*).
*   **Typography Controls**: Specify font families by category and role, such as pairing a serif font for headings with a clean sans-serif for body copy and metadata.
*   **Border & Surface Styling**: Explicitly define container geometry and component borders, specifying fully rounded pill buttons, 1px subtle neutral borders, or 2px solid dark borders depending on the target design language.

---

## 3. The 5-Tier Methodological Framework for Stitch

To eliminate layout breaks and context loss when building complex, multi-screen applications, Stitch prompts must be structured according to the **5-Tier Core Invariant Graph**.

| Primitive Tier | Key Architectural Function | Stitch UI Application | Primary Output Value |
| :--- | :--- | :--- | :--- |
| **Tier 1: Epistemic Gating** | Attentional filtering, vibe clamping & negative constraints | Strip conversational fluff, set strict hex/font tokens, ban cliché layouts | Clean Vibe Invariants & Type Bounds |
| **Tier 2: Decomposition** | Macro-planning & structural sequencing (SoT & LtM) | Decouple layout grid from component infill; execute incremental multi-pass edits | Executable Component Outlines |
| **Tier 3: Non-Linear Search** | Multi-path exploration, heuristic state scoring & backcasting | Explore parallel screen layouts (ToT); backcast from ideal terminal screen state ($S_T$) | High-Confidence UI Navigation Paths |
| **Tier 4: Verification & Alignment** | Claim verification, pre-mortems & anti-reset rubrics | Decoupled WCAG contrast audits; pre-mortems to block layout wipes on edit turns | Verified Screen Artifacts & Patch Logs |
| **Tier 5: Dynamic Execution** | Temporal anchoring & Git-style state compression | Anchor design tokens permanently; commit state diffs (`+ADD`, `-DEL`, `~MUT`) across turns | Production-Ready UI & Minimal State |

### Tier 1: Epistemic Signal Isolation & Attentional Gating
Tier 1 filters out conversational noise and establishes non-negotiable boundaries before Stitch processes user tokens.

*   **System 2 Attentional Filtering**: Strip conversational filler ("Please make me a nice app...") and isolate primitive variables. Define the screen strictly by its structural primitives: Header, Primary Navigation, Content Canvas, Sidebar, and Action Bar.
*   **Negative Constraint Boundaries (NCB)**: Standard generative models tend to revert to clichés. Use explicit negative constraints to prune default attractors:
    *   *Prohibit generic boilerplate*: Banned terms such as "modern", "synergy", or "clean" without explicit physical attributes.
    *   *Prevent unwanted resets*: Explicitly forbid Stitch from altering existing, verified layout grids when adding new sub-components.
*   **Grammar-Constrained Schema Scaffolding**: Enforce structured XML or markdown tags (`<layout_skeleton>`, `<theme_tokens>`, `<screen_components>`) to bound UI instructions cleanly.

### Tier 2: Algorithmic Structural Decomposition
Complex screens collapse when generated in a single monolithic pass. Tier 2 decouples layout planning from component detailing.

*   **Skeleton-of-Thought (SoT) for UI**: Split screen generation into two distinct phases:
    1.  *Phase 1 (The Skeleton)*: Define the spatial grid, column ratios, container boundaries, and major structural zones without inline styling or copy.
    2.  *Phase 2 (The Infill)*: Populate individual containers with copy, icons, form controls, and button states.
*   **Least-to-Most (LtM) Incremental Refinement**: As highlighted by community member @tempo during the construction of an industrial task dashboard, attempting to add filters, titles, icons, and table layouts in a single prompt breaks the layout. LtM enforces a strict topological sequence:
    *   *Pass 1*: Generate core structural layout and primary data grid.
    *   *Pass 2*: Inject control bars, search inputs, and filter dropdowns above the grid.
    *   *Pass 3*: Polish typography, align brand icons, and apply micro-interactions.
*   **Step-Back Abstraction**: Before prompting for a specific component (like a product card), step back to establish the overarching Design System invariants (spacing scale, color tokens, elevation levels).

### Tier 3: Non-Linear Latent Space Search & Optimization
When exploring novel UI concepts, Tier 3 prevents premature commitment to suboptimal layouts.

*   **Tree-of-Thoughts (ToT) Layout Tournaments**: Generate three orthogonal layout candidates (e.g., Node A: Card-based Grid; Node B: Split-Pane List-Detail; Node C: Full-Width Tabular View). Evaluate each branch against explicit heuristic criteria (Visual Information Density, Thumb-Reachability, Accessibility Contrast) before selecting the winning screen.
*   **Backcasting (Inverse Horizon Planning)**: Anchor the prompt on the idealized, fully populated terminal screen state ($S_T$). Reason backward to identify the prerequisite component dependencies required at $S_T-1$ and $S_T-2$ to ensure seamless data flow and zero visual overlap.
*   **Counterfactual Stress-Testing**: Stress-test proposed layouts against extreme edge conditions prior to finalizing:
    *   *Data Overflow*: How does the layout respond when product titles expand to 150 characters?
    *   *Viewport Constraints*: Does the multi-column desktop layout collapse cleanly into a single-stack mobile view?

### Tier 4: Reflexive Verification & Anti-Reset Controls
Tier 4 provides automated quality control, catching visual regressions and component drops before they ruin the design thread.

*   **Chain-of-Verification (CoVe) for Interfaces**: Execute a decoupled verification pass on generated screens:
    1.  *Atomic Claim Extraction*: List all required elements from the prompt.
    2.  *Verification Probing*: Check if element $X$ exists, if primary CTA color matches token $Y$, and if contrast ratios satisfy WCAG standards.
    3.  *Reconciliation*: Issue a surgical patch prompt targeting only missing or misaligned elements.
*   **Adversarial Pre-Mortem Inversion**: Assume the upcoming edit prompt will cause Stitch to wipe out existing table rows or reset brand colors (the "green dashboard" failure). Inject explicit protective guardrails into the prompt: *"Incorporate the new gear icon while locking all existing table CSS rules, row heights, and column alignments as immutable invariants."*
*   **Rubric-Guided Evaluation (RGE)**: Score generated screens against a 4-dimensional matrix: Spatial Hierarchy, Information SNR, Brand Alignment, and Interactive affordance.

### Tier 5: Context Lifecycle, Anchoring & State Compression
Over extended design sessions spanning 10+ screens, autoregressive models suffer from attention drift and context degradation. Tier 5 manages memory headroom.

*   **Temporal & Contextual Anchoring**: Clamp design tokens (e.g., Primary Color: `#1B4D3E`, Font: `Cinzel Serif`, Border Radius: `8px`) permanently at the head of every prompt to prevent style drift across turns.
*   **Deterministic State Compression (Git-Style Commits)**: Maintain context across long sessions by treating the UI state as an immutable version tree. Summarize working state changes as diff operations:
    ```diff
    --- a/Homepage_v1
    +++ b/Homepage_v2
    @@ Header_Container @@
    + [ADDED] Search Bar with 16px padding
    ~ [MUTATED] Primary CTA Button -> Updated background to Forest Green (#1B4D3E)
    - [EVICTED] Legacy sub-navigation links
    ```
*   **Reason and Act (ReAct) Interleaving**: Structure the design process into iterative loops: `Thought` (Identify UX gap) -> `Action` (Issue targeted Stitch prompt) -> `Observation` (Audit visual result and verify zero component drops).

---

## 4. Production Workflows & Case Studies

To demonstrate these principles in action, the following case studies illustrate how community-proven Stitch workflows map directly to our 5-Tier framework.

### Case Study A: Industrial Task Dashboard (The Factory Operator View)
*   **Context**: Building a high-density, two-row task table for factory operators displayed on a full-screen industrial monitor.
*   **The Problem**: Combining layout rules, filters, and icon placements into one prompt caused Stitch to reset the layout and break the two-row table structure.
*   **The 5-Tier Solution**:
    1.  *Tier 1 (Epistemic Isolation)*: Ban conversational fluff; define hard constraints (zero card wrappers, strictly two-row table layout).
    2.  *Tier 2 (Least-to-Most Sequencing)*:
        *   **Pass 1 (Core Layout)**: *"Create a web dashboard displaying a factory task list. Each task must consist of exactly two rows: Row 1 contains Task Title, Operator, Sector, Machine, Deadline, and Status in separate columns. Row 2 spans the full width directly below, showing the long Task Description."*
        *   **Pass 2 (Component Controls)**: *"Above the existing task table, add a single horizontal row of minimal filter dropdowns for Task Title, Operator, Sector, Machine, Deadline, and Status. Preserve all existing two-row table styles."*
        *   **Pass 3 (Header & Icon Alignment)**: *"Align the main dashboard title to the far left. Add a minimal gear icon in the top-right corner for admin settings. Do not modify the task table or filter row."*

### Case Study B: E-Commerce Product Detail Page (Japandi Aesthetic)
*   **Context**: Designing an elegant, high-end product detail page for an artisanal herbal tea store.
*   **The 5-Tier Solution**:
    1.  *Tier 1 (Vibe Clamping)*: Specify exact adjectives and colors: *"Japandi aesthetic, neutral taupe background, soft elegant serif typography, minimal black CTA buttons."*
    2.  *Tier 2 (Skeleton-of-Thought)*:
        *   *Skeleton*: 60/40 two-column split. Left column: Product gallery. Right column: Product metadata, pricing, variant selector, and brewing instructions.
        *   *Infill*: High-resolution macro imagery of organic herbal leaves, minimal counter selectors, and expandable accordion drawers for origin notes.

### Case Study C: Music Player Page with Dynamic Image-Theme Coordination
*   **Context**: Designing a music player interface for the single "Suburban Legends."
*   **The 5-Tier Solution**:
    1.  *Tier 2 & 5 (Image & Theme Coordination)*: Explicitly link image content with container styling: *"Music player page for 'Suburban Legends'. The album art is a macro, zoomed-in photograph of deep ocean water. Set the page background and player controls to match the deep teal and aquatic tones of the album art."*

---

## 5. Production Prompt Template Library

### Template 1: Zero-Shot Initial Screen Generation Engine
```markdown
[SYSTEM: STITCH UI ARCHITECT ACTIVE]
TARGET SCREEN: [INSERT SCREEN NAME / PURPOSE, e.g., Patient Triage Dashboard]
DESIGN SYSTEM VIBE: [INSERT ADJECTIVES, e.g., Minimalist, Clinical, High-Density]

1. COLOR PALETTE TOKENS:
   - Primary Surface: [COLOR / HEX, e.g., #F8F9FA]
   - Primary Brand Accent: [COLOR / HEX, e.g., #0A66C2]
   - Neutral Text / Borders: [COLOR / HEX, e.g., #111827 / 1px solid #E5E7EB]

2. TYPOGRAPHY & GEOMETRY:
   - Headings: [FONT CATEGORY, e.g., Bold Sans-Serif]
   - Body / Data: [FONT CATEGORY, e.g., Highly legible Monospace or Sans-Serif]
   - Component Geometry: [ROUNDED / PILL / SQUARE, e.g., Fully rounded pill buttons]

3. SKELETON LAYOUT GRID:
   - Header Bar: [LEFT: Title | RIGHT: Action Icons]
   - Main Canvas: [DEFINE GRID / SPATIAL RATIOS, e.g., 70% Primary Data Table | 30% Summary Sidebar]

4. COMPONENT INFILL:
   - Component 1: [SPECIFY EXACT CONTENT AND CONTROLS]
   - Component 2: [SPECIFY EXACT CONTENT AND CONTROLS]

NEGATIVE CONSTRAINTS (HARD BOUNDARIES):
- ZERO generic placeholder text; use realistic domain copy.
- DO NOT use bright saturated backgrounds; restrict color to brand accents.
```

### Template 2: Incremental Component Mutation & Refinement Engine
```markdown
[TARGET CONTAINER]: [SPECIFY CONTAINER / SECTION, e.g., Top Header Bar]
[MUTATION DIRECTIVE]: [SPECIFY EXACT CHANGE, e.g., Add a search bar with filter icon]

INVARIANT PRESERVATION LOCK:
- Preserve 100% of existing CSS grid layouts, primary brand colors, and typography scales across all other containers.
- DO NOT reset, re-render, or drop the following existing components: [LIST COMPONENT A, COMPONENT B].

EXECUTION PASS:
1. Isolate [TARGET CONTAINER].
2. Inject [MUTATION DIRECTIVE] with [SPECIFIC COMPONENT STYLING].
3. Re-align spatial padding to maintain WCAG accessibility standards.
```

### Template 3: Systemic Design Token & Copy Migration Engine
```markdown
[MIGRATION DIRECTIVE]: [SPECIFY TASK, e.g., Translate all copy to Spanish AND update primary theme to Warm Autumn]

SYSTEMIC TOKEN UPDATES:
- Primary Brand Accent: [OLD COLOR] -> [NEW COLOR, e.g., Forest Green]
- Background Surface: [OLD COLOR] -> [NEW COLOR, e.g., Soft Cream]
- Language Mapping: Convert 100% of headings, button labels, form placeholders, and micro-copy from [SOURCE LANGUAGE] to [TARGET LANGUAGE].

ASSET COORDINATION:
- Ensure all illustrative icons, badges, and image backgrounds update their color tinting to match the new Primary Brand Accent.
```

---

## 6. Stitch Anti-Pattern Registry & Operational Rulebook

### The 5 Lethal Pitfalls in Stitch Prompting
1.  **The Monolithic Dump (The 5000-Character Trap)**: Pounding Stitch with a 5000+ character master prompt in turn one guarantees component drops, missing fields, and broken layouts. *Fix*: Use Skeleton-of-Thought and Least-to-Most sequencing.
2.  **Layout + Component Blending**: Mixing spatial grid instructions with button styling or icon tweaks in a single prompt causes the model to lose track of the grid. *Fix*: Decouple layout structural prompts from component detailing prompts.
3.  **Unanchored Theme Drift**: Asking Stitch to "make it look modern" or "try a new color" without specifying hex codes or mood attributes causes radical, unpredictable visual shifts. *Fix*: Clamp design tokens explicitly.
4.  **Targeting Ambiguity**: Prompts like "change the button" leave Stitch guessing which button on a complex screen to modify. *Fix*: Use unambiguous reference paths (e.g., *"the primary green CTA button inside the login form container"*).
5.  **Unmonitored State Loss**: Assuming Stitch remembers prior screen rules during edit turns. *Fix*: Save a screenshot/checkpoint after every successful step, and use state-locking directives during edits.

### The 10 Invariant Rules of Stitch Engineering
1.  **One Major Structural Change Per Turn**: Never combine major grid restructuring with component additions.
2.  **Name Elements by Location and Content**: Always reference components by container and label (e.g., *"the 'Save Draft' button in the bottom drawer"*).
3.  **Specify Explicit Colors and Fonts**: Replace abstract terms with concrete palette names or hex values.
4.  **Coordinate Images with Palette Shifts**: When changing theme colors, explicitly instruct Stitch whether to update image overlays or illustrative icons.
5.  **Use Industry Standard UI/UX Terminology**: Terms like `navigation bar`, `hero section`, `card layout`, `accordion drawer`, and `segmented control` steer attention heads precisely.
6.  **Lock Invariants Before Editing**: Begin edit prompts by explicitly listing elements that must remain untouched.
7.  **Validate Image Styles**: Provide explicit artistic direction for imagery (e.g., *"macro photography"*, *"minimalist vector line art"*).
8.  **Enforce Realistic Domain Copy**: Avoid "Lorem Ipsum", which degrades spatial accuracy and causes misaligned text containers.
9.  **Audit Responsiveness Early**: Test desktop and mobile viewport behavior before adding secondary micro-features.
10. **Re-anchor Token Limits**: If a thread exceeds 10 turns, synthesize a Git-style state diff summary and re-anchor the screen specification in a fresh thread.
