---
name: front-end-designer
description: Apply opinionated, brand-driven front-end design principles to create web interfaces with universal design moats across typography, components, breathable hierarchy, and interactive signatures. Synthesize and maintain front-end-design-spec.md as the living visual source of truth. Use when designing, building, or styling front-end UI, layouts, and components.
---

# Front-End Designer (Opinionated Visual & Component Strategy)

This skill governs front-end design execution and visual specification. Front-end design is iterative and dynamic—therefore, this skill produces and maintains **`front-end-design-spec.md`** as the living **Visual Source of Truth** before and during component implementation.

---

## Prerequisites

Before executing design work, check for the existence of `brand-product-alignment-spec.md`.

- **If present**: Read the file to load the brand & product core vibe, boundaries, blacklisted clichés, and experience moat strategy.
- **If missing**: Inform the user naturally that brand/product boundaries are unanchored, and recommend running the `brand-product-alignment` skill first to lock down positioning.

---

## Core Design Principles

1. **Natural Collaboration**: Chat naturally like two designers at a studio whiteboard. Explore visual directions, token pairings, and layout dynamics collaboratively.
2. **Happy-Path Rejection (2nd & 3rd Idea Rule)**: Treat the 1st design idea as the path of least resistance—a generic commodity solution 90% of competitors use. Reject it. Iterate directly to 2nd and 3rd iterations to unlock unique, brand-anchored concepts.
3. **Universal Design Moat (Component-Wide Uncopyability)**: A design moat is NOT limited to WebGL or Canvas shaders. **Every single UI element must feature a distinct design moat**:
   - **Typography Moat**: Strictly ban generic, uninspired typography (plain Inter, Roboto, Arial, browser system defaults). Curate deeply opinionated font pairings (e.g., editorial display typefaces, distinct serif/geometric hybrids, custom tracking/kerning scales).
   - **Component Geometry Moat**: Custom card shapes, asymmetric borders, distinct elevation layers, and bespoke container geometry instead of stock rounded rectangles (`rounded-md shadow-md`).
   - **Interaction & Physics Moat**: Custom micro-interactions, tactile hover physics, cursor reactivity, state transitions, and custom scroll dynamics.
4. **Breathable Hierarchy & Low Cognitive Load**: Pace information visually. Grant every distinct content block generous, deliberate whitespace. Present one primary focal point per viewport to guide attention effortlessly.
5. **Sticky First Impression**: Engage the user within the first 3 seconds. The top fold must immediately project the brand's core lens and vibe, establishing visual authority before the user scrolls.
6. **Form & Function Equilibrium**: Balance visual expression with strict utility. Maintain clear interactive affordances, high contrast ratios, and intuitive user flows. Never degrade usability for aesthetic novelty.

---

## Execution Steps

### Step 1: Context & Visual Boundary Ingestion
Read `brand-product-alignment-spec.md` (or user prompt constraints). Extract:
- Core brand vibe & target 3-second emotion
- Blacklisted visual clichés and commodity tropes to avoid
- Brand experience moat strategy

**Completion Criterion**: 3+ required visual brand signatures and 3+ banned visual clichés are loaded.

### Step 2: Synthesis of `front-end-design-spec.md` (Visual Source of Truth)
Before writing code, synthesize the visual specification into `front-end-design-spec.md`:

```markdown
# Front-End Design Specification: [System / Product Name]

## 1. Typography & Token Palette (Opinionated Moat)
- **Display Font Signature**: [Display Font Name] (Weights, Stylistic Sets, Letter-Spacing)
- **Body Font Signature**: [Body Font Name] (Line-Height Ratio, Kerning)
- **Banned Fonts**: Inter, Roboto, Arial, Default System UI (unless customized)
- **Color Token System**: Surface, Text, Accent, and High-Contrast Focus tokens

## 2. Component Geometry & Layout Hierarchy
- **Breathable Grid & Spacing**: Padding scales, container bounds, section gaps
- **Component Geometry Moats**: Custom card structures, asymmetric borders, bespoke elevation layers

## 3. Interactive Physics & Micro-Moats
- **Hover & Focus States**: Tactile physics, micro-animations, cursor feedback
- **Technical Visual Moats**: WebGL/Canvas shaders, custom scroll dynamics (if applicable)

## 4. Top-Fold 3-Second First Impression Plan
- **Primary Focal Point**: Hero focal element and immediate brand projection
```

Present `front-end-design-spec.md` to the user for sign-off.

**Completion Criterion**: `front-end-design-spec.md` is written, presented, and approved as the living visual source of truth.

### Step 3: Token Framing & System CSS Setup
Translate `front-end-design-spec.md` into CSS variables / tokens in `index.css` or system styling files:
- Load the curated, opinionated Web Fonts via Google Fonts / `@font-face`.
- Define spacing tokens, typography scales, color surfaces, and transition timing functions.

**Completion Criterion**: CSS tokens and opinionated font faces are loaded and verified functional.

### Step 4: Component Assembly & Interactive Polish
Build UI components adhering to `front-end-design-spec.md`:
- Construct top-fold hero section for sticky 3-second impression.
- Apply universal component moats to cards, buttons, navigation, and inputs.
- Implement micro-interaction physics and custom interactive states.

**Completion Criterion**: All UI components are structured semantically, pass accessibility checks, reflect the universal design moat, and `front-end-design-spec.md` is updated to reflect any component refinements.
