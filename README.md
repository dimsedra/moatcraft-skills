# 🏰 Moatcraft

> **Opinionated Agentic Skills for Crafting Defensible Software & Uncopyable Moats.**

**Moatcraft** is a suite of production-grade agent skills designed to guide AI coding assistants through a continuous, opinionated development loop. It rejects commodity UI templates, generic 1st-idea happy-path traps, and sycophantic yes-man behaviors, focusing instead on building **defensible design moats, resilient backend architectures, and artifact-driven TDD execution.**

---

## 📦 Quick Install

Install the entire suite or individual skills using the open `skills` CLI:

### Install All Skills
```bash
npx skills add dimsedra/moatcraft-skills
```

### Install Specific Skill
```bash
npx skills add dimsedra/moatcraft-skills@brand-product-alignment
```

---

## 🔄 The Moatcraft Development Loop Architecture

```
                    ┌─────────────────────────┐
                    │ brand-product-alignment │ (Brand & Product Identity)
                    └────────────┬────────────┘
                                 │
                   ┌─────────────┴─────────────┐
                   ▼                           ▼
      ┌─────────────────────────┐ ┌─────────────────────────┐
      │   front-end-designer    │ │    backend-architect    │
      │ (Visual & UI Execution) │ │ (Technical System Spec) │
      └────────────┬────────────┘ └────────────┬────────────┘
                   │                           │
                   └─────────────┬─────────────┘
                                 │
                                 ▼
 ┌─────────────────────────────────────────────────────────────┐
 │                THE ACTIVE DEVELOPMENT LOOP                  │
 │                                                             │
 │            ┌───────────────────────────────────┐            │
 │ ┌─────────►│        implementation-tdd         │◄─────────┐ │
 │ │          │          (Red ➔ Green)            │          │ │
 │ │          └─────────────────┬─────────────────┘          │ │
 │ │                            │                            │ │
 │ │                            ▼                            │ │
 │ │          ┌───────────────────────────────────┐          │ │
 │ │          │          alignment-audit          │          │ │
 │ │          │     (Plan & Spec Fidelity)        │          │ │
 │ │          └─────────────────┬─────────────────┘          │ │
 │ │                            │                            │ │
 │ │             [Plan Deviations / Gaps?]                   │ │
 │ │             /                       \                   │ │
 │ │          (Yes)                     (Passed)             │ │
 │ │            │                          │                 │ │
 │ └────────────┘                          ▼                 │ │
 │                            ┌───────────────────┐          │ │
 │                            │    code-review    │          │ │
 │                            │(Quality & Robust) │          │ │
 │                            └─────────┬─────────┘          │ │
 │                                      │                    │ │
 │                        [Quality Breaches Found?]          │ │
 │                        /                       \          │ │
 │                     (Yes)                      (Pass)     │ │
 │                       │                          │        │ │
 │                       └──────────────────────────┼────────┘ │
 └──────────────────────────────────────────────────┼──────────┘
                                                    ▼
                                            Ship / Next Loop Iteration
```

---

## 🛠️ Included Skills

| Skill | Category | Description | Key Artifact / Output |
| :--- | :--- | :--- | :--- |
| **`brand-product-alignment`** | Strategy | Conducts fluid brand-product discovery to define positioning, identity boundaries, and experience moats. | `brand-product-alignment-spec.md` |
| **`front-end-designer`** | Front-End | Applies opinionated UI rules, breathable visual hierarchy, 2nd/3rd idea iteration, and WebGL/Canvas design moats. | Front-End Code / UI |
| **`backend-architect`** | Back-End | Conducts natural, jargon-free backend discovery for data flow, operational limits, SLAs, and technical moats. | `backend-architecture-spec.md` |
| **`implementation-tdd`** | Execution | Executes artifact-driven Red-Green TDD focusing strictly on functional compliance without premature optimization. | Passing Test Suite & Code |
| **`alignment-audit`** | Audit | Upstream auditor running before code review to catch plan deviations, missing deliverables, or unapproved scope creep. | `alignment-audit-report.md` |
| **`code-review`** | Quality | Spawns parallel sub-agents to conduct two-axis review (Standards & Spec) targeting code smells and edge-case robustness. | Dual-Axis Review Report |
| **`explain-and-teach`** | Cross-Cutting | Delivers adaptive, systemic explanations (Trade-offs, Ripple Effects, Mental Models) tailored for systemic thinkers. | Direct Response |
| **`agentic-dev-loop`** | Router | Orchestrates the continuous feedback loop between strategic discovery, TDD execution, auditing, and review. | Loop Orchestration |

---

## 💡 Core Operating Principles

1. **Happy-Path Rejection (2nd & 3rd Idea Iteration)**  
   1st ideas are usually the solution of least resistance—the generic solution 90% of competitors use. Moatcraft skills push past commodity solutions to unlock unique, brand-anchored concepts.

2. **Fluid Conversation & Behind-the-Scenes Checklists**  
   Discovery skills (`brand-product-alignment` and `backend-architect`) avoid rigid, robotic questionnaires. Dialogue flows naturally like co-founders at a whiteboard while tracking required parameters on behind-the-scenes checklists.

3. **Anti-Yes-Man Protocol**  
   Agents maintain the explicit right and duty to question unexamined assumptions, point out logical or technical contradictions, and offer proactive alternative recommendations.

4. **Objective Context Feeding & Sub-Agent Independence**  
   Sub-agents start with a blank context window. The main agent synthesizes and feeds a neutral **5-Layer Context Chain** (Product ➔ Phase ➔ Objective ➔ Task ➔ Review Scope) without dictating conclusions.

5. **Adaptive Explanation (No "Whole 5-Course Meal")**  
   `explain-and-teach` delivers only the exact slice requested (Trade-offs, Ripple Effects, or First-Principles Mental Models) without forcing unnecessary lengthy lectures.

---

## 📜 License

MIT License. Crafted for the Open Agent Skills Ecosystem.
