# Moatcraft

> **Opinionated Agentic Skills for Crafting Defensible Software and Architectural Moats**

[![skills.sh](https://skills.sh/b/dimsedra/moatcraft-skills)](https://skills.sh/dimsedra/moatcraft-skills)

Moatcraft is a suite of production-grade agent skills designed to guide AI coding assistants through a continuous development loop. It eliminates commodity UI templates, generic happy-path solutions, and sycophantic behavior, focusing instead on building defensible design moats, resilient backend architectures, and artifact-driven TDD execution.

---

## Installation

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

## Development Loop Architecture

```mermaid
flowchart TD
    A["brand-product-alignment<br/><i>(Pure Brand & Product Identity)</i>"] --> B1["front-end-designer<br/><i>(Visual & UI Execution)</i>"]
    A --> B2["backend-architect<br/><i>(Technical System Spec)</i>"]
    
    B1 --> MAP["progress-mapper<br/><i>(Roadmap & Task Decomposition)</i>"]
    B2 --> MAP
    
    MAP --> TDD["implementation-tdd<br/><i>(Red ➔ Green TDD)</i>"]
    
    subgraph Active_Development_Loop ["The Active Development Loop"]
        TDD --> AUDIT["alignment-audit<br/><i>(Plan & Spec Fidelity Check)</i>"]
        AUDIT -- "Deviations Detected" --> TDD
        AUDIT -- "Passed" --> REVIEW["code-review<br/><i>(Standards & Robustness Review)</i>"]
        REVIEW -- "Quality Breaches Found" --> TDD
    end
    
    REVIEW -- "Clean Pass" --> SHIP["Ship / Next Sub-Task / Iteration"]
```

---

## Skill Specifications

| Skill | Category | Description | Primary Output Artifact |
| :--- | :--- | :--- | :--- |
| **`brand-product-alignment`** | Strategy | Conducts fluid brand and product discovery to define positioning, identity boundaries, and experience moats. | `brand-product-alignment-spec.md` |
| **`front-end-designer`** | Front-End | Applies opinionated UI rules, breathable visual hierarchy, 2nd/3rd idea iteration, and WebGL/Canvas design moats. | Front-End UI Code |
| **`backend-architect`** | Back-End | Conducts natural, jargon-free backend discovery for data flow, operational limits, SLAs, and technical moats. | `backend-architecture-spec.md` |
| **`progress-mapper`** | Roadmap | Ingests brand/technical specs and decomposes them into a living roadmap of Milestones, Tasks, and atomic TDD sub-tasks. | `progress-map.md` |
| **`implementation-tdd`** | Execution | Executes artifact-driven Red-Green TDD focusing strictly on functional compliance without premature optimization. | Passing Test Suite & Code |
| **`alignment-audit`** | Audit | Upstream auditor running before code review to catch plan deviations, missing deliverables, or unapproved scope creep. | `alignment-audit-report.md` |
| **`code-review`** | Quality | Spawns parallel sub-agents to conduct two-axis review (Standards & Spec) targeting code smells and edge-case robustness. | Dual-Axis Review Report |
| **`explain-and-teach`** | Cross-Cutting | Delivers adaptive, systemic explanations (Trade-offs, Ripple Effects, Mental Models) tailored for systemic thinkers. | Direct Response |
| **`agentic-dev-loop`** | Router | Orchestrates the continuous feedback loop between strategic discovery, roadmap planning, TDD execution, auditing, and review. | Loop Orchestration |

---

## Operating Principles

1. **Happy-Path Rejection**  
   Initial design and architecture proposals are often paths of least resistance. Moatcraft skills push past generic solutions to uncover unique, brand-anchored concepts through 2nd and 3rd iterations.

2. **Fluid Conversation and Behind-the-Scenes Checklists**  
   Discovery skills (`brand-product-alignment` and `backend-architect`) avoid rigid questionnaires. Dialogue flows naturally like technical partners at a whiteboard while tracking required parameters on behind-the-scenes checklists.

3. **Anti-Sycophancy Protocol**  
   Agents maintain the explicit obligation to challenge unexamined assumptions, point out logical or technical contradictions, and offer proactive alternative recommendations.

4. **Objective Context Ingestion and Sub-Agent Independence**  
   Sub-agents operate autonomously. The main agent synthesizes and provides a neutral 5-Layer Context Chain (Product ➔ Phase ➔ Objective ➔ Task ➔ Review Scope) without dictating conclusions.

5. **Adaptive Modular Explanations**  
   `explain-and-teach` delivers only the specific slice requested (Trade-offs, Ripple Effects, or First-Principles Mental Models) without forcing unrequested lengthy lectures.

---

## License

MIT License. Developed for the Open Agent Skills Ecosystem.
