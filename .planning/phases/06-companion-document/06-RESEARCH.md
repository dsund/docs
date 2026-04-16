# Phase 6: Companion Document - Research

**Researched:** 2025-07-18
**Domain:** Markdown content authoring — standalone reference document expanding presentation slides with full command reference, advanced features, and detailed scenarios
**Confidence:** HIGH

## Summary

Phase 6 is the final phase of the GSD-presentation project. It takes the existing `companion.md` skeleton (7 sections + appendix, created in Phase 1) and fills it with comprehensive content that expands on the completed slide deck (`slides.md`, ~28 content slides across 8 sections). The companion document serves two audiences: presentation attendees who want deeper detail, and developers who never attended the talk but need to learn GSD from reading alone.

The primary authoring challenge is **depth calibration** — the companion must go meaningfully deeper than slides on key topics (command reference, workflow details, scenarios) without becoming an exhaustive manual. Per D-03, moderate expansion means key topics get deeper treatment while simpler topics stay concise. Three requirements (PRAC-05, PRAC-06, PRAC-07) introduce entirely NEW content not present in slides: phase insertion (`/gsd-insert-phase`), cross-AI review (`/gsd-review`), and autonomous mode (`/gsd-autonomous`). Per D-08, these integrate into their natural sections rather than being grouped separately.

The output is a single file (`companion.md`) written in standard markdown that renders correctly on GitHub, GitLab wikis, and any markdown viewer. No Marp directives, no special tooling. Swedish text with English technical terms per TERMINOLOGY.md, matching the presentation's "svengelska" voice.

**Primary recommendation:** Split into 3–4 plans following the document's natural arc: (1) Sections 1–3 (foundational — intro, GSD overview, on-ramp), (2) Section 4 (full workflow + phase insertion), (3) Sections 5–6 (scenarios + best practices + cross-AI review + autonomous mode), (4) Section 7 + Appendix (reference tables + GSD vs BMAD). Each plan writes to `companion.md` sequentially since sections build on each other.

<user_constraints>

## User Constraints (from CONTEXT.md)

### Locked Decisions

**Document Depth & Voice**
- D-01: Comprehensive guide — explain concepts + show examples + provide context. The reader should understand WHY, not just HOW
- D-02: Utbildande, approachable tone matching the slides — same "svengelska" voice as the presentation
- D-03: Moderate expansion on slides — key topics get deeper treatment, simpler topics stay concise. Not every slide needs a companion paragraph
- D-04: No length target — let the content determine the length. Focus on quality, not word count

**Relationship to Slides**
- D-05: Keep the existing companion.md outline structure (7 sections + appendix from Phase 1) — it maps well to the presentation arc
- D-06: Standalone with slide echoes — the companion stands on its own but may reference "som vi såg i presentationen" occasionally. No required cross-reading

**Advanced Features Coverage**
- D-07: Scenario-driven — each advanced feature gets a realistic scenario showing when and how to use it
- D-08: Place advanced features in their natural sections — phase insertion in "Full Workflow" (Section 4), cross-AI review in "Best Practices" (Section 6), autonomous mode in its own subsection. Not grouped in a separate "Advanced" section

**Command Reference Format**
- D-09: Curated command table — cover the most important 10–15 commands with Command | Description | När? columns. Quality over completeness
- D-10: Include `.planning/` file structure overview — file tree + brief explanation of each file's role
- D-11: Table format for command reference — scannable, quick lookup

**Carried Style Decisions**
- D-12: Swedish text with English technical terms per TERMINOLOGY.md (all phases)
- D-13: Copilot-only references, no Claude Code (Phase 2 D-10)
- D-14: Generic, relatable developer scenarios (Phase 4 D-07)

### Agent's Discretion
- Which 10–15 commands to include in the curated reference table
- Level of detail per section — where to expand heavily vs stay concise
- How to structure the `.planning/` file tree overview
- Terminal example format within the companion (code blocks with realistic output)
- Autonomous mode subsection placement within the document

### Deferred Ideas (OUT OF SCOPE)
None — discussion stayed within phase scope

</user_constraints>

<phase_requirements>

## Phase Requirements

| ID | Description | Research Support |
|----|-------------|------------------|
| COMP-01 | Markdown-dokument med fullständigt innehåll (wiki/repo-vänligt) | Standard markdown only — no Marp directives, no HTML beyond basic `<hr>`. Headings, tables, code blocks, blockquotes. Renders on GitHub/GitLab/any viewer. |
| COMP-02 | Djupare än slides — full command reference, detaljerade scenarion | Each companion section expands its slide counterpart with explanations, context, more examples. Section 7 adds curated command table (10–15 commands) and `.planning/` file tree not present in slides. |
| COMP-03 | Standalone-läsbart utan presentatör | Every concept must be self-contained. No "see slide X" references. Occasional "som vi såg i presentationen" echoes allowed (D-06) but document must make complete sense without them. |
| PRAC-05 | Phase insertion och roadmap adaptation (`/gsd-insert-phase`) | NEW content for Section 4 (Full Workflow). Scenario-driven: "Du är mitt i Phase 3 och inser att du behöver ett API först..." Shows command, what happens to roadmap, when to use it. |
| PRAC-06 | Cross-AI review (`/gsd-review`) — multi-AI peer review | NEW content for Section 6 (Best Practices). Scenario-driven: using a different AI to review work done by Copilot. Shows command and value proposition. |
| PRAC-07 | Autonomous mode (`/gsd-autonomous`) — end-game vision | NEW content — own subsection. Scenario-driven: running an entire phase hands-off. Framed as "end-game" for experienced users who trust the workflow. |

</phase_requirements>

## Standard Stack

### Core
| Technology | Version | Purpose | Why Standard |
|------------|---------|---------|--------------|
| Standard Markdown | CommonMark | Document format | Wiki/repo-friendly, renders everywhere without tooling (COMP-01). No Marp directives needed. |
| VS Code | current | Authoring environment | Live markdown preview, team already uses it |
| Git | current | Version control | Markdown diffs are readable, tracks companion evolution |

### Supporting
| Technology | Version | Purpose | When to Use |
|------------|---------|---------|-------------|
| TERMINOLOGY.md | project-local | Language consistency | Every section — ensures English terms are used per project policy |

### Alternatives Considered
| Instead of | Could Use | Tradeoff |
|------------|-----------|----------|
| Standard Markdown | MDX, AsciiDoc | More features but violates COMP-01 (wiki/repo-friendly, no special tooling) |
| Single companion.md file | Multiple linked .md files | Multi-file is harder to share as single reference; one file is simpler for the companion use case |

## Architecture Patterns

### Document Structure (companion.md)

The existing outline from Phase 1 defines the structure. Each section maps to slide deck sections:

```
companion.md
├── Header + tagline
├── Section 1: Introduktion               ← Slides Sections 1-2
│   ├── Problemet med ostrukturerad AI-assistans
│   └── Vad är ett agent framework?
├── Section 2: GSD i korthet               ← Slides Section 3
│   ├── Arkitektur: orchestrator + agents
│   ├── .planning/ — projektets minne
│   └── Kärnprincip: du bestämmer, GSD strukturerar
├── Section 3: Kom igång — On-Ramp         ← Slides Section 4
│   ├── /gsd-fast — triviala tasks
│   ├── /gsd-do — smart routing
│   ├── /gsd-quick — tasks med planering
│   └── Vilken ska jag välja? (beslutsträd)
├── Section 4: Full Workflow               ← Slides Section 5
│   ├── /gsd-new-project — från idé till roadmap
│   ├── Phase lifecycle: plan → execute → verify
│   ├── Projektminne: STATE.md och /gsd-resume-work
│   ├── Milestones och arkivering
│   └── ★ NEW: Phase insertion (/gsd-insert-phase)   ← PRAC-05
├── Section 5: Scenarion                   ← Slides Section 6
│   ├── Greenfield-projekt
│   ├── Brownfield: ny feature i befintlig kodbas
│   ├── Buggfixar och debugging
│   └── Quick fixes och config-ändringar
├── Section 6: Best Practices              ← Slides Section 7
│   ├── Tänk i outcomes
│   ├── Trust but verify
│   ├── När du INTE ska använda GSD
│   ├── Gradvis adoption
│   └── ★ NEW: Cross-AI review (/gsd-review)         ← PRAC-06
├── Section 7: Referens                    ← NEW (no slide equivalent)
│   ├── Kommandoöversikt (curated table)
│   ├── .planning/ filstruktur
│   └── Länkar och resurser
├── ★ Autonomous mode subsection           ← PRAC-07 (placement: agent discretion)
└── Appendix: GSD vs BMAD — kortjämförelse ← Slides Section 2 expanded
```

### Pattern 1: Slide-to-Companion Expansion
**What:** Each companion section takes a slide's key point and adds the WHY, the context, more examples, and edge cases the slides couldn't cover.
**When to use:** Every section that has a slide counterpart (Sections 1–6).
**Example:**

```markdown
## Slide says:
> ≤ 3 file edits → atomic commit → loggat i STATE.md

## Companion expands to:
### /gsd-fast — triviala tasks

`/gsd-fast` är det enklaste sättet att använda GSD. Ge den en kort
beskrivning av vad du vill göra, så fixar den det direkt — utan planning,
utan subagents, utan `.planning/`-mapp.

```bash
$ /gsd-fast "add .env to .gitignore"
✅ Done: Added .env to .gitignore
   Commit: a3f2e1d
   Files: .gitignore
```

**Begränsningar:** Max 3 filändringar. Om uppgiften kräver mer, använd
`/gsd-quick` istället. GSD säger till om du försöker göra för mycket.

**När du ska använda det:**
- Typos, småfixar, config-ändringar
- Du vet exakt vad som behöver göras
- Det tar en person 2 minuter manuellt
```

### Pattern 2: Scenario-Driven Advanced Features
**What:** Each advanced feature (PRAC-05, PRAC-06, PRAC-07) opens with a realistic developer scenario that motivates WHY you'd use the feature, then shows HOW.
**When to use:** All three advanced features.
**Example structure:**

```markdown
### Phase insertion — `/gsd-insert-phase`

Du är mitt i Phase 3 av ett API-projekt. Under implementation inser
du att du behöver en databasmigrering innan API-endpoints kan fungera.
Att starta om hela projektet vore slöseri — allt du gjort hittills
är korrekt.

```bash
$ /gsd-insert-phase "database migration setup" --before 3
✅ Phase 2.1 inserted: Database Migration
   Roadmap updated — Phase 3 becomes Phase 4
   Ready: /gsd-plan-phase 2.1
```

GSD numrerar om roadmappen automatiskt och bevarar alla befintliga
artifacts. Dina färdiga phases påverkas inte.

**När du behöver det:**
- Du upptäcker ett saknat steg mitt i arbetet
- En extern dependency kräver förberedelse du inte planerade
- Teamet bestämmer att scope ska utökas
```

### Pattern 3: Command Reference Table Format
**What:** Curated table of 10–15 essential commands with three columns: Command, Description, När?
**When to use:** Section 7 (Referens).
**Example:**

```markdown
### Kommandoöversikt

| Kommando | Beskrivning | När? |
|----------|-------------|------|
| `/gsd-fast` | Snabbfix utan planning | Triviala ändringar (≤3 filer) |
| `/gsd-quick` | Task med planner + executor | Ny feature, liten refaktor |
| `/gsd-do` | Smart routing till rätt kommando | Du vet inte vilket kommando du behöver |
| `/gsd-new-project` | Nytt projekt med full workflow | Greenfield — helt nytt projekt |
| `/gsd-map-codebase` | Kartlägger befintlig kodbas | Brownfield — innan du börjar ändra |
| ... | ... | ... |
```

### Pattern 4: .planning/ File Structure Overview
**What:** ASCII file tree + brief explanation of each file's role.
**When to use:** Section 7 (Referens) and referenced from Section 2.
**Example:**

```markdown
### .planning/ filstruktur

```
.planning/
├── PROJECT.md        # Vad vi bygger — vision, constraints, core value
├── REQUIREMENTS.md   # Alla krav med spårbarhet till phases
├── ROADMAP.md        # Phases med success criteria och beroenden
├── STATE.md          # Var projektet är just nu — progress, beslut
├── config.json       # GSD-konfiguration för detta projekt
└── phases/
    └── 01-namn/
        ├── 01-CONTEXT.md   # Beslut från /gsd-discuss-phase
        ├── 01-RESEARCH.md  # Domänresearch från /gsd-research-phase
        ├── 01-PLAN.md      # Executionsplan med tasks
        ├── 01-SUMMARY.md   # Resultat efter execution
        └── 01-VERIFICATION.md  # Goal-backward verification
```

Varje phase producerar sin egen uppsättning artifacts. Inget försvinner —
du kan alltid gå tillbaka och se vad som bestämdes och varför.
```

### Anti-Patterns to Avoid
- **Slide duplication:** Don't reproduce slide content word-for-word. Expand it — add context, examples, edge cases. The companion adds value beyond the slides.
- **Exhaustive command reference:** D-09 says curated 10–15 commands, not every possible GSD command. Quality over completeness.
- **Assumed presentation knowledge:** Per COMP-03, every concept must be self-contained. Don't write "as shown in the presentation" as the only explanation — explain the concept, then optionally add "som vi såg i presentationen" as a parenthetical.
- **Marp directives in companion:** No `---` slide separators, no `<!-- _class: -->` directives, no front matter. This is standard markdown.
- **Feature documentation style:** Don't write like a man page. Per D-01, explain WHY + show examples + provide context. More "textbook" than "reference manual."

## Content Mapping: Slides → Companion

This table maps each companion section to its slide source material and what expansion is needed:

| Companion Section | Slides Source | Expansion Focus | New Content (not in slides) |
|-------------------|---------------|-----------------|----------------------------|
| 1. Introduktion | Section 1 (problem) + Section 2 (concept) | Deeper "why" on unstructured AI problems, fuller agent framework explanation | None — but must stand alone |
| 2. GSD i korthet | Section 3 (mental model) | Agent roles explained, .planning/ as concept, wave execution details | None |
| 3. Kom igång | Section 4 (on-ramp) | Each command with more examples, clearer decision tree text, composable flags detail | None |
| 4. Full Workflow | Section 5 (lifecycle) | Artifact examples, STATE.md detail, lifecycle management | **PRAC-05: /gsd-insert-phase** |
| 5. Scenarion | Section 6 (scenarios) | Longer scenario walkthroughs, more commands shown per scenario | None |
| 6. Best Practices | Section 7 (best practices) | More prompt examples, deeper anti-pattern explanations, gradual adoption path | **PRAC-06: /gsd-review** |
| 7. Referens | No slide equivalent | Full command table, .planning/ tree, links | **Entirely new section** |
| Appendix | Section 2 (2 slides on BMAD) | Expanded philosophy comparison, use cases for each | None — but much deeper than 2 slides |

**Autonomous mode (PRAC-07)** placement is agent's discretion. Recommended: as a subsection within Section 4 (Full Workflow) after phase insertion, or as a standalone subsection between Section 6 and Section 7. Both are valid — the key is that it's framed as "end-game vision" for experienced users.

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| Terminology consistency | Manual memory of English/Swedish terms | Reference TERMINOLOGY.md during every section write | 20+ terms with specific rules; easy to accidentally use "fas" instead of "phase" |
| Decision tree format | Reinvent from scratch | Adapt the slides' ASCII decision tree for prose format | The slide version (slides.md Section 6) is already tested and comprehensive |
| Command descriptions | Write ad-hoc descriptions | Use slides' existing command explanations as starting point | Ensures consistency between presentation and companion |
| .planning/ structure | Guess at file contents | Base on this project's own `.planning/` directory as a real example | The project itself is a working example of GSD artifacts |

## Common Pitfalls

### Pitfall 1: Companion reads like slide notes
**What goes wrong:** Each section is just a slightly expanded version of the slide bullet points — adds a sentence or two but doesn't provide real depth.
**Why it happens:** Writer stays too close to slide structure, treating each slide as a paragraph template.
**How to avoid:** For each section, ask: "What would a reader who's never seen the slides need to understand this?" Write for THAT reader. Use slides as a content checklist, not a template.
**Warning signs:** Sections that are shorter than 3-4 paragraphs on key topics; no examples beyond what slides show.

### Pitfall 2: Advanced features feel bolted on
**What goes wrong:** Phase insertion, cross-AI review, and autonomous mode read like separate appendices jammed into random sections.
**Why it happens:** They're truly new content (not in slides) and the writer treats them differently from the expanded slide content.
**How to avoid:** Per D-08, place them in their natural sections and write them in the same voice and style as surrounding content. The scenario-driven approach (D-07) helps — start with a developer situation, not a feature description.
**Warning signs:** Sudden tone shift, no narrative connection to surrounding content, no scenario/motivation before the command example.

### Pitfall 3: English/Swedish term drift
**What goes wrong:** Terms drift across the document — "fas" in one place, "phase" in another; "arbetsflöde" somewhere, "workflow" elsewhere.
**Why it happens:** Long document, many sections, natural tendency to use Swedish equivalents in flowing prose.
**How to avoid:** Always consult TERMINOLOGY.md. Every English term in that table stays English. Swedish inflections are OK ("i en phase", "mellan phases") but the base term stays English.
**Warning signs:** Any term from the "Svenska (används INTE)" column appearing in the document.

### Pitfall 4: Decision tree loses interactivity in prose
**What goes wrong:** The slides' ASCII decision tree works because it's visual and compact. Translating it to prose creates a wall of text nobody reads.
**Why it happens:** Trying to preserve the tree structure in paragraph form.
**How to avoid:** Keep it as an ASCII tree or convert to a structured flowchart-style list. The companion can include the same ASCII tree from the slides and add prose guidance beneath it.
**Warning signs:** Multi-paragraph explanation that could be a simple visual.

### Pitfall 5: Too deep on reference, too shallow on narrative
**What goes wrong:** Section 7 (Referens) becomes an exhaustive command catalog while Sections 1-6 stay thin.
**Why it happens:** Reference content is easier to write (list commands, describe flags) than narrative content (explain concepts, tell stories).
**How to avoid:** D-09 explicitly limits commands to 10-15 curated entries. Spend the bulk of effort on Sections 1-6 where the real value is — the reference table is a lookup aid, not the main content.
**Warning signs:** Reference section is longer than any narrative section.

## Recommended Command Table Candidates (10–15 commands)

Based on analysis of the slide deck content and GSD's command spectrum, these commands cover the essential user journey:

| Command | Category | Rationale |
|---------|----------|-----------|
| `/gsd-fast` | On-ramp | Simplest entry point, no planning |
| `/gsd-quick` | On-ramp | First structured command with planning |
| `/gsd-do` | On-ramp | Smart router — good for uncertainty |
| `/gsd-new-project` | Full workflow | Greenfield entry point |
| `/gsd-plan-phase` | Full workflow | Phase planning step |
| `/gsd-execute-phase` | Full workflow | Phase execution step |
| `/gsd-verify-work` | Full workflow | Verification step |
| `/gsd-resume-work` | Lifecycle | Resume after pause — key differentiator |
| `/gsd-progress` | Lifecycle | Status check |
| `/gsd-map-codebase` | Brownfield | Essential for existing codebases |
| `/gsd-debug` | Specialist | Bug investigation |
| `/gsd-insert-phase` | Advanced | Phase insertion (PRAC-05) |
| `/gsd-review` | Advanced | Cross-AI review (PRAC-06) |
| `/gsd-autonomous` | Advanced | Autonomous mode (PRAC-07) |

14 commands — within the 10–15 target. Agent has discretion to adjust based on what feels right during writing. `/gsd-add-phase`, `/gsd-pause-work`, `/gsd-cleanup` are candidates if more are needed.

## Writing Guidelines

### Voice and Tone
- **Same voice as slides:** Utbildande, approachable, "svengelska"
- **Textbook, not manual:** Explain concepts with context and motivation, not just syntax
- **D-01 in practice:** For each topic — explain the concept (WHY), show an example (HOW), provide context (WHEN/WHERE)
- **Blockquotes for insights:** Use `>` blockquotes sparingly for key insights or memorable takeaways, matching slides pattern

### Terminal Examples Format
Based on established patterns from slides.md:
```bash
$ /gsd-command "description"
✅ Result description
   Detail line 1
   Detail line 2
```
- Use `bash` code fence (not plain code fence — different from slides' ASCII art which uses no language specifier)
- `$` prompt prefix for user commands
- `✅` for success output
- Indented detail lines for additional output
- Keep output compact and realistic but simplified

### Section Length Guidelines (agent discretion on exact lengths)
- **Sections 1-2 (Intro + Overview):** Medium — enough to orient a new reader (~500-800 words each)
- **Sections 3-4 (On-Ramp + Workflow):** Heavy — these are the core how-to sections with the most examples (~800-1200 words each)
- **Section 5 (Scenarios):** Medium-heavy — detailed walkthroughs but avoid repetition with Section 3-4 (~600-1000 words)
- **Section 6 (Best Practices):** Medium — principles + examples, including /gsd-review (~600-800 words)
- **Section 7 (Reference):** Compact — tables + tree + links, minimal prose (~400-600 words)
- **Appendix:** Short — expanded philosophy comparison (~300-500 words)

These are rough guidance, not strict limits. Per D-04, let content determine length.

## Markdown Rendering Considerations (COMP-01)

For wiki/repo-friendly rendering:

| Feature | Safe to Use | Avoid |
|---------|-------------|-------|
| `#`-`######` headings | ✅ Yes | Underline-style headings (`===`, `---` for H1/H2) — less portable |
| Tables (pipe syntax) | ✅ Yes | HTML tables — overkill and less readable in raw form |
| Fenced code blocks (```) | ✅ Yes | Indented code blocks — harder to maintain |
| Blockquotes (`>`) | ✅ Yes | |
| Bold (`**`), italic (`*`) | ✅ Yes | |
| Inline code (`` ` ``) | ✅ Yes | |
| Bullet lists (`-`) | ✅ Yes | |
| Numbered lists (`1.`) | ✅ Yes | |
| Horizontal rules (`---`) | ✅ Use sparingly | Could conflict with YAML front matter if at doc start |
| HTML tags | ❌ Avoid | `<details>`, `<summary>` — not supported everywhere |
| Marp directives | ❌ Never | `<!-- _class: -->`, front matter — this is NOT a Marp file |
| Emoji (Unicode) | ✅ Sparingly | Terminal output uses ✅ ❌ per established pattern |
| Nested tables | ❌ Avoid | Poor rendering across viewers |

## Plan Decomposition Recommendation

### Recommended: 4 Plans

**Plan 1 — Sections 1–3: Foundation (Wave 1)**
- Files: `companion.md`
- Requirements: COMP-01, COMP-02, COMP-03 (partially)
- Content: Introduktion (problem + framework concept), GSD i korthet (architecture + .planning/ + core principle), Kom igång (all 4 on-ramp subsections including decision tree)
- Rationale: These three sections establish the baseline knowledge. A reader finishing Section 3 understands what GSD is and how to start.

**Plan 2 — Section 4: Full Workflow + Phase Insertion (Wave 1, parallel with Plan 1)**
- Files: `companion.md`
- Requirements: COMP-02, PRAC-05
- Content: Full lifecycle walkthrough, artifact examples, project memory, milestones, AND new `/gsd-insert-phase` subsection with scenario
- Rationale: Section 4 is heavy and includes PRAC-05 (new content). Keeping it as a separate plan allows focused attention on the workflow details and the phase insertion scenario.
- **Note on parallelism:** Plans 1 and 2 write to the same file (`companion.md`) but to different sections. They CAN run in Wave 1 if the executor handles non-overlapping edits, but sequential execution (Wave 1 → Wave 2) is safer to avoid edit conflicts. Planner should decide based on risk tolerance.

**Plan 3 — Sections 5–6: Scenarios + Best Practices + Advanced Features (Wave 2)**
- Files: `companion.md`
- Requirements: COMP-02, PRAC-06, PRAC-07
- Content: All 4 scenario subsections expanded, best practices with /gsd-review scenario, autonomous mode subsection
- Depends on: Plans 1-2 (references on-ramp commands and workflow concepts)
- Rationale: Scenarios reference concepts from Sections 1-4. Best practices build on the workflow knowledge. Both PRAC-06 and PRAC-07 live here.

**Plan 4 — Section 7 + Appendix: Reference + Comparison (Wave 2 or 3)**
- Files: `companion.md`
- Requirements: COMP-01, COMP-02
- Content: Curated command table (10–15 commands), .planning/ file structure tree, links/resources, expanded GSD vs BMAD comparison
- Depends on: Plans 1-3 (command table references all commands introduced earlier)
- Rationale: Reference material is best written last — it summarizes everything that came before.

### Alternative: 3 Plans (if simpler scheduling preferred)
- Plan 1: Sections 1–4 (all foundational + workflow)
- Plan 2: Sections 5–6 (scenarios + best practices + all 3 advanced features)
- Plan 3: Section 7 + Appendix (reference + comparison)

## Project Constraints (from copilot-instructions.md)

The copilot-instructions.md contains embedded GSD state blocks with these actionable directives:

- **Format:** Marp-compatible markdown for slides + separate document for details — companion.md is that separate document
- **Language:** Svenska med engelska facktermer — natural svengelska (enforced via TERMINOLOGY.md)
- **Tone:** Utbildande, inte säljande — focus on "hur" snarare än "varför" (though D-01 says explain WHY too — balance both)
- **Audience:** Must work for both skeptics and enthusiasts
- **GSD workflow enforcement:** Don't make direct repo edits outside GSD workflow — Phase 6 follows the standard plan → execute workflow
- **Copilot-only:** No Claude Code references (D-13)

## Validation Architecture

### Test Framework
| Property | Value |
|----------|-------|
| Framework | PowerShell `Select-String` + manual review |
| Config file | None — ad-hoc validation commands |
| Quick run command | `powershell -Command "Select-String -Pattern 'TARGET' companion.md"` |
| Full suite command | PowerShell script checking all structural and content markers |

### Phase Requirements → Test Map
| Req ID | Behavior | Test Type | Automated Command | File Exists? |
|--------|----------|-----------|-------------------|-------------|
| COMP-01 | Wiki/repo-friendly markdown with full content | automated | `powershell -Command "if (Select-String -Pattern 'marp:|<!-- _class' companion.md) { exit 1 } else { Write-Host 'No Marp directives found' }"` | ❌ Wave 0 |
| COMP-02 | Deeper than slides — command reference, expanded scenarios | automated | `powershell -Command "Select-String -Pattern 'Kommandoöversikt' companion.md; Select-String -Pattern 'gsd-insert-phase' companion.md; Select-String -Pattern 'gsd-review' companion.md; Select-String -Pattern 'gsd-autonomous' companion.md"` | ❌ Wave 0 |
| COMP-03 | Standalone readable without presenter | manual-only | Manual review — read document without slides context, verify comprehension | N/A |
| PRAC-05 | Phase insertion (`/gsd-insert-phase`) explained with scenario | automated | `powershell -Command "Select-String -Pattern 'gsd-insert-phase' companion.md"` | ❌ Wave 0 |
| PRAC-06 | Cross-AI review (`/gsd-review`) explained with scenario | automated | `powershell -Command "Select-String -Pattern 'gsd-review' companion.md"` | ❌ Wave 0 |
| PRAC-07 | Autonomous mode (`/gsd-autonomous`) explained with scenario | automated | `powershell -Command "Select-String -Pattern 'gsd-autonomous' companion.md"` | ❌ Wave 0 |

### Sampling Rate
- **Per task commit:** `Select-String` for newly added section headings and key content markers
- **Per wave merge:** Full structural validation — all 7 section headings present, all 3 advanced features mentioned, no Marp directives, TERMINOLOGY.md compliance spot-check
- **Phase gate:** Full suite green + manual standalone readability review before `/gsd-verify-work`

### Wave 0 Gaps
- None — validation uses built-in PowerShell `Select-String` which is always available. No framework install needed.

### TERMINOLOGY.md Compliance Check
```powershell
# Spot-check for forbidden Swedish terms in companion.md
$forbidden = @("fas ", " faserna", "vägkarta", "arbetsflöde", "orkestrerare", "milstolpe", "ramverk", "förmåga", "verifiering", "exekvering", "kontextfönster", "kodbas", "felsökning", "driftsätta")
$found = @()
foreach ($term in $forbidden) {
  $matches = Select-String -Pattern $term -Path companion.md -CaseSensitive
  if ($matches) { $found += "$term (line $($matches.LineNumber -join ', '))" }
}
if ($found.Count -gt 0) { Write-Warning "Forbidden Swedish terms found: $($found -join '; ')" }
else { Write-Host "TERMINOLOGY.md compliance: PASS" }
```
Note: Some false positives possible (e.g., "kodbas" appears in TERMINOLOGY.md itself as the allowed English term). Verification should review flagged terms in context.

## State of the Art

| Old Approach | Current Approach | When Changed | Impact |
|--------------|------------------|--------------|--------|
| Separate reference docs per feature | Single companion document with integrated advanced features | D-08 decision | Advanced features don't get their own appendix — they integrate naturally |
| Exhaustive command reference | Curated 10–15 command table | D-09 decision | Reference section stays scannable, not overwhelming |
| Slides + companion cross-dependency | Standalone companion with optional echoes | D-06 decision | Companion must fully self-explain every concept |

## Open Questions

1. **Autonomous mode subsection placement**
   - What we know: D-08 says natural sections, not a separate "Advanced" group. Phase insertion goes in Section 4, cross-AI review goes in Section 6.
   - What's unclear: Where autonomous mode fits best — it could go in Section 4 (as the "end-game" of full workflow), Section 6 (as an advanced best practice), or between Section 6 and Section 7 as a transitional "what's next" piece.
   - Recommendation: Place as a subsection at the end of Section 4 (Full Workflow) — the progression is: basic lifecycle → phase insertion → autonomous mode. This creates a natural "more trust = less friction" arc within the workflow section. If the agent prefers, between Section 6 and Section 7 also works.

2. **Exact command count for reference table**
   - What we know: D-09 says 10–15 commands. 14 candidates identified above.
   - What's unclear: Whether all 14 warrant inclusion or if some are too niche for a curated table.
   - Recommendation: Start with all 14. If it feels crowded during writing, cut the least essential 2-3 (likely `/gsd-verify-work`, `/gsd-progress`, `/gsd-debug` which are more situational).

3. **Depth of GSD vs BMAD in Appendix**
   - What we know: Slides have a 3-row philosophy contrast table. STATE.md notes BMAD comparison details are "MEDIUM confidence and may need validation."
   - What's unclear: How much deeper the appendix should go beyond the slide's philosophy contrast.
   - Recommendation: Keep it concise — expand to 4-5 comparison dimensions (approach, agents, workflow, documentation, best for) but stay at philosophy level. Don't attempt feature-by-feature comparison. This matches D-09 from Phase 5 (balanced, no feature matrix).

## Sources

### Primary (HIGH confidence)
- `companion.md` — Current outline structure (7 sections + appendix)
- `slides.md` — Complete presentation content (28 content slides across 8 sections)
- `TERMINOLOGY.md` — Authoritative term list for language consistency
- `.planning/phases/06-companion-document/06-CONTEXT.md` — All user decisions for this phase
- `.planning/REQUIREMENTS.md` — Requirement definitions for COMP-01, COMP-02, COMP-03, PRAC-05, PRAC-06, PRAC-07

### Secondary (HIGH confidence — project artifacts)
- `.planning/phases/04-scenarios-best-practices/04-RESEARCH.md` — Decision tree content, scenario patterns, GSD command details
- `.planning/phases/05-framing-intro-landscape/05-RESEARCH.md` — Agent framework concept, BMAD comparison, problem statement narrative
- `.planning/ROADMAP.md` — Phase 6 success criteria and requirements mapping
- `.planning/PROJECT.md` — Project constraints and core value

### Tertiary (MEDIUM confidence)
- GSD command knowledge from training data — verified against slide content and prior phase research, but exact command flags/behavior may differ in latest version

## Metadata

**Confidence breakdown:**
- Standard stack: HIGH — standard markdown authoring, no special tooling
- Architecture: HIGH — document structure is locked (D-05), content mapping is clear from slides
- Content patterns: HIGH — established across 5 prior phases with consistent voice and formatting
- Advanced features (PRAC-05/06/07): MEDIUM — content is about GSD features from training data, verified against slides and prior research but exact behavior may vary
- Pitfalls: HIGH — common documentation authoring pitfalls, well-understood

**Research date:** 2025-07-18
**Valid until:** 2025-08-18 (stable — content authoring patterns don't change rapidly)
