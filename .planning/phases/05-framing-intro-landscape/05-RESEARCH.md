# Phase 5: Framing — Intro & Landscape - Research

**Researched:** 2025-07-18
**Domain:** Presentation content authoring — opening sections (problem statement, agent framework concept, GSD vs BMAD comparison, skeptics narrative)
**Confidence:** HIGH

## Summary

Phase 5 fills the two empty sections at the front of the slide deck: Section 1 ("Var är vi idag?") and Section 2 ("Vad finns?"). These sections were deliberately built last — the "payload first, framing second" strategy means we now know exactly what the intro must set up. The current deck has 44 slides covering Sections 3–8 with rich content on GSD architecture, on-ramp, lifecycle, scenarios, and best practices. Phase 5 adds ~7–9 content slides to the front, bringing the total to ~51–53 slides for a ~60-minute presentation (~1.15 min/slide average, appropriate for Marp decks with a mix of divider slides and talking-point slides).

The primary challenge is **tone calibration**: the intro must validate developer concerns about AI without dwelling on negativity (D-04: positive-first, skip the fear framing), establish shared vocabulary efficiently (what an AI agent framework actually is), and present GSD vs BMAD as a philosophy contrast rather than a feature comparison (D-07, D-09). All content must follow established patterns — spacious layout (one idea per slide), Swedish text with English technical terms per TERMINOLOGY.md, ASCII art in code blocks for visuals, and section dividers with `<!-- _class: divider -->`.

**Primary recommendation:** Write Section 1 as 4–5 slides (relatable pain → collaboration reframe → bridge) and Section 2 as 3–4 slides (agent framework concept → GSD vs BMAD philosophy contrast → bridge to Section 3). Total ~7–9 new content slides. Every slide must reference what the audience already knows (ChatGPT/Copilot Chat frustrations) and set up what comes next (the GSD deep-dive).

<user_constraints>

## User Constraints (from CONTEXT.md)

### Locked Decisions

**Problem Statement (CTXT-01)**
- D-01: Agent's Discretion — choose most compelling approach (pain recognition, technical list, before/after, or combination)
- D-02: Agent's Discretion — slide count and pacing for problem statement
- D-03: Reference typical ChatGPT/Copilot Chat frustrations the audience has lived — "you've pasted the same context into a new chat, re-explained what you're building." Ground in their experience.

**Skeptics Narrative (CTXT-04)**
- D-04: Positive-first reframing — skip "am I being replaced?" fear framing, go straight to AI as collaboration
- D-05: Dedicated slide early — collaboration message appears right after problem statement, before GSD content
- D-06: Agent's Discretion — choose best collaboration metaphor (role-based, analogy-based, or concrete output)

**Framework Comparison (CTXT-03)**
- D-07: Philosophy contrast, not feature table — workflow-centric (GSD) vs persona-based (BMAD). High-level, 1–2 slides max.
- D-08: GSD and BMAD only — no mention of other frameworks (Cursor, Roo Code, aider)
- D-09: Balanced presentation — present both fairly, let audience see reasoning, credibility over persuasion

**Concept Slide (CTXT-02)**
- D-10: Agent's Discretion — how to explain "AI agent framework" (building blocks, analogy, definition, or combination)
- D-11: Agent's Discretion — placement relative to GSD vs BMAD comparison (deductive vs inductive flow)

**Slide Style (carried from Phases 1–4)**
- D-12: Spacious layout — one idea per slide
- D-13: Section dividers: centered h1 + hr with `<!-- _class: divider -->`
- D-14: Terminal examples: bash fence, $ prompt, compact output
- D-15: ASCII art in code blocks for diagrams
- D-16: Copilot-only references, no Claude Code
- D-17: Swedish text with English technical terms per TERMINOLOGY.md

### Agent's Discretion
- Problem statement approach and slide count — D-01, D-02
- Collaboration metaphor — D-06
- Concept slide format and placement — D-10, D-11

### Deferred Ideas (OUT OF SCOPE)
None — discussion stayed within phase scope

</user_constraints>

<phase_requirements>

## Phase Requirements

| ID | Description | Research Support |
|----|-------------|------------------|
| SLIDE-02 | ~60 minuters presentationsinnehåll med tydlig sektionsuppdelning | Slide count analysis: current 44 slides + ~7-9 new = 51-53 total, section structure validated |
| CTXT-01 | Problem statement — varför agent frameworks behövs (context window limits, consistency, quality gates) | Pain recognition patterns, ChatGPT/Copilot Chat frustrations, established relatable framing |
| CTXT-02 | Konceptuell förklaring — vad är ett AI agent framework (LLM + instructions + tools + memory) | Building blocks model validated, ASCII visual approach, placement recommendations |
| CTXT-03 | Kort jämförelse GSD vs BMAD (workflow-centric vs persona-based) | BMAD philosophy validated at MEDIUM confidence, comparison table reduced to philosophy contrast per D-07 |
| CTXT-04 | Skeptics-to-practitioners narrative arc — adressera "ersätter AI mig?" tidigt | Positive-first reframing per D-04, collaboration slide placement per D-05, metaphor options per D-06 |

</phase_requirements>

## Project Constraints (from copilot-instructions.md)

The copilot-instructions.md establishes GSD workflow enforcement:
- Before making file changes, work through a GSD command
- Use `/gsd-execute-phase` for planned phase work
- Do not make direct repo edits outside a GSD workflow unless user explicitly asks

Technology stack from STATE.md:
- Marp CLI 4.3.1 for slide generation
- VS Code with Marp extension for live preview
- Default Marp theme, 16:9 aspect ratio
- Pagination enabled, no footer text

## Architecture Patterns

### Slide Deck Structure — Current State

```
slides.md (44 slides currently)
├── Title slide (lead)
├── Section 1 divider: "Var är vi idag?" ─── EMPTY (Phase 5 adds here)
│   └── <!-- Section 1: The Problem — slides added by Phase 5 -->
├── Section 2 divider: "Vad finns?" ─────── EMPTY (Phase 5 adds here)
│   └── <!-- Section 2: Framework Landscape — slides added by Phase 5 -->
├── Section 3 divider: "Hur fungerar det?"
│   └── 4 slides (Phase 3: mental model, agents, waves, .planning/)
├── Section 4 divider: "Börja enkelt"
│   └── 8 slides (Phase 2: spectrum, commands, install, bridge)
├── Section 5 divider: "Hela livscykeln"
│   └── 10 slides (Phase 3: lifecycle, artifacts, memory, verification)
├── Section 6 divider: "I din vardag"
│   └── 7 slides (Phase 4: decision tree, scenarios)
├── Section 7 divider: "Tänk så här"
│   └── 5 slides (Phase 4: best practices, anti-patterns)
└── Section 8 divider: "Börja på måndag"
    └── 2 slides (Phase 4: challenge, closing)
```

### Phase 5 Integration Points

**Section 1 content** inserts after line 63 (`<!-- Section 1: The Problem — slides added by Phase 5 -->`) and before line 65 (`---` separator before Section 2 divider).

**Section 2 content** inserts after line 74 (`<!-- Section 2: Framework Landscape — slides added by Phase 5 -->`) and before line 76 (`---` separator before Section 3 divider).

### Recommended Slide Layout for Phase 5

**Section 1: "Var är vi idag?" — 4-5 content slides**

| Slide | Content | Purpose |
|-------|---------|---------|
| 1.1 | Problem recognition — ChatGPT/Copilot Chat frustrations | Hook: "you've done this" (D-03) |
| 1.2 | The gap — what breaks without structure | Deepen the pain |
| 1.3 | Collaboration reframe — AI as teammate | Positive framing (D-04, D-05) |
| 1.4 | Bridge — "Frameworks solve this" | Transition to Section 2 |

**Section 2: "Vad finns?" — 3-4 content slides**

| Slide | Content | Purpose |
|-------|---------|---------|
| 2.1 | What is an AI agent framework? (building blocks) | Shared vocabulary (CTXT-02) |
| 2.2 | GSD vs BMAD philosophy contrast | Position, not sell (D-07, D-08, D-09) |
| 2.3 | Optional: Why GSD for this team (brief) | Context for the deep-dive |
| 2.4 | Bridge — "Let's see how it works" | Transition to Section 3 |

### Established Slide Patterns (MUST follow)

```markdown
---

<!-- _class: divider -->
<!-- _paginate: skip -->

# Section Title

<hr>

---

## Content Slide Title

Content here — one idea per slide.

> Blockquotes for key insights or memorable phrases.

---
```

**Code blocks:** 0.85em font, border-radius 4px, `bash` fence for terminal, plain fence for ASCII art.

**No `_class` directives on content slides** — only divider slides use class directives.

### Pattern: Problem Recognition Slide

Use before/after contrast or bullet list of relatable frustrations. Reference what the audience has experienced personally. Swedish with English terms per TERMINOLOGY.md.

```markdown
---

## Känner du igen det här?

"Jag har förklarat arkitekturen tre gånger — i tre olika chattar."

- Ny chat = ny kontext. Varje gång.
- AI:n glömmer beslut du tog igår
- Ingen verification — "3 filer skapade!" men inget fungerar
- Copy-paste av samma prompt, om och om igen

> Det funkar — tills uppgiften blir större.
```

### Pattern: Collaboration Reframe Slide

Positive-first framing. No fear, straight to partnership model. Use "du" frequently (D-04).

```markdown
---

## Du bestämmer, AI utför

Inte ersättning — **arbetsfördelning.**

**Du:**
- Arkitekturbeslut
- Kvalitetskrav
- Code review

**AI:**
- Research
- Boilerplate
- Repetitiva tasks

> Samma utveckling som IDE → linter → CI → AI-assistent.
```

### Pattern: Framework Concept Slide

ASCII building blocks in code fence. Define shared vocabulary before comparison.

```markdown
---

## Vad är ett AI agent framework?

```
  ┌─────────────────────────────────┐
  │          FRAMEWORK              │
  │                                 │
  │  ┌─────┐  ┌──────────────┐     │
  │  │ LLM │  │ Instructions │     │
  │  └─────┘  └──────────────┘     │
  │  ┌───────┐  ┌────────┐        │
  │  │ Tools │  │ Memory │        │
  │  └───────┘  └────────┘        │
  └─────────────────────────────────┘
```

LLM + instruktioner + verktyg + minne = **strukturerad AI-assistans.**
```

### Pattern: Philosophy Contrast (NOT feature table)

Keep to high-level principles. Balanced tone. Let the audience draw conclusions.

```markdown
---

## Två filosofier

| | GSD | BMAD |
|---|---|---|
| **Approach** | Workflow-centric | Persona-based |
| **Agents** | Researcher, Planner, Executor, Verifier | PM, Architect, Developer, QA |
| **Styrka** | Execution + verification | Strategic thinking + documentation |

Olika problem, olika lösningar.
Vi valde GSD för **execution med kvalitetskontroll.**
```

### Anti-Patterns to Avoid

- **Comparison trap:** Per D-07 and architecture research, max 1-2 slides on comparison. Don't build a feature matrix. Don't mention Cursor, aider, Windsurf, or Claude Code (D-08). The audience doesn't need to evaluate alternatives.
- **Fear framing:** Per D-04, don't open with "am I being replaced?" Don't dwell on negative scenarios. Go straight to collaboration.
- **Enthusiast bias:** Per Pitfall 4 from project research, avoid "amazing" or "game-changer" language. Use measured, technical, observational tone: "du har troligen upplevt..."
- **Abstract before concrete:** Don't define frameworks theoretically. Start with recognizable pain, then name the solution category.
- **Selling GSD over BMAD:** Per D-09, present both fairly. "Vi valde GSD för X" is fine; "GSD is better because Y" is not.

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| BMAD feature comparison | Feature-by-feature table | Philosophy contrast (workflow vs persona) | D-07 locks this — comparison trap wastes time and shifts focus |
| AI landscape survey | Multi-framework overview | GSD + BMAD only | D-08 locks this — other frameworks are out of scope |
| Complex visual diagrams | Multi-layered Mermaid or SVG | ASCII art in code blocks | D-15 — established pattern, works everywhere, terminal-native feel |

## BMAD Framework — Validated Positioning

**Confidence: MEDIUM** — core philosophy is well-established and stable; specific feature details may have evolved.

### What BMAD Is

BMAD (Breakthrough Method for Agile AI-Driven Development) is a persona-based AI agent framework. It simulates a development team by creating AI agents that role-play specific team members: Product Manager, Architect, Developer, QA Engineer. The user drives conversations with each persona to produce deliverables.

### Philosophy Contrast (for slides)

| Dimension | GSD | BMAD |
|-----------|-----|------|
| **Core philosophy** | Workflow-centric — structured phases with specialized functional agents | Persona-centric — simulate a dev team through AI role-play |
| **Agent model** | Named by function (researcher, planner, executor, verifier) | Named by role (PM, Architect, Developer, QA) |
| **Control flow** | Framework enforces workflow: discuss → research → plan → execute → verify | User drives conversations between personas |
| **Primary output** | Executable plans + verified code + persistent project memory | Strategic documents (PRD, architecture docs, user stories) |
| **Entry model** | Graduated: `/gsd-fast` (30 sec) → full workflow | Typically starts with PM persona to create PRD |
| **Sweet spot** | Execution management with quality gates | Strategic thinking and collaborative documentation |

### What to Say on Slides (per D-07, D-08, D-09)

- Philosophy difference only — one slide with a clean table
- Balanced: "Olika problem, olika lösningar"
- Why GSD was chosen: "execution med kvalitetskontroll" (what this team needs)
- Do NOT list specific features, agent counts, or technical details
- Do NOT mention any other frameworks

### STATE.md Blocker Resolution

STATE.md flags: "BMAD comparison details are MEDIUM confidence and may need validation before slide creation." The high-level philosophy contrast (workflow vs persona) is stable and well-established — this is the foundation of the BMAD approach and hasn't fundamentally changed. For the 1–2 slide philosophy contrast required by D-07, MEDIUM confidence is sufficient. Specific features and technical details are not needed and would violate the "philosophy contrast, not feature table" decision.

**Recommendation:** Proceed with the philosophy contrast as documented. Flag in the plan that the presenter should verify BMAD's current state before delivering the presentation, but this should not block slide creation.

## Narrative Flow — Section-by-Section

### Section 1: "Var är vi idag?" (Problem + Collaboration)

**Narrative arc:** Recognition → Deepening → Reframe → Bridge

1. **Hook with recognition (1 slide):** Reference ChatGPT/Copilot Chat frustrations. "Ny chat = ny kontext." The audience nods — they've done this. Keep it personal ("du har..."). (D-03)

2. **Deepen the gap (1 slide):** What breaks when tasks get bigger — context loss across sessions, no structured approach to multi-step work, no verification that the goal was actually met. Frame as ceiling, not failure.

3. **Collaboration reframe (1 slide):** Positive-first (D-04). Dedicated slide (D-05). AI as natural evolution of developer tools — IDE → linter → CI → AI. Developer decides, AI executes. "Du" everywhere. (D-06 discretion)

4. **Bridge to Section 2 (can be integrated into slide 3 or separate):** "Det finns ett namn för lösningen: agent frameworks."

**Time budget:** ~4–5 minutes
**Slide count:** 3–4 content slides

### Section 2: "Vad finns?" (Concept + Comparison)

**Narrative arc:** Define → Exemplify → Bridge

1. **What is an agent framework? (1 slide):** LLM + instructions + tools + memory = structured AI assistance. ASCII building blocks visual. Gives shared vocabulary. (D-10 discretion)

2. **GSD vs BMAD philosophy (1-2 slides):** Clean table with philosophy contrast. Balanced tone. "Vi valde GSD för execution med kvalitetskontroll." (D-07, D-08, D-09)

3. **Bridge to Section 3 (can be the closing line of comparison slide):** "Låt oss se hur GSD fungerar i praktiken." Links to the "Hur fungerar det?" section that already exists.

**Time budget:** ~3–4 minutes
**Slide count:** 2–3 content slides

### Placement Recommendation (D-11)

**Deductive flow (recommended):** Define concept first → then show GSD and BMAD as examples. This gives the audience a frame before the comparison, making the contrast more meaningful.

Rationale: The audience needs the "agent framework" vocabulary before they can meaningfully compare two approaches. Without it, "workflow-centric" and "persona-based" are abstract terms.

## Slide Count & Pacing Analysis

### Current Deck (without Phase 5)

| Section | Slides | Est. Time |
|---------|--------|-----------|
| Title | 1 | 0.5 min |
| S1 divider (empty) | 1 | — |
| S2 divider (empty) | 1 | — |
| S3: Hur fungerar det? | 1 div + 4 | 5 min |
| S4: Börja enkelt | 1 div + 8 | 10 min |
| S5: Hela livscykeln | 1 div + 10 | 13 min |
| S6: I din vardag | 1 div + 7 | 8 min |
| S7: Tänk så här | 1 div + 5 | 7 min |
| S8: Börja på måndag | 1 div + 2 | 3 min |
| **Total** | **44** | **~46 min** |

### After Phase 5 Additions

| Section | Slides | Est. Time |
|---------|--------|-----------|
| Title | 1 | 0.5 min |
| S1: Var är vi idag? | 1 div + 3-4 | 4-5 min |
| S2: Vad finns? | 1 div + 2-3 | 3-4 min |
| S3: Hur fungerar det? | 1 div + 4 | 5 min |
| S4: Börja enkelt | 1 div + 8 | 10 min |
| S5: Hela livscykeln | 1 div + 10 | 13 min |
| S6: I din vardag | 1 div + 7 | 8 min |
| S7: Tänk så här | 1 div + 5 | 7 min |
| S8: Börja på måndag | 1 div + 2 | 3 min |
| **Total** | **~51-53** | **~54-58 min** |

**Assessment:** 51–53 slides at ~54–58 minutes is appropriate for a ~60-minute presentation. Leaves 2–6 minutes for Q&A buffer and natural pauses. Satisfies SLIDE-02 requirement for ~60 minutes with clear section structure.

## Common Pitfalls

### Pitfall 1: The Comparison Trap
**What goes wrong:** The BMAD comparison expands into a detailed feature-by-feature analysis, consuming 5+ minutes and shifting focus from GSD education to framework evaluation.
**Why it happens:** The presenter knows both frameworks well and finds the differences interesting. Audience questions during the talk extend the comparison section.
**How to avoid:** Hard limit of 1–2 slides (D-07). Philosophy contrast only — no feature matrix, no agent count comparison, no workflow detail. One clean table + one sentence of context. Move on.
**Warning signs:** More than 2 slides in the comparison section. Rows in the table exceeding 4. Audience asking "so which is better?"

### Pitfall 2: Fear-First Opening
**What goes wrong:** The presentation opens with "Am I being replaced?" or "AI is disrupting everything" — the audience's anxiety spikes before any value is demonstrated.
**Why it happens:** Pitfall 2 from project research describes this as "the elephant." D-04 explicitly rules it out — positive-first.
**How to avoid:** Go straight to collaboration. Reference the natural evolution of tools: IDE → linter → CI → AI agent. The collaboration message must appear as a dedicated slide right after the problem statement (D-05).
**Warning signs:** Words like "hot-ämne," "disruption," "ersätter" in the opening slides.

### Pitfall 3: Abstract Problem Statement
**What goes wrong:** The problem is described in technical terms (context window limits, token budgets, stateless sessions) rather than in terms the audience has felt personally.
**Why it happens:** The presenter thinks technically. D-03 explicitly counters this: ground in ChatGPT/Copilot Chat frustrations they've lived.
**How to avoid:** Use "du" language: "Du har klistrat in samma kontext i en ny chat." "Du har förklarat arkitekturen tre gånger." Show the frustration first, name the technical cause second.
**Warning signs:** Terms like "context window" or "token limit" appearing before a relatable scenario.

### Pitfall 4: Concept Slide Too Deep
**What goes wrong:** The "what is an agent framework" slide becomes a mini-lecture on LLM architecture, tool-use patterns, and memory systems.
**Why it happens:** The concept is genuinely interesting and the presenter has deep knowledge.
**How to avoid:** One visual, one sentence each for the four building blocks (LLM, instructions, tools, memory). Total time: 1 minute. The audience needs vocabulary, not understanding of implementation. They'll get depth in Sections 3-5.
**Warning signs:** More than one slide on the concept. Technical terms like "function calling" or "retrieval augmented generation."

## Code Examples

### Section 1 — Problem Slide with Relatable Pain

```markdown
---

## Känner du igen det här?

"Jag har förklarat arkitekturen tre gånger — i tre olika chattar."

- Ny chat = ny kontext. Varje gång.
- AI:n glömmer beslut du tog igår
- Ingen verification — "3 filer skapade!" men fungerar det?
- Copy-paste av samma prompt, om och om igen

> Ju större uppgiften, desto mer faller isär.
```

### Section 1 — Collaboration Slide (Positive-First)

```markdown
---

## Utvecklarens nya arbetsfördelning

**Du:**
- Vad ska byggas
- Arkitekturbeslut
- Code review

**AI:**
- Research och analys
- Boilerplate och repetition
- Planering och implementation

> Samma resa: manuellt → IDE → linter → CI → **AI-assistent**
```

### Section 2 — Agent Framework Concept

```markdown
---

## Vad är ett AI agent framework?

```
  ┌──────────────────────────────────────┐
  │           AGENT FRAMEWORK            │
  │                                      │
  │  LLM            Instruktioner        │
  │  (hjärnan)      (hur den jobbar)     │
  │                                      │
  │  Verktyg        Minne                │
  │  (vad den kan)  (vad den kommer      │
  │                  ihåg)               │
  └──────────────────────────────────────┘
```

Utan framework: ChatGPT med copy-paste.
Med framework: **strukturerad assistent som minns.**
```

### Section 2 — Philosophy Contrast

```markdown
---

## Två filosofier

| | GSD | BMAD |
|---|---|---|
| **Approach** | Workflow-centric | Persona-based |
| **Agents** | Researcher, Planner, Executor, Verifier | PM, Architect, Developer, QA |
| **Styrka** | Execution + verification | Strategi + dokumentation |

Olika problem, olika verktyg.
Vi valde GSD — **execution med kvalitetskontroll.**
```

### Section Transition — Bridge to Section 3

```markdown
> Låt oss se hur GSD fungerar i praktiken.
```

The bridge line can be added as a blockquote at the bottom of the last Section 2 slide, or as a standalone minimal slide. Prefer integrating into the last content slide (less overhead, smoother flow).

## Terminology Reminders

Per TERMINOLOGY.md, the following English terms MUST be used (not Swedish equivalents):

| Use (English) | Don't use (Swedish) |
|---------------|---------------------|
| agent | agent (same) |
| framework | ramverk |
| workflow | arbetsflöde |
| prompt | prompt (same) |
| verification | verifiering |
| context window | kontextfönster |
| codebase | kodbas |

Swedish inflections OK: "ett agent framework," "i en workflow," "din codebase."

## Existing Content Cross-References

Phase 5 slides must set up content that already exists in later sections. Key connections:

| Phase 5 introduces... | Later section delivers... |
|----------------------|--------------------------|
| "AI:n glömmer beslut" (problem) | Section 5: STATE.md + `/gsd-resume-work` (solution) |
| "Ingen verification" (problem) | Section 5: Goal-backward verification (solution) |
| "Du bestämmer, AI utför" (reframe) | Section 7: "Du bestämmer, AI utför" slide (deepened) |
| Agent framework building blocks | Section 3: 18 agents, orchestrator pattern (detailed) |
| GSD = workflow-centric | Section 3+4+5: Full workflow demonstrated |
| "Execution med kvalitetskontroll" | Section 5: 4-level verification, Section 7: "Trust but verify" |

**Important:** Section 7 already has a "Du bestämmer, AI utför" slide. The collaboration slide in Section 1 should use different framing — perhaps the evolution analogy (IDE → linter → CI → AI) or role-based division (decisions vs execution) — so it complements rather than duplicates.

## Open Questions

1. **Exact collaboration metaphor (D-06)**
   - What we know: Three options identified — role-based ("du bestämmer, AI utför"), analogy-based (IDE → linter → CI evolution), concrete output showing division of labor
   - What's unclear: Which resonates best for this specific audience
   - Recommendation: The planner should choose the **evolution analogy** ("samma resa som IDE → linter → CI → AI") for the Section 1 collaboration slide, because the Section 7 best practices slide already uses the role-based "Du bestämmer, AI utför" framing. This avoids repetition and provides two complementary perspectives.

2. **Concept slide vs comparison ordering (D-11)**
   - What we know: Deductive (concept first → examples) vs inductive (examples first → generalize)
   - Recommendation: **Deductive** — define "agent framework" first, then show GSD and BMAD as two implementations. Gives the audience vocabulary before the comparison makes sense.

3. **BMAD accuracy for presentation delivery**
   - What we know: Philosophy contrast is stable; specific features may evolve
   - What's unclear: Whether BMAD has added new capabilities that change the positioning
   - Recommendation: Slides use philosophy-level contrast only (stable). Presenter should verify BMAD's current state before delivery, but this doesn't block slide authoring.

## Validation Architecture

### Test Framework

| Property | Value |
|----------|-------|
| Framework | Marp CLI 4.3.1 |
| Config file | Front matter in slides.md |
| Quick run command | `npx @marp-team/marp-cli slides.md --html` (verify renders) |
| Full suite command | `npx @marp-team/marp-cli slides.md --pdf` (verify full deck) |

### Phase Requirements → Test Map

| Req ID | Behavior | Test Type | Automated Command | File Exists? |
|--------|----------|-----------|-------------------|-------------|
| SLIDE-02 | ~60 min content with clear sections | manual | Count slides, estimate pacing | ✅ (slides.md) |
| CTXT-01 | Problem statement with relatable pain | manual | Visual review of Section 1 slides | ✅ (slides.md) |
| CTXT-02 | Agent framework concept explanation | manual | Visual review of concept slide | ✅ (slides.md) |
| CTXT-03 | GSD vs BMAD philosophy contrast | manual | Visual review of comparison slide | ✅ (slides.md) |
| CTXT-04 | Positive-first collaboration narrative | manual | Visual review of collaboration slide | ✅ (slides.md) |

### Sampling Rate
- **Per task commit:** `npx @marp-team/marp-cli slides.md --html` — verify Marp renders without errors
- **Per wave merge:** Full visual review of Section 1 and Section 2 in Marp preview
- **Phase gate:** Slide count validation (51–53 target), pacing estimate (~55–58 min), section coherence check

### Wave 0 Gaps
None — Marp infrastructure exists from Phase 1. All validation is visual/manual for content slides.

## Sources

### Primary (HIGH confidence)
- `slides.md` — Current deck with 44 slides, Section 1 and 2 insertion points verified
- `.planning/phases/05-framing-intro-landscape/05-CONTEXT.md` — All 17 locked decisions
- `.planning/research/ARCHITECTURE.md` — Section architecture, slide budgets, narrative arc
- `.planning/research/FEATURES.md` — Feature landscape, BMAD comparison table, anti-features
- `.planning/research/PITFALLS.md` — Pitfalls 1-4 directly relevant to Phase 5

### Secondary (MEDIUM confidence)
- `.planning/research/FEATURES.md` BMAD comparison — core philosophy validated across multiple training sources; specific features may have evolved
- `.planning/research/SUMMARY.md` — Research summary with BMAD gap flagged

### Tertiary (LOW confidence)
- None — all findings have at least MEDIUM confidence

## Metadata

**Confidence breakdown:**
- Narrative structure: HIGH — well-established patterns from project research, validated by 4 completed phases
- Slide content patterns: HIGH — established in Phases 1-4, fully documented in CONTEXT files
- BMAD comparison: MEDIUM — philosophy is stable, specifics may have evolved
- Slide count/pacing: HIGH — calculated from actual slide count in current deck

**Research date:** 2025-07-18
**Valid until:** 2025-08-18 (30 days — stable content domain, BMAD positioning may need refresh before presentation delivery)
