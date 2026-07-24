---
name: code-review
description: Conduct a product-aware, two-axis code review (Standards and Spec) evaluating code quality, edge-case robustness, and domain alignment comparing HEAD against a fixed point using parallel sub-agents. Categorize findings by urgency/importance level with explicit "WHY" rationales. Use when reviewing feature branches, Pull Requests (PRs), work-in-progress, or changes since a commit, tag, or branch.
---

# Code Review (Product-Aware Two-Axis Review)

This skill performs a product-aware, dual-axis code review evaluating **Code Quality & Robustness** alongside **Spec & Domain Alignment** for feature branches and Pull Requests. 

Findings are strictly classified by **Urgency & Importance** and mandate an explicit **"WHY" (Systemic Rationale & Consequence)** for every issue detected.

---

## 1. Operating Foundations

### A. Dual-Axis Review Model
A change can succeed on one axis and fail on the other:
- **Standards Pass, Spec Fail**: Code is clean and idiomatic, but violates domain rules or fails edge cases.
- **Spec Pass, Standards Fail**: Feature satisfies business requirements, but introduces architectural smells or fragile error handling.

### B. Urgency & Severity Matrix

| Level | Severity Label | Definition & Threshold | PR Gate Action |
| :--- | :--- | :--- | :--- |
| **🔴 Level 1** | **Critical (Blocker)** | Security vulnerabilities, data loss risks, unhandled crash conditions in primary flows, or breaking API changes. | **Merge Blocker**: Must fix immediately before PR approval. |
| **🟡 Level 2** | **High (Major)** | Major Fowler architectural smells, race conditions, unhandled timeouts/error swallowing, or severe performance bottlenecks. | **Action Required**: Should fix before merge unless explicitly waived. |
| **🔵 Level 3** | **Medium (Moderate)** | Standard code smells (duplicated logic, primitive obsession), minor edge-case gaps, or missing documentation. | **Recommended**: Can merge with follow-up task logged. |
| **⚪ Level 4** | **Low (Advisory)** | Naming clarity, micro-suggestions, or style polish. | **Advisory**: Optional polish, does not delay merge. |

### C. Mandatory Finding Schema (The "WHY" Requirement)
Every finding MUST connect the technical code detail directly with its high-level systemic/user impact:

```markdown
- **[Severity Badge] [File Location & Line Number]**: Brief Summary
  - **The "WHY" (Systemic Impact)**: Clear, non-jargon explanation of why this matters and what happens systemically if left unaddressed.
  - **Root Cause / Code Detail**: The specific code smell, missing edge-case check, or spec mismatch.
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

Invoke two sub-agents concurrently via `invoke_subagent` in a single tool call (`Subagents: [...]`). Inject the 5-Layer Context Chain into both sub-agents upfront.

### A. Standards & Quality Sub-Agent
- **Input**: Context Chain + `git diff` + Fowler Smells & Edge-Case Checklist.
- **Checklist Focus**:
  - *Fowler Smells*: Mysterious Name, Duplicated Code, Feature Envy, Primitive Obsession, Shotgun Surgery, Divergent Change.
  - *Robustness*: Unhandled exceptions/nulls, race conditions, stale cache reads, unclosed resources, silent error swallowing.
- **Output Requirement**: Findings grouped by Severity Level (🔴 Critical ➔ ⚪ Low) with explicit "WHY" (Systemic Impact) for each item.

### B. Spec & Product Alignment Sub-Agent
- **Input**: Context Chain + `git diff` + Approved Spec/PRD files.
- **Checklist Focus**:
  - Missing or partial spec requirements.
  - Scope creep / unrequested behavior.
  - Logic that breaks domain intent or user flows.
- **Output Requirement**: Findings grouped by Severity Level (🔴 Critical ➔ ⚪ Low) with quoted spec lines and explicit "WHY" (User/Business Impact) for each item.

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

## 2. Standards & Robustness Review

### 🔴 Critical (Blockers)
- **`src/services/payment.ts:L45`**: Unhandled Network Timeout
  - **The "WHY" (Systemic Impact)**: Leaves transactions in zombie state, causing client/DB data drift and lost revenue.
  - **Code Detail**: Fetch call lacks abort controller or timeout handler.
  - **Action**: Wrap call with `AbortSignal.timeout(5000)` and handle `TimeoutError`.

### 🟡 High (Major Issues)
...

### 🔵 Medium (Moderate Issues)
...

### ⚪ Low (Minor / Advisory)
...

---

## 3. Spec & Domain Review

### 🔴 Critical (Spec Blockers)
...

### 🟡 High (Major Spec Drift)
...

### 🔵 Medium (Moderate Spec Gaps)
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
