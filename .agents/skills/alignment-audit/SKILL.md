---
name: alignment-audit
description: Conduct a plan-and-spec alignment audit using auditor sub-agents to verify that implemented code diffs match approved plans/PRDs/specs 100% down to every item. Findings are categorized by urgency/importance level with explicit "WHY" (strategic & product impact) rationales. Use before PR merge.
---

# Alignment Audit (Plan & Specification Fidelity Audit)

This skill acts as an upstream plan & specification auditor executed **before** `code-review`. Its sole mandate is to verify that **100% of approved spec and plan deliverables are fully met without anything forgotten or omitted**.

> **Core Philosophy & Scope Boundary:**
> `alignment-audit` ensures **complete spec fidelity**. Even if the code quality, refactoring, or edge-case handling is not yet ideal (which is evaluated downstream by `code-review`), `alignment-audit` verifies that **every promised feature, task, schema requirement, and boundary constraint in the spec is present, delivered, and accounted for** — and that no unapproved scope creep was smuggled into the diff.

Findings are strictly classified by **Urgency & Importance** and mandate an explicit **"WHY" (Strategic & Product Impact)** for every discrepancy identified.

---

## 1. Operating Foundations

### A. Scope Boundary & Audit Purpose
- **What it audits**: 100% Spec Fidelity (are ALL promised features present without omission?), Missing Deliverables, and Scope Creep (unapproved code/architectural drift).
- **What it ignores**: Formatting, variable naming, code smells, and edge-case stress testing (handled downstream by `code-review`).

### B. Adversarial Skepticism & Critical Mindset by Design
Sub-agents are explicitly designed to be **skeptical, uncompromising, and critically adversarial**:
- **Zero Leniency**: The auditor MUST NOT assume a requirement is met just because code exists nearby. Every promised item must be empirically proven in the diff.
- **Scope Creep Vigilance**: Actively look for unapproved refactors, unrequested side-features, or architectural changes disguised as bug fixes.
- **Unforgiving Spec Comparison**: Compare line-by-line against `progress-map.md` and spec artifacts with zero benefit of the doubt.

### C. Secret Protection & Credential Redaction Protocol
- **Sanitized Diff Exposure**: Before passing diff context to sub-agents or generating report output, **redact and mask all credentials, tokens, passwords, and private keys** (e.g. replace with `[REDACTED_CREDENTIAL]`).
- **No Verbatim Secret Quoting**: Sub-agents and report generators must **NEVER output raw secret strings or credential hunks**. Refer to locations using file paths and line numbers (`src/auth.ts:L42`) rather than embedding raw diff hunks.

### D. Urgency & Severity Matrix

| Level | Severity Label | Definition & Threshold | Audit Gate Impact |
| :--- | :--- | :--- | :--- |
| **Level 1** | **Critical (Spec Blocker)** | Core feature promised in spec is completely missing, unapproved architectural pivot introduced, or hardcoded credentials detected. | **Gate Status: DEVIATION DETECTED (Blocker)**. Must resolve or revert before proceeding. |
| **Level 2** | **High (Significant Drift)** | Partial implementation of key requirement, unannounced public interface/schema change, or unapproved complexity added. | **Gate Status: DEVIATION DETECTED**. Requires resolution or spec sign-off. |
| **Level 3** | **Medium (Minor Gap)** | Secondary requirement deferred, minor UI copy/layout variation, or harmless utility co-located in diff. | **Gate Status: PASS WITH WARNING**. Can proceed with follow-up task logged. |
| **Level 4** | **Low (Advisory)** | Ambiguity in plan vs. diff requiring user clarification rather than code rollback. | **Gate Status: PASSED (Advisory)**. Informative only. |

### E. Mandatory Finding Schema (The "WHY" Requirement)
Every discrepancy reported MUST connect the spec gap directly with its strategic product/system impact:

```markdown
- **[Severity Badge] [Spec Section / File Location]**: Discrepancy Summary
  - **The "WHY" (Strategic & Product Impact)**: Clear, non-jargon explanation of why this missing or altered item matters, what user experience or system goal is compromised, and the business/technical risk of leaving it as-is.
  - **Spec Expectation vs. Diff Reality**: Quoted spec requirement vs. conceptual description of diff reality (no raw secret dumps).
  - **Alignment Action**: Concrete step to achieve 100% spec completeness (e.g. implement missing logic, revert unapproved code, or update spec artifact with user sign-off).
```

---

## 2. Context Synthesis & Diff Discovery

### Step 1: Plan Artifact & Sanitized Diff Pinning
1. **Plan Sources**: `progress-map.md`, `brand-product-alignment-spec.md`, `front-end-design-spec.md`, `backend-architecture-spec.md`, `implementation_plan.md`, or GitHub Issues (`#123`).
2. **Git Comparison**: Pin base ref (`origin/main`), capture `git diff <base-ref>...HEAD`, and sanitize any credentials/tokens before injecting into prompts.

### Step 2: Canonical 5-Layer Context Synthesis (Main Agent)
Synthesize objective background facts directly into the canonical **5-Layer Context Chain**:
1. **Product & Brand Understanding**: App purpose, target audience, and core architecture.
2. **Active Branch & Target Scope**: Feature branch name (`feat/...`) and target milestone/issue (`#123`).
3. **Phase Objective**: Stated sub-task goals from `progress-map.md`.
4. **Active Task & Spec Contracts**: Planned spec requirements vs. delivered diff summary.
5. **Execution & Harness Constraints**: Focus on 100% spec completeness and scope creep detection (`git diff origin/main...HEAD`).

---

## 3. Auditor Sub-Agent Execution

Spawn a dedicated auditor sub-agent via `invoke_subagent` (`Role: "Plan Alignment Auditor"`, `Model: "flash"` for standard diffs, `"pro"` for complex multi-file architectural changes).

### Auditor Sub-Agent Prompt Instructions
- **Input**: Canonical 5-Layer Context Block + Approved Spec/Plan text + Sanitized `git diff` output.
- **Task Brief**:
  *"Act as an uncompromising Specification Auditor. Verify if 100% of promised spec items are fully met. Compare code diff against approved spec across 3 categories: 
   (a) **Fully Delivered**: Features/tasks promised in the plan that are completely implemented.
   (b) **Missing or Partial**: Tasks explicitly promised in the plan that are missing or incomplete in the diff.
   (c) **Unplanned Deviations & Scope Creep**: Modifications, additions, or architectural changes present in the diff that were NEVER mentioned or approved in the plan.
   
   Group findings by Severity (Critical ➔ Low). For EVERY finding in (b) and (c), state: (1) Location/Spec requirement; (2) The 'WHY' (Strategic & Product Impact); (3) Spec Expectation vs Diff Reality; (4) Alignment Action. Do NOT comment on formatting, code smells, or edge-case quality. Do not output raw secrets or credential strings. Keep under 500 words."*

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

### Fully Delivered Items (100% Spec Coverage Check)
- [Item 1 from Plan] (Commit: `a1b2c3d`)

### Critical Discrepancies (Spec Blockers / Omissions)
- **[Spec Section / File Location]**: [Summary]
  - **The "WHY" (Strategic Impact)**: [Why this matters to product/user flow]
  - **Spec vs Diff**: Quoted plan `"..."` vs Diff reality
  - **Alignment Action**: [Steps to achieve 100% completeness]

### High Severity Discrepancies (Significant Drift)
...

### Medium Severity Discrepancies (Minor Gaps)
...

### Low Severity Items (Advisories / Clarifications)
...

---

## 3. Audit Gate Decision
- **Status Summary**: N Critical | N High | N Medium | N Low
- **Decision**: 
  - **PASSED**: 100% spec completeness achieved. Ready for `code-review`.
  - **PASS WITH WARNING**: Minor non-critical gaps. Proceed to `code-review` with follow-up task logged.
  - **DEVIATION DETECTED**: Critical/High spec gaps or scope creep present. Cycle back to `implementation-tdd` to fulfill specs or revert unapproved changes.
```
