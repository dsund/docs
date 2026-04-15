# Project Research Summary

**Project:** GSD-presentation (AI Agent Framework Education)
**Domain:** Developer education — 45-minute presentation + companion markdown document
**Researched:** 2025-07-17
**Confidence:** HIGH

## Executive Summary

This project is a **developer education presentation**, not a software product. The deliverables are a Marp slide deck (~45 min) and a companion markdown reference document, both in Swedish with English technical terms preserved. The subject matter is the GSD (Get Shit Done) AI agent framework, presented to a mixed audience ranging from AI-skeptics to early adopters. Research confirms that Marp CLI is the right (and only necessary) tooling — this is a content authoring project with zero build complexity.

The recommended approach, validated across all four research dimensions, is to build around a **"Ladder" narrative arc** of progressive complexity. The presentation hooks the audience with shared pain (unstructured AI assistance plateaus), converts skeptics through a zero-friction on-ramp (`/gsd-fast` in 30 seconds), then earns permission to show the full GSD lifecycle. The command spectrum (`/gsd-fast` → `/gsd-quick` → `/gsd-do` → `/gsd-new-project`) is both the key pedagogical device and GSD's genuine UX differentiator. Content should be built **payload-first**: the On-Ramp and Full Workflow sections first, framing sections (intro, landscape) last — because you can't write a sharp hook until you know what it's setting up.

The primary risks are **tone and trust**, not technology. Five critical pitfalls all center on credibility: showing a "magic show" without failure modes, ignoring the "am I being replaced?" fear, skipping the on-ramp to show the impressive-but-overwhelming full workflow first, enthusiast bias in framing, and hiding what goes wrong. Every one of these is preventable through deliberate content structure — which the architecture research has already mapped in detail. The presentation must educate, not evangelize; demonstrate, not sell; and end with an action close ("do this Monday"), not a summary.

## Key Findings

### Recommended Stack

Marp CLI (v4.3.1) is the sole production dependency. It converts markdown to PDF/HTML/PPTX with zero build pipeline. The project needs VS Code (with Marp extension for live preview), Git for versioning, and Node.js ≥18 as Marp's runtime. No other tooling is justified — reveal.js and Slidev were evaluated and rejected as overengineered for a content-focused single presentation. Inline CSS overrides in the markdown file handle all styling needs; a full custom Marp theme is unnecessary for one deck.

**Core technologies:**
- **Marp CLI**: Slide generation (markdown → PDF/HTML) — markdown-native, Git-friendly, `marp slides.md --pdf` and done
- **VS Code + Marp extension**: Authoring with live preview — team already uses VS Code
- **Standard Markdown**: Companion reference document — no special tooling needed to read

**Content domain stack** (what the presentation teaches about):
- **GSD framework**: Primary subject — orchestrator + 18 specialized agents, graduated entry points
- **BMAD**: Comparison point only — persona-based approach as counterpoint to GSD's workflow-based approach
- **Aider, Claude Code, Cursor, Copilot Agent**: Brief landscape mentions (1-2 slides total) to position the category

### Expected Features

**Must have (table stakes):**
- Problem statement: why agent frameworks exist (context loss, inconsistency, no verification)
- Shared vocabulary: what an AI agent framework actually is
- GSD core workflow overview: new-project → discuss → plan → execute → verify
- Command spectrum on-ramp: `/gsd-fast` → `/gsd-do` → `/gsd-quick` → `/gsd-new-project`
- Planning artifacts (`.planning/` directory, STATE.md as project memory)
- Practical scenarios: greenfield, brownfield, quick fixes, debugging
- Best practices with anti-patterns and prompt crafting guidance
- Concrete command examples with realistic terminal output
- "Start Monday" action close with zero-friction first step
- Swedish text with English technical terms (svengelska policy)
- Companion markdown document as post-talk reference

**Should have (differentiators — elevate from tool walkthrough to memorable education):**
- Command spectrum as *adoption strategy* visual (the graduated on-ramp)
- "Task completion ≠ Goal achievement" verification philosophy
- Agent specialization vs persona simulation (GSD vs BMAD distinction)
- Composable quality flags (`--discuss`, `--research`, `--full`)
- Skeptic-to-practitioner narrative arc with head-on concern addressing
- Mental model shifts (think in outcomes, you = decisions, AI = execution)
- Escape hatches: when NOT to use agents (builds credibility)

**Defer (companion doc only, not slides):**
- Cross-AI review (`/gsd-review`) — cool but niche
- Autonomous mode (`/gsd-autonomous`) — end-game concept, not introductory
- Phase insertion (`/gsd-insert-phase`) — important but not day-one
- Model profiles — reference material, not presentation material
- Full command catalog (40+ commands) — point to `/gsd-help`

### Architecture Approach

The presentation follows an 8-section "Ladder" arc with strict information dependencies and deliberate attention curve management. Two sections are core: **Section 4 (On-Ramp, 8 min, 18%)** and **Section 5 (Full Workflow, 12 min, 27%)** — together consuming 45% of presentation time. The "how" content (sections 3-6) dominates at 71%, with "why" framing at 18% and "what next" close at 11%. Total slide budget: 38-48 slides.

**Major components:**
1. **Slide deck (Marp markdown)** — 8 sections, ~40 slides, progressive complexity arc with attention resets
2. **Companion document (standard markdown)** — mirrors presentation structure but serves as reference, includes full command catalog and expanded scenarios
3. **Terminology reference** — English/Swedish term list created before slide authoring to ensure consistency

**Key architectural patterns:**
- Progressive disclosure: simplest interaction first, complexity layered on
- Concrete before abstract: show command output, then explain mechanism
- Permission ramp: each section earns right to go deeper
- Decision tree as takeaway: scenario → command mapping (the slide people photograph)
- Payload-first build order: write On-Ramp and Full Workflow before writing the intro

### Critical Pitfalls

1. **The "Magic Show" Effect** — Show realistic flows including iteration and correction, not cherry-picked perfect outputs. Include at least one "here's what went wrong and how to course-correct" example. Frame as collaboration, not button-pressing.

2. **Ignoring "Am I Being Replaced?"** — Address head-on in the first 5 minutes. Position explicitly: AI handles tedious parts, developer makes decisions. Use "du" frequently ("du bestämmer", "du reviewar"). Emphasize understanding code is MORE important with AI, not less.

3. **Skipping the On-Ramp** — The on-ramp section MUST come before the full workflow. Start with `/gsd-fast` (30 seconds, zero overhead). The curious-but-cautious middle (60% of audience) will check out if they see complex phase diagrams before seeing a one-shot command.

4. **Enthusiast's Bias** — Validate skepticism explicitly: "If you're skeptical, good." Use measured, technical language — never "amazing" or "game-changer." Include limitations and "when NOT to use this" content. Let the tool prove itself through demonstration.

5. **Hiding Failure Modes** — Dedicate a section to what happens when AI output is wrong. Teach the correction loop. Frame debugging AI output as a skill, not a tool defect. Set realistic expectations (~80% right, 20% needs adjustment).

## Implications for Roadmap

Based on research, the build order should follow the architecture's "payload first, framing second" principle. Content creation phases map to the presentation's section dependencies, not its linear section order.

### Phase 1: Foundation & Setup
**Rationale:** Terminology consistency (Pitfall 11) must be solved before any content is written. Marp skeleton with theme/styling establishes the visual language all subsequent slides follow. This phase is tiny but prevents rework.
**Delivers:** Marp slide skeleton with front matter, inline CSS styling, section divider templates. Swedish/English terminology reference list. Project file structure (slides.md + companion doc outline).
**Addresses:** Language consistency (table stake), clear slide structure (table stake)
**Avoids:** Pitfall 11 (language inconsistency)

### Phase 2: Core Payload — On-Ramp
**Rationale:** Architecture research is unambiguous: "If this section doesn't land, nothing else matters." This is where skeptics convert. Build and polish first. The command spectrum is the single most memorable GSD concept.
**Delivers:** Slides for Section 4 (On-Ramp, ~8-10 slides): `/gsd-fast` → `/gsd-do` → `/gsd-quick` → teaser of full workflow. Command examples with realistic terminal output. The complexity ladder visual.
**Addresses:** Command spectrum (table stake + differentiator), getting started (table stake), live-looking command examples (table stake)
**Avoids:** Pitfall 3 (skipping on-ramp), Pitfall 1 (magic show — include realistic examples here)

### Phase 3: Core Payload — Full Workflow
**Rationale:** Main content mass. Depends on On-Ramp being done (progressive complexity — audience must see simple before complex). Requires crafting artifact examples (ROADMAP.md, PLAN.md snippets) which take iteration time.
**Delivers:** Slides for Section 5 (Full Workflow, ~10-12 slides): project initialization, phase lifecycle, project memory & continuity. Simplified artifact examples. Lifecycle diagram.
**Addresses:** GSD core workflow overview (table stake), planning artifacts (table stake), persistent project memory (differentiator), verification philosophy (differentiator)
**Avoids:** Pitfall 7 (theory-heavy — balance architecture with practical examples), Pitfall 10 (no verification — make review visible)

### Phase 4: Scenarios & Practices
**Rationale:** Ties On-Ramp + Full Workflow together. Can't write good scenarios without knowing exactly what was covered in phases 2-3. The decision tree (scenario → command) is the takeaway slide people photograph.
**Delivers:** Slides for Section 6 (Scenarios, ~5-6 slides): decision flowchart, greenfield/brownfield/debugging/quick-fix scenarios. Slides for Section 7 (Best Practices, ~3-4 slides): mental model shifts, anti-patterns, prompt crafting guidance. Section 8 (Getting Started, ~2-3 slides): action close.
**Addresses:** Practical scenarios (table stake), best practices (table stake), anti-patterns (differentiator), "Start Monday" challenge (differentiator), escape hatches (differentiator)
**Avoids:** Pitfall 5 (hiding failures — include correction scenario), Pitfall 8 (single use case — show spectrum), Pitfall 9 (prompt crafting afterthought), Pitfall 12 (no action close), Pitfall 13 (ignoring brownfield — lead scenarios with brownfield)

### Phase 5: Framing — Intro, Landscape & Mental Model
**Rationale:** "Writing the opening first is tempting but wrong — you don't know what you're setting up yet." Now that payload is done, the hook and framing can be precisely targeted. Section 3 (Mental Model) is written knowing exactly which concepts sections 4-5 need pre-loaded.
**Delivers:** Slides for Section 1 (Problem, ~4-5 slides), Section 2 (Landscape, ~2-3 slides), Section 3 (Mental Model, ~4-5 slides). GSD vs BMAD comparison table (2-3 slides max). Agent architecture diagram.
**Addresses:** Problem statement (table stake), what is an agent framework (table stake), GSD vs BMAD (table stake), agent specialization vs personas (differentiator), orchestrator pattern (differentiator)
**Avoids:** Pitfall 2 ("Am I being replaced?" — address in Section 1), Pitfall 4 (enthusiast bias — measured opening tone), Pitfall 6 (comparison trap — max 2-3 slides)

### Phase 6: Companion Document
**Rationale:** Expand slides into full reference AFTER presentation narrative is locked. The companion doc serves a different purpose (reference vs narrative) and has different structure (full command catalog, expanded scenarios, BMAD comparison appendix).
**Delivers:** Complete markdown companion document: all sections expanded, full command reference table, detailed scenarios with terminal transcripts, terminology glossary, links and resources.
**Addresses:** Companion document (table stake), deferred content (command catalog, detailed brownfield guide)
**Avoids:** N/A — by this phase the narrative is settled

### Phase 7: Review & Polish
**Rationale:** The meta-pitfall: "the presenter has already completed their own adoption journey." Final review by someone who HASN'T used GSD. Attention curve check. Terminology consistency audit. Time-run the slide count.
**Delivers:** Reviewed, polished slide deck and companion document. Verified terminology consistency. Validated time budget against slide count. PDF/HTML output generated via Marp CLI.
**Addresses:** All minor pitfalls (language, attention levels, completeness)
**Avoids:** Pitfall 14 (one technical level), Pitfall 15 (not acknowledging AI limits), meta-pitfall (presenter's blind spot)

### Phase Ordering Rationale

- **Phases 2-3 before 5** because the Ladder arc's core insight is progressive complexity — you must know your payload before you can write a hook that sets it up. This directly follows the architecture research's build order recommendation.
- **Phase 1 first** because terminology inconsistency is a minor pitfall that causes rework if not solved upfront. A 30-minute investment saves hours of find-and-replace later.
- **Phase 4 after 2-3** because scenarios and best practices reference both the on-ramp and full workflow — they're the synthesis layer.
- **Phase 6 after 5** because the companion document expands the slides, so the slides must be stable first.
- **Phase 7 last** because review requires complete content and benefits from fresh eyes after a gap.

### Research Flags

Phases likely needing deeper research during planning:
- **Phase 3 (Full Workflow):** Artifact examples (ROADMAP.md, PLAN.md snippets) need to be realistic but simplified. May need `/gsd-research-phase` to craft good representative samples.
- **Phase 5 (Framing):** The GSD vs BMAD comparison needs validation — BMAD details are MEDIUM confidence and may have evolved. Verify before presentation delivery.

Phases with standard patterns (skip research):
- **Phase 1 (Foundation):** Marp setup is well-documented. Terminology reference is straightforward.
- **Phase 2 (On-Ramp):** GSD command spectrum is HIGH confidence from primary source analysis.
- **Phase 4 (Scenarios):** Pedagogical patterns are well-established; scenarios follow directly from content already built.
- **Phase 7 (Review):** Standard review checklist, no domain research needed.

## Confidence Assessment

| Area | Confidence | Notes |
|------|------------|-------|
| Stack | **HIGH** | Marp versions verified via npm registry. Minimal tooling = minimal risk. |
| Features | **HIGH** | GSD v1.29.0 internals analyzed directly. Feature landscape comprehensively mapped with clear table stakes / differentiator / anti-feature categorization. |
| Architecture | **HIGH** | Presentation architecture patterns are well-established pedagogy. 8-section structure with time budgets, dependency graph, and attention curve is thoroughly designed. |
| Pitfalls | **HIGH** | 15 pitfalls identified across 3 severity tiers. Developer education and AI tool adoption patterns are well-documented domains. GSD-specific manifestations are somewhat inferred but directionally sound. |

**Overall confidence:** HIGH

### Gaps to Address

- **BMAD comparison accuracy:** MEDIUM confidence. Core concepts are directionally correct but specific BMAD features may have evolved since training cutoff. **Action:** Validate BMAD details against current documentation before Phase 5 slide creation.
- **AI agent landscape currency:** Tools like Claude Code, Cursor, and Copilot Agent Mode evolve rapidly. Brief mentions in the landscape slide may need updating. **Action:** Quick check of current state during Phase 5 planning.
- **Realistic artifact examples:** The presentation needs simplified but authentic ROADMAP.md and PLAN.md snippets. These don't exist yet and need to be crafted to feel real without being overwhelming. **Action:** Craft during Phase 3 with possible research spike.
- **Time budget validation:** The 8-section / 45-minute allocation is well-reasoned but theoretical. Actual slide pacing can only be validated by time-running the finished deck. **Action:** Built into Phase 7 review.

## Sources

### Primary (HIGH confidence)
- GSD Framework v1.29.0 — full workflow definitions, 18 agent definitions, template system, CLI tooling, help reference (40+ commands)
- npm registry — Marp CLI v4.3.1 (2026-03-16), Marp Core v4.3.0, reveal.js v6.0.1, Slidev v52.14.2

### Secondary (MEDIUM confidence)
- BMAD Method — persona-based AI development framework. Core concepts verified through multiple training sources; specific features may have evolved.
- AI agent landscape (Claude Code, Cursor, Copilot Agent, Aider, Windsurf) — training data 2024-2025, rapidly evolving field.
- AI tool adoption patterns — community patterns from developer advocacy research.

### Tertiary (LOW confidence)
- None — all research areas had at least MEDIUM confidence sources.

---
*Research completed: 2025-07-17*
*Ready for roadmap: yes*
