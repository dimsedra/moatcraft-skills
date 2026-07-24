---
name: progress-mapper
description: Generate and maintain a high-level progress map and task/sub-task tracker after brand-product and technical specs are established. Use when mapping out execution phases, tracking development progress, linking tasks to git branches/issues, or breaking down specs into actionable TDD tasks.
---

# Progress Mapper (High-Level Development Tracker)

This skill acts as the **strategic bridge** between specification discovery (`brand-product-alignment`, `backend-architect`, `front-end-designer`) and active execution (`implementation-tdd` ➔ `alignment-audit` ➔ `code-review`).

It ingests established specification artifacts and decomposes them into a structured, living roadmap of Milestones, Tasks, and atomic Sub-Tasks stored in `progress-map.md`, mapped directly to **Git branches, GitHub Issues, and commit SHAs**.

---

## Operating Principle: Route-Aware Task Decomposition

The progress mapper adapts dynamically based on the active strategy route:

1. **Front-End First Route**: Decomposes visual hierarchy, layout tokens, top-fold hero components, interactive states, and design moat extensions into sequential tasks.
2. **Back-End First Route**: Decomposes domain data models, persistence schemas, API endpoints, error resilience mechanisms, and backend technical moats into sequential tasks.
3. **Full-Stack Route**: Maps foundational backend data contracts first, followed by corresponding front-end consumption and interactive polish.

---

## Living Roadmap & Git Integration Protocol

The progress map is **a living document, not a rigid script**. Real-world engineering requires constant adaptation and full Git integration:

1. **Git Branch & Issue Mapping**:
   - Each Milestone/Task maps to an explicit **Git feature branch** (`branch: feat/component-name`) and optionally a **GitHub Issue** (`Issue #123`).
   - Atomic sub-tasks record their **completing Git Commit SHA** upon successful passage through `alignment-audit` and `code-review` (`[x] Sub-Task 1.1.1 (Commit: 730fb64)`).
2. **Continuous Refinement**: Tasks and sub-tasks can be refined, split, added, or re-prioritized at any point as new technical or product insights emerge during development.
3. **Phase & Task Reopening**: If an audit finding (`alignment-audit`), code review flaw (`code-review`), or product shift reveals a gap in a previously completed milestone, **the item can be reopened**:
   - Change completed status `[x]` back to `[ ]` (e.g. `[ ] Sub-Task 1.1.2 [Reopened: Discovered concurrent state bug]`).
   - Inject corrective atomic sub-tasks into `progress-map.md`.
   - Re-route the reopened sub-tasks into `implementation-tdd` to ensure full test coverage and audit compliance before re-closing.

---

## Execution Steps

### Step 1: Specification Ingestion & Validation (Main Agent Responsibility)
**The main agent MUST perform specification discovery directly** by reading existing spec artifacts:
- `brand-product-alignment-spec.md` (Brand/Product boundaries, vibe, experience moat)
- `backend-architecture-spec.md` (Data boundaries, API contracts, technical moat)
- `front-end-design-spec.md` (Visual hierarchy, opinionated typography, surface textures)

> **Inferred-Spec Guard Check**: Scan ingested spec artifacts for `[INFERRED — Review Required]` tags. If unverified inferred sections exist, **pause and request user sign-off** before generating roadmap tasks.

**Completion Criterion**: All active spec artifacts are ingested, verified free of unreviewed inferred tags, and the primary entry route (Front-End First, Back-End First, or Full-Stack) is identified.

### Step 2: Milestone & Atomic Sub-Task Breakdown
Decompose the ingested specifications into a hierarchical task structure:
- **Milestones (Phases)**: High-level logical stages of development mapped to Git Feature Branches.
- **Tasks**: Feature capabilities or architectural components linked to an optional issue tracker (`Issue #123`, `JIRA-456`, `Linear-789`, or standalone without tracker).
- **Sub-Tasks**: **Atomic TDD-sized units of work** (each small enough to be executed in a single `implementation-tdd` cycle, audited by `alignment-audit`, and reviewed by `code-review`).

**Completion Criterion**: Complete hierarchy (Milestones ➔ Tasks ➔ Atomic Sub-Tasks) is mapped with explicit Git branch assignments.

### Step 3: Progress Map Artifact Generation (`progress-map.md`)
Synthesize the roadmap into `progress-map.md` at the project root:

```markdown
# Development Progress Map: [Product / System Name]

## Execution Overview
- **Strategy Route**: [Front-End First | Back-End First | Full-Stack]
- **Target Git Branch**: `feat/main-feature`
- **Associated Issue**: `Issue #101`
- **Active Phase**: Milestone 1
- **Current Completion**: 0% (0/N Sub-Tasks completed)

---

## Milestone 1: Core Foundation & Moat Setup
> **Branch**: `feat/milestone-1-foundation` | **Issue**: `#101`

- [ ] **Task 1.1: [Feature / Architecture Component]**
  - [ ] Sub-Task 1.1.1: [Atomic TDD Scope] `[Status: Pending]`
  - [ ] Sub-Task 1.1.2: [Atomic TDD Scope] `[Status: Pending]`

- [ ] **Task 1.2: [Feature / Architecture Component]**
  - [ ] Sub-Task 1.2.1: [Atomic TDD Scope] `[Status: Pending]`

---

## Milestone 2: [Next Phase Name]
> **Branch**: `feat/milestone-2-core` | **Issue**: `#102`

- [ ] **Task 2.1: [Feature / Component]**
  - [ ] Sub-Task 2.1.1: [Atomic TDD Scope] `[Status: Pending]`
```

Present `progress-map.md` to the user for confirmation.

**Completion Criterion**: `progress-map.md` is generated, presented, and locked for the initial iteration.

### Step 4: Dynamic Progress Tracking & Refinement Loop
As development proceeds through the active loop:
1. Select the next pending atomic sub-task from `progress-map.md`.
2. Execute via `implementation-tdd` on the feature branch (Red ➔ Green).
3. Verify via `alignment-audit` and `code-review`.
4. Upon **Clean Pass**, commit changes and update `progress-map.md` by checking off `[x]` with the commit SHA:
   `[x] Sub-Task 1.1.1 (Commit: 730fb64)`.
5. If issues arise or specs evolve, apply the **Living Roadmap Protocol** to refine tasks or reopen completed phases.

**Completion Criterion**: `progress-map.md` remains updated and refined with Git commit references as the living source of truth.
