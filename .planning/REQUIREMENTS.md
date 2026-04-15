# Requirements: GSD-presentation

**Defined:** 2026-04-15
**Core Value:** Utvecklare ska förstå hur man använder GSD i sin vardag — från lättviktiga tasks till fullskaliga projekt — och kunna börja direkt efter presentationen.

## v1 Requirements

Requirements for initial release. Each maps to roadmap phases.

### Slide Deck

- [ ] **SLIDE-01**: Marp-kompatibel slide-deck i markdown-format
- [ ] **SLIDE-02**: ~60 minuters presentationsinnehåll med tydlig sektionsuppdelning
- [ ] **SLIDE-03**: Visuell command spectrum — `/gsd-fast` → `/gsd-quick` → `/gsd-do` → full workflow
- [ ] **SLIDE-04**: Realistiska terminal-exempel (code blocks med prompts och output)
- [ ] **SLIDE-05**: Svenska text med engelska facktermer genomgående

### Content — Problem & Kontext

- [ ] **CTXT-01**: Problem statement — varför agent frameworks behövs (context window limits, consistency, quality gates)
- [ ] **CTXT-02**: Konceptuell förklaring — vad är ett AI agent framework (LLM + instructions + tools + memory)
- [ ] **CTXT-03**: Kort jämförelse GSD vs BMAD vs andra frameworks (workflow-centric vs persona-based)
- [ ] **CTXT-04**: Skeptics-to-practitioners narrative arc — adressera "ersätter AI mig?" tidigt

### Content — GSD Deep-Dive

- [ ] **DEEP-01**: Core workflow overview (new-project → discuss → plan → execute → verify)
- [ ] **DEEP-02**: Agent arkitektur — 18 specialized agents, orchestrator pattern, wave-based execution
- [ ] **DEEP-03**: Planning artifacts walkthrough (`.planning/` directory: PROJECT.md, ROADMAP.md, STATE.md)
- [ ] **DEEP-04**: Persistent project memory (STATE.md, `/gsd-resume-work`, `/gsd-progress`)
- [ ] **DEEP-05**: Goal-backward verification ("task completion ≠ goal achievement", 4 nivåer)
- [ ] **DEEP-06**: Composable flags pattern (`/gsd-quick --discuss --research --full`)

### Content — On-Ramp & Praktisk Användning

- [ ] **PRAC-01**: Getting started — installation och första kommandot
- [ ] **PRAC-02**: On-ramp: börja light med `/gsd-fast` (≤3 edits, no planning)
- [ ] **PRAC-03**: Graduated complexity — `/gsd-quick` → `/gsd-do` → full workflow
- [ ] **PRAC-04**: Brownfield awareness — `/gsd-map-codebase` för befintlig kod
- [ ] **PRAC-05**: Phase insertion och roadmap adaptation (`/gsd-insert-phase`)
- [ ] **PRAC-06**: Cross-AI review (`/gsd-review`) — multi-AI peer review
- [ ] **PRAC-07**: Autonomous mode (`/gsd-autonomous`) — end-game vision
- [ ] **PRAC-08**: Project lifecycle — hantera `.planning/`, starta nya projekt, byta mellan projekt, rensa och börja om

### Content — Best Practices & Mindset

- [ ] **BEST-01**: Mental model shifts — tänk outcomes inte steg, decisions vs execution
- [ ] **BEST-02**: Prompt crafting — hur man pratar med agents för bästa resultat
- [ ] **BEST-03**: Escape hatches — när man INTE ska använda agents
- [ ] **BEST-04**: Anti-patterns — vaga prompts, skippa verification, micro-management
- [ ] **BEST-05**: "Start Monday" challenge — konkret nästa steg efter presentationen

### Content — Scenarion

- [ ] **SCEN-01**: Greenfield-projekt — full workflow från idé till implementation
- [ ] **SCEN-02**: Brownfield — jobba med befintlig kodbas
- [ ] **SCEN-03**: Quick fix / debugging — snabba insatser med `/gsd-fast` och `/gsd-debug`
- [ ] **SCEN-04**: Decision tree — "vilket kommando ska jag använda?"

### Companion Document

- [ ] **COMP-01**: Markdown-dokument med fullständigt innehåll (wiki/repo-vänligt)
- [ ] **COMP-02**: Djupare än slides — full command reference, detaljerade scenarion
- [ ] **COMP-03**: Standalone-läsbart utan presentatör

## v2 Requirements

Deferred to future release. Tracked but not in current roadmap.

### Extended Material

- **EXT-01**: Command cheat sheet / reference card (separat handout)
- **EXT-02**: Workshop-format version (hands-on 2h variant)
- **EXT-03**: Video recording med voiceover
- **EXT-04**: Interaktiva demo-scripts

## Out of Scope

| Feature | Reason |
|---------|--------|
| Live demo-scripts | Presentationen är konceptuell/visuell per scope-beslut |
| GSD internals (implementation details) | Fokus på användning, inte hur GSD är byggt |
| Företagsspecifika exempel | Generella scenarion som alla kan relatera till |
| Engelskspråkig version | Svenska med engelska termer — en version räcker för v1 |
| Marp custom theme | Default theme räcker; polish i v2 |

## Traceability

Which phases cover which requirements. Updated during roadmap creation.

| Requirement | Phase | Status |
|-------------|-------|--------|
| SLIDE-01 | Phase 1 | Pending |
| SLIDE-02 | Phase 5 | Pending |
| SLIDE-03 | Phase 2 | Pending |
| SLIDE-04 | Phase 2 | Pending |
| SLIDE-05 | Phase 1 | Pending |
| CTXT-01 | Phase 5 | Pending |
| CTXT-02 | Phase 5 | Pending |
| CTXT-03 | Phase 5 | Pending |
| CTXT-04 | Phase 5 | Pending |
| DEEP-01 | Phase 3 | Pending |
| DEEP-02 | Phase 3 | Pending |
| DEEP-03 | Phase 3 | Pending |
| DEEP-04 | Phase 3 | Pending |
| DEEP-05 | Phase 3 | Pending |
| DEEP-06 | Phase 3 | Pending |
| PRAC-01 | Phase 2 | Pending |
| PRAC-02 | Phase 2 | Pending |
| PRAC-03 | Phase 2 | Pending |
| PRAC-04 | Phase 4 | Pending |
| PRAC-05 | Phase 6 | Pending |
| PRAC-06 | Phase 6 | Pending |
| PRAC-07 | Phase 6 | Pending |
| PRAC-08 | Phase 3 | Pending |
| BEST-01 | Phase 4 | Pending |
| BEST-02 | Phase 4 | Pending |
| BEST-03 | Phase 4 | Pending |
| BEST-04 | Phase 4 | Pending |
| BEST-05 | Phase 4 | Pending |
| SCEN-01 | Phase 4 | Pending |
| SCEN-02 | Phase 4 | Pending |
| SCEN-03 | Phase 4 | Pending |
| SCEN-04 | Phase 4 | Pending |
| COMP-01 | Phase 6 | Pending |
| COMP-02 | Phase 6 | Pending |
| COMP-03 | Phase 6 | Pending |

**Coverage:**
- v1 requirements: 35 total
- Mapped to phases: 35 ✓
- Unmapped: 0

---
*Requirements defined: 2026-04-15*
*Last updated: 2026-04-15 after initial definition*
