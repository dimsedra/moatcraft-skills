---
name: moatcraft-onboarding
description: Agent guide for onboarding new users into the Moatcraft workflow — both explaining how it works AND integrating the workflow environment into the user's project. Adapts setup to project state (clean slate, mid-development, or workflow migration). Use automatically when Moatcraft skills are first installed, or when a user asks how the Moatcraft workflow operates.
---

# Moatcraft Onboarding (Explain + Integrate)

This skill has two jobs:
1. **Explain** — Walk the user through how the Moatcraft workflow operates so they genuinely understand what they're working with.
2. **Integrate** — Actually set up the Moatcraft workflow environment in the user's project, adapted to their specific starting conditions.

Both happen together during onboarding. The user should walk away both understanding the system and having a working environment ready to use.

---

## 1. When to Activate

Activate this skill automatically when:
- Moatcraft skills are **first installed** in a new project (no prior spec artifacts exist).
- Moatcraft skills are installed into a **project already in progress** (existing code, configs, or partial specs detected).
- A user **asks how the Moatcraft workflow works** or what the skills do.
- A user seems confused about the development loop or skill invocation order.

---

## 2. Project State Detection

Before beginning, silently assess the project state:

- **Clean Slate** — No `src/`, no `package.json`/`pyproject.toml`/`go.mod`, no existing spec files. This is a brand new project.
- **Mid-Development** — Existing source code, dependencies, possibly partial docs/specs, git history. The project has momentum.
- **Workflow Migration** — Existing CI/CD configs, other agent skill files (`.cursor/`, `.claude/`, etc.), custom linting/review pipelines. The user is coming from another toolchain.

These categories aren't mutually exclusive — a mid-development project may also be a workflow migration. Detect all applicable signals.

---

## 3. Onboarding Tone & Approach

- **Use `explain-and-teach` principles**: High-level human abstractions, intuitive mental models, zero jargon dumps.
- **Conversational, not ceremonial**: Like a co-founder explaining the team's dev philosophy over coffee.
- **Offer, don't force**: *"This is your first time using Moatcraft — want me to walk you through how it works and set up the environment for your project?"* If the user declines, proceed directly to their requested task.
- **Explain while doing**: Don't treat explanation and setup as separate phases. As you create each artifact or directory, briefly explain why it exists. The user learns the system by watching it get built.

---

## 4. What to Explain (High-Level Walkthrough)

Weave these into a narrative — not a dry list of skill names:

### A. The Problem Moatcraft Solves
Most AI coding tools produce generic, interchangeable output. If you removed the logo, you couldn't tell one product from another. Moatcraft anchors every design choice, architecture decision, and line of code to a defensible identity.

### B. How the Workflow Flows (The Mental Model)

1. **First, we figure out who you are** — Brand, product identity, what makes you different. This anchors everything downstream.
2. **Then, we translate that into specs** — Front-end visual specs (textures, typography, spatial rhythm) and backend architecture specs (data flow, reliability, technical moats). Living documents, not frozen requirements.
3. **We map out what to build** — Specs decomposed into a living roadmap of milestones and atomic tasks.
4. **We build with discipline** — Red-Green TDD on isolated Git branches.
5. **We verify twice before shipping** — Alignment audit (does it match the spec?) then code review (is it robust?). Issues loop back for fixes before merge.
6. **The loop is alive** — Mid-flight requirement shifts cascade re-audits downstream. Contradictions escalate upstream.

### C. What the User Should Expect from the Agent
- Push back on generic first ideas and iterate toward unique solutions.
- Challenge assumptions constructively when contradictions or hidden trade-offs appear.
- Default to high-level mental models; technical code details only when asked.
- Ask for sign-off on specs before building — no surprises.

### D. What the User Owns
- **Every spec artifact is theirs** — `brand-product-alignment-spec.md`, `front-end-design-spec.md`, `backend-architecture-spec.md`, `progress-map.md`. Version-controlled, living documents reviewable and editable at any time.
- **The user drives strategic direction** — The agent proposes, challenges, and executes, but the user makes the final call.

### E. Where Your Judgment Is Still Irreplaceable (The Limits of "Clean Pass")
Be transparent: a "Clean Pass" means the code matches the spec and meets quality standards. It does **not** mean:

- **The spec itself was right** — A flawed assumption baked into the spec will be faithfully implemented. The system checks *fidelity to the plan*, not *whether the plan was wise*.
- **The product will resonate with real users** — Market fit and emotional resonance are human judgment calls.
- **The trade-offs are acceptable to your context** — Business reality, timeline, and risk tolerance are yours to weigh.
- **All edge cases are covered** — Domain-specific edge cases never articulated in the spec won't be tested.

**If you don't bring your judgment**: The system builds exactly what the spec says, verifies it passes, and ships it — even if the spec was incomplete or the feature doesn't matter. Clean Pass = *internal consistency*, not *external correctness*.

---

## 5. Environment Integration (Adapted Per Project State)

After the walkthrough (or interleaved with it), the agent sets up the Moatcraft working environment. What gets set up depends on the project state detected in Section 2.

### A. Clean Slate Setup

Full scaffolding — the project is empty, so everything gets created from scratch:

1. **Create spec directory**: `docs/specs/` (or project-appropriate equivalent). This is where all Moatcraft spec artifacts will live.
2. **Scaffold empty spec templates**: Create placeholder files that signal the workflow structure:
   - `docs/specs/brand-product-alignment-spec.md` — empty, to be filled during brand discovery.
   - `docs/specs/front-end-design-spec.md` — empty, to be synthesized from brand spec.
   - `docs/specs/backend-architecture-spec.md` — empty, to be synthesized from discovery.
   - `docs/specs/progress-map.md` — empty, to be generated after specs are approved.
3. **Git conventions**: If a git repo exists, confirm branching strategy. Moatcraft defaults to feature branches per task (`feat/task-slug`, `fix/task-slug`) with PRs into main/develop. Adapt to the user's existing branch convention if they have one.
4. **Initial commit**: Stage the scaffolded structure and commit: `chore: scaffold moatcraft spec directory and workflow structure`.
5. **Route to first skill**: `brand-product-alignment` — the natural starting point for a clean slate.

### B. Mid-Development Setup

The project has existing code but no Moatcraft specs. The agent meets the project where it is:

1. **Scan the codebase** — Read `README.md`, existing component structure, API routes, styling tokens/variables, `package.json`/dependency manifests, and recent git history to understand what already exists.
2. **Create spec directory**: Same as clean slate — `docs/specs/` (or adapt to the project's existing docs convention if one is established).
3. **Draft inferred specs** — Rather than starting from blank templates, the agent should **pre-populate spec files with inferred content** from the codebase scan:
   - `brand-product-alignment-spec.md` — Inferred brand positioning, target user, product differentiators based on README, marketing copy, or app metadata.
   - `front-end-design-spec.md` — Inferred design tokens, color palette, typography, component patterns from existing CSS/styled-components/theme files.
   - `backend-architecture-spec.md` — Inferred data models, API structure, infrastructure patterns from existing backend code.
   - Mark every inferred section with `[INFERRED — Review Required]` so the user knows what needs their sign-off vs. what was auto-detected.
4. **Present inferred specs for review** — *"I've drafted initial specs from your existing codebase. Take a look — correct anything that's off, and confirm what's accurate. Once you sign off, we can start the loop."*
5. **Git conventions**: Detect existing branching strategy from git history and adapt. Don't impose a new convention if one is already in use.
6. **Generate initial progress map** — If the user has a clear next milestone (or one is inferable from issues/TODO comments), draft an initial `progress-map.md` with the immediate phase decomposed.
7. **Route to next step**: User reviews inferred specs → corrects and approves → `progress-mapper` for the next phase of work.

### C. Workflow Migration Setup

The user has existing dev tooling. Moatcraft integrates alongside, not over, what already works:

1. **Inventory existing tooling** — Detect CI/CD configs (`.github/workflows/`, `Jenkinsfile`, etc.), other agent skills (`.cursor/`, `.claude/`, `.windsurf/`), linting configs (`.eslintrc`, `.prettierrc`), and project management artifacts (issues, project boards, existing roadmaps).
2. **Clarify what Moatcraft adds vs. overlaps**:
   - Existing CI/CD and linting → **stays as-is**. Moatcraft doesn't replace build pipelines or formatters.
   - Existing code review automation → Moatcraft's dual-axis review (alignment audit + code quality) **complements** it. Explain the difference: Moatcraft checks *spec fidelity* and *strategic coherence*, not just lint rules and test coverage.
   - Existing project boards/issue trackers → `progress-map.md` is a **spec-anchored living document** that works alongside external trackers. It's not a replacement for Jira/Linear/GitHub Issues — it's the strategic decomposition layer that feeds into them.
   - Existing agent skills → Moatcraft skills can coexist. If there's overlap, discuss with the user which to use for what.
3. **Create spec directory**: Adapt location to the project's existing doc structure. If they already have `docs/`, use `docs/specs/`. If they use a wiki or external docs, place specs where the user prefers.
4. **Scaffold or infer specs**: Same logic as mid-development — infer from existing code, mark as `[INFERRED — Review Required]`.
5. **Incremental adoption**: Explicitly offer: *"You don't have to adopt everything at once. We can start with just the spec layer and add the dev loop later when you're ready."* The user picks which skills to activate now.
6. **Route to user's immediate need**: Don't force a linear path. If the user came to Moatcraft because they want better design, start with `front-end-designer`. If they want structured development, start with `progress-mapper`. Match the entry point to their motivation.

---

## 6. Integration Completion Criteria

Onboarding integration is considered complete when:
- [ ] Spec directory exists in the project and is committed to git.
- [ ] Spec files exist (either empty templates for clean slate, or inferred drafts for existing projects).
- [ ] For mid-development/migration: inferred specs have been presented for user review.
- [ ] Git branching convention is acknowledged (either established or adapted to existing).
- [ ] User knows which skill to invoke next and why.
- [ ] User has expressed understanding of the workflow (even if brief — a "makes sense" is sufficient).

---

## 7. Ongoing Reference

If at any point during development the user asks *"Why are we doing this?"*, *"What's the point of this audit?"*, or *"How does this fit into the bigger picture?"*, use `explain-and-teach` to answer — anchoring the explanation back to the workflow mental model established during onboarding.
