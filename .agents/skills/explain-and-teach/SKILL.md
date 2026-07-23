---
name: explain-and-teach
description: Provide adaptive, high-level systemic explanations of technical decisions, architecture trade-offs, and design rationale using natural human abstractions and mental models for non-overly-technical users. Use when the user asks "why", requests an explanation of choices, or wants to understand trade-offs or mental models.
---

# Explain and Teach (Adaptive Systemic Explanation)

This skill provides flexible, high-signal explanations of technical decisions, architectural trade-offs, and mental models.

> **Target User Assumption & Framing:**  
> Assume the user is **not overly technical**. The user is an intuitive, systemic thinker who grasps high-level concepts, architectural trade-offs, and natural human abstractions effortlessly. **Do NOT dump low-level code syntax, raw function signatures, or technical jargon** unless the user explicitly requests code-level technical specifics.

---

## Operating Core: Match the Requested Slice

Deliver **ONLY** the specific conceptual slice requested. Do NOT force a rigid multi-section template unless the user explicitly asks for a full deep-dive.

### Explanation Branches (Pick ONE based on user prompt):

#### Branch A: Trade-off & Decision Rationale (When user asks *"Why A over B?"*, *"What's the trade-off?"*)
Deliver a high-level conceptual trade-off breakdown:
- **Selected Path vs. Rejected Alternatives (2nd/3rd ideas)** using plain human logic.
- **Net Gain vs. Net Cost** (e.g. *"We gain instant search speed, but trade off extra storage footprint"*).
- *No low-level code dumps or syntax walkthroughs.*

#### Branch B: Systemic Ripple Effect (When user asks *"How does this affect X?"*, *"What breaks if Y changes?"*)
Deliver a clear cause-and-effect map using intuitive abstractions:
- High-level flow across system boundaries (Component A ➔ Component B).
- What changes for the user or product experience if a boundary is altered.

#### Branch C: Mental Model Anchor (When user asks *"How does this work fundamentally?"*, *"What's the core concept?"*)
Deliver a clean, first-principles mental model:
- 1-2 sentence intuitive analogy using natural human concepts (e.g., *"Think of this as a restaurant pass-through window where..."*).

#### Branch D: Code-Level Technical Deep-Dive (ONLY when user explicitly asks *"Show me the code details"* or *"How is this implemented technically?"*)
Deliver low-level code syntax, function signatures, and technical mechanics.

---

## Communication Style & Cognitive Calibration

- **High-Level Abstractions First**: Communicate using natural human logic, clear mental models, and intuitive analogies.
- **On-Demand Technical Depth**: Keep technical code details hidden until explicitly requested.
- **High Signal, Zero Patronizing Fluff**: Respect the user's strong natural cognitive speed. Omit conversational filler, condescending summaries, and hand-waving.
- **Transparent 2nd & 3rd Ideas**: Always explain *why* alternatives were considered and discarded in plain language.
