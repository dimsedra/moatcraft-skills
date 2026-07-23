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

### Phase 2: Technical Specification Layer
2. **Technical Spec & Execution Branching**:
   - **`backend-architect`**: Establishes **Technical System Specifications**, data ownership, API paradigms, reliability targets, and backend technical moats. Generates `backend-architecture-spec.md`.
   - **`front-end-designer`**: Establishes **Front-End Visual & Interactive Specifications**, 2nd/3rd idea UI concepts, breathable hierarchy, and WebGL/Canvas visual moats.

### Phase 3: Active Development Loop (Iterative Core)
3. **`implementation-tdd`**: Execute artifact-driven TDD (Red ➔ Green). Write failing tests mapping to technical/brand specifications, then write minimal code to pass them.
4. **`alignment-audit`**: Audit the diff against technical and brand spec artifacts (`backend-architecture-spec.md`, `brand-product-alignment-spec.md`, `implementation_plan.md`) for plan fidelity, missing deliverables, or scope creep.
   - **Loop Trigger**: If `alignment-audit` reports `DEVIATION DETECTED`, cycle back immediately to `implementation-tdd` to fulfill missing specs or revert unapproved changes.
5. **`code-review`**: Perform a parallel two-axis review (Standards & Spec) evaluating code quality, Fowler smells, and edge-case robustness.
   - **Loop Trigger**: If `code-review` reports quality breaches, unhandled exceptions, or architectural smells, cycle back to `implementation-tdd` to adjust tests and refactor logic.

### Cross-Cutting Skill: `explain-and-teach`
- **`explain-and-teach`**: Can fire at **any point** in the development loop whenever the user asks *"why"*, requests rationale, or wants to understand trade-offs. Adapts dynamically to deliver ONLY the requested slice (Trade-offs, Ripple Effects, or Mental Models) without forcing a rigid full-lecture template.

### Phase 4: Loop Exit & Completion
- Once both `alignment-audit` (Plan Fidelity) and `code-review` (Quality & Robustness) report **Clean Pass**, the iteration loop closes.
- The feature is ready for merge/ship, and the agent initiates the next development loop iteration.
