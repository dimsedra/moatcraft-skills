---
name: alignment-audit
description: Conduct a plan-and-spec alignment audit using auditor sub-agents to verify that implemented code diffs match approved plans/PRDs/specs. Findings are categorized by urgency/importance level with explicit "WHY" (strategic & product impact) rationales. Use before PR merge.
---

# Alignment Audit (Plan & Specification Fidelity Audit)

This skill acts as an upstream plan & specification auditor executed **before** `code-review`. It verifies whether actual code diffs match approved implementation plans, PRDs, or specification artifacts.

Findings are strictly classified by **Urgency & Importance** and mandate an explicit **"WHY" (Strategic & Product Impact)** for every discrepancy identified.

> **Scope Note:** This skill ignores code quality, style, and refactoring smells (which are evaluated by `code-review`). It focuses strictly on **Plan Fidelity**, **Missing Deliverables**, and **Unapproved Deviations/Scope Creep**.

---

## 1. Operating Foundations

### A. Scope Boundary & Audit Purpose
- **What it audits**: Plan Fidelity (are promised features present?), Missing Deliverables, and Scope Creep (unapproved code/architectural drift).
- **What it ignores**: Formatting, variable naming, and internal code quality smells (handled downstream by `code-review`).

### B. Urgency & Severity Matrix

| Level | Severity Label | Definition & Threshold | Audit Gate Impact |
| :--- | :--- | :--- | :--- |
| **🔴 Level 1** | **Critical (Spec Blocker)** | Core feature promised in spec is missing, unapproved architectural pivot introduced, or scope creep violating security/brand boundaries. | **Gate Status: DEVIATION DETECTED (Blocker)**. Must resolve or revert before proceeding. |
| **🟡 Level 2** | **High (Significant Drift)** | Partial implementation of key requirement, unannounced public interface/schema change, or unapproved complexity added without spec update. | **Gate Status: DEVIATION DETECTED**. Requires resolution or spec sign-off. |
| **🔵 Level 3** | **Medium (Minor Gap)** | Secondary requirement deferred, minor UI copy/layout variation, or harmless utility co-located in diff. | **Gate Status: PASS WITH WARNING**. Can proceed with follow-up task logged. |
| **⚪ Level 4** | **Low (Advisory)** | Ambiguity in plan vs. diff requiring user clarification rather than code rollback. | **Gate Status: PASSED (Advisory)**. Informative only. |

### C. Mandatory Finding Schema (The "WHY" Requirement)
Every discrepancy reported MUST connect the spec gap directly with its strategic product/system impact:

```markdown
- **[Severity Badge] [Spec Section / Diff Hunk]**: Discrepancy Summary
  - **The "WHY" (Strategic & Product Impact)**: Clear, non-jargon explanation of why this matters, what user experience or system goal is compromised, and the business/technical risk of leaving it as-is.
  - **Spec Expectation vs. Diff Reality**: Exact quote from spec vs. what is actually present in `git diff`.
  - **Alignment Action**: Concrete step to achieve alignment (e.g. implement missing logic, revert unapproved code, or update spec artifact with user sign-off).
```

---

## 2. Context Synthesis & Diff Discovery

### Step 1: Plan Artifact & Diff Pinning
1. **Plan Sources**: `progress-map.md`, `brand-product-alignment-spec.md`, `front-end-design-spec.md`, `backend-architecture-spec.md`, `implementation_plan.md`, or GitHub Issues (`#123`).
2. **Git Comparison**: Pin base ref (`origin/main`) and capture `git diff <base-ref>...HEAD`.

### Step 2: 5-Layer Context Synthesis (Main Agent)
Synthesize objective background facts directly (do NOT delegate to sub-agents):
1. **Product Understanding**: App purpose and high-level architecture.
2. **Active Branch & Issue**: Feature branch name (`feat/...`) and target PR / Issue.
3. **Current Phase Objective**: Stated sub-task goals from `progress-map.md`.
4. **Planned Specs vs. Delivered Diff**: List of planned items vs. modified files in diff.
5. **Audit Boundary Constraints**: Focus on spec compliance and deviation detection.

---

## 3. Auditor Sub-Agent Execution

Spawn a dedicated auditor sub-agent via `invoke_subagent` (`Role: "Plan Alignment Auditor"`).

### Auditor Sub-Agent Prompt Instructions
- **Input**: 5-Layer Context Block + Approved Spec/Plan text + `git diff` output.
- **Task Brief**:
  *"Compare code diff against approved spec across 3 categories: (a) Fully Delivered; (b) Missing or Partial; (c) Unplanned Deviations & Scope Creep. Group findings by Severity (🔴 Critical ➔ ⚪ Low). For EVERY finding in (b) and (c), state: (1) Location/Spec quote; (2) The 'WHY' (Strategic & Product Impact); (3) Spec Expectation vs Diff Reality; (4) Alignment Action. Do NOT comment on formatting or code smells. Keep under 500 words."*

---

## 4. Structured Audit Reporting & Gate Decision

Synthesize findings into `alignment-audit-report.md`:

```markdown
# Alignment Audit Report

## 1. Product, Branch & PR Context
- **Product**: [Product Understanding]
- **Target Branch**: `feat/feature-name` ➔ `main`
- **Associated Issue / PR**: `#123`
- **Plan Artifact**: [Link to Plan/Spec File]

---

## 2. Plan Fidelity Audit

### ✅ Fully Delivered Items
- [Item 1 from Plan] (Commit: `a1b2c3d`)

### 🔴 Critical Discrepancies (Blockers)
- **[Spec Section / Diff Hunk]**: [Summary]
  - **The "WHY" (Strategic Impact)**: [Why this matters to product/user flow]
  - **Spec vs Diff**: Quoted plan `"..."` vs Diff reality
  - **Alignment Action**: [Steps to resolve]

### 🟡 High Severity Discrepancies (Significant Drift)
...

### 🔵 Medium Severity Discrepancies (Minor Gaps)
...

### ⚪ Low Severity Items (Advisories / Clarifications)
...

---

## 3. Audit Gate Decision
- **Status Summary**: N Critical | N High | N Medium | N Low
- **Decision**: 
  - 🟢 **PASSED**: Zero Critical/High discrepancies. Ready for `code-review`.
  - 🟡 **PASS WITH WARNING**: Only Medium/Low gaps present. Proceed to `code-review` with follow-up task logged.
  - 🔴 **DEVIATION DETECTED**: Critical/High discrepancies present. Cycle back to `implementation-tdd` to fulfill specs or revert unapproved changes.
```
