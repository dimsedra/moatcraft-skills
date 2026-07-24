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
- Moatcraft skills are installed into a **project already in progress** (existing code, configs, or partial specs detected).
- A user **asks how the Moatcraft workflow works** or what the skills do.
- A user seems confused about the development loop or skill invocation order.

---

## 2. Project State Detection

Before beginning the walkthrough, the agent should silently assess the project state by scanning for existing signals:

- **Clean Slate** (no `src/`, no `package.json`/`pyproject.toml`/`go.mod`, no existing spec files): Full onboarding from Phase 1 (brand-product-alignment).
- **Mid-Development** (existing source code, dependencies, possibly partial docs/specs, git history): The user is adopting Moatcraft into a project that already has momentum. The workflow needs to meet them where they are, not demand they start over.
- **Workflow Migration** (existing CI/CD configs, other agent skill files, `.cursor/`, `.claude/`, custom linting/review pipelines): The user is coming from another workflow or toolchain. Acknowledge what they already have and explain how Moatcraft layers in — not replaces — their existing setup where possible.

---

## 3. Onboarding Tone & Approach

- **Use `explain-and-teach` principles**: High-level human abstractions, intuitive mental models, zero jargon dumps. The user should walk away feeling they genuinely understand the workflow, not that they were lectured at.
- **Conversational, not ceremonial**: This is not a contract signing. It is a casual, transparent walkthrough — like a co-founder explaining the team's development philosophy to a new collaborator over coffee.
- **Offer, don't force**: On first detection, the agent should offer: *"This is your first time using Moatcraft — want me to walk you through how the workflow operates so you know what to expect?"* If the user declines, proceed directly to the requested task.

---

## 4. What to Cover (High-Level Walkthrough)

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

### E. Where Your Judgment Is Still Irreplaceable (The Limits of "Clean Pass")
Be transparent: the automated loop catches a lot, but there are dimensions it **cannot evaluate for you**. A "Clean Pass" from alignment audit and code review means the code matches the spec and meets quality standards — it does **not** mean:

- **The spec itself was right** — If the brand positioning or architecture spec had a flawed assumption baked in, a Clean Pass will faithfully verify code that implements that flaw perfectly. The system checks *fidelity to the plan*, not *whether the plan was wise*.
- **The product will resonate with real users** — Market fit, emotional resonance, and whether a feature actually solves a real problem are judgment calls no automated loop can make. That is your territory.
- **The trade-offs are acceptable to your context** — The agent surfaces trade-offs and pushes back, but ultimately whether a particular performance/cost/complexity trade-off is worth it depends on your business reality, timeline, and risk tolerance.
- **Edge cases beyond the spec exist** — Code review catches structural edge cases (null handling, race conditions), but domain-specific edge cases that were never articulated in the spec will not be tested.

**What happens if you don't bring your judgment**: The system will build exactly what the spec says, verify it passes, and ship it — even if the spec was incomplete, the positioning was off, or the feature doesn't matter to your users. Clean Pass means *internal consistency*, not *external correctness*.

---

## 5. Mid-Development & Workflow Migration Handling

If the project is **not a clean slate**, the agent must adapt the onboarding and entry point accordingly:

### A. Mid-Development Entry (Existing Codebase, No Moatcraft Specs Yet)
The user has code but no Moatcraft spec artifacts. The agent should:

1. **Acknowledge the existing work** — *"I can see you've already got a codebase going. Moatcraft doesn't ask you to throw any of that away — we just need to backfill the strategic foundation so the loop has something to anchor to."*
2. **Propose a lightweight spec backfill** — Rather than running the full discovery from scratch, the agent should offer to **infer and draft initial specs from the existing codebase** (reading `README.md`, existing component structure, API routes, styling tokens, git history) and present them for the user's review and correction.
3. **Route to the right entry point** — Skip brand-product-alignment if the product identity is already obvious from context. If specs can be inferred, start at `progress-mapper` to decompose the next phase of work. Let the user decide what feels right.

### B. Workflow Migration (Coming from Another Toolchain)
The user has existing CI/CD, linting configs, other agent skills, or review pipelines. The agent should:

1. **Respect what already works** — *"I see you've got [existing setup]. Moatcraft isn't trying to replace everything — it layers on top. Your existing CI and linting stay as they are."*
2. **Clarify what Moatcraft adds vs. what it overlaps** — If the user already has code review automation, explain how Moatcraft's dual-axis review complements it. If they have project boards, explain how `progress-map.md` is a spec-anchored living document that works alongside their tracking tool.
3. **Don't demand a clean migration** — The user can adopt Moatcraft skills incrementally. They can start with just `brand-product-alignment` and `front-end-designer` and add the active dev loop later when they're ready.

---

## 6. After the Walkthrough

Once the user feels oriented, guide them to the appropriate starting point based on project state:

- **Clean Slate**: *"Ready to start? The first step is usually figuring out your brand and product identity. Want to kick that off?"* → Route to `brand-product-alignment`.
- **Mid-Development**: *"Since you already have code, let me draft some initial specs from what's here so we can anchor the loop. Want me to do that?"* → Route to spec backfill, then `progress-mapper`.
- **Workflow Migration**: *"Let's figure out where Moatcraft slots into your current setup without disrupting what's already working."* → Route to whichever skill addresses the user's immediate need.

---

## 7. Ongoing Reference

If at any point during development the user asks *"Why are we doing this?"*, *"What's the point of this audit?"*, or *"How does this fit into the bigger picture?"*, use `explain-and-teach` to answer — anchoring the explanation back to the workflow mental model established during onboarding.
