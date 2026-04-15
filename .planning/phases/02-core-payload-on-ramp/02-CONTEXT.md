# Phase 2: Core Payload — On-Ramp - Context

**Gathered:** 2026-04-15
**Status:** Ready for planning

<domain>
## Phase Boundary

Deliver the "Börja enkelt" (Section 4) slides: a command spectrum visual showing the `/gsd-fast` → `/gsd-quick` → `/gsd-do` → full workflow progression, realistic terminal examples for each level, step-by-step installation guide, and graduated complexity narrative. The audience leaves this section thinking "I could start using this today."

</domain>

<decisions>
## Implementation Decisions

### Command Spectrum Visual
- **D-01:** Horizontal left-to-right progression — a "complexity dial" showing the path from simple to full workflow
- **D-02:** ASCII art in a code block — pure markdown, terminal-native feel, works everywhere
- **D-03:** Medium detail per level — command name + short description + "use when" hint
- **D-04:** Single spectrum slide only — punchy overview; deeper details come in follow-up slides per command

### Terminal Examples
- **D-05:** Relatable developer scenarios — "fix a bug", "add a feature" — things the audience has done themselves
- **D-06:** Compact format — 3-5 lines per example: prompt + command + key output line. Readable from the back of the room
- **D-07:** One terminal example per spectrum level — `/gsd-fast`, `/gsd-quick`, `/gsd-do`, plus a full workflow tease (4 examples total)
- **D-08:** Standard `$` prompt style — clean and universal

### Getting Started / Installation
- **D-09:** Step-by-step installation — prerequisites, install command, verify, first command (2+ slides)
- **D-10:** Copilot CLI only — show GitHub Copilot Extensions install path, no Claude Code
- **D-11:** Agent's Discretion: Installation slides ordering — before or after command spectrum (pick what flows best narratively)

### Slide Density & Narrative Arc
- **D-12:** Spacious layout — one idea per slide, more slides, easy to follow from the back of the room
- **D-13:** Agent's Discretion: Slide count for this section (target comfortable pacing within ~60 min total across 8 sections)
- **D-14:** Section ends with a "gateway" tease — "but what if your task is bigger? That's the full workflow..." — bridges to Phase 3's "Hela livscykeln" section

### Agent's Discretion
- Installation slide ordering (before or after command spectrum) — D-11
- Total slide count for Section 4 — D-13

</decisions>

<canonical_refs>
## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### Project Definition
- `.planning/PROJECT.md` — Project vision, constraints (Marp format, ~60 min, svenska + engelska), key decisions
- `.planning/REQUIREMENTS.md` — Full requirement list; Phase 2 covers SLIDE-03, SLIDE-04, PRAC-01, PRAC-02, PRAC-03
- `.planning/ROADMAP.md` — Phase details, success criteria, build order rationale

### Phase 1 Foundation
- `slides.md` — Marp skeleton with Section 4 "Börja enkelt" placeholder (line 92-97) where content goes
- `TERMINOLOGY.md` — Swedish/English term policy; all slides must follow this
- `companion.md` — Companion document outline; Section 3 "Kom igång — On-Ramp" maps to this phase
- `.planning/phases/01-foundation-setup/01-CONTEXT.md` — Phase 1 decisions: 16:9, default theme, page numbers only, section divider style

</canonical_refs>

<code_context>
## Existing Code Insights

### Reusable Assets
- `slides.md` — Marp skeleton with inline CSS for `.divider`, `.lead`, and code block styling already in place
- `TERMINOLOGY.md` — Authoritative term list for consistent language across all slides

### Established Patterns
- Section dividers use `<!-- _class: divider -->` with `<hr>` tag and centered `h1` (D-04 from Phase 1)
- Content slides use standard Marp `---` separators with default pagination
- Code blocks styled at `0.85em` with `border-radius: 4px`

### Integration Points
- New content inserts after `<!-- Section 4: The On-Ramp — slides added by Phase 2 -->` comment in slides.md (line 96)
- Companion document Section 3 "Kom igång — On-Ramp" will be expanded in Phase 6 based on slide content created here

</code_context>

<specifics>
## Specific Ideas

- The command spectrum slide is intended to be the "slide people photograph" — the one visual takeaway from this section
- Terminal examples should feel authentic — real developer scenarios, not contrived demos
- The section should build confidence: "this is easy to start, and it scales with you"

</specifics>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope

</deferred>

---

*Phase: 02-core-payload-on-ramp*
*Context gathered: 2026-04-15*
