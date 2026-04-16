# Phase 1: Foundation & Setup - Research

**Researched:** 2025-07-17
**Domain:** Marp slide deck skeleton, language policy, companion document structure
**Confidence:** HIGH

## Summary

Phase 1 is a greenfield skeleton phase. No code exists — the repo contains only `.planning/` and `copilot-instructions.md`. The deliverables are: (1) a Marp-compatible slide deck file with front matter, inline CSS, and section divider templates, (2) a Swedish/English terminology reference defining which GSD terms stay in English, and (3) a companion document outline with section placeholders matching the presentation arc.

The Marp configuration is locked by user decisions: 16:9 aspect ratio, default theme, page numbers only (no footer text), and section dividers with bold centered titles and subtle separator lines. The project-level research already verified Marp CLI 4.3.1 as the toolchain, and the architecture research established an 8-section presentation structure with a companion document outline. This phase creates the empty containers that all subsequent content phases fill.

**Primary recommendation:** Create three files — `slides.md` (Marp deck with front matter + CSS + section placeholders), `TERMINOLOGY.md` (term reference table), and `companion.md` (document outline with section headers) — all at repo root for maximum visibility.

<user_constraints>
## User Constraints (from CONTEXT.md)

### Locked Decisions
- **D-01:** Aspect ratio is 16:9 (modern widescreen, standard for tech presentations)
- **D-02:** Use the default Marp theme — custom theme is deferred to v2 per PROJECT.md
- **D-03:** Pagination: page numbers only, no footer text — clean and minimal
- **D-04:** Section divider slides use bold centered title with a subtle separator line for clear visual breaks between sections

### Agent's Discretion
- File organization — single vs split slide files, folder structure for assets
- Terminology reference format — list vs table, level of detail
- Visual identity — code block styling for terminal examples, typography choices within default theme constraints
- Companion document outline structure

### Deferred Ideas (OUT OF SCOPE)
None — discussion stayed within phase scope
</user_constraints>

<phase_requirements>
## Phase Requirements

| ID | Description | Research Support |
|----|-------------|------------------|
| SLIDE-01 | Marp-kompatibel slide-deck i markdown-format | Marp front matter syntax, directives, inline CSS patterns, and section divider templates documented below. Verified Marp CLI 4.3.1 on npm. |
| SLIDE-05 | Svenska text med engelska facktermer genomgående | Terminology reference patterns researched. PROJECT.md explicitly states: "Inga försvenskningar av engelska begrepp — 'phase' inte 'fas', 'roadmap' inte 'vägkarta'". Term list derived from GSD concepts and presentation content. |
</phase_requirements>

## Project Constraints (from copilot-instructions.md)

The copilot-instructions.md is a GSD-managed file containing:
- **GSD Workflow Enforcement:** All repo edits must go through GSD commands (`/gsd-quick`, `/gsd-execute-phase`, etc.) — no direct edits outside a GSD workflow unless the user explicitly asks to bypass
- **Project definition:** Swedish presentation with English technical terms, Marp format, ~45 min (note: ROADMAP.md says ~60 min — use ROADMAP as authoritative since it was created later)
- **Stack:** Marp CLI 4.3.1, VS Code + Marp extension, default theme + CSS overrides, highlight.js bundled

## Standard Stack

### Core

| Library | Version | Purpose | Why Standard |
|---------|---------|---------|--------------|
| Marp CLI | 4.3.1 | Slide rendering (HTML, PDF, PPTX) from markdown | Mandated by PROJECT.md. Verified on npm registry 2026-03-16. |
| Marp Core | 4.3.0 | Rendering engine (bundled with CLI) | Provides themes, syntax extensions, highlight.js |
| Marp for VS Code | latest | Live preview during authoring | Real-time WYSIWYG for slide editing |

### Supporting

| Library | Version | Purpose | When to Use |
|---------|---------|---------|-------------|
| highlight.js | bundled | Code syntax highlighting in slides | Automatic — included in Marp Core |
| Git | ≥2.38 | Version control | Always — markdown diffs are readable |

### Alternatives Considered

| Instead of | Could Use | Tradeoff |
|------------|-----------|----------|
| Single `.md` file | Split files per section | Single file is simpler, all phases edit same file. Splitting adds complexity for no gain on a single deck. |
| Inline `<style>` block | Separate CSS file | Inline keeps everything in one file and is sufficient for a single presentation per project research. |
| Default theme | Gaia or Uncover theme | **Locked decision D-02**: default theme. Gaia has lead-class slides built-in but default is cleaner for technical content. |

**Installation:**
```bash
npm install -g @marp-team/marp-cli@4.3.1
```

**VS Code extension:** `marp-team.marp-vscode` (install from marketplace)

## Architecture Patterns

### Recommended Project Structure

```
docs/                          # repo root
├── slides.md                  # Marp slide deck (single file, all sections)
├── companion.md               # Companion reference document
├── TERMINOLOGY.md             # Swedish/English term reference
├── assets/                    # Images, diagrams (if needed later)
│   └── (empty for now)
├── .planning/                 # GSD planning artifacts (existing)
└── copilot-instructions.md    # Project instructions (existing)
```

**Rationale:** All content files at repo root for maximum discoverability. Single slide file because Marp operates on one file per deck and all content phases (2–5) will add sections to the same file. The `assets/` directory is a placeholder for future phases that may need images or diagrams.

### Pattern 1: Marp Front Matter with Inline CSS

**What:** Marp uses YAML front matter for global directives and an inline `<style>` block for CSS overrides. This keeps the entire deck self-contained.

**When to use:** Always — this is the standard Marp authoring pattern for single-deck projects.

**Example — complete front matter for this project:**
```markdown
---
marp: true
theme: default
paginate: true
size: 16:9
---

<style>
/* Section divider slides */
section.divider {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}
section.divider h1 {
  font-size: 2.5em;
  font-weight: bold;
  margin-bottom: 0.3em;
}
section.divider hr {
  width: 40%;
  border: none;
  border-top: 3px solid #ccc;
  margin-top: 0;
}

/* Code blocks — terminal-style for command examples */
pre {
  font-size: 0.85em;
}
code {
  border-radius: 4px;
}

/* Lead slides (title slide) */
section.lead {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>
```

**Source:** Project research STACK.md (Marp Configuration Guide) + CONTEXT.md decisions D-01 through D-04.

### Pattern 2: Section Divider Slides

**What:** Section transitions use a CSS class applied via local directive to create visually distinct break slides.

**When to use:** Between each of the 8 presentation sections.

**Example:**
```markdown
---

<!-- _class: divider -->
<!-- _paginate: skip -->

# Börja enkelt

---
```

**Key details:**
- `<!-- _class: divider -->` applies the divider CSS class to just this slide (underscore prefix = local scope)
- `<!-- _paginate: skip -->` hides the page number on divider slides (cleaner look)
- The `h1` element renders bold and centered per the CSS
- An `hr` (`---` within the slide, or explicit `<hr>`) creates the subtle separator line below the title

### Pattern 3: Slide Separation

**What:** Marp uses `---` (three dashes on their own line) as slide separators. This is the same syntax as YAML front matter but Marp treats them as page breaks after the first one.

**When to use:** Between every slide.

**Example:**
```markdown
---

# Slide Title

Content here

---

# Next Slide

More content
```

### Pattern 4: Companion Document as Structured Outline

**What:** The companion document mirrors the 8-section presentation arc but serves as a standalone reference. Phase 1 creates empty section headers with brief descriptions; content phases 2–5 fill them. Phase 6 does the final companion document work.

**When to use:** Phase 1 creates the skeleton, later phases populate it.

**Source:** Architecture research — Document Structure section.

### Anti-Patterns to Avoid

- **Multiple slide files:** Marp renders one file = one deck. Splitting into multiple files creates assembly complexity with no benefit for a single presentation.
- **Custom theme file:** Decision D-02 locks this to default theme. A separate `.css` theme file is overkill for one deck. Use inline `<style>`.
- **Footer text in front matter:** Decision D-03 explicitly excludes footer text. Do NOT add `footer:` or `header:` directives.
- **Swedish translations of English terms:** PROJECT.md explicitly says "phase" not "fas", "roadmap" not "vägkarta". The terminology reference exists to codify this.

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| Slide rendering | Custom HTML/CSS pipeline | Marp CLI `marp slides.md --pdf` | Marp handles all rendering, pagination, scaling |
| Code highlighting | Custom syntax highlighting CSS | highlight.js (bundled in Marp Core) | Already included, supports all languages |
| Slide numbering | Manual page numbers | `paginate: true` directive | Automatic, respects `_paginate: skip` |
| Section divider layout | Per-slide inline styles | CSS class `.divider` applied via `_class` | Write once, apply to all dividers consistently |

**Key insight:** Marp is intentionally minimal — its power is that you write markdown and get slides. Don't fight the tool by adding complexity.

## Common Pitfalls

### Pitfall 1: Front Matter Syntax Errors
**What goes wrong:** YAML front matter must be the very first thing in the file (no blank lines before `---`). A stray newline or BOM character before the front matter breaks Marp rendering.
**Why it happens:** Editors sometimes add BOM or authors add a comment before front matter.
**How to avoid:** Start the file with `---` on line 1, no exceptions. Validate with Marp VS Code preview immediately.
**Warning signs:** Marp preview shows raw markdown instead of rendered slides.

### Pitfall 2: Confusing Slide Separator with Horizontal Rule
**What goes wrong:** Inside a slide, `---` creates a new slide break, not a horizontal rule (`<hr>`). Authors intending a visual separator accidentally create an empty slide.
**Why it happens:** Standard markdown uses `---` for horizontal rules. Marp overrides this.
**How to avoid:** Use explicit `<hr>` tag for horizontal rules within slides. Reserve `---` exclusively for slide breaks.
**Warning signs:** Unexpected blank slides in the preview.

### Pitfall 3: Global vs Local Directive Confusion
**What goes wrong:** Setting `paginate: false` without the underscore prefix (`_paginate: false`) turns off pagination for ALL subsequent slides, not just the current one.
**Why it happens:** Marp's scoping rule is subtle — underscore prefix = local (this slide only), no prefix = global (this slide and all after it).
**How to avoid:** Always use underscore prefix for per-slide overrides: `<!-- _paginate: skip -->`, `<!-- _class: divider -->`, `<!-- _backgroundColor: #1a1a2e -->`.
**Warning signs:** Styles "leak" to slides after the intended one.

### Pitfall 4: Size Directive Placement
**What goes wrong:** The `size: 16:9` directive must be in the YAML front matter, not in an HTML comment directive. Placing it as `<!-- size: 16:9 -->` does nothing.
**Why it happens:** Most Marp directives work in both front matter and HTML comments, but `size` is front-matter-only.
**How to avoid:** Always put `size: 16:9` in the YAML front matter block.
**Warning signs:** Slides render in 4:3 despite having a size directive.

### Pitfall 5: Term Inconsistency Across Phases
**What goes wrong:** Without a terminology reference from phase 1, subsequent content phases independently decide whether to write "fas" or "phase", "arbetsflöde" or "workflow", leading to inconsistent language.
**Why it happens:** Natural Swedish instinct is to translate, especially for common words. Different phases written at different times may make different choices.
**How to avoid:** Create the terminology reference in phase 1 and reference it in all content phases. The reference is the single source of truth for language choices.
**Warning signs:** Mixed Swedish/English for the same concept across slides.

## Code Examples

### Complete Marp Slide Deck Skeleton

```markdown
---
marp: true
theme: default
paginate: true
size: 16:9
---

<style>
/* Section divider slides */
section.divider {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}
section.divider h1 {
  font-size: 2.5em;
  font-weight: bold;
  margin-bottom: 0.3em;
}
section.divider hr {
  width: 40%;
  border: none;
  border-top: 3px solid #ccc;
  margin-top: 0;
}

section.lead {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

pre {
  font-size: 0.85em;
}
</style>

<!-- _class: lead -->
<!-- _paginate: skip -->

# AI Agent Frameworks — GSD

*Hur du arbetar effektivt med AI-assisterad utveckling*

---

<!-- _class: divider -->
<!-- _paginate: skip -->

# Var är vi idag?

<hr>

---

<!-- Section 1: The Problem — slides will be added by Phase 5 -->

---

<!-- _class: divider -->
<!-- _paginate: skip -->

# Vad finns?

<hr>

---

<!-- Section 2: Framework Landscape — slides will be added by Phase 5 -->

---

<!-- Additional section dividers follow the same pattern... -->
```

**Source:** Synthesized from ARCHITECTURE.md section structure, STACK.md Marp configuration guide, and CONTEXT.md decisions.

### Terminology Reference Format

```markdown
# Terminologi — Svenska/Engelska

## Princip

Svenska löptext, engelska facktermer. Ingen försvenskning av etablerade begrepp.

| Engelska (används) | Svenska (används INTE) | Kontext |
|---------------------|------------------------|---------|
| phase | fas | GSD workflow stages |
| roadmap | vägkarta | Project planning |
| agent | agent | AI agent (same in both) |
| workflow | arbetsflöde | Process descriptions |
| orchestrator | orkestrerare | GSD architecture |
| milestone | milstolpe | Project checkpoints |
| prompt | prompt | AI interaction |
| commit | commit | Git operations |
| skill | förmåga | Copilot skills |
| framework | ramverk | Tool category |
| on-ramp | — | Graduated entry concept |
| brownfield | — | Existing codebase |
| greenfield | — | New project |
```

**Source:** PROJECT.md language policy + GSD concepts from FEATURES.md.

### Companion Document Outline

```markdown
# Arbeta effektivt med AI Agent Frameworks — GSD

> Kompletterande dokument till presentationen. Kan läsas standalone.

## 1. Introduktion
### Problemet med ostrukturerad AI-assistans
### Vad är ett agent framework?

## 2. GSD i korthet
### Arkitektur: orchestrator + agents
### .planning/ — projektets minne
### Kärnprincip: du bestämmer, GSD strukturerar

## 3. Kom igång — On-Ramp
### /gsd-fast — triviala tasks
### /gsd-do — smart routing
### /gsd-quick — tasks med planering
### Vilken ska jag välja? (beslutsträd)

## 4. Full Workflow
### /gsd-new-project — från idé till roadmap
### Phase lifecycle: plan → execute → verify
### Projektminne: STATE.md och /gsd-resume-work
### Milestones och arkivering

## 5. Scenarion
### Greenfield-projekt
### Brownfield: ny feature i befintlig kodbas
### Buggfixar och debugging
### Quick fixes och config-ändringar

## 6. Best Practices
### Tänk i outcomes
### Trust but verify
### När du INTE ska använda GSD
### Gradvis adoption

## 7. Referens
### Kommandoöversikt
### .planning/ filstruktur
### Länkar och resurser

## Appendix
### GSD vs BMAD — kortjämförelse
```

**Source:** ARCHITECTURE.md — Document Architecture section (verified structure).

## Presentation Section Map

For context on what section placeholders the slide skeleton must contain. This is derived from the project's architecture research and drives the section divider templates.

| # | Section Title (Swedish) | Filled By Phase | Time Budget |
|---|------------------------|-----------------|-------------|
| — | Title slide | Phase 1 (skeleton) | — |
| 1 | Var är vi idag? (The Problem) | Phase 5 | 5 min |
| 2 | Vad finns? (Framework Landscape) | Phase 5 | 3 min |
| 3 | Hur fungerar det? (GSD Mental Model) | Phase 3 | 5 min |
| 4 | Börja enkelt (The On-Ramp) ⭐ | Phase 2 | 8 min |
| 5 | Hela livscykeln (Full Workflow) ⭐ | Phase 3 | 12 min |
| 6 | I din vardag (Scenarios) | Phase 4 | 7 min |
| 7 | Tänk så här (Best Practices) | Phase 4 | 3 min |
| 8 | Börja på måndag (Getting Started) | Phase 4 | 2 min |

**Note:** The build order (Phases 2→3→4→5) differs from the presentation order (Sections 1→2→3→4→5→6→7→8). The skeleton must have placeholders for ALL 8 sections even though they are filled out of numerical order.

## Environment Availability

| Dependency | Required By | Available | Version | Fallback |
|------------|------------|-----------|---------|----------|
| Node.js | Marp CLI runtime | ✓ | 22.14.0 | — |
| npm | Package installation | ✓ | 11.12.0 | — |
| Marp CLI | Slide rendering | ✗ (not installed) | 4.3.1 (on npm) | `npm install -g @marp-team/marp-cli@4.3.1` |
| Marp VS Code Extension | Live preview | ✗ (not installed) | latest | Install `marp-team.marp-vscode` |
| VS Code | Authoring environment | ✓ | 1.115.0 | — |
| Git | Version control | ✓ | 2.38.1 | — |

**Missing dependencies with no fallback:**
- None — all missing items have straightforward install steps.

**Missing dependencies with fallback:**
- **Marp CLI:** Not installed globally. Install with `npm install -g @marp-team/marp-cli@4.3.1`. Alternatively, use `npx @marp-team/marp-cli` for on-demand execution.
- **Marp VS Code Extension:** Not installed. Install `marp-team.marp-vscode` for live preview. Not strictly required — slides can be previewed via `marp slides.md --preview` (CLI server mode).

## Validation Architecture

### Test Framework

| Property | Value |
|----------|-------|
| Framework | Manual validation (no automated test framework — this is a content/markdown project) |
| Config file | none |
| Quick run command | `marp slides.md --pdf -o /dev/null` (validates Marp parsing) |
| Full suite command | Manual review: open in VS Code with Marp extension, verify all sections render |

### Phase Requirements → Test Map

| Req ID | Behavior | Test Type | Automated Command | File Exists? |
|--------|----------|-----------|-------------------|-------------|
| SLIDE-01 | Marp-compatible slide deck exists with correct front matter | smoke | `marp slides.md --pdf -o test-output.pdf && del test-output.pdf` | ❌ Wave 0 |
| SLIDE-05 | Terminology reference exists with English/Swedish term mapping | manual | Visual inspection of TERMINOLOGY.md | ❌ Wave 0 |

### Sampling Rate
- **Per task commit:** Open `slides.md` in VS Code Marp preview — verify renders correctly
- **Per wave merge:** Generate PDF with `marp slides.md --pdf` — confirm no errors
- **Phase gate:** All three files exist, slide deck renders in Marp, all 8 section dividers present, terminology table has ≥10 terms

### Wave 0 Gaps
- [ ] Install Marp CLI: `npm install -g @marp-team/marp-cli@4.3.1`
- [ ] Install Marp VS Code extension: `marp-team.marp-vscode`

*(Automated testing beyond Marp rendering validation is not applicable to a markdown content project)*

## Open Questions

1. **Exact section titles in Swedish**
   - What we know: Architecture research provides both English section names and Swedish equivalents for some sections
   - What's unclear: Final Swedish titles for section dividers should match the presentation tone ("Var är vi idag?" vs "Problemet")
   - Recommendation: Use the Swedish titles from the architecture research as-is — they were designed to be conversational and audience-friendly. Content phases can refine later.

2. **Number of GSD terms in terminology reference**
   - What we know: PROJECT.md says "phases, roadmap, agents, etc." — a minimum set
   - What's unclear: How exhaustive the list should be
   - Recommendation: Start with ~15–20 core terms covering GSD concepts, Git terms, and AI agent vocabulary. Content phases will surface additional terms as they write slides.

## Sources

### Primary (HIGH confidence)
- `.planning/research/STACK.md` — Marp CLI versions, directives, configuration patterns (verified via npm registry)
- `.planning/research/ARCHITECTURE.md` — 8-section presentation arc, companion document structure, slide design principles
- `.planning/PROJECT.md` — Language policy, constraints, scope
- `.planning/phases/01-foundation-setup/01-CONTEXT.md` — Locked decisions D-01 through D-04

### Secondary (MEDIUM confidence)
- `.planning/research/FEATURES.md` — GSD feature landscape, terminology concepts
- `.planning/research/PITFALLS.md` — Presentation pitfalls (informs structure, not directly phase 1)

### Tertiary (LOW confidence)
- None — all findings sourced from project artifacts and verified Marp documentation

## Metadata

**Confidence breakdown:**
- Standard stack: HIGH — Marp CLI version verified via npm, tooling is simple and well-documented
- Architecture: HIGH — presentation structure comes from project's own architecture research, companion document outline is explicit
- Pitfalls: HIGH — Marp syntax pitfalls are well-known and documented; terminology consistency is a process/discipline issue with clear prevention

**Research date:** 2025-07-17
**Valid until:** 2025-08-17 (stable domain — Marp and markdown conventions don't change frequently)
