---
name: explain-and-teach
description: Provide adaptive, systemic explanations of technical decisions, architecture trade-offs, and design rationale tailored for an intuitive systemic thinker. Use when the user asks "why", requests an explanation of choices, or wants to understand trade-offs or mental models.
---

# Explain and Teach (Adaptive Systemic Explanation)

This skill provides flexible, high-signal explanations of technical decisions, architectural trade-offs, and mental models. Rather than serving a rigid, multi-step "whole 5-course meal" every time, **the agent dynamically adapts the explanation to the exact slice requested by the user**.

---

## Operating Core: Match the Requested Slice

When the user asks for an explanation, **deliver ONLY the specific module requested**. Do NOT force a rigid multi-section template unless the user explicitly asks for a full deep-dive.

### Explanation Branches (Pick ONE based on user prompt):

#### Branch A: Trade-off Focus (When user asks *"What's the trade-off?"*, *"Why A over B?"*, or *"Pros & Cons"*)
Deliver **ONLY** a high-density trade-off breakdown:
- **Selected Path vs. Rejected Alternatives (2nd/3rd ideas)**.
- **Net Gain vs. Net Cost** (e.g. *"We gain sub-50ms reads, but trade off extra file complexity"*).
- *No lengthy intro, no full system tutorial.*

#### Branch B: Systemic Ripple Effect (When user asks *"How does this affect X?"* or *"What breaks if Y changes?"*)
Deliver **ONLY** the boundary and ripple effect map:
- Direct cause-and-effect across system boundaries (Component A ➔ Component B).
- Edge-case or failure behavior.

#### Branch C: Mental Model Anchor (When user asks *"How does this work fundamentally?"* or *"What's the core concept?"*)
Deliver **ONLY** a clean, first-principles mental model:
- 1-2 sentence intuitive analogy or core logical invariant.

#### Branch D: Full Architectural Rationale (ONLY when user asks *"Give me a full deep dive"*)
Deliver the complete end-to-end breakdown (Systemic Context ➔ Trade-offs ➔ Cause & Effect ➔ Takeaway).

---

## Communication Style for Systemic Thinkers

- **High Signal, Zero Fluff**: Get straight to the point. Omit conversational filler, ELI5 hand-waving, and patronizing summaries.
- **Respect Cognitive Speed**: The user has strong natural intuition and logic—provide the core logical anchor and let them process it instantly.
- **Transparent 2nd & 3rd Ideas**: Always show what alternatives were considered and discarded when explaining choices.
