# GSD-presentation

## What This Is

En 45-minuters utbildningspresentation riktad till utvecklare om hur man arbetar effektivt med AI agent frameworks — med fokus på GSD (Get Shit Done). Materialet levereras som ett markdown-dokument (wiki/repo) samt en Marp slide-deck, båda skrivna på svenska med engelska facktermer bibehållna.

## Core Value

Utvecklare i teamet ska förstå **hur** man använder GSD i sin vardag — från lättviktiga one-off tasks till fullskaliga projekt — och kunna börja direkt efter presentationen.

## Requirements

### Validated

- [x] Slide-deck i Marp-format (~45 min presentation) — Validated in Phase 1: Foundation & Setup (skeleton)
- [x] Språkpolicy: svenska med engelska termer — Validated in Phase 1: Foundation & Setup (TERMINOLOGY.md)
- [x] On-ramp: hur man börjar light (`/gsd-quick`, `/gsd-fast`, `/gsd-do`) — Validated in Phase 2: Core Payload — On-Ramp
- [x] GSD deep-dive: arkitektur, workflow, nyckelkoncept — Validated in Phase 3: Core Payload — Full Workflow (Section 3: mental model)
- [x] Full workflow: new-project → plan → execute lifecycle — Validated in Phase 3: Core Payload — Full Workflow (Section 5: lifecycle)
- [x] Scenarion: greenfield, brownfield, debugging, quick fixes — Validated in Phase 4: Scenarios & Best Practices (Section 6)
- [x] Best practices: hur man tänker och promptar för bästa resultat — Validated in Phase 4: Scenarios & Best Practices (Section 7)

### Active

- [ ] Slide-deck i Marp-format (~45 min presentation) — content to be added in Phase 5
- [ ] Markdown-dokument med fullständigt innehåll (wiki/repo-vänligt)
- [ ] Introduktion: varför AI agent frameworks — problemet de löser
- [ ] Kort jämförelse: GSD vs BMAD vs andra frameworks
- [ ] Språkpolicy: svenska med engelska termer (phases, roadmap, agents etc.) — policy established, applied in Phases 3–6

### Out of Scope

- Live demo-material eller demo-scripts — presentationen är konceptuell/visuell
- Djupgående teknisk implementation av GSD:s internals — fokus är på användning
- Företagsspecifika exempel — generella scenarion som alla kan relatera till
- Videoinspelning eller voiceover — enbart textbaserat material

## Context

- Publiken är en blandad grupp: från AI-skeptiker till early adopters
- Alla är utvecklare men med varierande erfarenhet av AI-assisterad utveckling
- Presentatören är Tech Lead och vill utbilda teamet
- GSD är installerat via Copilot CLI skills-systemet
- Materialet ska kunna läsas standalone (utan presentatör) men primärt användas vid presentation
- Inga försvenskningar av engelska begrepp — "phase" inte "fas", "roadmap" inte "vägkarta"

## Constraints

- **Format**: Marp-kompatibel markdown för slides + separat dokument för detaljer
- **Längd**: ~45 minuter presentation (begränsar antal slides och djup per ämne)
- **Språk**: Svenska med engelska facktermer — naturlig svengelska
- **Ton**: Utbildande, inte säljande — fokus på "hur" snarare än "varför"
- **Publik**: Måste fungera för både skeptiker och entusiaster

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| Marp för slides | Markdown-native, versioneringsbart, ingen PowerPoint-dependency | — Pending |
| Svenska + engelska termer | Naturligt för svensk dev-kontext, undviker krystad försvenskning | — Pending |
| GSD som huvudfokus med kort framework-jämförelse | Teamet ska använda GSD — jämförelse ger kontext men ska inte förvirra | — Pending |
| On-ramp med light commands först | Sänker tröskeln — visa att man kan börja utan full workflow | — Pending |

## Evolution

This document evolves at phase transitions and milestone boundaries.

**After each phase transition** (via `/gsd-transition`):
1. Requirements invalidated? → Move to Out of Scope with reason
2. Requirements validated? → Move to Validated with phase reference
3. New requirements emerged? → Add to Active
4. Decisions to log? → Add to Key Decisions
5. "What This Is" still accurate? → Update if drifted

**After each milestone** (via `/gsd-complete-milestone`):
1. Full review of all sections
2. Core Value check — still the right priority?
3. Audit Out of Scope — reasons still valid?
4. Update Context with current state

---
*Last updated: 2026-04-16 after Phase 5 completion — Framing intro & landscape slides added (Sections 1 & 2)*
