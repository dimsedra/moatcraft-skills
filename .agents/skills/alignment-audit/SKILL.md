---
name: alignment-audit
description: Conduct a plan-and-spec alignment audit using auditor sub-agents to verify that implemented code diffs match approved plans/PRDs/specs. Findings are categorized by urgency/importance level with explicit "WHY" (strategic & product impact) rationales. Use before PR merge.
---

# Alignment Audit

This skill acts as an upstream plan & specification auditor executed **before** `code-review`. It verifies whether the actual code diff on a feature branch or Pull Request matches approved implementation plans, PRDs, or specification artifacts. 

Findings are strictly formatted by **Urgency & Importance Level** and include an explicit **"WHY" (Strategic & Product Impact)** for every discrepancy identified.

> **Scope Note:** This skill ignores code quality, style, and refactoring smells (which are evaluated by `code-review`). It focuses strictly on **Plan Fidelity**, **Missing Deliverables**, and **Unapproved Deviations/Scope Creep**.

---

## Execution Workflow Sequence

`git checkout -b feat/...` ➔ `implementation-tdd` (Red ➔ Green) ➔ `alignment-audit` ➔ `code-review` ➔ `PR Merge`

---

## Urgency & Importance Classification Matrix

Every discrepancy identified during alignment audit MUST be classified into one of the following 4 levels:

| Level | Severity Label | Definition & Threshold | Audit Gate Impact |
| :--- | :--- | :--- | :--- |
| **🔴 Level 1** | **Critical (Spec Blocker)** | Core feature promised in spec is completely omitted, unapproved architectural pivot introduced, or scope creep that violates security/brand identity boundaries. | **Gate Status: DEVIATION DETECTED (Blocker)**. Must resolve or revert before proceeding. |
| **🟡 Level 2** | **High (Significant Drift)** | Partial implementation of key requirement, unannounced public interface/schema change, or unapproved complexity added without spec update. | **Gate Status: DEVIATION DETECTED**. Requires resolution or spec sign-off. |
| **🔵 Level 3** | **Medium (Minor Gap / Acceptable Refactor)** | Secondary requirement deferred, minor UI copy/text variation, or harmless utility co-located in diff. | **Gate Status: PASS WITH WARNING**. Can proceed with follow-up task logged. |
| **⚪ Level 4** | **Low (Advisory / Spec Clarification)** | Ambiguity in plan vs. diff that requires user clarification rather than code rollback. | **Gate Status: PASSED (Advisory)**. Informative only. |

---

## Mandatory Finding Schema (The "WHY" Requirement)

Every missing item, incomplete feature, or unplanned deviation reported MUST articulate the **"WHY" (Strategic & Product Impact)** — explaining *why* the discrepancy matters to product vision, user experience, system architecture, or brand positioning:

```markdown
- **[Severity Badge] [Plan Section / Diff Hunk]**: Discrepancy Summary
  - **The "WHY" (Strategic & Product Impact)**: Clear, non-jargon explanation of why this discrepancy matters, what user experience or system goal is compromised, and the business/technical risk of leaving it as-is.
  - **Spec Expectation vs. Diff Reality**: Exact quote from spec vs. what is actually present in `git diff`.
  - **Alignment Action**: Concrete step to achieve alignment (e.g. implement missing logic, revert unapproved code, or update spec artifact with user sign-off).
```

---

## Execution Steps

### Step 1: Plan Artifact, Branch & Diff Pinning
Locate the authoritative plan/specification source and target git comparison point:
1. **Plan Sources**: Look for `progress-map.md`, `brand-product-alignment-spec.md`, `front-end-design-spec.md`, `backend-architecture-spec.md`, `implementation_plan.md`, or GitHub Issues (`#123`).
2. **Git Branch & PR Target**: Pin the base comparison ref (e.g. `git rev-parse origin/main` or target PR base branch) and capture `git diff <base-ref>...HEAD`.

**Completion Criterion**: Spec artifact is loaded, feature branch verified, and non-empty PR diff is captured.

### Step 2: 5-Layer Context Synthesis (Main Agent Responsibility)
**The main agent MUST perform the context discovery directly** by inspecting repository documentation (`README.md`, `PRD.md`, `docs/`, `specs/`) and recent `git log`. **Do NOT delegate context discovery to sub-agents**, as sub-agents start with a blank context window.

> **Crucial Independence Rule (Informative, Non-Directive Context):**
> The main agent provides purely **objective background facts** (product domain, active feature branch, PRD requirements, git commit list). The main agent **MUST NOT dictate conclusions, express opinions on pass/fail status, or steer the sub-agent toward a preferred finding**. Sub-agents must remain completely autonomous and form unbiased judgements strictly from the empirical code diff and specification artifacts.

Synthesize a neutral, objective 5-layer context block to feed into the auditor sub-agent:

1. **Product Understanding**: Objective purpose of the app/system and high-level architecture.
2. **Active Branch & Issue**: Feature branch name (`feat/...`) and associated PR / GitHub Issue (`#123`).
3. **Current Phase Objective**: Stated sub-task goals from `progress-map.md`.
4. **Planned Specs vs. Delivered Diff**: List of planned items vs. list of modified files in `git diff`.
5. **Audit Boundary Constraints**: Objective focus on spec compliance and deviation detection.

**Completion Criterion**: 5-layer objective context block synthesized directly by the main agent and ready for sub-agent prompt injection.

### Step 3: Auditor Sub-Agent Spawning
Spawn a dedicated auditor sub-agent via `invoke_subagent` (`TypeName: "research"` or `"self"`, `Role: "Plan Alignment Auditor"`).

#### Auditor Sub-Agent Prompt Instructions
Inject:
- The 5-Layer Context Block from Step 2.
- Full text of the approved plan/spec artifact (`progress-map.md` / `spec.md`).
- Complete `git diff` and commit list (`git log origin/main..HEAD`).
- Task brief:
  *"Act as an uncompromising Specification Auditor. Compare the code diff against the approved plan/spec across 3 categories:
   (a) **Fully Delivered**: Features/tasks promised in the plan that are completely implemented.
   (b) **Missing or Partial**: Tasks explicitly promised in the plan that are missing or incomplete in the diff.
   (c) **Unplanned Deviations & Scope Creep**: Modifications, additions, or architectural changes present in the diff that were NEVER mentioned or approved in the plan.
   
   Categorize all findings by Severity: 🔴 Critical (Spec Blocker), 🟡 High (Significant Drift), 🔵 Medium (Minor Gap), ⚪ Low (Advisory).
   For EVERY finding in (b) and (c), you MUST state:
   1. Location / Spec quote
   2. The 'WHY' (Strategic & Product Impact — explain clearly why this discrepancy matters to the product/user/system)
   3. Spec Expectation vs Diff Reality
   4. Alignment Action.
   Do NOT comment on code formatting or variable names. Keep under 500 words."*

**Completion Criterion**: Auditor sub-agent launched and audit report received.

### Step 4: Audit Synthesis & Gate Decision
Synthesize the sub-agent's findings into `alignment-audit-report.md` (and present summary to user):

```markdown
# Alignment Audit Report

## 1. Product, Branch & PR Context
- **Product**: [Product Understanding]
- **Target Branch**: `feat/feature-name` -> `main`
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
- ...

### 🔵 Medium Severity Discrepancies (Minor Gaps)
- ...

### ⚪ Low Severity Items (Advisories / Clarifications)
- ...

---

## 3. Audit Gate Decision
- **Status**: [🟢 PASSED | 🟡 PASS WITH WARNING | 🔴 DEVIATION DETECTED]
- **Critical Blockers**: N
- **High Drift Items**: N
- **Recommendation**: [Proceed to `code-review` OR Resolve Plan Deviations First]
```

Present the summary to the user and specify whether to proceed directly to `code-review`.

**Completion Criterion**: `alignment-audit-report.md` written and gate decision presented.
