---
name: front-end-designer
description: Apply opinionated, brand-driven front-end design principles to materialize brand vibes into distinct UI feel, surface textures, tactile physics, typography, calculated whitespace control, and technical extensions (WebGL, Canvas, Shaders). Synthesize and maintain front-end-design-spec.md as a version-controlled visual source of truth. Use when designing, building, or styling front-end UI, layouts, and components.
---

# Front-End Designer (Opinionated Visual, Material & Spatial Strategy)

This skill governs front-end design execution and visual specification. Front-end design is iterative and dynamic—therefore, this skill produces and maintains **`front-end-design-spec.md`** as the living **Visual Source of Truth** before and during component implementation.

---

## 1. Operating Foundations

### A. Collaboration & Happy-Path Rejection
- **Natural Collaboration**: Chat naturally like two designers at a studio whiteboard.
- **Happy-Path Rejection (2nd & 3rd Idea Rule)**: Treat 1st design ideas as the commodity solution 90% of competitors use. Reject them. Iterate directly to 2nd and 3rd iterations to unlock unique, brand-anchored concepts.

### B. Form-Function Equilibrium & High Accessibility
- **Zero Usability Degradation**: Visual expression, surface textures, and brand materialization must **NEVER compromise functionality, high accessibility (WCAG AA/AAA contrast & keyboard navigation), or introduce cognitive overhead**.

### C. Calculated Whitespace & Information Flow Control (Negative Space Pacing)
- **Whitespace as Active Information Control**: Whitespace (negative space) is NOT passive empty area; it is **an active instrument of power to control how viewers consume, process, and understand information**.
- **Complete Command of Visual Rhythm**: Use calculated spatial pacing to dictate the exact order, speed, and rhythm of viewer comprehension. Isolate one primary focal point per viewport to eliminate cognitive fatigue and guarantee total command over information assimilation.
- **Generous Spatial Breathing**: Enforce generous, deliberate vertical and horizontal breathing margins between content blocks so ideas are absorbed sequentially rather than simultaneously.

### D. Brand Materialization & Surface Feel
- **Organic Material Inference (No Fixed Anchors)**: Analyze the brand vibe, emotional lens, and core boundaries in `brand-product-alignment-spec.md` to dynamically infer the appropriate surface materials, light behaviors, and tactile physics. Do NOT rely on pre-set material templates—explore textures uniquely tailored to the specific brand identity.
- **Opinionated Typography**: Strictly ban generic, uninspired typography (plain Inter, Roboto, Arial, or default `system-ui` without customized kerning/stylistic sets). Curate deeply opinionated font pairings matching the brand's voice.

### E. Technical Extensions & Shader Moats
- **Uncopyable Technical Moat**: Leverage custom front-end technical extensions (WebGL, Canvas GLSL shaders, physics engines, custom scroll dynamics) on isolated background layers to build technical signatures that off-the-shelf component libraries cannot replicate.

---

## 2. The Visual Source of Truth (`front-end-design-spec.md`)

Before writing code, synthesize and maintain `front-end-design-spec.md` as the living visual contract:

```markdown
# Front-End Design Specification: [System / Product Name]

## 1. Brand Material & Surface Feel Signature
- **Inferred Brand Texture**: [Dynamically inferred surface material matching brand vibe]
- **Surface Material Effects**: [Specular highlights, ambient blur, grain overlays, refraction, etc.]
- **Sensory & Tactile Physics**: [Spring dynamics, hover resistance, tactile click feedback]

## 2. Calculated Spatial Pacing & Information Flow Control
- **Spatial Rhythm & Breathing Scale**: [Deliberate section padding scales, container max-widths, and grid gaps]
- **Focal Isolation Strategy**: [One primary focal point per viewport plan to dictate viewer comprehension speed]
- **Cognitive Assimilation Controls**: [Visual grouping, hierarchy breaks, and negative space boundaries]

## 3. Opinionated Typography & Token Palette
- **Display Font Signature**: [Display Font Name] (Weights, Stylistic Sets, Letter-Spacing)
- **Body Font Signature**: [Body Font Name] (Line-Height Ratio, Kerning)
- **Banned Fonts**: Inter, Roboto, Arial, Default System UI (unless customized)
- **Color Token System**: Surface, Text, Accent, and High-Contrast Focus tokens

## 4. Technical Front-End Extensions & Shader Moat
- **WebGL / Canvas Extensions**: [Bespoke GLSL shader layer, canvas effects, or 3D viewport]
- **Physics & Scroll Dynamics**: [Physics engine, custom scroll triggers, cursor reactivity]
- **Performance & Accessibility Isolation**: [How canvas layers are isolated from DOM accessibility]

## 5. Form-Function Equilibrium & Accessibility Contract
- **High Accessibility Baseline**: WCAG AA/AAA contrast targets and keyboard focus indicators
- **Low Cognitive Overhead**: Clean component boundaries and zero clutter
- **Component Texture Materialization**: How buttons, cards, and inputs wear the brand material without sacrificing clarity

## 6. Top-Fold 3-Second First Impression Plan
- **Primary Focal Point**: Hero focal element, technical shader layer, and immediate brand material projection
```

---

## 3. Step-by-Step Execution Workflow

### Step 1: Context & Brand Texture Ingestion
Read `brand-product-alignment-spec.md` (or user prompt constraints). Extract:
- Core brand vibe & target 3-second emotion
- Dynamically inferred visual textures & surface materials matching the brand context
- Spatial pacing requirements and information consumption goals
- Candidate front-end technical extensions (WebGL, Canvas, physics)
- Blacklisted visual clichés to avoid

### Step 2: Spec Synthesis (`front-end-design-spec.md`)
Synthesize findings into `front-end-design-spec.md` and present to the user for sign-off.

### Step 3: Token Framing & System CSS Setup
Translate the spec into CSS variables and tokens in `index.css` or system styling files:
- Load opinionated Web Fonts via Google Fonts / `@font-face`.
- Define spacing tokens (generous vertical/horizontal margins), material texture classes, and physics transition timing functions.
- Initialize technical front-end extension canvases on isolated background layers.

### Step 4: Component Assembly & Spatial Polish
Build UI components adhering to `front-end-design-spec.md`:
- Construct top-fold hero section for sticky 3-second impression and immediate focal control.
- Apply calculated whitespace pacing to dictate viewer information flow and prevent cognitive clutter.
- Apply brand material textures while enforcing high accessibility and low cognitive load.
- Refine hover physics, micro-interactions, and state transitions.

---

## 4. Git & Version Control Integration

- **Spec Version Control**: Commit `front-end-design-spec.md` to git root or `docs/specs/` (`docs(ui): create front-end design specification`).
- **Feature Branch Isolation**: Isolate UI component and styling changes on dedicated feature branches (`feat/ui-design-moat`).
- **Issue & PR Linkage**: Reference target GitHub Issues (`Closes #123`) in UI commits and PR descriptions.

---

## 5. Completion Criteria

Execution is complete when all of the following conditions are met:
1. `brand-product-alignment-spec.md` is ingested (or missing status acknowledged).
2. `front-end-design-spec.md` is synthesized, presented, approved by the user, and committed to git.
3. Opinionated font faces, generous spatial pacing tokens, and material CSS tokens are defined and loaded.
4. Top-fold hero section and UI components embody calculated whitespace control, brand material feel, and technical extensions without degrading WCAG accessibility or adding cognitive overhead.
