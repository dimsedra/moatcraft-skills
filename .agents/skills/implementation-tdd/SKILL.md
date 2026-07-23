---
name: implementation-tdd
description: Execute TDD-based feature implementation driven by plan and spec artifacts. Focuses on Red-Green test-driven development to fulfill artifact requirements without premature code optimization. Use when implementing features, fixes, or meaningful code changes.
---

# Implementation TDD (Artifact-Driven TDD)

This skill governs feature implementation through **Test-Driven Development (TDD)** anchored directly to project specification and implementation artifacts.

> **Scope & Philosophy Note:**
> The primary focus of this skill is **Artifact Compliance and Functional Correctness (Red ➔ Green)**. Do not over-engineer or obsess over code aesthetics initially; code quality, refactoring, and edge-case hardening will be evaluated downstream by `code-review`.

---

## Workflow Sequence

`implementation-tdd` ➔ `alignment-audit` ➔ `code-review`

---

## Execution Steps

### Step 1: Context & Artifact Ingestion (Main Agent Responsibility)
**The main agent MUST perform context discovery directly** by ingesting project documentation (`README.md`, `PRD.md`, `specs/`, `implementation_plan.md`) and identifying the local test runner setup (e.g., `vitest`, `jest`, `pytest`, `go test`).

Synthesize a structured 5-layer context block:
1. **Product Understanding**: Core domain purpose and system architecture.
2. **Current Phase / Stage**: Active roadmap phase or development milestone.
3. **Current Phase Objective**: Target feature goals for this phase.
4. **Target Task & Artifact Specs**: The exact requirements, data contracts, and behavior promised in the plan artifact.
5. **Test Scope & Harness Constraints**: Test runner command, test file patterns, and environment setups.

**Completion Criterion**: 5-layer context block synthesized, target test framework identified, and artifact specs loaded.

### Step 2: The Red Phase (Write Failing Tests First)
Before writing implementation code, write unit or integration tests strictly mapping to the requirements in the plan artifact:
1. Create or update test files under the repository's standard test directories.
2. Write test cases covering every behavioral requirement and contract specified in the plan artifact.
3. **Run the test suite** to observe tests failing (verifying state goes **Red**). Confirm failure is due to missing implementation, not syntax/configuration errors.

**Completion Criterion**: Tests are written, covering all planned artifact requirements, and verified **Red** (failing cleanly on missing logic).

### Step 3: The Green Phase (Minimal Implementation)
Write the minimal production code necessary to make all failing tests pass:
1. Implement logic directly addressing the assertions written in Step 2.
2. Focus purely on fulfilling the artifact specification. **Do not add unrequested abstractions, extra hooks, or premature optimizations.**
3. **Run the test suite** to verify state turns **Green**.

**Completion Criterion**: All test cases pass (**Green**), fulfilling the functional requirements of the plan artifact.

### Step 4: Artifact Compliance Verification
Verify implementation completeness against the plan artifact:
1. Cross-check each requirement in `implementation_plan.md` or PRD against the passing test suite.
2. Ensure no unrequested scope creep was introduced during the Green phase.

**Completion Criterion**: All plan artifact requirements are verified Green, and the branch is ready for `alignment-audit`.
