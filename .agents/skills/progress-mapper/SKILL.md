---
name: progress-mapper
description: Generate and maintain a high-level progress map and task/sub-task tracker after brand-product and technical specs are established. Use when mapping out execution phases, tracking development progress, or breaking down specs into actionable TDD tasks.
---

# Progress Mapper (High-Level Development Tracker)

This skill acts as the **strategic bridge** between specification discovery (`brand-product-alignment`, `backend-architect`, `front-end-designer`) and active execution (`implementation-tdd` ➔ `alignment-audit` ➔ `code-review`).

It ingests established specification artifacts and decomposes them into a structured, living roadmap of Milestones, Tasks, and atomic Sub-Tasks stored in `progress-map.md`.

---

## Operating Principle: Route-Aware Task Decomposition

The progress mapper adapts dynamically based on the active strategy route:

1. **Front-End First Route**: Decomposes visual hierarchy, layout tokens, top-fold hero components, interactive states, and design moat extensions into sequential tasks.
2. **Back-End First Route**: Decomposes domain data models, persistence schemas, API endpoints, error resilience mechanisms, and backend technical moats into sequential tasks.
3. **Full-Stack Route**: Maps foundational backend data contracts first, followed by corresponding front-end consumption and interactive polish.

---

## Living Roadmap Protocol (Constant Refinement & Reopening Rules)

The progress map is **a living document, not a rigid script**. Real-world engineering requires constant adaptation:

1. **Continuous Refinement**: Tasks and sub-tasks can be refined, split, added, or re-prioritized at any point as new technical or product insights emerge during development.
2. **Phase & Task Reopening**: If an audit finding (`alignment-audit`), code review flaw (`code-review`), or product shift reveals a gap in a previously completed milestone, **the item can be reopened**:
   - Change completed status `[x]` back to `[ ]` (e.g. `[ ] Sub-Task 1.1.2 [Reopened: Discovered concurrent state bug]`).
   - Inject corrective atomic sub-tasks into `progress-map.md`.
   - Re-route the reopened sub-tasks into `implementation-tdd` to ensure full test coverage and audit compliance before re-closing.
3. **Refinement Triggers**:
   - *Audit / Review Findings*: Gaps or scope deviations identified downstream.
   - *Technical Discovery*: Unexpected edge cases or API constraints discovered during the Red-Green TDD phase.
   - *Product Evolution*: Updated brand, UI, or backend architecture requirements.

---

## Execution Steps

### Step 1: Specification Ingestion (Main Agent Responsibility)
**The main agent MUST perform specification discovery directly** by reading existing spec artifacts:
- `brand-product-alignment-spec.md` (Brand/Product boundaries, vibe, experience moat)
- `backend-architecture-spec.md` (Data boundaries, API contracts, technical moat)
- Front-End UI design specs or component plans

**Completion Criterion**: All active spec artifacts are ingested, and the primary entry route (Front-End First, Back-End First, or Full-Stack) is identified.

### Step 2: Milestone & Atomic Sub-Task Breakdown
Decompose the ingested specifications into a hierarchical task structure:
- **Milestones (Phases)**: High-level logical stages of development.
- **Tasks**: Feature capabilities or architectural components.
- **Sub-Tasks**: **Atomic TDD-sized units of work** (each small enough to be executed in a single `implementation-tdd` cycle, audited by `alignment-audit`, and reviewed by `code-review`).

**Completion Criterion**: Complete hierarchy (Milestones ➔ Tasks ➔ Atomic Sub-Tasks) is mapped without unassigned requirements.

### Step 3: Progress Map Artifact Generation (`progress-map.md`)
Synthesize the roadmap into `progress-map.md` at the project root:

```markdown
# Development Progress Map: [Product / System Name]

## Execution Overview
- **Strategy Route**: [Front-End First | Back-End First | Full-Stack]
- **Active Phase**: Milestone 1
- **Current Completion**: 0% (0/N Sub-Tasks completed)

---

## Milestone 1: Core Foundation & Moat Setup
- [ ] **Task 1.1: [Feature / Architecture Component]**
  - [ ] Sub-Task 1.1.1: [Atomic TDD Scope] `[Status: Pending]`
  - [ ] Sub-Task 1.1.2: [Atomic TDD Scope] `[Status: Pending]`

- [ ] **Task 1.2: [Feature / Architecture Component]**
  - [ ] Sub-Task 1.2.1: [Atomic TDD Scope] `[Status: Pending]`

---

## Milestone 2: [Next Phase Name]
- [ ] **Task 2.1: [Feature / Component]**
  - [ ] Sub-Task 2.1.1: [Atomic TDD Scope] `[Status: Pending]`
```

Present `progress-map.md` to the user for confirmation.

**Completion Criterion**: `progress-map.md` is generated, presented, and locked for the initial iteration.

### Step 4: Dynamic Progress Tracking & Refinement Loop
As development proceeds through the active loop:
1. Select the next pending atomic sub-task from `progress-map.md`.
2. Execute via `implementation-tdd` (Red ➔ Green).
3. Verify via `alignment-audit` and `code-review`.
4. Upon **Clean Pass**, update `progress-map.md` by checking off `[x]` the completed sub-task.
5. If issues arise or specs evolve, apply the **Living Roadmap Protocol** to refine tasks or reopen completed phases.

**Completion Criterion**: `progress-map.md` remains updated and refined as the living source of truth throughout the development loop.
