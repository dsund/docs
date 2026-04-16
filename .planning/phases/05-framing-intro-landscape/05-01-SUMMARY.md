---
phase: 05-framing-intro-landscape
plan: "01"
subsystem: presentation
tags: [marp, slides, intro, problem-statement, agent-framework, bmad, collaboration]

requires:
  - phase: 01-foundation-setup
    provides: Marp skeleton with section dividers and slide styles
  - phase: 03-core-payload-full-workflow
    provides: Section 3 GSD mental model content that Section 2 bridges into
  - phase: 04-scenarios-best-practices
    provides: Section 7 "Du bestämmer, AI utför" slide to avoid duplication

provides:
  - Section 1 content slides (problem recognition, gap deepening, collaboration reframe)
  - Section 2 content slides (agent framework concept, GSD vs BMAD philosophy contrast)
  - Bridge narratives connecting Section 1→2→3

affects: [companion-document, phase-06-polish]

tech-stack:
  added: []
  patterns: [blockquote-bridge, ascii-building-blocks, philosophy-contrast-table]

key-files:
  created: []
  modified: [slides.md]

key-decisions:
  - "Used evolution analogy (IDE→Linter→CI→AI) for collaboration reframe instead of role-based metaphor, since Section 7 already has 'Du bestämmer, AI utför'"
  - "Deductive flow for Section 2: define agent framework concept first, then show GSD vs BMAD as examples"
  - "3 data rows in comparison table (Approach, Agents, Styrka) — philosophy-level only, no feature matrix"

patterns-established:
  - "Blockquote bridge: closing blockquote on last slide of section tees up next section's topic"
  - "ASCII building blocks: labeled box diagram for conceptual visuals"

requirements-completed: [SLIDE-02, CTXT-01, CTXT-02, CTXT-03, CTXT-04]

duration: 5min
completed: 2026-04-16
---

# Phase 5 Plan 01: Framing Intro & Landscape Summary

**5 content slides across Sections 1–2: relatable ChatGPT/Copilot frustrations → collaboration reframe via tool evolution → agent framework building blocks → GSD vs BMAD philosophy contrast — all in Swedish with English technical terms, positive-first framing, no fear language**

## Performance

- **Duration:** 5 min
- **Started:** 2026-04-16T09:05:00Z
- **Completed:** 2026-04-16T09:10:00Z
- **Tasks:** 2
- **Files modified:** 1

## Accomplishments

### Task 1: Section 1 — Problem Statement and Collaboration Reframe
- Added 3 content slides after Section 1 divider ("Var är vi idag?")
- **Slide 1 — "Känner du igen det här?"**: Opening quote + 4 relatable ChatGPT/Copilot Chat frustrations (lost context, forgotten decisions, no verification, copy-paste prompts)
- **Slide 2 — "Det som saknas"**: Three concrete gaps (kontext, struktur, kvalitet) framed as ceiling not failure
- **Slide 3 — "Nästa steg i en bekant resa"**: Evolution analogy (Manuellt → IDE → Linter → CI → AI-assistent) with bridge to agent frameworks
- Commit: `01f29d9`

### Task 2: Section 2 — Agent Framework Concept and GSD vs BMAD Comparison
- Added 2 content slides after Section 2 divider ("Vad finns?")
- **Slide 1 — "Vad är ett AI agent framework?"**: ASCII building blocks diagram (LLM + Instruktioner + Verktyg + Minne) with before/after contrast
- **Slide 2 — "Två filosofier"**: Clean 3-row comparison table (Approach, Agents, Styrka), balanced "Olika problem, olika verktyg" framing, bridge to Section 3
- Total slide count: 51 (target: 49–53) ✓
- Commit: `4845784`

## Decisions Made

1. **Evolution analogy over role-based metaphor (D-06):** Section 7 already has "Du bestämmer, AI utför" — used IDE → Linter → CI → AI evolution instead to avoid duplication and reinforce the "natural next step" narrative
2. **Deductive flow (D-11):** Defined "agent framework" concept first, then showed GSD vs BMAD as two examples — gives audience vocabulary before comparison
3. **Philosophy-only contrast (D-07, D-09):** 3 data rows only (Approach, Agents, Styrka), balanced "Olika problem, olika verktyg" — no feature matrix, no selling

## Verification Results

- ✅ `Känner du igen det här?` slide present
- ✅ `Det som saknas` slide present
- ✅ `Nästa steg i en bekant resa` slide present
- ✅ `Vad är ett AI agent framework?` slide with ASCII diagram present
- ✅ `Två filosofier` slide with GSD/BMAD comparison table present
- ✅ No fear framing ("ersätter AI mig", "am I being replaced") detected
- ✅ No forbidden framework mentions (Cursor, aider, Windsurf, Claude Code, Roo Code)
- ✅ No `_class` or `_paginate` directives on content slides
- ✅ Bridge narratives: Section 1→"agent frameworks"→Section 2→"i praktiken"→Section 3
- ✅ Total slide count: 51 (within 49–53 target range)

## Deviations from Plan

None — plan executed exactly as written.

## Known Stubs

None — all content is final presentation material.
