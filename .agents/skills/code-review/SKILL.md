---
name: code-review
description: Conduct a product-aware, two-axis code review (Standards and Spec) evaluating code quality, edge-case robustness, and domain alignment comparing HEAD against a fixed point using parallel sub-agents. Use when reviewing branches, PRs, work-in-progress, or changes since a commit, tag, or branch.
---

# Code Review (Product-Aware Two-Axis Review)

This skill performs a rigorous code review focusing on **code quality**, **edge-case robustness**, and **domain correctness**. Because sub-agents start with a blank context window, the main agent synthesizes a **5-Layer Context Chain** before spawning parallel sub-agents to evaluate the diff across **Standards** and **Spec** axes.

## Workflow Sequence

`alignment-audit` ➔ `code-review`

> **Upstream Dependency:** Run the `alignment-audit` skill prior to `code-review` to confirm that all changes match approved plans and PRDs without scope creep. Once alignment is verified, execute `code-review` to evaluate code quality, edge-case robustness, and standards.

## Why Two Axes

A code change can succeed on one axis and fail on the other:
- **Standards Pass, Spec Fail**: Code is clean and robust according to conventions, but fails edge cases or implements incorrect product logic.
- **Spec Pass, Standards Fail**: Code satisfies product requirements, but introduces fragile edge cases, poor exception handling, or maintainability smells.

---

## Execution Steps

### Step 1: Fixed Point Pinning & Diff Validation
Identify the comparison target supplied by the user (commit SHA, branch, tag, `main`, `HEAD~N`). If omitted, prompt the user for the fixed point.

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
1. Issue references in commit messages (`#123`, `Closes #45`, `!67`) via `docs/agents/issue-tracker.md`.
2. User-provided path argument.
3. Spec/PRD files under `docs/`, `specs/`, or `.scratch/` matching the branch or feature.
4. If missing, prompt user. If unavailable, mark Spec axis as "No spec available".

#### B. Standards & Robustness Sources
1. Documented repository standards (`CODING_STANDARDS.md`, `CONTRIBUTING.md`, `STYLE_GUIDE.md`).
2. The Fowler Smell Baseline & Edge-Case Robustness Checklist (injected into Standards sub-agent):
   - **Mysterious Name**: Function, variable, or type name does not reveal domain intent. → Rename clearly.
   - **Duplicated Code**: Identical logic shape across multiple hunks or files. → Extract shared helper.
   - **Feature Envy**: Method reaches into another object's data more than its own. → Move method to target object.
   - **Data Clumps**: Group of fields/params traveling together consistently. → Bundle into value object.
   - **Primitive Obsession**: Primitive standing in for a domain concept. → Wrap in domain type.
   - **Repeated Switches**: Duplicate `switch`/`if` cascades across change. → Replace with map or polymorphism.
   - **Shotgun Surgery**: Single logical change forces scattered edits across many files. → Co-locate related modules.
   - **Divergent Change**: Single module edited for multiple unrelated reasons. → Split by single responsibility.
   - **Speculative Generality**: Unrequested hooks, params, or abstractions. → Remove and inline.
   - **Message Chains**: Deep `a.b().c().d()` navigation. → Delegate walk behind single method.
   - **Middle Man**: Class/function mostly delegating onward. → Call real target direct.
   - **Refused Bequest**: Subclass overriding or ignoring most inherited behavior. → Use composition.
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
- Task brief: *"Analyze code quality and robustness per file/hunk: (a) Documented standard breaches (cite file + rule); (b) Code smells (name smell + quote hunk); (c) Edge-case risks, unhandled exceptions, or state invalidation risks. Distinguish hard breaches from judgement calls. Skip tooling-enforced items. Under 400 words."*

#### B. Spec & Product Sub-Agent Prompt
Include:
- The 5-Layer Context Chain from Step 2.
- Full `git diff` output and commit list.
- Full text or path of the Spec / Issue / PRD.
- Task brief: *"Analyze product alignment: (a) Missing or partial spec requirements; (b) Unrequested behavior / scope creep; (c) Implemented logic that breaks domain intent or user flow. Quote spec lines for each finding. Under 400 words."* *(If spec is missing, report "No spec available".)*

**Completion Criterion**: Both sub-agents launched concurrently and responses received.

### Step 5: Aggregation & Dual Reporting
Present findings verbatim or lightly formatted under separate headers:

```markdown
## 1. Product & Review Context
- **Product**: [Layer 1 Summary]
- **Current Phase & Objective**: [Layer 2 & 3 Summary]
- **Work Being Reviewed**: [Layer 4 & 5 Summary]

---

## 2. Standards & Robustness Review
[Standards Sub-Agent Output]

---

## 3. Spec & Domain Review
[Spec Sub-Agent Output]

---

## 4. Summary & Action Items
- **Standards & Robustness Axis**: X findings (Worst: [Brief description or "None"])
- **Spec & Domain Axis**: Y findings (Worst: [Brief description or "None"])
```

Do not merge or re-rank findings across axes.

**Completion Criterion**: Dual-axis report presented side-by-side with 5-layer context header and independent single-line summaries per axis.
