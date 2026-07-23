---
name: agentic-dev-loop
description: Orchestrate the continuous agentic development loop across brand alignment, front-end design, TDD implementation, alignment auditing, and two-axis code review. Use when guiding a feature, refactor, or iteration through the full development loop.
---

# Agentic Development Loop

This skill defines and orchestrates the **Continuous Agentic Development Loop**. Development is not a one-way linear pipeline; it is an iterative feedback loop where audit failures and code review findings cycle back into TDD implementation until quality and spec fidelity are locked.

---

## The Development Loop Architecture

```
                    ┌─────────────────────────┐
                    │ brand-product-alignment │ (Pure Brand & Product Identity)
                    └────────────┬────────────┘
                                 │
                   ┌─────────────┴─────────────┐
                   ▼                           ▼
      ┌─────────────────────────┐ ┌─────────────────────────┐
      │   front-end-designer    │ │    backend-architect    │
      │ (Visual & UI Execution) │ │ (Technical System Spec) │
      └────────────┬────────────┘ └────────────┬────────────┘
                   │                           │
                   └─────────────┬─────────────┘
                                 │
                                 ▼
 ┌─────────────────────────────────────────────────────────────┐
 │                THE ACTIVE DEVELOPMENT LOOP                  │
 │                                                             │
 │            ┌───────────────────────────────────┐            │
 │ ┌─────────►│        implementation-tdd         │◄─────────┐ │
 │ │          │          (Red ➔ Green)            │          │ │
 │ │          └─────────────────┬─────────────────┘          │ │
 │ │                            │                            │ │
 │ │                            ▼                            │ │
 │ │          ┌───────────────────────────────────┐          │ │
 │ │          │          alignment-audit          │          │ │
 │ │          │     (Plan & Spec Fidelity)        │          │ │
 │ │          └─────────────────┬─────────────────┘          │ │
 │ │                            │                            │ │
 │ │             [Plan Deviations / Gaps?]                   │ │
 │ │             /                       \                   │ │
 │ │          (Yes)                     (Passed)             │ │
 │ │            │                          │                 │ │
 │ └────────────┘                          ▼                 │ │
 │                            ┌───────────────────┐          │ │
 │                            │    code-review    │          │ │
 │                            │(Quality & Robust) │          │ │
 │                            └─────────┬─────────┘          │ │
 │                                      │                    │ │
 │                        [Quality Breaches Found?]          │ │
 │                        /                       \          │ │
 │                     (Yes)                      (Pass)     │ │
 │                       │                          │        │ │
 │                       └──────────────────────────┼────────┘ │
 └──────────────────────────────────────────────────┼──────────┘
                                                    ▼
                                            Ship / Next Loop Iteration
```

---

## Loop Dynamics & Skill Responsibilities

### Phase 1: Brand & Product Alignment Layer
1. **`brand-product-alignment`**: Focuses purely on brand-product positioning, product vibe, 3-second impression, boundaries (*what it is vs. what it is not*), and blacklisted clichés. Generates `brand-product-alignment-spec.md`.

### Phase 2: Technical Specification & Roadmap Layer
2. **Technical Spec Branching**:
   - **`backend-architect`**: Establishes **Technical System Specifications**, data ownership, API paradigms, reliability targets, and backend technical moats. Generates `backend-architecture-spec.md`.
   - **`front-end-designer`**: Establishes **Front-End Visual Specifications**, opinionated typography, universal component moats, 2nd/3rd idea UI concepts, and interactive physics. Generates `front-end-design-spec.md`.
3. **`progress-mapper` (Roadmap & Progress Bridge)**:
   - Ingests spec artifacts (`brand-product-alignment-spec.md`, `front-end-design-spec.md`, `backend-architecture-spec.md`) and breaks them down into a living roadmap of Milestones, Tasks, and atomic `implementation-tdd` sub-tasks stored in `progress-map.md`.

### Phase 3: Active Development Loop (Iterative Core)
4. **`implementation-tdd`**: Execute artifact-driven TDD (Red ➔ Green). Select the next pending sub-task from `progress-map.md`, write failing tests mapping to specs, then write minimal code to pass them.
5. **`alignment-audit`**: Audit the diff against technical/brand spec artifacts for plan fidelity, missing deliverables, or scope creep.
   - **Loop Trigger**: If `alignment-audit` reports `DEVIATION DETECTED`, cycle back immediately to `implementation-tdd` to fulfill missing specs or revert unapproved changes.
6. **`code-review`**: Perform a parallel two-axis review (Standards & Spec) evaluating code quality, Fowler smells, and edge-case robustness.
   - **Loop Trigger**: If `code-review` reports quality breaches, unhandled exceptions, or architectural smells, cycle back to `implementation-tdd` to adjust tests and refactor logic. Upon **Clean Pass**, mark the sub-task complete `[x]` in `progress-map.md`.

### Cross-Cutting Skill: `explain-and-teach`
- **`explain-and-teach`**: Can fire at **any point** in the development loop whenever the user asks *"why"*, requests rationale, or wants to understand trade-offs. Adapts dynamically to deliver ONLY the requested slice (Trade-offs, Ripple Effects, or Mental Models) without forcing a rigid full-lecture template.

### Phase 4: Loop Exit & Completion
- Once both `alignment-audit` (Plan Fidelity) and `code-review` (Quality & Robustness) report **Clean Pass**, the iteration loop closes.
- The feature is ready for merge/ship, and the agent initiates the next development loop iteration.
