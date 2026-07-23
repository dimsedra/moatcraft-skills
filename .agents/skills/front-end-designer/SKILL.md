---
name: front-end-designer
description: Apply opinionated, brand-driven front-end design principles to create web interfaces with a strong design moat, breathable hierarchy, and balanced form & function. Use when designing, building, or styling front-end UI, layouts, and components.
---

# Front-End Designer

This skill governs front-end design execution, ensuring every interface is deeply opinionated, brand-anchored, and defensible against generic design tropes.

## Prerequisites

Before executing design work, check for the existence of `brand-product-alignment-spec.md`.

- **If present**: Read the file to load the brand & product core vibe, boundaries, blacklisted clichés, and experience moat strategy.
- **If missing**: Inform the user naturally that brand/product boundaries are unanchored, and recommend running the `brand-product-alignment` skill first to lock down positioning.

---

## Conversational & Design Principles (Natural Collaboration)

1. **Natural Collaboration**: When presenting visual directions or choices to the user, chat naturally like two designers exploring ideas at a studio. Avoid robotic checklists or jargon soup.
2. **Happy-Path Rejection**: Treat your first design idea as the path of least resistance—a generic solution 90% of competitors would use. Reject it. Iterate directly to the 2nd and 3rd iterations to unlock unique, brand-anchored concepts.
3. **Uniquely Opinionated Identity**: Design every choice (typography, color relationships, component geometry, interactive states) so it feels exclusive to the brand. If another brand can swap logos into the layout without visual dissonance, the design is a failure.
4. **Breathable Hierarchy & Low Cognitive Load**: Pace information visually. Grant every distinct content block generous, deliberate whitespace. Present one primary focal point per viewport to guide the audience's attention effortlessly.
5. **Sticky First Impression**: Engage the user within the first 3 seconds. The top fold must immediately project the brand's core lens and vibe, establishing visual authority before the user scrolls.
6. **Form & Function Equilibrium**: Balance visual expression with strict utility. Maintain clear interactive affordances, high contrast ratios, and intuitive user flows. Never degrade usability for aesthetic novelty.
7. **Technical Design Moat**: Incorporate custom front-end extensions (such as WebGL, Canvas shaders, physics micro-interactions, or custom scroll dynamics) to build a technical and visual moat that off-the-shelf component libraries cannot replicate.

---

## Execution Steps

Follow this sequential workflow when building or styling UI:

### Step 1: Context & Boundary Ingestion
Read `brand-product-alignment-spec.md` (or user prompt constraints). Extract:
- Core brand vibe & target 3-second emotion
- Blacklisted visual clichés to avoid
- Defined design moat mechanisms

**Completion Criterion**: A clear list of 3+ required brand signatures and 3+ banned visual anti-patterns is established before writing code.

### Step 2: Spatial & Visual Hierarchy Framing
Define the layout grid, typography scale, and color token palette in `index.css` or system tokens:
- Set generous spacing variables for section padding and content gaps.
- Choose distinct, high-personality font pairings matching the brand identity.
- Establish high-contrast surface and text tokens for maximum accessibility.

**Completion Criterion**: Core CSS variables and tokens are defined, showing breathable spacing and clean visual hierarchy.

### Step 3: Layout & Component Assembly
Build components adhering to curated visual flow:
- Construct the top fold to deliver a sticky first impression.
- Apply the 2nd/3rd idea principle to component cards, hero sections, and navigation.
- Ensure low cognitive load by grouping related information and isolating key actions.

**Completion Criterion**: All UI components are structured semantically, pass accessibility checks, and reflect the brand's opinionated identity.

### Step 4: Design Moat & Interactive Polish
Integrate signature interactive elements:
- Add micro-animations, custom cursor behaviors, or WebGL/Canvas visual effects specified in the moat strategy.
- Refine hover, focus, and transition states for smooth tactile feedback.

**Completion Criterion**: The interface features a distinct, technical design moat that is verified functional without performance bottlenecks.
