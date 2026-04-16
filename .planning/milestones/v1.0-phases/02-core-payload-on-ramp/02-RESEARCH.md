# Phase 2: Core Payload — On-Ramp - Research

**Researched:** 2026-04-15
**Domain:** Marp slide content — GSD command spectrum, terminal examples, installation, graduated complexity narrative
**Confidence:** HIGH

## Summary

Phase 2 delivers the "Börja enkelt" section (Section 4) of the Marp slide deck: the command spectrum visual, realistic terminal examples, getting started/installation slides, and the graduated complexity narrative. This is the first content phase — the skeleton from Phase 1 is in place with section dividers, CSS, and the insertion point at line 96 (`<!-- Section 4: The On-Ramp — slides added by Phase 2 -->`).

The core challenge is information design, not technology. The content must be accurate to the actual GSD command system (verified by reading the workflow source files), visually scannable from the back of a room (per D-12: spacious layout), and narratively compelling enough that skeptics think "I could start using this today." ASCII art for the spectrum visual must work inside Marp's code block rendering (0.85em font, 4px border-radius, already in the CSS). Terminal examples need to feel authentic — real developer scenarios, not contrived demos.

All GSD command details in this research were verified against the actual workflow source files (`~/.copilot/get-shit-done/workflows/fast.md`, `quick.md`, `do.md`, `new-project.md`, `help.md`) and the npm registry (`get-shit-done-cc@1.36.0`). The installation path is `npx get-shit-done-cc@latest`, which auto-detects the runtime environment (Copilot, Claude Code, Gemini, Codex, OpenCode).

**Primary recommendation:** Build 8–10 slides for this section: 1 command spectrum overview, 4 terminal examples (one per level), 2 installation/getting started slides, 1 gateway bridge slide, plus optional narrative connectors. Insert all after the Section 4 comment marker in slides.md.

<user_constraints>
## User Constraints (from CONTEXT.md)

### Locked Decisions
- **D-01:** Horizontal left-to-right progression — a "complexity dial" showing the path from simple to full workflow
- **D-02:** ASCII art in a code block — pure markdown, terminal-native feel, works everywhere
- **D-03:** Medium detail per level — command name + short description + "use when" hint
- **D-04:** Single spectrum slide only — punchy overview; deeper details come in follow-up slides per command
- **D-05:** Relatable developer scenarios — "fix a bug", "add a feature" — things the audience has done themselves
- **D-06:** Compact format — 3-5 lines per example: prompt + command + key output line. Readable from the back of the room
- **D-07:** One terminal example per spectrum level — `/gsd-fast`, `/gsd-quick`, `/gsd-do`, plus a full workflow tease (4 examples total)
- **D-08:** Standard `$` prompt style — clean and universal
- **D-09:** Step-by-step installation — prerequisites, install command, verify, first command (2+ slides)
- **D-10:** Copilot CLI only — show GitHub Copilot Extensions install path, no Claude Code
- **D-12:** Spacious layout — one idea per slide, more slides, easy to follow from the back of the room
- **D-14:** Section ends with a "gateway" tease — "but what if your task is bigger? That's the full workflow..." — bridges to Phase 3's "Hela livscykeln" section

### Agent's Discretion
- **D-11:** Installation slides ordering — before or after command spectrum (pick what flows best narratively)
- **D-13:** Total slide count for Section 4 (target comfortable pacing within ~60 min total across 8 sections)

### Deferred Ideas (OUT OF SCOPE)
None — discussion stayed within phase scope
</user_constraints>

<phase_requirements>
## Phase Requirements

| ID | Description | Research Support |
|----|-------------|------------------|
| SLIDE-03 | Visuell command spectrum — `/gsd-fast` → `/gsd-quick` → `/gsd-do` → full workflow | Verified all 4 command levels from GSD source. ASCII art pattern documented with exact command names, descriptions, and "use when" guidance. Fits in a single Marp code block at 0.85em. |
| SLIDE-04 | Realistiska terminal-exempel (code blocks med prompts och output) | 4 terminal examples designed from actual GSD workflow behavior: fast (typo fix), quick (add feature), do (smart router), full workflow (new project). Output patterns taken from real workflow step definitions. |
| PRAC-01 | Getting started — installation och första kommandot | Install path verified: `npx get-shit-done-cc@latest` (npm v1.36.0). Prerequisites: Node.js ≥18, VS Code + GitHub Copilot. First command: `/gsd-fast`. |
| PRAC-02 | On-ramp: börja light med `/gsd-fast` (≤3 edits, no planning) | `/gsd-fast` behavior verified from source: ≤3 file edits, no subagents, no PLAN.md, atomic commit, logs to STATE.md. Scope check auto-redirects to `/gsd-quick` if task is non-trivial. |
| PRAC-03 | Graduated complexity — `/gsd-quick` → `/gsd-do` → full workflow | Composable flag system verified: `--discuss`, `--research`, `--full` are independently addable. `/gsd-do` is a smart router/dispatcher. Full workflow = `/gsd-new-project` → plan → execute → verify. |
</phase_requirements>

## Project Constraints (from copilot-instructions.md)

- **GSD Workflow Enforcement:** All repo edits go through GSD commands — no direct edits outside a GSD workflow
- **Language:** Svenska with engelska facktermer (per TERMINOLOGY.md — "phase" not "fas", "workflow" not "arbetsflöde")
- **Format:** Marp markdown, 16:9, default theme, paginate: true
- **Tone:** Utbildande, inte säljande — "hur" rather than "varför"
- **Slide styling:** Section dividers use `<!-- _class: divider -->`, code blocks at 0.85em with 4px border-radius

## Standard Stack

### Core

| Library | Version | Purpose | Why Standard |
|---------|---------|---------|--------------|
| Marp CLI | 4.3.1 | Slide rendering from markdown | Mandated by project. Verified on npm (published 2026-03-16). |
| Marp Core | 4.3.0 | Rendering engine (bundled with CLI) | Provides highlight.js for code block syntax highlighting |
| VS Code + Marp Extension | latest | Live preview during authoring | Instant feedback for slide layout adjustments |

### Supporting

No additional dependencies for this phase. Content is pure Marp markdown inserted into the existing `slides.md`.

## Architecture Patterns

### Slide Insertion Pattern

All new slides are inserted after the Section 4 comment marker in `slides.md`:

```markdown
<!-- Section 4: The On-Ramp — slides added by Phase 2 -->

---

<!-- new slide content here -->
```

Each new content slide starts with `---` (Marp slide separator). No `_class` directive needed for regular content slides — only dividers use `<!-- _class: divider -->`.

### Recommended Slide Structure for Section 4

```
Section 4 divider (already exists at line 91-92)
├── Slide 4.1: Command Spectrum Visual (the "slide people photograph")
├── Slide 4.2: /gsd-fast — terminal example
├── Slide 4.3: /gsd-quick — terminal example  
├── Slide 4.4: /gsd-do — terminal example
├── Slide 4.5: Full workflow — terminal example (tease)
├── Slide 4.6: Installation — prerequisites + install command
├── Slide 4.7: Installation — verify + first command
├── Slide 4.8: Gateway bridge — "men om uppgiften är större?" → Section 5
```

**Rationale for ordering (Agent's Discretion D-11):** Spectrum first, then examples that prove each level works, then "here's how to get started", then bridge forward. This order follows the persuasion arc: *show the menu → prove it's real → show how to order → tease what's next*. Installation after examples is better than before because the audience needs to *want* GSD before they care *how* to install it.

**Slide count (Agent's Discretion D-13):** 8 slides for Section 4. With 8 sections in the full deck and ~60 minutes total, each section averages ~7.5 minutes. 8 slides at ~45-60 seconds each = ~6-8 minutes, which fits well. This is the on-ramp — it should move briskly to build momentum.

### Pattern: ASCII Art Command Spectrum in Marp

The spectrum visual (D-01, D-02, D-03, D-04) must fit in a single Marp code block. Key constraints:

- Marp renders code blocks with `highlight.js` — use a plain text fence (no language specifier) to avoid syntax coloring
- Code blocks use 0.85em font (from existing CSS) — approximately 80-90 characters per line on 16:9
- Horizontal left-to-right progression needs to fit within this width
- Medium detail: command name + 1-line description + "use when" hint

**Recommended approach:**

````markdown
```
 /gsd-fast          /gsd-quick             /gsd-do            Full Workflow
 ─────────          ──────────             ───────            ─────────────
 Fix a typo         Add a feature          "Just do it"       New project
 ≤3 file edits      Plan → Execute         Smart router       Plan → Execute → Verify
 No planning        + --discuss             Routes intent     Phases, milestones,
 Just do it.        + --research            to right command  persistent memory
                    + --full
                    
 ◄── enklare ─────────────────────────────────────── mer struktur ──►
```
````

This fits within ~85 characters width and shows all 4 levels with the "complexity dial" metaphor.

### Pattern: Terminal Examples in Marp

Terminal examples (D-05, D-06, D-07, D-08) use fenced code blocks with `bash` or `shell` language for syntax highlighting. Key patterns:

- `$` prompt prefix (D-08)
- 3-5 lines max per example (D-06)
- Show command + key output, not full verbose output
- Relatable scenarios (D-05)

**Font size consideration:** The existing CSS sets `pre` at 0.85em. For terminal examples that need to be readable from the back of the room, this is fine for 3-5 lines. Do NOT add more lines — it defeats the purpose.

### Pattern: Slide Text in Swedish with English Terms

Per TERMINOLOGY.md, slide text follows svengelska conventions:

```markdown
## Börja med `/gsd-fast`

Perfekt för triviala ändringar — en typo, en config-ändring, en glömd import.

- ≤ 3 file edits, ingen planning
- Atomic commit med conventional message
- Loggas i STATE.md automatiskt
```

Key term usage: "file edits" (not "filändringar"), "planning" (not "planering"), "commit" (not "incheckning"), "workflow" (not "arbetsflöde"). Swedish grammar with English nouns.

### Anti-Patterns to Avoid

- **Wall of text slides:** D-12 demands spacious layout. One idea per slide. If a slide has more than ~5 bullet points, it needs splitting.
- **Verbose terminal output:** D-06 says 3-5 lines. Don't show full GSD banners, progress bars, or multi-step output. Show the *essence*: command → key result.
- **Technical accuracy over clarity:** The spectrum visual is a teaching tool, not documentation. Slight simplification is acceptable if it serves comprehension.
- **Mixing languages awkwardly:** Don't switch language mid-sentence without reason. Follow TERMINOLOGY.md patterns — English terms in Swedish grammar flow.
- **Forgetting the section divider exists:** The "Börja enkelt" divider slide already exists at line 91-92. Don't recreate it.

## Verified GSD Command Details

Source: Actual workflow files at `~/.copilot/get-shit-done/workflows/` (v1.29.0 installed, v1.36.0 on npm)

### `/gsd-fast` — Trivial Inline Execution

| Property | Value |
|----------|-------|
| **Purpose** | Execute trivial task inline, no subagent overhead |
| **Scope limit** | ≤3 file edits, ≤1 minute, no new dependencies, no research |
| **Creates** | Nothing — no PLAN.md, no SUMMARY.md |
| **Agents** | None — runs inline in current context |
| **Output** | Atomic git commit + logs to STATE.md |
| **Auto-redirect** | If task is non-trivial → suggests `/gsd-quick` |
| **Example tasks** | Fix typo, update config, add missing import, rename variable, add .gitignore entry |
| **Commit style** | Conventional: `fix:`, `feat:`, `docs:`, `chore:`, `refactor:` |

**Plausible terminal example:**
```
$ /gsd-fast "add .env to .gitignore"
✅ Done: Added .env to .gitignore
   Commit: a3f2e1d
   Files: .gitignore
```

### `/gsd-quick` — Small Tasks with Planning

| Property | Value |
|----------|-------|
| **Purpose** | Execute small ad-hoc tasks with GSD guarantees |
| **Creates** | `.planning/quick/NNN-slug/PLAN.md` + `SUMMARY.md` |
| **Agents** | Planner + Executor (spawned as subagents) |
| **Flags** | `--discuss` (surface gray areas), `--research` (investigate approaches), `--full` (plan checking + verification) |
| **Composable** | All flags combine: `--discuss --research --full` |
| **Tracking** | Updates STATE.md "Quick Tasks Completed" table |
| **Requirement** | Needs active project with ROADMAP.md |

**Plausible terminal example:**
```
$ /gsd-quick "add dark mode toggle to settings page"
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 GSD ► QUICK TASK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Planning... 3 tasks identified
Executing... ██████████ 3/3
✅ Done — dark mode toggle added
```

### `/gsd-do` — Smart Router / Dispatcher

| Property | Value |
|----------|-------|
| **Purpose** | Analyze freeform text, route to best GSD command |
| **Creates** | Nothing — it's a dispatcher |
| **Behavior** | Matches intent to routing table, confirms, hands off |
| **Ambiguity** | Asks user to pick between top 2-3 options |
| **Key insight** | Never does the work itself — routes to the right specialist |

**Routing examples from source:**
| User says | Routes to |
|-----------|-----------|
| "fix the login button" | `/gsd-quick` or `/gsd-debug` |
| "refactor the auth system" | `/gsd-add-phase` |
| "start a new project" | `/gsd-new-project` |
| "where am I?" | `/gsd-progress` |

**Plausible terminal example:**
```
$ /gsd-do "refactor the auth system"
 GSD ► ROUTING
 Input: refactor the auth system
 Routing to: /gsd-add-phase
 Reason: Multi-file refactor needs full phase
```

### Full Workflow — `/gsd-new-project` → Plan → Execute → Verify

| Property | Value |
|----------|-------|
| **Purpose** | Full project lifecycle from idea to completion |
| **Flow** | `new-project` → deep questioning → research → requirements → roadmap → plan → execute → verify |
| **Creates** | Full `.planning/` directory: PROJECT.md, REQUIREMENTS.md, ROADMAP.md, STATE.md, research/ |
| **Agents** | 18+ specialized agents: researcher, planner, executor, verifier, etc. |
| **Key features** | Persistent project memory, wave-based execution, phase lifecycle |
| **Session continuity** | `/gsd-resume-work`, `/gsd-progress` |
| **Quality gates** | Plan checking, goal-backward verification |

**Plausible terminal example (tease — not full detail):**
```
$ /gsd-new-project
 Vad vill du bygga? > En REST API för kundhantering
 Researching domain... 4 parallel agents
 Requirements defined: 12 items
 Roadmap: 5 phases created
 Ready: /gsd-plan-phase 1
```

### Installation Path

**Decision D-10:** Show GitHub Copilot Extensions install path only, no Claude Code.

**Verified from npm registry and GSD update workflow:**

| Step | Command / Action |
|------|-----------------|
| **Prerequisites** | Node.js ≥18 LTS, VS Code with GitHub Copilot extension |
| **Install** | `npx get-shit-done-cc@latest` |
| **What happens** | Installer auto-detects runtime (Copilot/Claude/Gemini/Codex), installs to `~/.copilot/get-shit-done/` for Copilot |
| **Verify** | `/gsd-help` in Copilot Chat |
| **Update** | Same command: `npx get-shit-done-cc@latest` |
| **First command** | `/gsd-fast "fix a typo"` — instant gratification, zero project setup needed |

**Note for slides:** The `npx get-shit-done-cc@latest` command works regardless of runtime but the presentation focuses on Copilot per D-10. Don't mention Claude Code, OpenCode, Gemini, or Codex install paths.

**Important nuance:** `/gsd-fast` works without a project (no `.planning/` needed for STATE.md logging — it skips silently). `/gsd-quick` requires an active project. This makes `/gsd-fast` the perfect first command for the "first taste" slide.

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| Slide rendering | Custom HTML/CSS slide system | Marp's built-in markdown rendering | Already configured in Phase 1 with correct themes and CSS |
| Code syntax highlighting | Manual formatting | Marp's bundled highlight.js | Automatically applies to fenced code blocks |
| Slide pagination | Manual numbering | `paginate: true` in front matter | Already set globally in slides.md |
| Terminal-looking code blocks | Custom CSS per block | Standard fenced code blocks with `bash` language tag | The existing CSS styles all `pre` blocks at 0.85em |

## Common Pitfalls

### Pitfall 1: ASCII Art Breaking on Different Screen Sizes
**What goes wrong:** The command spectrum ASCII art looks great in VS Code preview but breaks when projected or rendered to PDF at different sizes.
**Why it happens:** Monospace fonts have different metrics across renderers. Line lengths that look fine in one font wrap in another.
**How to avoid:** Keep ASCII art lines under 80 characters. Test in both VS Code Marp preview AND actual PDF/HTML output. Use simple box-drawing characters (─, │, ├, └) that render consistently.
**Warning signs:** Lines wrapping in preview, characters misaligning.

### Pitfall 2: Too Much Output in Terminal Examples
**What goes wrong:** Terminal examples show 10+ lines of realistic GSD output, making them unreadable from the back of the room.
**Why it happens:** Desire for accuracy overwhelms readability. Real GSD output includes banners, progress bars, subagent spawning messages.
**How to avoid:** D-06 says 3-5 lines max. Show: prompt + command (1 line), key status (1-2 lines), result (1 line). Cut everything else.
**Warning signs:** Needing to reduce font size to fit a terminal example.

### Pitfall 3: Inconsistent Language Mixing
**What goes wrong:** Some slides use "planering" while others use "planning". Some use "verktyg" while others use "tool".
**Why it happens:** TERMINOLOGY.md has 20+ terms but it's easy to forget mid-authoring.
**How to avoid:** Cross-reference TERMINOLOGY.md for every slide. Key terms for this phase: phase, workflow, commit, planning, execution, verification, codebase, debugging, on-ramp.
**Warning signs:** A slide that reads like "pure Swedish" probably has an unintentional translation.

### Pitfall 4: Section Divider Duplication
**What goes wrong:** Creating a new "Börja enkelt" divider slide when one already exists at line 91-92.
**Why it happens:** Not reading the existing slides.md carefully enough.
**How to avoid:** Insert content AFTER line 96 (`<!-- Section 4: The On-Ramp — slides added by Phase 2 -->`). The section divider at lines 91-92 is already there and correct.
**Warning signs:** Two consecutive divider slides in Section 4.

### Pitfall 5: Forgetting the Gateway Bridge
**What goes wrong:** Section 4 ends abruptly after installation without bridging to Section 5 ("Hela livscykeln").
**Why it happens:** Focus on the on-ramp content makes you forget the narrative arc.
**How to avoid:** D-14 explicitly requires a gateway tease slide. Last slide in Section 4 should create curiosity about the full workflow. Something like: "Men vad händer när uppgiften är större?" → leads into Phase 3's content.
**Warning signs:** Section 4 feels like it ends with "install GSD" instead of building forward momentum.

### Pitfall 6: `/gsd-fast` vs `/gsd-quick` Confusion
**What goes wrong:** Slides blur the distinction between fast and quick, making the spectrum feel like two similar options.
**Why it happens:** Both handle "small tasks" — the distinction (no planning vs. planning with subagents) is subtle.
**How to avoid:** Emphasize the bright line: `/gsd-fast` = zero overhead, inline, ≤3 edits, no files created. `/gsd-quick` = lightweight planning, planner + executor agents, creates PLAN.md. The difference is *planning*, not *size*.
**Warning signs:** Audience couldn't explain when to use fast vs. quick.

## Code Examples

### Example 1: Marp Slide with Terminal Example

```markdown
---

## `/gsd-fast` — noll overhead

Perfekt för triviala ändringar. Ingen planning, inga subagents.

```bash
$ /gsd-fast "add .env to .gitignore"
✅ Done: Added .env to .gitignore
   Commit: a3f2e1d
   Files: .gitignore
```

≤ 3 file edits → automatic commit → loggat i STATE.md
```

### Example 2: Command Spectrum Slide

```markdown
---

## Command Spectrum

```
  /gsd-fast        /gsd-quick          /gsd-do          Full Workflow
  ─────────        ──────────          ───────          ─────────────
  Fixa en typo     Lägg till feature   Beskriv vad      Helt nytt projekt
  ≤3 edits         Plan → Execute      du vill göra     Phases, roadmap,
  Ingen planning   Composable flags:   → smart routing  research, verify
                   --discuss
                   --research
                   --full

  ◄── enklare ──────────────────────────────── mer struktur ──►
```

Börja till vänster. Flytta höger när du behöver mer.
```

### Example 3: Installation Slide

```markdown
---

## Kom igång — 3 steg

**1. Förutsättningar**
- Node.js ≥18 och VS Code med GitHub Copilot

**2. Installera**
```bash
$ npx get-shit-done-cc@latest
```

**3. Kör ditt första kommando**
```bash
$ /gsd-fast "fix the typo in README"
✅ Done — zero setup needed
```
```

### Example 4: Gateway Bridge Slide

```markdown
---

## Men om uppgiften är större?

`/gsd-fast` fixar typon.
`/gsd-quick` lägger till en feature.

Men tänk om du ska bygga en hel REST API?
Eller refaktorera ett auth-system?

**Då behöver du hela workflow:en.**

*Nästa: Hela livscykeln →*
```

## Validation Architecture

### Test Framework

| Property | Value |
|----------|-------|
| Framework | Marp CLI 4.3.1 (slide rendering validation) |
| Config file | Front matter in `slides.md` |
| Quick run command | `npx @marp-team/marp-cli slides.md --html -o /dev/null 2>&1` (validates markdown parses) |
| Full suite command | `npx @marp-team/marp-cli slides.md -o slides.html && start slides.html` (visual inspection) |

### Phase Requirements → Test Map

| Req ID | Behavior | Test Type | Automated Command | File Exists? |
|--------|----------|-----------|-------------------|-------------|
| SLIDE-03 | Command spectrum visual renders correctly in code block | manual-only | Visual inspection of Marp preview | ❌ Content not yet created |
| SLIDE-04 | Terminal examples render with syntax highlighting | manual-only | Visual inspection of Marp preview | ❌ Content not yet created |
| PRAC-01 | Installation steps are accurate and complete | manual-only | Verify `npx get-shit-done-cc@latest` command works | ❌ Content not yet created |
| PRAC-02 | `/gsd-fast` example is realistic and accurate | manual-only | Cross-reference with `/gsd-fast` workflow source | ❌ Content not yet created |
| PRAC-03 | Graduated complexity shows clear progression | manual-only | Review spectrum visual + examples for clarity | ❌ Content not yet created |

**Justification for manual-only:** This phase creates presentation content (Marp slides), not code. Validation is inherently visual — does the slide look right when rendered? Is the ASCII art aligned? Are terminal examples readable? Automated tests cannot assess these qualities. The key validation is Marp rendering + visual review.

### Sampling Rate
- **Per task commit:** Render slides in VS Code Marp preview and verify new slides display correctly
- **Per wave merge:** Full `npx @marp-team/marp-cli slides.md -o slides.html` build + visual review
- **Phase gate:** All new slides render correctly, ASCII art aligned, terminal examples highlighted, no broken markdown

### Wave 0 Gaps
None — existing Marp infrastructure from Phase 1 covers all rendering needs. No test framework to install for content authoring.

## Open Questions

1. **Exact character width for ASCII art on projected 16:9**
   - What we know: Marp renders code blocks at 0.85em in the default theme. At 16:9 this gives roughly 80-90 chars per line.
   - What's unclear: The exact character count depends on the audience's projector resolution and the specific monospace font Marp uses (system-dependent).
   - Recommendation: Keep ASCII art under 75 characters wide for safety margin. Test with actual Marp HTML output at full screen.

2. **`/gsd-fast` without a project — exact STATE.md behavior**
   - What we know: The fast.md workflow says "if `.planning/STATE.md` exists, append to table. If table doesn't exist, skip silently."
   - What's unclear: Can you literally run `/gsd-fast` in an empty directory? (Probably yes — it just skips the STATE.md step)
   - Recommendation: For the installation slide, show `/gsd-fast` as the first command. It works even without a project, making it the perfect zero-friction entry.

## Sources

### Primary (HIGH confidence)
- `~/.copilot/get-shit-done/workflows/fast.md` — Full `/gsd-fast` workflow definition (scope limits, output format, guardrails)
- `~/.copilot/get-shit-done/workflows/quick.md` — Full `/gsd-quick` workflow definition (flags, subagent spawning, composability)
- `~/.copilot/get-shit-done/workflows/do.md` — Full `/gsd-do` routing table and dispatcher behavior
- `~/.copilot/get-shit-done/workflows/new-project.md` — Full workflow initialization flow
- `~/.copilot/get-shit-done/workflows/help.md` — Complete GSD command reference (all commands with usage examples)
- `npm view get-shit-done-cc` — npm registry: v1.36.0, description confirms multi-runtime support
- `slides.md` (repo) — Existing Marp skeleton, CSS, section structure, insertion points
- `TERMINOLOGY.md` (repo) — Language policy for Swedish/English term usage

### Secondary (MEDIUM confidence)
- `~/.copilot/get-shit-done/workflows/update.md` — Installation/update mechanism (confirmed `npx get-shit-done-cc@latest`)

## Metadata

**Confidence breakdown:**
- Standard stack: HIGH — Same as Phase 1, no new tools
- Architecture: HIGH — Marp slide patterns verified, command details verified from source
- Pitfalls: HIGH — Based on concrete Marp rendering constraints and content design principles
- Command accuracy: HIGH — All command details verified against actual workflow source files

**Research date:** 2026-04-15
**Valid until:** 2026-05-15 (stable — Marp and GSD commands unlikely to change significantly)
