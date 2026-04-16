# Phase 6: Companion Document - Context

**Gathered:** 2026-04-16
**Status:** Ready for planning

<domain>
## Phase Boundary

Deliver a standalone markdown reference document (companion.md) that expands on the presentation with full command details, advanced features (phase insertion, cross-AI review, autonomous mode), and detailed scenarios. A developer who has NOT attended the presentation can read this document and understand GSD well enough to start using it. The document is wiki/repo-friendly markdown.

</domain>

<decisions>
## Implementation Decisions

### Document Depth & Voice
- **D-01:** Comprehensive guide — explain concepts + show examples + provide context. The reader should understand WHY, not just HOW
- **D-02:** Utbildande, approachable tone matching the slides — same "svengelska" voice as the presentation
- **D-03:** Moderate expansion on slides — key topics get deeper treatment, simpler topics stay concise. Not every slide needs a companion paragraph
- **D-04:** No length target — let the content determine the length. Focus on quality, not word count

### Relationship to Slides
- **D-05:** Keep the existing companion.md outline structure (7 sections + appendix from Phase 1) — it maps well to the presentation arc
- **D-06:** Standalone with slide echoes — the companion stands on its own but may reference "som vi såg i presentationen" occasionally. No required cross-reading

### Advanced Features Coverage
- **D-07:** Scenario-driven — each advanced feature gets a realistic scenario showing when and how to use it (e.g., "Du är mitt i Phase 3 och inser att du behöver ett API först...")
- **D-08:** Place advanced features in their natural sections — phase insertion in "Full Workflow" (Section 4), cross-AI review in "Best Practices" (Section 6), autonomous mode in its own subsection. Not grouped in a separate "Advanced" section

### Command Reference Format
- **D-09:** Curated command table — cover the most important 10–15 commands with Command | Description | När? columns. Quality over completeness
- **D-10:** Include `.planning/` file structure overview — file tree + brief explanation of each file's role
- **D-11:** Table format for command reference — scannable, quick lookup

### Slide Density & Style (carried from Phases 1–5)
- **D-12:** Swedish text with English technical terms per TERMINOLOGY.md (all phases)
- **D-13:** Copilot-only references, no Claude Code (Phase 2 D-10)
- **D-14:** Generic, relatable developer scenarios (Phase 4 D-07)

### Agent's Discretion
- Which 10–15 commands to include in the curated reference table
- Level of detail per section — where to expand heavily vs stay concise
- How to structure the `.planning/` file tree overview
- Terminal example format within the companion (code blocks with realistic output)
- Autonomous mode subsection placement within the document

</decisions>

<canonical_refs>
## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### Project Definition
- `.planning/PROJECT.md` — Project vision, constraints (Marp format, ~60 min, svenska + engelska), key decisions
- `.planning/REQUIREMENTS.md` — Full requirement list; Phase 6 covers COMP-01, COMP-02, COMP-03, PRAC-05, PRAC-06, PRAC-07
- `.planning/ROADMAP.md` — Phase details, success criteria, build order rationale

### Prior Phase Context
- `.planning/phases/01-foundation-setup/01-CONTEXT.md` — Phase 1 decisions: 16:9, default theme, page numbers, section divider style
- `.planning/phases/02-core-payload-on-ramp/02-CONTEXT.md` — Phase 2 decisions: spacious layout, terminal style, ASCII art, Copilot-only, gateway bridge
- `.planning/phases/03-core-payload-full-workflow/03-CONTEXT.md` — Phase 3 decisions: agent discretion on visualization, carried style patterns
- `.planning/phases/04-scenarios-best-practices/04-CONTEXT.md` — Phase 4 decisions: decision tree all-English, generic scenarios, concrete prompt examples
- `.planning/phases/05-framing-intro-landscape/05-CONTEXT.md` — Phase 5 decisions: problem statement, collaboration reframe, balanced BMAD comparison

### Content Sources
- `companion.md` — Existing outline (7 sections + appendix) established in Phase 1. This is the file being expanded
- `slides.md` — Complete slide deck with all 8 sections of content. The companion expands on this
- `TERMINOLOGY.md` — Swedish/English term policy; companion must follow this

</canonical_refs>

<code_context>
## Existing Code Insights

### Reusable Assets
- `companion.md` — Outline with 7 sections + appendix already structured: Introduktion, GSD i korthet, Kom igång, Full Workflow, Scenarion, Best Practices, Referens, Appendix (GSD vs BMAD)
- `slides.md` — Full presentation content across 8 sections with terminal examples, ASCII diagrams, decision trees, and conceptual explanations that can be expanded
- `TERMINOLOGY.md` — Authoritative term list for consistent language

### Established Patterns
- Swedish prose with English technical terms (TERMINOLOGY.md)
- Terminal examples: bash fence, `$` prompt, compact output (from slides)
- ASCII art in code blocks for diagrams (from slides)
- Generic developer scenarios: REST API, legacy refactor, etc.
- Copilot-only references throughout

### Integration Points
- `companion.md` is the target file — expand the existing outline placeholders with full content
- Advanced features (PRAC-05, PRAC-06, PRAC-07) are NEW content not in slides — they integrate into existing sections rather than creating new ones
- Section 7 "Referens" gets the curated command table and `.planning/` file structure
- Appendix "GSD vs BMAD" expands on the philosophy comparison from Phase 5's slides

</code_context>

<specifics>
## Specific Ideas

- The companion should feel like the "textbook" to the slides' "lecture notes" — same voice, more depth on key topics
- Advanced features use scenario-driven explanations: realistic developer situations that motivate WHY you'd use `/gsd-insert-phase`, `/gsd-review`, or `/gsd-autonomous`
- The command reference table is a practical quick-lookup tool — Command | Description | När? — not an exhaustive reference
- "som vi såg i presentationen" echoes are allowed but the document must make sense without them

</specifics>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope

</deferred>

---

*Phase: 06-companion-document*
*Context gathered: 2026-04-16*
