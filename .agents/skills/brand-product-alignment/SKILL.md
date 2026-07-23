---
name: brand-product-alignment
description: Conduct an interactive, probing brand & product discovery session to extract brand-product positioning, hard boundaries, anti-patterns, and experience moats. Synthesize brand-product-alignment-spec.md as a version-controlled specification. Use when defining, aligning, or locking down brand & product identity before front-end design or backend architecture.
---

# Brand & Product Alignment (Fluid Discovery)

This skill governs **pure brand positioning, product philosophy, and audience perception alignment**. Human dialogue is naturally fluid and non-linear—therefore, **this skill does NOT enforce a rigid A ➔ B ➔ C linear questionnaire**.

Instead, the conversation flows organically while the agent maintains a **Behind-the-Scenes Brand & Product Context Checklist** to ensure all necessary dimensions are covered for downstream implementation.

---

## Operating Principle: Fluid Conversation, Anti-Yes-Man Protocol

1. **Fluid Human Dialogue**: Let the conversation flow naturally wherever the user takes it. Respond, react, and build upon ideas organically rather than forcing rigid step transitions.
2. **Active Push-Back & Anti-Yes-Man Rule (NEVER Be a Yes-Man)**:
   - The agent **MUST NOT be a passive listener or a sycophantic yes-man**.
   - The agent has the **explicit right and obligation to question choices, point out logical contradictions, push back on unexamined assumptions, and offer proactive alternative recommendations**.
   - If the user proposes a choice that creates a hidden trade-off or violates a previously agreed boundary, call it out constructively: *"Pilihan ini bagus untuk X, tapi membuat kontradiksi dengan batas Y yang tadi kita sepakati. Bagaimana kalau kita pertimbangkan opsi Z?"*
3. **Behind-the-Scenes Checklist Tracking**: Dynamically check off required brand-product dimensions as they are naturally discussed during conversation.
4. **Jargon-Free & Grounded**: Translate abstract concepts into concrete, real-world human feelings and visual/product examples.

---

## Required Brand & Product Context Checklist

The agent must ensure all 5 items are checked off before generating the spec:

- [ ] **1. 3-Second Perception Lens & Product Vibe**: The exact emotional anchor, target impression, and product lens within 3 seconds of interaction.
- [ ] **2. Identity & Product Boundaries ("What It IS vs. What It IS NOT")**: At least 3 positive brand/product traits vs. 3 banned identities/behaviors.
- [ ] **3. Blacklisted Industry Clichés & Anti-Patterns**: At least 3 overused marketing, visual, or product positioning tropes explicitly banned.
- [ ] **4. Brand-Product Differentiation & Experience Moat**: The core personality and uncopyable experience/technical signature.
- [ ] **5. Non-Negotiable Usability & Quality Contract**: Primary user capability or quality baseline that aesthetic or structural choices must never compromise.

---

## Execution & Artifact Synthesis

Once all 5 items on the checklist are checked off through natural conversation, synthesize findings into `brand-product-alignment-spec.md`:

```markdown
# Brand & Product Alignment Specification: [Product / Brand Name]

## 1. Brand-Product Vibe & 3-Second Perception Lens
- **Core Vibe**: ...
- **3-Second Impression**: ...
- **Target Perception Lens**: ...

## 2. Brand & Product Boundaries ("What It IS vs. What It IS NOT")
| Product Trait (IS) | Banned Identity (IS NOT) |
| :--- | :--- |
| ... | ... |

## 3. Blacklisted Industry Clichés & Anti-Patterns
- ❌ ...

## 4. Brand-Product Differentiation & Experience Moat
- **Product Personality Signature**: ...
- **Defensible Experience Moat**: ...

## 5. Non-Negotiable Usability Contract
- **Core Capability Baseline**: ...
```

---

## Git & Version Control Integration

- **Spec Version Control**: Commit `brand-product-alignment-spec.md` to git root or `docs/specs/` using conventional commits (`docs(brand): create brand and product alignment spec`).
- **Issue Linkage**: Link the commit/spec to active GitHub Issues or project milestones (`Refs #123` / `Closes #45`).

**Completion Criterion**: All 5 items on the Brand & Product Context Checklist are fulfilled through fluid conversation, `brand-product-alignment-spec.md` is approved by the user, and committed to git.
