# Phase 3: Core Payload — Full Workflow - Context

**Gathered:** 2026-04-15
**Status:** Ready for planning

<domain>
## Phase Boundary

Deliver the "Hela livscykeln" (Section 5) and "Hur fungerar det?" (Section 3) slides: explaining the complete GSD lifecycle from project initialization through verification, agent architecture, planning artifacts, persistent project memory, and goal-backward verification. The audience leaves understanding how GSD works end-to-end — not just the quick commands from Section 4, but the full machinery behind serious projects.

</domain>

<decisions>
## Implementation Decisions

### Workflow Visualization
- **D-01:** Agent's Discretion: Choose the best narrative approach for the 5-step lifecycle (new-project → discuss → plan → execute → verify). Options include step-by-step build-up, single overview + deep-dives, or linear pipeline. Pick what works best for a 60-min presentation flow.
- **D-02:** Agent's Discretion: Composable flags (--discuss, --research, --full) placement — integrate into workflow steps, show on dedicated slide, or reference back to Phase 2's /gsd-quick example. Pick the least repetitive approach.
- **D-03:** Agent's Discretion: Mix of conceptual diagrams and terminal examples. Phase 2 was terminal-heavy; this section can balance conceptual understanding with selective terminal output for key steps.

### Agent Architecture Depth
- **D-04:** Agent's Discretion: How many of the 18 specialized agents to show. Simplified orchestrator pattern is key — show that agents collaborate, not that there are exactly 18 of them. Avoid overwhelming the audience.
- **D-05:** Agent's Discretion: Wave-based execution presentation — show the concept of parallel waves without implementation details.

### Artifact Examples
- **D-06:** Agent's Discretion: How to present .planning/ directory files (ROADMAP.md, STATE.md, PLAN.md). Realistic but simplified excerpts preferred — the audience should see what these files look like without reading full content. Per STATE.md blocker: "Artifact examples need to be realistic but simplified."
- **D-07:** Agent's Discretion: Whether to show a file tree or inline code snippets or both.

### Persistent Memory & Project Lifecycle
- **D-08:** Agent's Discretion: How to convey that GSD remembers project state across sessions (STATE.md, /gsd-resume-work, /gsd-progress). This is a key differentiator vs ad-hoc AI usage.
- **D-09:** Agent's Discretion: Project lifecycle management (starting, switching, cleaning up projects) — keep minimal, mention capabilities without deep-diving.

### Verification Narrative
- **D-10:** Agent's Discretion: How to convey "task completion ≠ goal achievement." This is GSD's strongest philosophical point — make it memorable. Options: comparison slide, concrete example, before/after visualization.
- **D-11:** Agent's Discretion: How many verification levels to show (4 levels exist: self-check, automated, goal-backward, human UAT). Showing all 4 may be too much — pick the most impactful.

### Slide Density & Narrative Arc (carried from Phase 2)
- **D-12:** Spacious layout — one idea per slide (per Phase 2 D-12)
- **D-13:** Section divider style: centered title + hr (per Phase 1 D-04)
- **D-14:** Terminal examples: bash fence, $ prompt, compact output (per Phase 2 D-06/D-08)
- **D-15:** Copilot-only references, no Claude Code (per Phase 2 D-10)
- **D-16:** Swedish text with English technical terms per TERMINOLOGY.md

### Agent's Discretion
- Workflow visualization approach (overview vs progressive reveal vs pipeline) — D-01
- Composable flags placement and depth — D-02
- Conceptual vs terminal example balance — D-03
- Agent architecture simplification level — D-04, D-05
- Artifact example format and depth — D-06, D-07
- Persistent memory presentation — D-08
- Project lifecycle depth — D-09
- Verification narrative style — D-10, D-11

</decisions>

<canonical_refs>
## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### Project Definition
- `.planning/PROJECT.md` — Project vision, constraints (Marp format, ~60 min, svenska + engelska), key decisions
- `.planning/REQUIREMENTS.md` — Full requirement list; Phase 3 covers DEEP-01, DEEP-02, DEEP-03, DEEP-04, DEEP-05, DEEP-06, PRAC-08
- `.planning/ROADMAP.md` — Phase details, success criteria, build order rationale

### Prior Phase Context
- `.planning/phases/01-foundation-setup/01-CONTEXT.md` — Phase 1 decisions: 16:9, default theme, page numbers, section divider style
- `.planning/phases/02-core-payload-on-ramp/02-CONTEXT.md` — Phase 2 decisions: spacious layout, terminal style, Copilot-only, gateway bridge pattern
- `.planning/phases/02-core-payload-on-ramp/02-01-SUMMARY.md` — What Phase 2 built (8 slides, command spectrum, terminal examples)

### Content Sources
- `slides.md` — Current slide deck with Section 3 and Section 5 placeholders where Phase 3 content goes
- `TERMINOLOGY.md` — Swedish/English term policy; all slides must follow this
- `companion.md` — Companion document outline; relevant sections map to this phase

</canonical_refs>

<code_context>
## Existing Code Insights

### Reusable Assets
- `slides.md` — Marp skeleton with Section 3 ("Hur fungerar det?") and Section 5 ("Hela livscykeln") placeholders ready for content
- Phase 2's terminal example pattern — bash fence, $ prompt, 3-5 lines, relatable scenario
- Phase 2's ASCII art pattern — plain code fence (no language specifier) for diagrams

### Established Patterns
- Section dividers: `<!-- _class: divider -->` with `<hr>` tag and centered h1
- Content slides: standard `---` separator, no class directives, paginated
- Code blocks: 0.85em font size with border-radius 4px
- One idea per slide — spacious layout for back-of-room readability

### Integration Points
- Section 3 content inserts after `<!-- Section 3: GSD Mental Model — slides added by Phase 3 -->` comment
- Section 5 content inserts after `<!-- Section 5: Full Workflow — slides added by Phase 3 -->` comment
- Phase 2's gateway bridge slide ("Men om uppgiften är större?") leads directly into Section 5 — the narrative handoff must feel seamless

</code_context>

<specifics>
## Specific Ideas

- The Phase 2 gateway bridge ("Men om uppgiften är större? Då behöver du hela workflow:en.") creates a narrative expectation — Section 5 must deliver on that promise immediately
- Artifact examples should feel authentic — use GSD's own file formats (ROADMAP.md, STATE.md) as realistic content, not generic placeholders
- "Task completion ≠ goal achievement" is the philosophical core of GSD's value proposition — this concept should be the most memorable moment in the section
- Phase 2 already teased /gsd-new-project in the Full Workflow slide — Section 5 can reference that and go deeper

</specifics>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope

</deferred>

---

*Phase: 03-core-payload-full-workflow*
*Context gathered: 2026-04-15*
