# Roadmap: GSD-presentation

## Overview

This project delivers a 60-minute developer education presentation (Marp slide deck) and a companion markdown reference document about the GSD framework. The build order follows "payload first, framing second" — core how-to content is written before the introductory framing, because you can't write a sharp hook until you know what it's setting up. The companion document expands slides into a standalone reference after the presentation narrative is locked.

## Phases

**Phase Numbering:**
- Integer phases (1, 2, 3): Planned milestone work
- Decimal phases (2.1, 2.2): Urgent insertions (marked with INSERTED)

Decimal phases appear between their surrounding integers in numeric order.

- [ ] **Phase 1: Foundation & Setup** - Marp skeleton, terminology reference, and file structure
- [ ] **Phase 2: Core Payload — On-Ramp** - Command spectrum, getting started, and graduated complexity slides
- [ ] **Phase 3: Core Payload — Full Workflow** - GSD lifecycle, agent architecture, artifacts, and verification slides
- [ ] **Phase 4: Scenarios & Best Practices** - Decision tree, real-world scenarios, mindset shifts, and action close slides
- [ ] **Phase 5: Framing — Intro & Landscape** - Problem statement, agent framework concept, GSD vs BMAD, and skeptics arc slides
- [ ] **Phase 6: Companion Document** - Standalone markdown reference with expanded content and advanced features

## Phase Details

### Phase 1: Foundation & Setup
**Goal**: Project skeleton and language policies are established so all subsequent content phases build on a consistent foundation
**Depends on**: Nothing (first phase)
**Requirements**: SLIDE-01, SLIDE-05
**Success Criteria** (what must be TRUE):
  1. A Marp-compatible slide deck file exists with correct front matter, inline CSS styling, and section divider templates ready for content
  2. A Swedish/English terminology reference list exists defining which GSD terms stay in English (phases, roadmap, agents, etc.)
  3. The companion document has a structured outline with section placeholders matching the presentation arc
**Plans:** 1 plan

Plans:
- [x] 01-01-PLAN.md — Project skeleton: Marp slide deck, terminology reference, companion outline

### Phase 2: Core Payload — On-Ramp
**Goal**: Audience can see exactly how to start using GSD with zero-friction entry points and understand the graduated complexity path from simple to full workflow
**Depends on**: Phase 1
**Requirements**: SLIDE-03, SLIDE-04, PRAC-01, PRAC-02, PRAC-03
**Success Criteria** (what must be TRUE):
  1. The command spectrum visual clearly shows the progression from `/gsd-fast` → `/gsd-quick` → `/gsd-do` → full workflow with when-to-use guidance for each level
  2. Realistic terminal examples show actual command invocations with plausible output for at least `/gsd-fast` and `/gsd-quick` scenarios
  3. Getting started content covers installation and running a first command with near-zero setup overhead
  4. The graduated complexity narrative makes a convincing case that you can start light today and scale up as trust grows
**Plans:** 1 plan

Plans:
- [x] 02-01-PLAN.md — Section 4 slides: command spectrum, terminal examples, installation, gateway bridge

### Phase 3: Core Payload — Full Workflow
**Goal**: Audience understands the complete GSD lifecycle from project initialization through verification, including how GSD maintains project memory across sessions
**Depends on**: Phase 2
**Requirements**: DEEP-01, DEEP-02, DEEP-03, DEEP-04, DEEP-05, DEEP-06, PRAC-08
**Success Criteria** (what must be TRUE):
  1. The core workflow (new-project → discuss → plan → execute → verify) is explained with clear transitions, and composable flags (`--discuss`, `--research`, `--full`) are shown as the mechanism to tune assistance level
  2. Agent architecture is presented showing how specialized agents collaborate through the orchestrator pattern without overwhelming the audience with all 18 agents
  3. Planning artifacts (`.planning/` directory, ROADMAP.md, STATE.md) are shown with realistic simplified examples that feel authentic
  4. Persistent project memory (STATE.md, `/gsd-resume-work`, `/gsd-progress`) and project lifecycle management (starting, switching, cleaning up projects) are explained as key differentiators
  5. Goal-backward verification ("task completion ≠ goal achievement") is clearly distinguished from simple task checking
**Plans:** 2 plans

Plans:
- [x] 03-01-PLAN.md — Section 3 mental model slides (agent architecture, waves, .planning/ directory)
- [x] 03-02-PLAN.md — Section 5 full lifecycle slides (workflow, artifacts, memory, verification) + visual verification

### Phase 4: Scenarios & Best Practices
**Goal**: Audience can map their real-world situations to specific GSD commands, with clear guidance on mindset shifts, prompt crafting, anti-patterns, and a concrete next step to take Monday morning
**Depends on**: Phase 3
**Requirements**: PRAC-04, SCEN-01, SCEN-02, SCEN-03, SCEN-04, BEST-01, BEST-02, BEST-03, BEST-04, BEST-05
**Success Criteria** (what must be TRUE):
  1. A decision tree or flowchart maps common developer scenarios to specific GSD commands — the slide people photograph
  2. Greenfield, brownfield, and quick fix/debugging scenarios each show distinct workflows with appropriate entry points (`/gsd-new-project`, `/gsd-map-codebase`, `/gsd-fast`, `/gsd-debug`)
  3. Mental model shifts (think outcomes not steps, you decide / AI executes) and prompt crafting guidance are stated as actionable principles
  4. Anti-patterns (vague prompts, skipping verification, micro-management) and escape hatches (when NOT to use agents) are presented with equal weight — honesty builds credibility
  5. A concrete "Start Monday" challenge gives the audience a zero-friction first step they can take immediately after the presentation
**Plans:** 2 plans

Plans:
- [ ] 04-01-PLAN.md — Section 6: Decision tree & scenarios (greenfield, brownfield, quick fix)
- [ ] 04-02-PLAN.md — Sections 7-8: Best practices, anti-patterns, escape hatches & Start Monday

### Phase 5: Framing — Intro & Landscape
**Goal**: The presentation opens with a compelling problem statement and positions GSD within the AI agent landscape, earning permission to go deep before the technical content begins
**Depends on**: Phase 4
**Requirements**: SLIDE-02, CTXT-01, CTXT-02, CTXT-03, CTXT-04
**Success Criteria** (what must be TRUE):
  1. The problem statement articulates why agent frameworks exist (context loss, inconsistency, no verification) in terms developers feel personally
  2. "What is an AI agent framework" (LLM + instructions + tools + memory) gives the audience shared vocabulary before the GSD deep-dive
  3. The GSD vs BMAD comparison highlights workflow-centric vs persona-based approaches concisely (≤3 slides) without becoming a comparison trap
  4. The skeptics-to-practitioners narrative arc addresses "am I being replaced?" head-on in the opening minutes and positions AI as collaboration, not replacement
  5. The complete slide deck has coherent section structure and content volume appropriate for ~60 minutes of presentation
**Plans**: TBD

### Phase 6: Companion Document
**Goal**: A standalone markdown reference document expands on the presentation with full command details, advanced features, and detailed scenarios — usable without a presenter
**Depends on**: Phase 5
**Requirements**: COMP-01, COMP-02, COMP-03, PRAC-05, PRAC-06, PRAC-07
**Success Criteria** (what must be TRUE):
  1. The companion document covers all presentation topics with deeper detail, expanded examples, and full command reference beyond what the slides provide
  2. Advanced features — phase insertion (`/gsd-insert-phase`), cross-AI review (`/gsd-review`), and autonomous mode (`/gsd-autonomous`) — are explained with usage context and examples
  3. A developer who has NOT attended the presentation can read this document and understand GSD well enough to start using it
  4. The document is wiki/repo-friendly markdown that renders correctly without special tooling
**Plans**: TBD

## Progress

**Execution Order:**
Phases execute in numeric order: 1 → 2 → 3 → 4 → 5 → 6

| Phase | Plans Complete | Status | Completed |
|-------|----------------|--------|-----------|
| 1. Foundation & Setup | 0/1 | Not started | - |
| 2. Core Payload — On-Ramp | 0/0 | Not started | - |
| 3. Core Payload — Full Workflow | 0/0 | Not started | - |
| 4. Scenarios & Best Practices | 0/0 | Not started | - |
| 5. Framing — Intro & Landscape | 0/0 | Not started | - |
| 6. Companion Document | 0/0 | Not started | - |
