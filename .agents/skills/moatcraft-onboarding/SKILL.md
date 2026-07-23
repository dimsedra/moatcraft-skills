---
name: moatcraft-onboarding
description: Conduct an interactive onboarding session and generate moatcraft-contract.md to align human users and AI agents on operating principles, skill rationale, and execution workflows. Use when introducing new users to Moatcraft or initializing a project.
---

# Moatcraft Onboarding & Working Contract

This skill introduces new users to the **Moatcraft** development suite, demystifying the "why" behind each skill, eliminating blackbox confusion, and establishing an explicit **Working Contract (`moatcraft-contract.md`)** between the human co-founder and the AI agent.

---

## 1. Why Moatcraft Exists (The Strategic Rationale)

Most AI coding tools operate as "blackboxes"—they generate quick commodity code, blindly agree with questionable design choices, and produce generic UI templates that lack defensible identity.

Moatcraft exists to build **Defensible Architectural & Design Moats** through a continuous, artifact-driven development loop:
- **No Commodity UI**: Pushes past 1st generic ideas to 2nd/3rd brand-anchored concepts.
- **No Sycophancy**: Pushes back constructively on logical/technical contradictions.
- **No Unchecked Code**: Every feature is verified via TDD, spec alignment audits, and dual-axis code reviews.

---

## 2. The Skill Suite Architecture & Rationale

| Layer | Skill | Why It Exists (The "Why") |
| :--- | :--- | :--- |
| **Strategy** | `brand-product-alignment` | Establishes identity boundaries ("What it IS vs. IS NOT") so code reflects brand authority. |
| **Visual Spec** | `front-end-designer` | Materializes brand textures, opinionated fonts, and calculated whitespace without breaking usability. |
| **Backend Spec** | `backend-architect` | Defines data flow, SLAs, reliability targets, and technical moats in jargon-free dialogue. |
| **Roadmap** | `progress-mapper` | Decomposes specs into living, git-mapped tasks and atomic Red-Green TDD sub-tasks. |
| **Execution** | `implementation-tdd` | Executes artifact-driven Red-Green TDD on isolated feature branches. |
| **Fidelity** | `alignment-audit` | Upstream auditor preventing scope creep and unapproved plan deviations before PR merge. |
| **Quality** | `code-review` | Dual-axis review evaluating code smells (Fowler baseline) and domain correctness. |
| **Learning** | `explain-and-teach` | Delivers adaptive, high-level mental models and human abstractions without fluff. |
| **Orchestration**| `agentic-dev-loop` | Manages the bi-directional feedback loop and upstream cascade re-audits. |

---

## 3. The Working Contract Principles

When initializing Moatcraft, the human user and AI agent agree to 5 Core Mandates:

1. **The Anti-Yes-Man Mandate**: The agent is obligated to challenge unexamined assumptions, reject generic 1st ideas, and offer proactive alternative recommendations.
2. **Form-Function Equilibrium**: Aesthetics and surface materials must never compromise WCAG accessibility, intuitive usability, or add cognitive noise.
3. **Calculated Whitespace Control**: Whitespace is an active instrument of power to control how viewers consume and digest information.
4. **Bi-Directional Cascade**: Strategic shifts trigger downstream spec re-audits; execution contradictions trigger upstream escalations.
5. **High-Level Human Abstractions First**: Explanations default to intuitive mental models; low-level code mechanics are provided on demand in hybrid form.

---

## 4. Execution Workflow

### Step 1: Interactive Onboarding Dialogue
Walk the user through the 5 Working Contract Mandates and the skill suite rationale in conversational, high-level terms. Ask:
- *What type of project are you building? (Front-End First, Back-End First, or Full-Stack)*
- *What is the primary defensible moat you want to achieve?*

### Step 2: Synthesis of `moatcraft-contract.md`
Generate `moatcraft-contract.md` at the project root:

```markdown
# Moatcraft Working Contract: [Project Name]

## 1. Project Alignment & Moat Target
- **Primary Strategy Route**: [Front-End First | Back-End First | Full-Stack]
- **Target Moat Signature**: ...

## 2. Core Working Principles
- [x] Anti-Yes-Man Protocol Active (Agent pushes back on commodity solutions)
- [x] Form-Function Equilibrium (WCAG AA/AAA compliance enforced)
- [x] Calculated Whitespace Control (Information flow pacing active)
- [x] Bi-Directional Cascade Protocol (Upstream/downstream re-alignment enabled)
- [x] High-Level Abstractions First (Hybrid code mapping on demand)

## 3. Active Skill Pipeline & Next Step
- **Next Recommended Skill**: `brand-product-alignment` or `agentic-dev-loop`
```

Commit `moatcraft-contract.md` to git (`docs(setup): initialize moatcraft working contract`).

### Step 3: Route Handoff
Guide the user directly into the next recommended skill (`brand-product-alignment` or `agentic-dev-loop`).
