# Phase 5: Framing — Intro & Landscape - Context

**Gathered:** 2026-04-16
**Status:** Ready for planning

<domain>
## Phase Boundary

Deliver the opening sections of the presentation: Section 1 ("Var är vi idag?") with a compelling problem statement and skeptics-to-practitioners arc, and Section 2 ("Vad finns?") with an "AI agent framework" concept explanation and GSD vs BMAD comparison. The audience leaves these sections understanding WHY agent frameworks exist, WHAT they are, and how GSD compares — earning permission to go deep in the subsequent technical sections.

</domain>

<decisions>
## Implementation Decisions

### Problem Statement (CTXT-01)
- **D-01:** Agent's Discretion: Choose the most compelling approach — developer pain recognition, technical problem list, before/after contrast, or a combination. Pick what opens strongest.
- **D-02:** Agent's Discretion: Slide count and pacing for the problem statement section. Balance impact with brevity.
- **D-03:** Reference typical ChatGPT/Copilot Chat frustrations the audience has lived — "you've pasted the same context into a new chat, re-explained what you're building." Ground the problem in their experience, make it personal and relatable.

### Skeptics Narrative (CTXT-04)
- **D-04:** Positive-first reframing — skip the fear framing ("am I being replaced?"), go straight to AI as collaboration. Don't dwell on negativity; position AI as a teammate from the start.
- **D-05:** Dedicated slide early — the collaboration message appears right after the problem statement, before any GSD-specific content. Sets the tone for everything that follows.
- **D-06:** Agent's Discretion: Choose the best collaboration metaphor — role-based ("du bestämmer, AI utför"), analogy-based (compare to IDE/linter/CI evolution), or concrete output showing what developer vs agent does. Pick what resonates most naturally.

### Framework Comparison (CTXT-03)
- **D-07:** Philosophy contrast, not feature table — workflow-centric (GSD) vs persona-based (BMAD). High-level positioning only, 1–2 slides max.
- **D-08:** GSD and BMAD only — no mention of other frameworks (Cursor rules, Roo Code, aider). Keeps focus tight under the "Vad finns?" section header.
- **D-09:** Balanced presentation — present both frameworks fairly, let the audience see the reasoning behind choosing GSD rather than selling it. Credibility over persuasion.

### Concept Slide (CTXT-02)
- **D-10:** Agent's Discretion: How to explain "AI agent framework" (LLM + instructions + tools + memory). Options: building blocks visual (ASCII diagram), analogy contrast with plain AI ("ChatGPT = brain without memory"), definition + unpack, or combination. Pick what gives shared vocabulary fastest.
- **D-11:** Agent's Discretion: Placement relative to the GSD vs BMAD comparison — define concept first then show examples (deductive), or compare first then generalize (inductive). Pick the better narrative flow.

### Slide Density & Style (carried from Phases 1–4)
- **D-12:** Spacious layout — one idea per slide (Phase 2 D-12)
- **D-13:** Section dividers: centered h1 + hr (Phase 1 D-04)
- **D-14:** Terminal examples: bash fence, $ prompt, compact output (Phase 2 D-06/D-08)
- **D-15:** ASCII art in code blocks for diagrams (Phase 2 D-02)
- **D-16:** Copilot-only references, no Claude Code (Phase 2 D-10)
- **D-17:** Swedish text with English technical terms per TERMINOLOGY.md

### Agent's Discretion
- Problem statement approach and slide count — D-01, D-02
- Collaboration metaphor — D-06
- Concept slide format and placement — D-10, D-11

</decisions>

<canonical_refs>
## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### Project Definition
- `.planning/PROJECT.md` — Project vision, constraints (Marp format, ~60 min, svenska + engelska), key decisions
- `.planning/REQUIREMENTS.md` — Full requirement list; Phase 5 covers SLIDE-02, CTXT-01, CTXT-02, CTXT-03, CTXT-04
- `.planning/ROADMAP.md` — Phase details, success criteria, build order rationale

### Prior Phase Context
- `.planning/phases/01-foundation-setup/01-CONTEXT.md` — Phase 1 decisions: 16:9, default theme, page numbers, section divider style
- `.planning/phases/02-core-payload-on-ramp/02-CONTEXT.md` — Phase 2 decisions: spacious layout, terminal style, ASCII art, Copilot-only, gateway bridge
- `.planning/phases/03-core-payload-full-workflow/03-CONTEXT.md` — Phase 3 decisions: agent discretion on visualization, carried style patterns
- `.planning/phases/04-scenarios-best-practices/04-CONTEXT.md` — Phase 4 decisions: decision tree all-English, generic scenarios, concrete prompt examples

### Content Sources
- `slides.md` — Current slide deck with Section 1 ("Var är vi idag?") and Section 2 ("Vad finns?") placeholders where Phase 5 content goes (lines 63 and 74)
- `TERMINOLOGY.md` — Swedish/English term policy; all slides must follow this
- `companion.md` — Companion document outline; Sections 1–2 map to this phase's content

### Domain-Specific
- STATE.md blocker: "BMAD comparison details are MEDIUM confidence and may need validation before slide creation" — researcher should verify BMAD positioning

</canonical_refs>

<code_context>
## Existing Code Insights

### Reusable Assets
- `slides.md` — Marp skeleton with Section 1 and Section 2 dividers already in place with Swedish titles ("Var är vi idag?", "Vad finns?")
- Phase 2's ASCII art pattern — plain code fence for diagrams, can be used for agent framework building blocks visual
- Phase 3's conceptual diagram patterns — wave diagrams, .planning/ directory tree visualizations
- Phase 4's decision tree pattern — established ASCII visual vocabulary for complex concepts

### Established Patterns
- Section dividers: `<!-- _class: divider -->` with `<hr>` tag and centered h1
- Content slides: standard `---` separator, no class directives, paginated
- Code blocks: 0.85em font size with border-radius 4px
- One idea per slide — spacious layout for back-of-room readability
- Gateway bridge pattern: sections end with a tease for the next section

### Integration Points
- Section 1 content inserts after `<!-- Section 1: The Problem — slides added by Phase 5 -->` comment in slides.md (line 63)
- Section 2 content inserts after `<!-- Section 2: Framework Landscape — slides added by Phase 5 -->` comment in slides.md (line 74)
- Section 2 leads into Section 3 ("Hur fungerar det?") which already has Phase 3's GSD mental model content — the transition from framework comparison to GSD deep-dive must feel natural
- Title slide already says "AI Agent Frameworks — GSD" — the intro sections must earn that framing

</code_context>

<specifics>
## Specific Ideas

- The problem statement should reference ChatGPT/Copilot Chat frustrations the audience has actually experienced — lost context, re-explaining architecture, AI forgetting decisions
- Skeptics arc uses positive-first framing — no "am I being replaced?" fear, straight to collaboration as the natural evolution of developer tools
- The collaboration slide comes early, before any GSD content — it sets the emotional foundation
- BMAD comparison stays high-level and balanced — philosophy contrast (workflow-centric vs persona-based), not a feature comparison. Let the audience draw their own conclusions about why GSD was chosen
- The overall narrative flow: relatable pain → collaboration reframe → "what are these frameworks?" → how GSD and BMAD approach it differently → ready for GSD deep-dive

</specifics>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope

</deferred>

---

*Phase: 05-framing-intro-landscape*
*Context gathered: 2026-04-16*
