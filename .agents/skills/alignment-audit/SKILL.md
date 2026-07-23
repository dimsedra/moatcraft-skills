---
name: alignment-audit
description: Conduct a plan-and-spec alignment audit using auditor sub-agents to verify that implemented code matches approved plans/PRDs without scope creep or missing items before code-review. Use when verifying work against an implementation plan or spec.
---

# Alignment Audit

This skill acts as an upstream plan & specification auditor executed **before** `code-review`. It verifies whether the actual code diff matches the approved implementation plan, PRD, or specification artifacts.

> **Scope Note:** This skill ignores code quality, style, and refactoring smells (which are evaluated by `code-review`). It focuses strictly on **Plan Fidelity**, **Missing Deliverables**, and **Unapproved Deviations/Scope Creep**.

---

## Execution Workflow Sequence

`implementation-tdd` ➔ `alignment-audit` ➔ `code-review`

```
[Implementation Plan / Spec]
          │
          ▼
   implementation-tdd (Red ➔ Green)
          │
          ▼
    alignment-audit (Plan Fidelity Check)
          │
          ▼
      code-review (Quality & Edge Cases)
```

---

## Execution Steps

### Step 1: Plan Artifact & Diff Pinning
Locate the authoritative plan/specification source and target git ref:
1. **Plan Sources**: Look for `implementation_plan.md`, `brand-product-alignment-spec.md`, `backend-architecture-spec.md`, PRD files under `docs/` or `specs/`, or issue tracker items.
2. **Git Ref**: Pin the target comparison point (`git rev-parse <fixed-point>`) and capture `git diff <fixed-point>...HEAD`.

**Completion Criterion**: Plan/spec artifact is loaded and non-empty `git diff` is captured. If plan or diff is missing, prompt the user.

### Step 2: 5-Layer Context Synthesis (Main Agent Responsibility)
**The main agent MUST perform the context discovery directly** by inspecting repository documentation (`README.md`, `PRD.md`, `docs/`, `specs/`) and recent `git log`. **Do NOT delegate context discovery to sub-agents**, as sub-agents start with a blank context window.

> **Crucial Independence Rule (Informative, Non-Directive Context):**
> The main agent provides purely **objective background facts** (product domain, active phase, PRD requirements, git commit summary). The main agent **MUST NOT dictate conclusions, express opinions on pass/fail status, or steer the sub-agent toward a preferred finding**. Sub-agents must remain completely autonomous and form unbiased judgements strictly from the empirical code diff and specification artifacts.

Synthesize a neutral, objective 5-layer context block to feed into the auditor sub-agent:

1. **Product Understanding**: Objective purpose of the app/system and high-level architecture.
2. **Current Phase / Stage**: Current roadmap phase or milestone.
3. **Current Phase Objective**: Stated feature goals for this phase.
4. **Planned Specs vs. Delivered Diff**: List of planned items vs. list of modified files (without preliminary judgement).
5. **Audit Boundary Constraints**: Objective focus on spec compliance and deviation detection.

**Completion Criterion**: 5-layer objective context block synthesized directly by the main agent and ready for sub-agent prompt injection.

### Step 3: Auditor Sub-Agent Spawning
Spawn a dedicated auditor sub-agent via `invoke_subagent` (`TypeName: "research"` or `"self"`, `Role: "Plan Alignment Auditor"`).

#### Auditor Sub-Agent Prompt Instructions
Inject:
- The 5-Layer Context Block from Step 2.
- Full text of the approved plan/spec artifact (`implementation_plan.md` / PRD).
- Complete `git diff` and commit list.
- Task brief:
  *"Act as an uncompromising Specification Auditor. Compare the code diff against the approved plan/spec across 3 categories:
   (a) **Fully Delivered**: Features/tasks promised in the plan that are completely implemented.
   (b) **Missing or Partial**: Tasks explicitly promised in the plan that are missing or incomplete in the diff.
   (c) **Unplanned Deviations & Scope Creep**: Modifications, additions, or architectural changes present in the diff that were NEVER mentioned or approved in the plan.
   Quote exact lines from the plan artifact for every finding. Do NOT comment on code formatting, variable names, or refactoring. Keep under 400 words."*

**Completion Criterion**: Auditor sub-agent launched and audit report received.

### Step 4: Audit Synthesis & Gate Decision
Synthesize the sub-agent's findings into `alignment-audit-report.md`:

```markdown
# Alignment Audit Report

## 1. Product & Phase Context
- **Product**: [Product Understanding]
- **Current Phase**: [Phase & Objective]
- **Plan Artifact**: [Link to Plan/Spec File]

---

## 2. Plan Fidelity Audit

### ✅ Fully Delivered Items
- [Item 1 from Plan]
- [Item 2 from Plan]

### ⚠️ Missing or Incomplete Items
- [Missing Item 1] — *Quoted Plan Spec*: `"..."`

### 🚨 Unplanned Deviations & Scope Creep
- [Unplanned Change 1] — *Diff Hunk*: `file.ts:L45-L60` (Not in approved plan)

---

## 3. Audit Gate Decision
- **Status**: [PASSED | DEVIATION DETECTED]
- **Recommendation**: [Proceed to `code-review` OR Resolve Plan Deviations First]
```

Present the summary to the user and specify whether to proceed directly to `code-review`.

**Completion Criterion**: `alignment-audit-report.md` written and gate decision presented.
