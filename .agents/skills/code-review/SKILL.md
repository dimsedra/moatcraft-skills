---
name: code-review
description: Conduct a product-aware code quality and contextual "What-If" stress-testing review comparing HEAD against a fixed point using parallel sub-agents. Evaluates code health, Fowler smells, and stress-tests realistic failure scenarios ("Given work A, if B happens, will it break?"). Categorize findings by urgency level with explicit "WHY" rationales. Use when reviewing feature branches, PRs, or commits.
---

# Code Review (Code Quality & Contextual "What-If" Stress-Testing)

This skill performs a product-aware code review focused on **Code Health & Maintainability** and **Contextual "What-If" Stress-Testing** for feature branches and Pull Requests.

> **Separation of Concerns Note:** Plan fidelity and ensuring every spec item is 100% met are audited upstream by `alignment-audit`. `code-review` assumes spec completeness and focuses strictly on code quality, refactoring, and **stress-testing how the code behaves when subjected to realistic "What-If" scenarios**.

Findings are strictly classified by **Urgency & Importance** and mandate an explicit **"WHY" (Systemic Rationale & Consequence)** for every issue detected.

---

## 1. Operating Foundations

### A. Dual-Axis Technical Focus

#### Axis 1: Code Health & Maintainability
- Fowler code smells (Mysterious Name, Duplicated Code, Feature Envy, Primitive Obsession, Shotgun Surgery, etc.).
- DRY principles, modularity, readability, and technical debt reduction.

#### Axis 2: Contextual "What-If" Stress-Testing & Robustness
- **The Core Paradigm**: *"Given feature/work context A, if scenario B occurs, will it break?"*
- **Relevance Rule**: Stress-testing must NOT be generic or arbitrary. It must be **strictly contextual to the work being reviewed**:
  - *If building a Payment Flow (A)*: Stress-test payment gateway timeouts, double-submission clicks, expired tokens, network drops mid-transaction, and invalid currency payloads.
  - *If building a Search/Filter Component (A)*: Stress-test empty query states, special character injections, rapid keystroke race conditions, and massive result sets.
  - *If building an Async Queue Worker (A)*: Stress-test queue backlog spikes, worker thread crashes, duplicate job processing, and unhandled rejection loops.

### B. Urgency & Severity Matrix

| Level | Severity Label | Definition & Threshold | PR Gate Action |
| :--- | :--- | :--- | :--- |
| **🔴 Level 1** | **Critical (Blocker)** | Security vulnerabilities, data loss/corruption risks, or fatal crashes triggered under realistic "What-If" scenario B. | **Merge Blocker**: Must fix immediately before PR approval. |
| **🟡 Level 2** | **High (Major)** | Major Fowler smells, subtle race conditions, unhandled timeouts/error swallowing, or degraded state handling under "What-If" conditions. | **Action Required**: Should fix before merge unless explicitly waived. |
| **🔵 Level 3** | **Medium (Moderate)** | Standard code smells (duplicated logic, primitive obsession), minor edge-case gaps, or missing inline documentation. | **Recommended**: Can merge with follow-up task logged. |
| **⚪ Level 4** | **Low (Advisory)** | Naming clarity, micro-suggestions, or style polish. | **Advisory**: Optional polish, does not delay merge. |

### C. Mandatory Finding Schema (The "WHY" Requirement)
Every finding MUST connect the technical flaw or "What-If" failure directly to its systemic impact:

```markdown
- **[Severity Badge] [File Location & Line Number]**: Brief Summary
  - **Contextual "What-If" Scenario**: *"Given [Work A], if [Scenario B] happens..."*
  - **The "WHY" (Systemic Impact)**: Clear, non-jargon explanation of what breaks systemically or for the user if left unaddressed.
  - **Root Cause / Code Detail**: The specific code smell, missing check, or state invalidation risk.
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
4. **Work Done (Work A)**: Objective summary of modifications in the diff.
5. **Stress-Test Surface Area**: Specific boundary conditions and realistic failure scenarios relevant to Work A.

---

## 3. Parallel Sub-Agent Execution

Invoke two technical sub-agents concurrently via `invoke_subagent` in a single tool call (`Subagents: [...]`). Inject the 5-Layer Context Chain into both sub-agents upfront.

### A. Code Health & Maintainability Sub-Agent
- **Input**: Context Chain + `git diff` + Fowler Code Smells Baseline.
- **Checklist Focus**:
  - *Fowler Smells*: Mysterious Name, Duplicated Code, Feature Envy, Primitive Obsession, Repeated Switches, Shotgun Surgery, Divergent Change, Speculative Generality, Message Chains, Middle Man.
  - *Architecture & Cleanliness*: Single Responsibility violations, tight coupling, hardcoded values, missing type safety.
- **Output Requirement**: Findings grouped by Severity Level (🔴 Critical ➔ ⚪ Low) with explicit "WHY" (Maintainability Impact) for each item.

### B. Contextual "What-If" Stress-Testing Sub-Agent
- **Input**: Context Chain + `git diff` + Feature Context (Work A).
- **Checklist Focus**:
  - Formulate 3-5 realistic **"What-If" scenarios** specifically tailored to Work A: *"If user/system does B, does A break?"*
  - *Exception & Boundary Recovery*: Null/undefined payload fields, boundary inputs, timeouts, network drops.
  - *Concurrency & State Machine Invalidation*: Concurrent mutations, race conditions, stale cache reads, unclosed resources.
- **Output Requirement**: Findings grouped by Severity Level (🔴 Critical ➔ ⚪ Low) with explicit "What-If" scenario descriptions and "WHY" (Systemic Risk) for each item.

---

## 4. Structured Dual Reporting & PR Gate Decision

Synthesize findings into the final review report:

```markdown
# Code Review Report

## 1. Context & Scope
- **Target Branch**: `feat/feature-name` ➔ `main`
- **Associated Issue**: `#123`
- **Reviewed Work (Work A)**: [Layer 4 Summary]

---

## 2. Code Health & Maintainability Review

### 🔴 Critical (Blockers)
- **`src/services/payment.ts:L45`**: Mysterious Name & Tight Coupling
  - **The "WHY" (Maintainability Impact)**: Increases cognitive overhead and risk of regression during future maintenance.
  - **Code Detail**: Variable `x` obscures payment token state.
  - **Action**: Rename to `paymentToken` and encapsulate logic.

### 🟡 High (Major Issues)
...

### 🔵 Medium (Moderate Issues)
...

### ⚪ Low (Minor / Advisory)
...

---

## 3. Contextual "What-If" Stress-Testing Review

### 🔴 Critical (Runtime Stress-Test Failures)
- **`src/api/checkout.ts:L88`**: Unhandled Timeout under Payment Retry
  - **Contextual "What-If" Scenario**: *"Given checkout payment flow, if network times out during gateway retry..."*
  - **The "WHY" (Systemic Impact)**: Leaves transactions in zombie state, causing client/DB data drift and lost revenue.
  - **Code Detail**: Fetch call lacks abort controller or timeout handler.
  - **Action**: Wrap call with `AbortSignal.timeout(5000)` and handle `TimeoutError`.

### 🟡 High (Major Stress-Test Risks)
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
  - 🔴 **RE-ROUTE TO TDD**: Critical blockers or stress-test failures present. Cycle back to `implementation-tdd`.
```
