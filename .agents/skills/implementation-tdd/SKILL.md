---
name: implementation-tdd
description: Execute TDD-based feature implementation driven by plan and spec artifacts. Focuses on Git-committed Red-Green test-driven development on feature branches to fulfill artifact requirements without premature code optimization. Use when implementing features, fixes, or meaningful code changes.
---

# Implementation TDD (Artifact-Driven TDD)

This skill governs feature implementation through **Test-Driven Development (TDD)** anchored directly to project specification artifacts and executed on **Git feature branches with Red-Green commit discipline**.

> **Scope & Philosophy Note:**
> The primary focus of this skill is **Artifact Compliance and Functional Correctness (Red ➔ Green)**. Do not over-engineer or obsess over code aesthetics initially; code quality, refactoring, and edge-case hardening will be evaluated downstream by `code-review`.

---

## Workflow Sequence

`git checkout -b feat/...` ➔ `implementation-tdd` (Red ➔ Green Commit) ➔ `alignment-audit` ➔ `code-review` ➔ `PR Merge`

---

## Execution Steps

### Step 1: Context, Branch & Artifact Ingestion
**The main agent MUST perform context discovery directly**:
1. Check active Git branch (`git branch --show-current`). Ensure development is isolated on a feature branch (e.g., `feat/feature-name` or `fix/issue-name`).
2. Ingest project specs (`brand-product-alignment-spec.md`, `backend-architecture-spec.md`, `front-end-design-spec.md`, `progress-map.md`).
3. Identify the local test runner setup (e.g., `vitest`, `jest`, `pytest`, `go test`).

Synthesize a structured 5-layer context block:
1. **Product Understanding**: Core domain purpose and system architecture.
2. **Active Git Branch & Issue**: Current branch name (`feat/...`) and target GitHub Issue (`#123`).
3. **Current Phase Objective**: Target sub-task from `progress-map.md`.
4. **Target Task & Artifact Specs**: Exact requirements and contracts promised in the spec artifacts.
5. **Test Scope & Harness Constraints**: Test runner command, test file patterns, and environment setups.

**Completion Criterion**: 5-layer context block synthesized, feature branch verified, and test framework identified.

### Step 2: The Red Phase (Failing Tests & Git Red Commit)
Before writing implementation code, write unit or integration tests strictly mapping to the requirements in the spec artifact:
1. Create or update test files under the repository's standard test directories.
2. Write test cases covering every behavioral requirement and contract specified in the spec artifact.
3. **Run the test suite** to observe tests failing (verifying state goes **Red**). Confirm failure is due to missing implementation, not syntax/configuration errors.
4. **Git Red Commit**: Stage and commit the failing tests (`git commit -m "test(scope): add failing test for [feature] (Red)"`).

**Completion Criterion**: Tests are written, verified **Red**, and committed to Git under a `test(...)` Red commit signature.

### Step 3: The Green Phase (Minimal Implementation & Git Green Commit)
Write the minimal production code necessary to make all failing tests pass:
1. Implement logic directly addressing the assertions written in Step 2.
2. Focus purely on fulfilling the artifact specification. **Do not add unrequested abstractions, extra hooks, or premature optimizations.**
3. **Run the test suite** to verify state turns **Green**.
4. **Git Green Commit**: Stage and commit the passing implementation code (`git commit -m "feat(scope): implement [feature] (Green) - Closes #123"`).

**Completion Criterion**: All test cases pass (**Green**), committed under a `feat(...)` Green commit signature linking the GitHub Issue.

### Step 4: Artifact & Git Alignment Verification
Verify implementation completeness against specs:
1. Cross-check each requirement in `progress-map.md` and spec artifacts against the passing test suite.
2. Verify `git status` is clean and all commits are staged on the feature branch.

**Completion Criterion**: All spec requirements are verified Green, commits are cleanly logged, and the branch is ready for `alignment-audit`.
