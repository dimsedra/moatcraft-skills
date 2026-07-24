---
name: code-review
description: Conduct a product-aware, two-axis code review (Standards and Spec) evaluating code quality, edge-case robustness, and domain alignment comparing HEAD against a fixed point using parallel sub-agents. Categorize findings by urgency/importance level with explicit "WHY" rationales. Use when reviewing feature branches, Pull Requests (PRs), work-in-progress, or changes since a commit, tag, or branch.
---

# Code Review (Product-Aware Two-Axis Review)

This skill performs a rigorous code review focusing on **code quality**, **edge-case robustness**, and **domain correctness** for feature branches and Pull Requests (PRs). Findings are strictly formatted by **Urgency & Importance Level** and include an explicit **"WHY" (Systemic Rationale & Consequence)** for every issue detected.

Because sub-agents start with a blank context window, the main agent synthesizes a **5-Layer Context Chain** before spawning parallel sub-agents to evaluate the diff across **Standards** and **Spec** axes.

---

## Workflow Sequence

`alignment-audit` ➔ `code-review` ➔ `PR Approval / Merge`

> **Upstream Dependency:** Run the `alignment-audit` skill prior to `code-review` to confirm that all changes match approved plans and PRDs without scope creep. Once plan alignment is verified, execute `code-review` to evaluate code quality, edge-case robustness, and standards.

---

## Urgency & Importance Classification Matrix

Every finding identified during code review MUST be classified into one of the following 4 levels:

| Level | Severity Label | Definition & Threshold | PR Impact |
| :--- | :--- | :--- | :--- |
| **🔴 Level 1** | **Critical (Blocker)** | Security vulnerabilities, data loss/corruption risks, unhandled crash conditions in primary flows, breaking API contract changes without migration, or severe domain logic bugs. | **Merge Blocker**: Must fix immediately before PR approval. |
| **🟡 Level 2** | **High (Major)** | Significant Fowler architectural smells, subtle race conditions, unhandled edge-case error states (e.g. unhandled timeouts, silent swallowing), or severe performance bottlenecks. | **Action Required**: Should fix before merge unless explicitly waived. |
| **🔵 Level 3** | **Medium (Moderate)** | Standard code smells (duplicated logic, primitive obsession, feature envy), minor edge-case gaps, missing documentation on complex algorithms, or sub-optimal data patterns. | **Recommended**: Can merge with follow-up task or quick cleanup. |
| **⚪ Level 4** | **Low (Minor / Advisory)** | Stylistic micro-suggestions, variable naming clarity, minor refactoring polish, or non-blocking optimization hints. | **Advisory**: Optional polish, does not delay merge. |

---

## Mandatory Finding Schema (The "WHY" Requirement)

Every finding reported MUST articulate the **"WHY" (Systemic Rationale & Consequence)** — bridging the technical code detail with its high-level impact on user experience, system stability, security, or maintainability:

```markdown
- **[Severity Badge] [File Location & Line Number]**: Brief Summary
  - **The "WHY" (Systemic Impact)**: Clear, jargon-free explanation of why this matters and what happens systemically if left unaddressed.
  - **Root Cause / Code Detail**: The specific code smell, missing edge-case check, or spec mismatch.
  - **Remediation Action**: Concrete code fix or refactoring steps.
```

---

## Execution Steps

### Step 1: Fixed Point Pinning & PR Diff Validation
Identify the comparison target supplied by the user (PR target branch `origin/main`, commit SHA, branch, tag, `HEAD~N`). If omitted, default to `origin/main`.

Validate the reference and capture diff inputs:
1. Verify ref validity: `git rev-parse <fixed-point>`
2. Capture commit list: `git log <fixed-point>..HEAD --oneline`
3. Capture merge-base diff: `git diff <fixed-point>...HEAD`

**Completion Criterion**: Ref resolves successfully, diff is non-empty, and commit summary is captured. If ref is invalid or diff is empty, halt execution.

### Step 2: 5-Layer Context Synthesis (Main Agent Responsibility)
**The main agent MUST perform the context discovery directly** by reading repository documentation (`README.md`, `PRD.md`, `docs/`, `specs/`, issue tracker) and `git log`. **Do NOT delegate context discovery to sub-agents**, as sub-agents start with a blank context window.

> **Crucial Independence Rule (Informative, Non-Directive Context):**
> The main agent provides purely **objective background facts** (product domain, active phase, PRD requirements, git commit summary). The main agent **MUST NOT dictate conclusions, express opinions on pass/fail status, or steer the sub-agent toward a preferred finding**. Sub-agents must remain completely autonomous and form unbiased judgements strictly from the empirical code diff and specification artifacts.

Synthesize a neutral, objective **5-Layer Context Chain** to feed into both sub-agents:

1. **Product Understanding**: Objective purpose of the app/system, target users, and high-level architecture.
2. **Current Phase / Stage**: Objective development roadmap phase or release cycle stage.
3. **Current Phase Objective**: Stated feature set or milestone targeted in this phase.
4. **Current Task / Work Done**: List of capabilities, fixes, or refactors present in the commit log and diff (without preliminary evaluation).
5. **Review Scope & Robustness Targets**: Objective list of quality metrics, edge-case areas, state transitions, and data flow touchpoints to inspect.

**Completion Criterion**: All 5 layers of the objective context chain are synthesized directly by the main agent and ready for sub-agent prompt injection.

### Step 3: Spec & Standards Discovery

#### A. Spec Sources (in priority order)
1. Issue references in commit messages (`#123`, `Closes #45`, `!67`) or PR descriptions.
2. User-provided path argument (`progress-map.md`, `spec.md`).
3. Spec/PRD files under `docs/`, `specs/`, or `.scratch/` matching the branch or feature.
4. If missing, prompt user. If unavailable, mark Spec axis as "No spec available".

#### B. Standards & Robustness Sources
1. Documented repository standards (`CODING_STANDARDS.md`, `CONTRIBUTING.md`, `STYLE_GUIDE.md`).
2. The Fowler Smell Baseline & Edge-Case Robustness Checklist (injected into Standards sub-agent):
   - **Mysterious Name**: Function, variable, or type name does not reveal domain intent.
   - **Duplicated Code**: Identical logic shape across multiple hunks or files.
   - **Feature Envy**: Method reaches into another object's data more than its own.
   - **Data Clumps**: Group of fields/params traveling together consistently.
   - **Primitive Obsession**: Primitive standing in for a domain concept.
   - **Repeated Switches**: Duplicate `switch`/`if` cascades across change.
   - **Shotgun Surgery**: Single logical change forces scattered edits across many files.
   - **Divergent Change**: Single module edited for multiple unrelated reasons.
   - **Speculative Generality**: Unrequested hooks, params, or abstractions.
   - **Message Chains**: Deep `a.b().c().d()` navigation.
   - **Middle Man**: Class/function mostly delegating onward.
   - **Refused Bequest**: Subclass overriding or ignoring most inherited behavior.
   - **Edge-Case & Robustness Checklist**:
     - *Null/Undefined & Unhandled Exceptions*: Boundary inputs, network timeouts, missing payload fields.
     - *State Machine Invalidation*: Concurrent mutations, race conditions, stale cache reads.
     - *Resource Leaks & Error Recovery*: Unclosed sockets, unhandled promise rejections, silent error swallowing.

**Completion Criterion**: Spec source identified (or marked missing) and repository standards + robustness checklist prepared.

### Step 4: Parallel Sub-Agent Spawning
Invoke two sub-agents concurrently using `invoke_subagent` in a single tool call (`Subagents: [...]`). Inject the complete **5-Layer Context Chain** from Step 2 into both sub-agents upfront so they inspect diffs with full product and situational awareness.

#### A. Standards & Quality Sub-Agent Prompt
Include:
- The 5-Layer Context Chain from Step 2.
- Full `git diff` output and commit list.
- Repo standards + Fowler Smell Baseline + Edge-Case & Robustness Checklist.
- Task brief:
  *"Analyze code quality and robustness per file/hunk. Group findings by Severity: 🔴 Critical (Blocker), 🟡 High (Major), 🔵 Medium (Moderate), ⚪ Low (Minor). For EVERY finding, you MUST include: (1) Location & Summary; (2) The 'WHY' (Systemic Rationale & Consequence — explain why this matters systemically and what happens if unaddressed); (3) Code detail; (4) Actionable fix. Skip tooling-enforced items. Under 500 words."*

#### B. Spec & Product Sub-Agent Prompt
Include:
- The 5-Layer Context Chain from Step 2.
- Full `git diff` output and commit list.
- Full text or path of the Spec / Issue / PRD.
- Task brief:
  *"Analyze product alignment: (a) Missing or partial spec requirements; (b) Unrequested behavior / scope creep; (c) Implemented logic that breaks domain intent or user flow. Group findings by Severity: 🔴 Critical (Blocker), 🟡 High (Major), 🔵 Medium (Moderate), ⚪ Low (Minor). Quote spec lines for each finding. For EVERY finding, explicitly state the 'WHY' (Systemic & User Flow Impact). Under 500 words."* *(If spec is missing, report "No spec available".)*

**Completion Criterion**: Both sub-agents launched concurrently and responses received.

### Step 5: Aggregation & Structured Dual Reporting
Synthesize sub-agent outputs into a structured dual-axis report sorted by Urgency/Importance Level:

```markdown
# Code Review Report

## 1. Product & PR Context
- **Product**: [Layer 1 Summary]
- **Target PR / Branch**: `feat/feature-name` -> `main`
- **Associated Issue**: `#123`
- **Current Phase & Objective**: [Layer 2 & 3 Summary]
- **Work Being Reviewed**: [Layer 4 & 5 Summary]

---

## 2. Standards & Robustness Review

### 🔴 Critical (Blockers)
- **`path/to/file.ts:L45`**: [Brief Summary]
  - **The "WHY" (Systemic Impact)**: [Consequence if left unaddressed]
  - **Detail**: [Code smell / unhandled exception]
  - **Action**: [Remediation steps]

### 🟡 High (Major Issues)
- ...

### 🔵 Medium (Moderate Issues)
- ...

### ⚪ Low (Minor / Advisory)
- ...

---

## 3. Spec & Domain Review

### 🔴 Critical (Spec Blockers)
- ...

### 🟡 High (Major Spec Drift)
- ...

### 🔵 Medium (Moderate Spec Gaps)
- ...

### ⚪ Low (Minor Advisory)
- ...

---

## 4. Summary & PR Gate Recommendation
- **Critical Findings**: N (Must resolve before merge)
- **High Findings**: N (Should resolve before merge)
- **Medium/Low Findings**: N (Advisory / Follow-up)
- **PR Gate Decision**: [🟢 APPROVE | 🟡 REQUEST CHANGES | 🔴 RE-ROUTE TO TDD]
```

Do not merge or re-rank findings across axes, but ensure every finding is classified by Urgency Level and includes its "WHY" rationale.

**Completion Criterion**: Dual-axis report presented with 5-layer context header, severity-grouped findings with "WHY" explanations, and PR decision.
