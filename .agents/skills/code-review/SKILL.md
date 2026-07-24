---
name: code-review
description: Conduct a rigorous code quality and edge-case robustness review comparing HEAD against a fixed point using parallel sub-agents. Categorize findings by urgency/importance level with explicit "WHY" rationales. Use when reviewing feature branches, Pull Requests (PRs), work-in-progress, or changes since a commit, tag, or branch.
---

# Code Review (Code Quality & Edge-Case Robustness Review)

This skill performs a rigorous code review focusing on **Code Health & Maintainability** alongside **Edge-Case & Runtime Robustness** for feature branches and Pull Requests.

> **Separation of Concerns Note:** Plan fidelity, missing spec deliverables, and scope creep are audited upstream by `alignment-audit`. `code-review` focuses strictly on code quality, architecture smells, and technical robustness.

Findings are strictly classified by **Urgency & Importance** and mandate an explicit **"WHY" (Systemic Rationale & Consequence)** for every issue detected.

---

## 1. Operating Foundations

### A. Dual-Axis Technical Focus
- **Axis 1: Code Health & Maintainability**: Refactoring smells (Fowler smells), DRY violations, naming clarity, modularity, and technical debt.
- **Axis 2: Edge-Case & Runtime Robustness**: Unhandled exceptions, boundary conditions, async race conditions, resource leaks, and state invalidation.

### B. Urgency & Severity Matrix

| Level | Severity Label | Definition & Threshold | PR Gate Action |
| :--- | :--- | :--- | :--- |
| **🔴 Level 1** | **Critical (Blocker)** | Security vulnerabilities, data loss risks, unhandled crash conditions in primary flows, or memory leaks. | **Merge Blocker**: Must fix immediately before PR approval. |
| **🟡 Level 2** | **High (Major)** | Major Fowler architectural smells, subtle race conditions, unhandled timeouts/error swallowing, or severe performance bottlenecks. | **Action Required**: Should fix before merge unless explicitly waived. |
| **🔵 Level 3** | **Medium (Moderate)** | Standard code smells (duplicated logic, primitive obsession), minor edge-case gaps, or missing inline documentation. | **Recommended**: Can merge with follow-up task logged. |
| **⚪ Level 4** | **Low (Advisory)** | Naming clarity, micro-suggestions, or style polish. | **Advisory**: Optional polish, does not delay merge. |

### C. Mandatory Finding Schema (The "WHY" Requirement)
Every finding MUST connect technical code detail directly with its high-level systemic impact:

```markdown
- **[Severity Badge] [File Location & Line Number]**: Brief Summary
  - **The "WHY" (Systemic Impact)**: Clear, non-jargon explanation of why this matters and what happens systemically if left unaddressed.
  - **Root Cause / Code Detail**: The specific code smell, missing edge-case check, or state invalidation risk.
  - **Remediation Action**: Concrete code fix or refactoring steps.
```

---

## 2. Context Synthesis & Diff Discovery

### Step 1: Fixed Point Pinning & Diff Capture
1. Resolve target reference (default: `origin/main`): `git rev-parse <fixed-point>`
2. Capture commit history: `git log <fixed-point>..HEAD --oneline`
3. Capture merge-base diff: `git diff <fixed-point>...HEAD`

### Step 2: 5-Layer Context Synthesis (Main Agent)
Synthesize objective background facts directly (do NOT delegate to sub-agents):
1. **Product Understanding**: App purpose, target users, high-level architecture.
2. **Current Phase**: Roadmap stage or release cycle phase.
3. **Phase Objective**: Feature set or milestone targeted in this branch.
4. **Work Done**: Objective summary of modifications in the diff.
5. **Review Targets**: Key quality metrics, data flow touchpoints, and edge-case boundaries.

---

## 3. Parallel Sub-Agent Execution

Invoke two technical sub-agents concurrently via `invoke_subagent` in a single tool call (`Subagents: [...]`). Inject the 5-Layer Context Chain into both sub-agents upfront.

### A. Code Health & Maintainability Sub-Agent
- **Input**: Context Chain + `git diff` + Fowler Code Smells Baseline.
- **Checklist Focus**:
  - *Fowler Smells*: Mysterious Name, Duplicated Code, Feature Envy, Primitive Obsession, Repeated Switches, Shotgun Surgery, Divergent Change, Speculative Generality, Message Chains, Middle Man.
  - *Architecture & Cleanliness*: Single Responsibility violations, tight coupling, hardcoded values, missing type safety.
- **Output Requirement**: Findings grouped by Severity Level (🔴 Critical ➔ ⚪ Low) with explicit "WHY" (Systemic/Maintainability Impact) for each item.

### B. Edge-Case & Runtime Robustness Sub-Agent
- **Input**: Context Chain + `git diff` + Robustness Checklist.
- **Checklist Focus**:
  - *Exception & Error Recovery*: Unhandled exceptions, null/undefined dereferences, missing payload fields, network timeouts, silent error swallowing.
  - *Concurrency & State*: Race conditions, stale cache reads, unclosed sockets/streams, state machine invalidations.
  - *Resource & Performance*: Unclosed event listeners, memory leaks, inefficient loops.
- **Output Requirement**: Findings grouped by Severity Level (🔴 Critical ➔ ⚪ Low) with explicit "WHY" (Systemic/Runtime Risk) for each item.

---

## 4. Structured Dual Reporting & PR Gate Decision

Synthesize findings into the final review report:

```markdown
# Code Review Report

## 1. Context & Scope
- **Target Branch**: `feat/feature-name` ➔ `main`
- **Associated Issue**: `#123`
- **Review Scope**: [Layer 4 & 5 Summary]

---

## 2. Code Health & Maintainability Review

### 🔴 Critical (Blockers)
- **`src/services/payment.ts:L45`**: Mysterious Name & Tight Coupling
  - **The "WHY" (Systemic Impact)**: Increases cognitive overhead and risk of regression during future maintenance.
  - **Code Detail**: Variable `x` obscures payment token state.
  - **Action**: Rename to `paymentToken` and encapsulate logic.

### 🟡 High (Major Issues)
...

### 🔵 Medium (Moderate Issues)
...

### ⚪ Low (Minor / Advisory)
...

---

## 3. Edge-Case & Runtime Robustness Review

### 🔴 Critical (Runtime Blockers)
- **`src/api/checkout.ts:L88`**: Unhandled Network Timeout
  - **The "WHY" (Systemic Impact)**: Leaves transactions in zombie state, causing client/DB data drift and lost revenue.
  - **Code Detail**: Fetch call lacks abort controller or timeout handler.
  - **Action**: Wrap call with `AbortSignal.timeout(5000)` and handle `TimeoutError`.

### 🟡 High (Major Robustness Risks)
...

### 🔵 Medium (Moderate Edge Cases)
...

### ⚪ Low (Minor Advisory)
...

---

## 4. PR Gate Recommendation
- **Status Summary**: N Critical | N High | N Medium | N Low
- **Decision**: 
  - 🟢 **APPROVE**: Zero Critical/High issues. Ready to merge.
  - 🟡 **REQUEST CHANGES**: High issues present. Resolution required before merge.
  - 🔴 **RE-ROUTE TO TDD**: Critical blockers or fundamental smells present. Cycle back to `implementation-tdd`.
```
