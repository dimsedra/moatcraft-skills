---
name: moatcraft-onboarding
description: Agent guide for explaining the Moatcraft workflow to new users on first install. Walk users through how the development loop works, why each skill exists, and what to expect — using high-level human abstractions. Use automatically when Moatcraft skills are first installed in a project, or when a user asks how the Moatcraft workflow operates.
---

# Moatcraft Onboarding (Agent Workflow Guide)

This skill is **an internal agent guide**, not a user-facing questionnaire. It instructs the agent on how to transparently walk new users through the Moatcraft development workflow so they understand what they are working with — eliminating the "blackbox" sensation of installing skills without knowing what they do or why they exist.

---

## 1. When to Activate

Activate this skill automatically when:
- Moatcraft skills are **first installed** in a new project (no prior spec artifacts exist).
- A user **asks how the Moatcraft workflow works** or what the skills do.
- A user seems confused about the development loop or skill invocation order.

---

## 2. Onboarding Tone & Approach

- **Use `explain-and-teach` principles**: High-level human abstractions, intuitive mental models, zero jargon dumps. The user should walk away feeling they genuinely understand the workflow, not that they were lectured at.
- **Conversational, not ceremonial**: This is not a contract signing. It is a casual, transparent walkthrough — like a co-founder explaining the team's development philosophy to a new collaborator over coffee.
- **Offer, don't force**: On first detection, the agent should offer: *"This is your first time using Moatcraft — want me to walk you through how the workflow operates so you know what to expect?"* If the user declines, proceed directly to the requested task.

---

## 3. What to Cover (High-Level Walkthrough)

When the user accepts the walkthrough, explain the following concepts using natural human logic. Do NOT recite skill names as a dry list — weave them into a narrative of how a product gets built:

### A. The Problem Moatcraft Solves
Most AI coding tools produce generic, interchangeable output. If you removed the logo, you couldn't tell one product from another. Moatcraft exists to make sure that doesn't happen — every design choice, architecture decision, and line of code is anchored to a defensible identity.

### B. How the Workflow Flows (The Mental Model)
Walk the user through the natural progression:

1. **First, we figure out who you are** — Before writing any code, we have a conversation about your brand, product identity, and what makes you different. This becomes the anchor for everything downstream.
2. **Then, we translate that into specs** — Your identity gets materialized into concrete front-end visual specs (textures, typography, spatial rhythm) and backend architecture specs (data flow, reliability, technical moats). These are living documents, not frozen requirements.
3. **We map out what to build** — The specs get decomposed into a living roadmap of milestones and atomic tasks. This roadmap is flexible — it adapts as we learn more during development.
4. **We build with discipline** — Every task follows Red-Green TDD on isolated Git branches. Write the test first (it fails), then write the minimum code to make it pass.
5. **We verify twice before shipping** — First, an alignment audit checks whether what we built actually matches the specs (no scope creep, no missing items). Then, a code review evaluates quality and edge-case robustness. If either finds issues, we loop back and fix before merging.
6. **The loop is alive** — If requirements shift mid-flight (and they always do), the system cascades re-audits downstream. If we discover a fundamental contradiction during coding, we escalate back upstream to resolve it at the right level.

### C. What the User Should Expect from the Agent
- The agent will **push back on generic first ideas** and iterate toward unique solutions.
- The agent will **challenge assumptions** constructively if it spots contradictions or hidden trade-offs.
- Explanations will default to **high-level mental models**; technical code details are provided only when asked.
- The agent will **ask for sign-off on specs** before building, so there are no surprises.

### D. What the User Owns
- **Every spec artifact is theirs** — `brand-product-alignment-spec.md`, `front-end-design-spec.md`, `backend-architecture-spec.md`, `progress-map.md`. These are version-controlled, living documents the user can review, edit, and approve at any time.
- **The user drives strategic direction** — The agent proposes, challenges, and executes, but the user makes the final call on brand positioning, visual direction, and architectural trade-offs.

---

## 4. After the Walkthrough

Once the user feels oriented, guide them to the natural starting point:
- *"Ready to start? The first step is usually figuring out your brand and product identity. Want to kick that off?"*
- Route to `brand-product-alignment` or `agentic-dev-loop` based on user preference.

---

## 5. Ongoing Reference

If at any point during development the user asks *"Why are we doing this?"*, *"What's the point of this audit?"*, or *"How does this fit into the bigger picture?"*, use `explain-and-teach` to answer — anchoring the explanation back to the workflow mental model established during onboarding.
