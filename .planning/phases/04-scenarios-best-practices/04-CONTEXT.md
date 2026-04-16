# Phase 4: Scenarios & Best Practices - Context

**Gathered:** 2026-04-16
**Status:** Ready for planning

<domain>
## Phase Boundary

Deliver Sections 6–8 of the slide deck: real-world scenarios mapping developer situations to GSD commands (Section 6: "I din vardag"), mindset shifts and best practices including prompt crafting and anti-patterns (Section 7: "Tänk så här"), and a concrete "Start Monday" call-to-action (Section 8: "Börja på måndag"). The decision tree slide is the "slide people photograph" for this phase.

</domain>

<decisions>
## Implementation Decisions

### Decision Tree (SCEN-04)
- **D-01:** All-English for the decision tree content — keeps it universal, terse, and "photographable" (exception to the Swedish pattern used elsewhere in the deck)
- **D-02:** Include specialist commands beyond the command spectrum — `/gsd-debug`, `/gsd-map-codebase`, `/gsd-insert-phase` etc., not just the 4 main levels
- **D-03:** Agent's Discretion: Visual format (ASCII flowchart vs table vs Q&A list) — pick what works best for readability on a slide
- **D-04:** Agent's Discretion: Whether to fit on one dense slide or split across multiple — depends on how many commands need to fit

### Scenarios (SCEN-01, SCEN-02, SCEN-03)
- **D-05:** Agent's Discretion: Scenario structure format — command highlights, before/after contrast, or mini-walkthrough. Pick what fits best within a 60-min presentation
- **D-06:** Agent's Discretion: Relative depth per scenario — equal weight or emphasize the most relevant one based on audience needs
- **D-07:** Generic developer scenarios — "REST API", "legacy refactor", relatable to any developer

### Best Practices & Anti-Patterns (BEST-01, BEST-02, BEST-03, BEST-04)
- **D-08:** Agent's Discretion: Presentation format — side-by-side do/don't, principles-first, or anti-pattern gallery. Pick what's most impactful
- **D-09:** Agent's Discretion: Escape hatches (when NOT to use agents) depth — per success criteria, should have real weight to build credibility
- **D-10:** Concrete prompt examples for prompt crafting guidance — show actual good/bad prompts (e.g., "Fix the bug" vs "The login form returns 401 when valid credentials are submitted")

### "Start Monday" Challenge (BEST-05)
- **D-11:** Agent's Discretion: The specific call-to-action and whether it's a single action or tiered for different comfort levels. Pick the most compelling close

### Slide Density & Style (carried from Phases 1–3)
- **D-12:** Spacious layout — one idea per slide (Phase 2 D-12)
- **D-13:** Section dividers: centered h1 + hr (Phase 1 D-04)
- **D-14:** Terminal examples: bash fence, $ prompt, compact output (Phase 2 D-06/D-08)
- **D-15:** ASCII art in code blocks for diagrams (Phase 2 D-02)
- **D-16:** Copilot-only references, no Claude Code (Phase 2 D-10)
- **D-17:** Swedish text with English technical terms per TERMINOLOGY.md (except decision tree — see D-01)

### Agent's Discretion
- Decision tree visual format and slide count — D-03, D-04
- Scenario structure, depth balance, and format — D-05, D-06
- Best practices presentation style — D-08
- Escape hatches weight — D-09
- "Start Monday" challenge format and content — D-11

</decisions>

<canonical_refs>
## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### Project Definition
- `.planning/PROJECT.md` — Project vision, constraints (Marp format, ~60 min, svenska + engelska), key decisions
- `.planning/REQUIREMENTS.md` — Full requirement list; Phase 4 covers PRAC-04, SCEN-01–04, BEST-01–05
- `.planning/ROADMAP.md` — Phase details, success criteria, build order rationale

### Prior Phase Context
- `.planning/phases/01-foundation-setup/01-CONTEXT.md` — Phase 1 decisions: 16:9, default theme, page numbers, section divider style
- `.planning/phases/02-core-payload-on-ramp/02-CONTEXT.md` — Phase 2 decisions: spacious layout, terminal style, ASCII art, Copilot-only, gateway bridge
- `.planning/phases/03-core-payload-full-workflow/03-CONTEXT.md` — Phase 3 decisions: agent discretion on visualization approaches, carried style patterns

### Content Sources
- `slides.md` — Current slide deck with Section 6, 7, 8 placeholders where Phase 4 content goes
- `TERMINOLOGY.md` — Swedish/English term policy; all slides must follow this (except decision tree per D-01)
- `companion.md` — Companion document outline; Sections 5 and 6 map to this phase's content

</canonical_refs>

<code_context>
## Existing Code Insights

### Reusable Assets
- `slides.md` — Marp skeleton with Section 6 ("I din vardag"), Section 7 ("Tänk så här"), Section 8 ("Börja på måndag") placeholders ready for content
- Phase 2's command spectrum ASCII art pattern — can be adapted for the decision tree
- Phase 3's wave diagram and goal-backward verification ASCII — established the visual vocabulary for complex concepts
- Phase 2's terminal example pattern — bash fence, $ prompt, 3-5 lines

### Established Patterns
- Section dividers: `<!-- _class: divider -->` with `<hr>` tag and centered h1
- Content slides: standard `---` separator, no class directives, paginated
- Code blocks: 0.85em font size with border-radius 4px
- One idea per slide — spacious layout
- Gateway bridge pattern: section ends with a tease for the next section

### Integration Points
- Section 6 content inserts after `<!-- Section 6: Scenarios — slides added by Phase 4 -->` comment in slides.md (line 468)
- Section 7 content inserts after `<!-- Section 7: Best Practices — slides added by Phase 4 -->` comment in slides.md (line 478)
- Section 8 content inserts after `<!-- Section 8: Getting Started — slides added by Phase 4 -->` comment in slides.md (line 489)
- Phase 5 (Intro & Landscape) comes after this — Phase 4 closes the practical content before the framing sections are backfilled

</code_context>

<specifics>
## Specific Ideas

- The decision tree is the "slide people photograph" for this section — it should be visually memorable and self-contained
- Decision tree uses all-English for universality, unlike the rest of the deck
- Prompt crafting examples should show concrete good/bad prompts — actionable, not theoretical
- Scenarios should use generic developer situations everyone can relate to (REST API, legacy refactor, etc.)

</specifics>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope

</deferred>

---

*Phase: 04-scenarios-best-practices*
*Context gathered: 2026-04-16*
