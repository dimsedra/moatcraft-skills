---
name: explain-and-teach
description: Provide adaptive, high-level systemic explanations of technical decisions, architecture trade-offs, and design rationale using natural human abstractions and mental models. Use when the user asks "why", requests an explanation of choices, or wants to understand trade-offs or mental models.
---

# Explain and Teach (Adaptive Systemic Explanation)

This skill delivers flexible, high-signal explanations of technical decisions, architectural trade-offs, and conceptual models.

---

## 1. Human Cognitive Architecture Principle

Human cognition processes **high-level mental models, cause-and-effect relationships, functional abstractions, and natural analogies** far more efficiently than parse-heavy code syntax or implementation jargon.

- **Default Communication State**: Explain decisions using clear human logic, intuitive abstractions, and structural mental models.
- **Hybrid Low-Level Mapping**: When low-level code mechanics are explicitly requested, **NEVER present pure isolated code dumps**. The explanation must remain **hybrid**—effortlessly mapping every line of code, parameter, or syntax structure back to its high-level mental model and trade-off rationale.
- **High Signal, Zero Condescension**: Omit conversational filler, patronizing hand-waving, and redundant summaries. Deliver direct, high-density rationale.

---

## 2. Operating Core: Match the Requested Slice

Deliver **ONLY** the specific conceptual module requested by the user prompt. Do NOT force a rigid multi-section template unless the user explicitly requests a full deep-dive.

### Explanation Branches:

#### Branch A: Trade-off & Rationale (When prompt asks *"Why A over B?"*, *"What's the trade-off?"*)
Deliver a high-level trade-off breakdown:
- **Selected Path vs. Rejected Alternatives (2nd/3rd ideas)** using plain human logic.
- **Net Gain vs. Net Cost** (e.g., *"Gains instant search performance at the cost of higher memory footprint"*).
- Omit code dumps and implementation mechanics.

#### Branch B: Systemic Ripple Effect (When prompt asks *"How does this affect X?"*, *"What breaks if Y changes?"*)
Deliver a cause-and-effect boundary map using intuitive abstractions:
- Direct flow across system boundaries (Component A ➔ Component B).
- Structural consequences for the product or user experience.

#### Branch C: Mental Model Anchor (When prompt asks *"How does this work fundamentally?"*, *"What's the core concept?"*)
Deliver a clean, first-principles mental model:
- 1-2 sentence intuitive analogy or logical invariant that grounds the concept instantly.

#### Branch D: Hybrid Technical Code Mechanics (ONLY when prompt asks *"Show me the code"* or *"How is this implemented technically?"*)
Deliver a hybrid code breakdown that anchors implementation to concept:
- Present the essential code block/signature.
- **Effortlessly map specific code lines directly back to the high-level mental model** (e.g., *"Line 42 enforces the concurrency boundary we defined in the high-level model..."*).
- Never output unanchored, isolated syntax dumps.

---

## 3. Transparency of Alternatives

When explaining any design or architectural decision, always disclose:
1. The **primary choice** selected.
2. The **2nd and 3rd alternative ideas** that were considered and discarded.
3. The **underlying trade-off rationale** behind the rejection.
