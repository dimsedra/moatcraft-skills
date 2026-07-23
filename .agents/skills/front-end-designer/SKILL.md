---
name: front-end-designer
description: Apply opinionated, brand-driven front-end design principles to materialize brand vibes into distinct UI feel, surface textures, tactile physics, typography, and technical extensions (WebGL, Canvas, Physics Shaders). Synthesize and maintain front-end-design-spec.md as the living visual source of truth. Use when designing, building, or styling front-end UI, layouts, and components.
---

# Front-End Designer (Opinionated Visual, Material & Technical Extension Strategy)

This skill governs front-end design execution and visual specification. Front-end design is iterative and dynamic—therefore, this skill produces and maintains **`front-end-design-spec.md`** as the living **Visual Source of Truth** before and during component implementation.

---

## Prerequisites

Before executing design work, check for the existence of `brand-product-alignment-spec.md`.

- **If present**: Read the file to load the brand & product core vibe, boundaries, blacklisted clichés, and experience moat strategy.
- **If missing**: Inform the user naturally that brand/product boundaries are unanchored, and recommend running the `brand-product-alignment` skill first to lock down positioning.

---

## Core Design Principles

1. **Natural Collaboration**: Chat naturally like two designers at a studio whiteboard. Explore visual directions, material textures, and layout dynamics collaboratively.
2. **Happy-Path Rejection (2nd & 3rd Idea Rule)**: Treat the 1st design idea as the path of least resistance—a generic commodity solution 90% of competitors use. Reject it. Iterate directly to 2nd and 3rd iterations to unlock unique, brand-anchored concepts.
3. **Form Must Never Compromise Function (High Accessibility & Low Cognitive Load)**:
   - **Zero Usability Degradation**: Visual expression, surface textures, and brand materialization must **NEVER compromise functionality, high accessibility (WCAG AA/AAA contrast & keyboard navigation), or introduce cognitive overhead**.
   - **Moat via Brand-Derived Feel & Materials**: The design moat comes from the **sensory feel, visual textures, surface materials, and tactile physics** inferred directly from `brand-product-alignment-spec.md` to reinforce the brand identity:
     - *Example 1 (Fluid/Precision Brand)*: Infer **Liquid Glass textures**, dynamic light refraction, subtle chromatic sheen, and fluid spring physics.
     - *Example 2 (Tactile Monolith Brand)*: Infer **Matte Obsidian depth**, brushed metallic borders, heavy tactile resistance, and subtle grain overlays.
     - *Example 3 (Editorial Craft Brand)*: Infer **Paper-grain warmth**, high-contrast editorial typography, and ink-bleed hover accents.
4. **Leverage Technical Front-End Extensions (WebGL, Canvas, Shaders, Physics Engines)**:
   - **Uncopyable Technical Moat**: Incorporate custom front-end technical extensions (such as WebGL canvas viewports, custom GLSL fragment shaders, physics micro-interaction engines, or custom scroll dynamics) to build a technical and visual moat that off-the-shelf component libraries cannot replicate.
   - **Performance & Accessibility Isolation**: Render heavy visual shaders or canvas effects on dedicated background layers or WebGL canvases, keeping DOM elements accessible, semantic, and performant.
5. **Non-Generic, Opinionated Typography**:
   - Strictly ban generic, uninspired typography (plain Inter, Roboto, Arial, or default `system-ui` without customized kerning/stylistic sets).
   - Curate deeply opinionated font pairings (e.g., editorial display typefaces, distinct serif/geometric hybrids) matching the brand's voice.
6. **Breathable Hierarchy & Low Cognitive Overhead**: Pace information visually. Grant every distinct content block generous, deliberate whitespace. Present one primary focal point per viewport to guide attention effortlessly without visual noise.
7. **Sticky First Impression**: Engage the user within the first 3 seconds. The top fold must immediately project the brand's core lens and vibe, establishing visual authority before the user scrolls.

---

## Execution Steps

### Step 1: Context, Brand Texture & Extension Ingestion
Read `brand-product-alignment-spec.md` (or user prompt constraints). Extract:
- Core brand vibe & target 3-second emotion
- Inferred visual textures & surface materials (e.g. liquid glass, matte obsidian, warm paper grain, neon refraction)
- Candidate front-end technical extensions (WebGL shaders, Canvas effects, physics engines)
- Blacklisted visual clichés to avoid

**Completion Criterion**: 3+ brand signatures, surface materials, and planned technical extensions are loaded before writing code.

### Step 2: Synthesis of `front-end-design-spec.md` (Visual Source of Truth)
Synthesize the visual, material, and extension specification into `front-end-design-spec.md`:

```markdown
# Front-End Design Specification: [System / Product Name]

## 1. Brand Material & Feel Signature (The Surface Moat)
- **Inferred Brand Texture**: [e.g. Liquid Glass / Matte Obsidian / Warm Paper Grain]
- **Surface Material Effects**: [Refraction, Blur, Sheen, Grain, Border Specular Highlights]
- **Sensory & Tactile Physics**: [Spring dynamics, hover resistance, tactile click feedback]

## 2. Technical Front-End Extensions & Shader Moat
- **WebGL / Canvas Extensions**: [e.g. GLSL background liquid shader / Canvas particle grain]
- **Physics & Scroll Dynamics**: [Physics engine, custom scroll triggers, cursor reactivity]
- **Performance & Accessibility Isolation**: [How canvas layers are isolated from DOM accessibility]

## 3. Typography & Token Palette
- **Display Font Signature**: [Display Font Name] (Weights, Stylistic Sets, Letter-Spacing)
- **Body Font Signature**: [Body Font Name] (Line-Height Ratio, Kerning)
- **Banned Fonts**: Inter, Roboto, Arial, Default System UI (unless customized)
- **Color Token System**: Surface, Text, Accent, and High-Contrast Focus tokens

## 4. Form-Function Equilibrium & Accessibility Contract
- **High Accessibility Baseline**: WCAG AA/AAA contrast targets and keyboard focus indicators
- **Low Cognitive Overhead**: Clean component boundaries and zero clutter
- **Component Texture Materialization**: How buttons, cards, and inputs wear the brand material without sacrificing clarity

## 5. Top-Fold 3-Second First Impression Plan
- **Primary Focal Point**: Hero focal element, technical shader layer, and immediate brand material projection
```

Present `front-end-design-spec.md` to the user for sign-off.

**Completion Criterion**: `front-end-design-spec.md` is written, presented, and approved as the living visual source of truth.

### Step 3: Token Framing & Extension Setup
Translate `front-end-design-spec.md` into CSS variables / tokens and extension initializers in `index.css` or system styling files:
- Load opinionated Web Fonts via Google Fonts / `@font-face`.
- Define spacing tokens, material texture classes (backdrop filters, specular borders, grain overlays), and physics transition timing functions.
- Initialize technical front-end extension canvases or shader pipelines on isolated background layers.

**Completion Criterion**: CSS tokens, material texture utilities, opinionated font faces, and extension canvas pipelines are loaded and verified functional.

### Step 4: Component Assembly & Material Polish
Build UI components adhering to `front-end-design-spec.md`:
- Construct top-fold hero section integrating the primary focal element and background technical extensions.
- Apply brand material textures (e.g. liquid glass sheen) while enforcing high accessibility and low cognitive load.
- Refine hover physics, micro-interactions, and state transitions.

**Completion Criterion**: All UI components are structured semantically, pass accessibility checks, embody the brand's material feel, leverage technical extensions, and `front-end-design-spec.md` is updated.
