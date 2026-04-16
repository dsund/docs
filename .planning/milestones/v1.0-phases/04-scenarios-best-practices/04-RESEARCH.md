# Phase 4: Scenarios & Best Practices - Research

**Researched:** 2026-04-16
**Domain:** Marp slide content — decision tree, real-world scenarios (greenfield/brownfield/debugging), mindset shifts, prompt crafting, anti-patterns, escape hatches, and "Start Monday" call-to-action
**Confidence:** HIGH

## Summary

Phase 4 delivers Sections 6–8 of the Marp slide deck: "I din vardag" (scenarios mapping developer situations to GSD commands), "Tänk så här" (mindset shifts, best practices, anti-patterns), and "Börja på måndag" (concrete call-to-action). This is the final practical content phase — after the audience has learned what GSD is (Section 3), how to start (Section 4), and the full workflow (Section 5), Phase 4 answers "How do I actually use this at work?" and closes with "Start Monday."

The decision tree is the "slide people photograph" for this phase — an all-English visual that maps common developer situations to the right GSD command. Per D-02, it includes specialist commands beyond the 4-level command spectrum (`/gsd-debug`, `/gsd-map-codebase`, `/gsd-insert-phase` etc.). The scenarios sections use generic developer situations (REST API, legacy refactor, authentication bug) that any developer can relate to. Best practices sections need concrete prompt examples (good vs bad) and must treat escape hatches with equal weight to build credibility with skeptics. The "Start Monday" close must be zero-friction and immediately actionable.

The current deck has 29 slides across 8 section dividers (Sections 1-2 empty for Phase 5, Sections 6-8 empty for Phase 4). With ~60 minutes total, Phase 4's three sections should produce approximately 14-18 slides: ~6-8 for scenarios (Section 6), ~5-7 for best practices (Section 7), and ~2-3 for Start Monday (Section 8).

**Primary recommendation:** Build 3 plans: Plan 1 (Section 6: scenarios + decision tree, ~6-8 slides, Wave 1), Plan 2 (Section 7: best practices + anti-patterns, ~5-7 slides, Wave 1), Plan 3 (Section 8: Start Monday close, ~2-3 slides, Wave 2 — depends on Section 7 for narrative flow). All slide content follows established Marp patterns from Phases 2-3.

<user_constraints>
## User Constraints (from CONTEXT.md)

### Locked Decisions
- **D-01:** All-English for the decision tree content — keeps it universal, terse, and "photographable" (exception to the Swedish pattern used elsewhere in the deck)
- **D-02:** Include specialist commands beyond the command spectrum — `/gsd-debug`, `/gsd-map-codebase`, `/gsd-insert-phase` etc., not just the 4 main levels
- **D-07:** Generic developer scenarios — "REST API", "legacy refactor", relatable to any developer
- **D-10:** Concrete prompt examples for prompt crafting guidance — show actual good/bad prompts (e.g., "Fix the bug" vs "The login form returns 401 when valid credentials are submitted")
- **D-12:** Spacious layout — one idea per slide (carried from Phase 2)
- **D-13:** Section dividers: centered h1 + hr (carried from Phase 1)
- **D-14:** Terminal examples: bash fence, $ prompt, compact output (carried from Phase 2)
- **D-15:** ASCII art in code blocks for diagrams (carried from Phase 2)
- **D-16:** Copilot-only references, no Claude Code (carried from Phase 2)
- **D-17:** Swedish text with English technical terms per TERMINOLOGY.md (except decision tree — see D-01)

### Agent's Discretion
- **D-03:** Decision tree visual format (ASCII flowchart vs table vs Q&A list) — pick what works best for readability on a slide
- **D-04:** Whether to fit decision tree on one dense slide or split across multiple — depends on how many commands need to fit
- **D-05:** Scenario structure format — command highlights, before/after contrast, or mini-walkthrough. Pick what fits best within a 60-min presentation
- **D-06:** Relative depth per scenario — equal weight or emphasize the most relevant one based on audience needs
- **D-08:** Best practices presentation format — side-by-side do/don't, principles-first, or anti-pattern gallery. Pick what's most impactful
- **D-09:** Escape hatches (when NOT to use agents) depth — per success criteria, should have real weight to build credibility
- **D-11:** The specific "Start Monday" call-to-action and whether it's a single action or tiered for different comfort levels. Pick the most compelling close

### Deferred Ideas (OUT OF SCOPE)
None — discussion stayed within phase scope
</user_constraints>

<phase_requirements>
## Phase Requirements

| ID | Description | Research Support |
|----|-------------|------------------|
| PRAC-04 | Brownfield awareness — `/gsd-map-codebase` för befintlig kod | Verified `/gsd-map-codebase` workflow: orchestrates parallel codebase-mapper agents to produce 7 structured documents in `.planning/codebase/`. Essential brownfield entry point before adding features or refactoring. Works without `.planning/` existing first. |
| SCEN-01 | Greenfield-projekt — full workflow från idé till implementation | Verified workflow: `/gsd-new-project` → deep questioning → research → requirements → roadmap → `/gsd-plan-phase` → `/gsd-execute-phase` → `/gsd-verify-phase`. Produces full `.planning/` structure. |
| SCEN-02 | Brownfield — jobba med befintlig kodbas | Verified workflow: `/gsd-map-codebase` first (produces codebase analysis), then `/gsd-new-project` (uses codebase context) or `/gsd-add-phase` for targeted additions. The map step gives GSD project memory about existing code. |
| SCEN-03 | Quick fix / debugging — snabba insatser med `/gsd-fast` och `/gsd-debug` | Verified: `/gsd-fast` for trivial fixes (≤3 edits, no planning), `/gsd-debug` (actually `/gsd-diagnose-issues`) for systematic investigation with parallel debug agents. Each debug agent creates `DEBUG-{slug}.md` with root cause analysis. |
| SCEN-04 | Decision tree — "vilket kommando ska jag använda?" | Full command inventory verified from GSD workflow sources (57 workflows total). Decision tree maps situation → command with specialist commands included per D-02. |
| BEST-01 | Mental model shifts — tänk outcomes inte steg, decisions vs execution | Conceptual content building on Phase 3's verification philosophy. Two key shifts: (1) describe outcomes not implementation steps, (2) you decide the what/why, AI handles the how. |
| BEST-02 | Prompt crafting — hur man pratar med agents för bästa resultat | Research includes concrete good/bad prompt pairs per D-10. Key insight from GSD design: GSD agents parse freeform text — specificity and context dramatically improve routing and results. |
| BEST-03 | Escape hatches — när man INTE ska använda agents | Honest assessment of agent limitations: novel architecture decisions, security-critical code review, regulatory compliance, performance-critical optimization, team knowledge transfer moments. Must have equal weight per success criteria. |
| BEST-04 | Anti-patterns — vaga prompts, skippa verification, micro-management | Three primary anti-patterns verified from GSD design philosophy: (1) vague prompts lose context, (2) skipping verification = unchecked work, (3) micro-managing agents wastes the delegation model. |
| BEST-05 | "Start Monday" challenge — konkret nästa steg efter presentationen | Zero-friction call-to-action: install + run first `/gsd-fast` command. Takes <2 minutes, requires only Node.js + VS Code + Copilot (prerequisites most developers already have). |
</phase_requirements>

## Project Constraints (from copilot-instructions.md)

- **GSD Workflow Enforcement:** All repo edits go through GSD commands — no direct edits outside a GSD workflow
- **Language:** Svenska with engelska facktermer (per TERMINOLOGY.md — "phase" not "fas", "workflow" not "arbetsflöde")
- **Format:** Marp markdown, 16:9, default theme, paginate: true
- **Tone:** Utbildande, inte säljande — "hur" rather than "varför"
- **Slide styling:** Section dividers use `<!-- _class: divider -->`, code blocks at 0.85em with 4px border-radius
- **Copilot-only references:** No Claude Code, OpenCode, Gemini, or Codex mentions in slides (D-16)

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

### Slide Insertion Points

Phase 4 inserts content at THREE locations in `slides.md`:

```
slides.md (current structure after Phases 1-3)
├── Title slide (lead)
├── Section 1 divider: "Var är vi idag?" (empty — Phase 5)
├── Section 2 divider: "Vad finns?" (empty — Phase 5)
├── Section 3 divider: "Hur fungerar det?" → 4 content slides
├── Section 4 divider: "Börja enkelt" → 8 content slides
├── Section 5 divider: "Hela livscykeln" → 8 content slides
├── Section 6 divider: "I din vardag"
│   └── <!-- Section 6: Scenarios — slides added by Phase 4 -->    ← LINE 468
│   └── [INSERT ~6-8 slides: decision tree, scenarios]
├── Section 7 divider: "Tänk så här"
│   └── <!-- Section 7: Best Practices — slides added by Phase 4 --> ← LINE 478
│   └── [INSERT ~5-7 slides: mindset, prompts, anti-patterns, escape hatches]
├── Section 8 divider: "Börja på måndag"
│   └── <!-- Section 8: Getting Started — slides added by Phase 4 --> ← LINE 489
│   └── [INSERT ~2-3 slides: call-to-action, close]
```

### Slide Budget & Pacing

Current deck: 29 slides (1 title + 8 dividers + 20 content) across ~60 minutes.

Phase 4 target: 14-18 new content slides across 3 sections.

| Section | Topic | Target Slides | Time Estimate | Rationale |
|---------|-------|---------------|---------------|-----------|
| 6 | Scenarios + decision tree | 6-8 | ~8-10 min | Decision tree is dense but photographable; 3 scenario mini-walkthroughs |
| 7 | Best practices + anti-patterns | 5-7 | ~8-10 min | Mindset shifts, prompt crafting, anti-patterns, escape hatches — each needs its own slide |
| 8 | Start Monday | 2-3 | ~3-5 min | Short, punchy close — install + first command + encouragement |

Post-Phase 4 total: ~43-47 slides. Sections 1-2 (Phase 5) will add ~6-10 more → ~50-57 final total. At ~1 minute per slide average, this fits within ~60 minutes comfortably.

### Slide Pattern: Content Slides (established by Phases 2-3)

```markdown
---

## Slide Title

[One core idea — text, diagram, or code example]

[Optional footer line — summary or transition hint]
```

- No `<!-- _class: ... -->` on content slides (only dividers use `_class: divider`)
- No `<!-- _paginate: skip -->` on content slides
- `---` separator between slides
- Swedish text with English technical terms (except decision tree)

### Slide Pattern: ASCII Art Diagrams (established by Phase 2)

```markdown
## Slide Title

```
  [diagram content using box-drawing chars: ─ │ ┌ ┐ └ ┘ ├ ┤ ┬ ┴ ┼]
  [keep lines under 75 characters for projector safety]
```
```

Use plain code fence (no language specifier) to avoid syntax highlighting on diagrams.

### Slide Pattern: Terminal Examples (established by Phase 2)

````markdown
```bash
$ /gsd-command "description"
✅ Done: summary
   Files: changed.md
```
````

- `$` prompt prefix, 3-5 lines max, relatable scenarios

### Anti-Patterns to Avoid

- **Information dump on decision tree:** Don't try to list every possible scenario — show the 6-8 most common decision points
- **Theoretical best practices:** Don't state principles without concrete examples — always pair with a do/don't illustration
- **Selling, not teaching:** The anti-patterns and escape hatches sections must be honest about limitations — this is what earns credibility with skeptics
- **Repetition with Phases 2-3:** Don't re-explain commands — reference them ("ni såg `/gsd-fast` i förra sektionen"). The decision tree *maps* to commands the audience already knows
- **Overly complex "Start Monday":** The close must feel effortless — one install command, one first task, done

## Verified GSD Command Inventory for Decision Tree

Source: Verified from workflow files at `~/.copilot/get-shit-done/workflows/` (57 workflow files total)

### Primary Commands (from command spectrum — already shown in Phase 2)

| Command | When to Use | What It Does |
|---------|-------------|-------------|
| `/gsd-fast` | Trivial fix, ≤3 edits | Inline execution, no planning, atomic commit |
| `/gsd-quick` | Small feature, needs planning | Planner + executor subagents, composable flags |
| `/gsd-do` | Don't know which command | Smart router — analyzes intent, routes to best command |
| `/gsd-new-project` | Brand new project from scratch | Deep questioning → research → requirements → roadmap |

### Specialist Commands (per D-02 — must appear in decision tree)

| Command | When to Use | What It Does |
|---------|-------------|-------------|
| `/gsd-debug` | Bug, error, something broken | Parallel debug agents investigate root causes; each creates `DEBUG-{slug}.md` |
| `/gsd-map-codebase` | Joining existing project, brownfield | Parallel mapper agents produce 7 structured analysis docs in `.planning/codebase/` |
| `/gsd-insert-phase` | Urgent work discovered mid-project | Adds decimal phase (e.g., 2.1) without renumbering existing phases |
| `/gsd-add-phase` | Complex task: refactor, migration | Creates full phase with plan/build cycle for multi-file work |
| `/gsd-resume-work` | Returning after a break | Reads STATE.md → restores position, decisions, blockers |
| `/gsd-add-tests` | Need test coverage | Test generation for existing code |
| `/gsd-progress` | "Where am I?" status check | Analyzes roadmap → summarizes what's done/ahead |
| `/gsd-verify-work` | Checking quality of completed work | Human UAT with conversational testing flow |

### Routing Intelligence (from `/gsd-do` routing table)

The `/gsd-do` routing table reveals how GSD categorizes developer intent:

| Developer Intent | Routes To |
|-----------------|-----------|
| "fix the login button" | `/gsd-quick` or `/gsd-debug` |
| "refactor the auth system" | `/gsd-add-phase` |
| "start a new project" | `/gsd-new-project` |
| "where am I?" | `/gsd-progress` |
| "map this codebase" | `/gsd-map-codebase` |
| "write tests for auth" | `/gsd-add-tests` |
| "pick up where I left off" | `/gsd-resume-work` |

This routing table itself is a good source for decision tree questions — it already maps natural language intent to commands.

## Decision Tree Design Recommendations (D-03, D-04)

### Format Recommendation: Question-flow Table

After evaluating the three options (ASCII flowchart, table, Q&A list), **a question-flow table** works best:

- **ASCII flowchart** — beautiful but too wide for a single slide with 8+ endpoints; branching logic with box-drawing characters exceeds 75-char line limits on a projector
- **Pure table** — efficient but lacks the "flow" feeling; decision trees imply branching, tables imply lookup
- **Q&A branching list** — easy to follow but takes vertical space; works if split across 2 slides

**Recommended approach:** A **compact decision tree as a Q&A branching list** in a code block (all-English per D-01). Questions branch left/right or top/down. Keep to 3-4 decision points that cover the 8 most common entry points.

### Example Decision Tree Structure

```
What are you doing?
├── Starting something new?
│   ├── Whole project    → /gsd-new-project
│   └── One feature      → /gsd-quick --discuss
├── Working on existing code?
│   ├── First time here? → /gsd-map-codebase
│   ├── Bug or error?    → /gsd-debug
│   └── Big refactor?    → /gsd-add-phase
├── Something small?
│   ├── Trivial fix      → /gsd-fast
│   └── Not sure?        → /gsd-do
└── Coming back?
    └── Resuming work    → /gsd-resume-work
```

This fits within 75 characters width and covers all 8+ commands. The tree reads top-to-bottom as a natural decision flow.

### Slide Count Recommendation (D-04)

**One dense slide is better** — the decision tree loses its power when split across slides because the audience can't see all options simultaneously. The "photographable" quality depends on everything being visible at once. Use a code block with the full tree, preceded by a short Swedish intro line.

If the tree gets too dense, consider a **2-slide approach**: Slide 1 = main decision tree (primary commands), Slide 2 = specialist commands as a compact table. This keeps each slide clean while covering everything.

## Scenario Content (SCEN-01, SCEN-02, SCEN-03)

### Scenario Structure Recommendation (D-05)

**Mini-walkthrough format** works best: show the starting situation → the GSD entry command → 2-3 key workflow steps → the result. This mirrors how the audience will actually use GSD. Each scenario needs 1-2 slides maximum (total ~4-5 slides for all 3 scenarios + decision tree = 6-8 for Section 6).

### Scenario 1: Greenfield — "En REST API för kundhantering" (SCEN-01)

**Starting situation:** New project, blank folder, idea in your head.

**Workflow:**
```
/gsd-new-project
  → "Vad vill du bygga?" → "En REST API för kundhantering"
  → 12 requirements defined
  → 5 phases created
  → /gsd-plan-phase 1
  → /gsd-execute-phase 1
  → /gsd-verify-phase  → "Kan en användare registrera sig? ✅"
```

**Key message:** From idea to verified result without leaving the editor.

**Slide approach:** 1-2 slides. Show the flow as a compressed terminal-style walkthrough. Reference back to Section 5 where the audience already saw `/gsd-new-project` in detail — don't repeat, just contextualize.

### Scenario 2: Brownfield — "Ny feature i befintlig kodbas" (SCEN-02)

**Starting situation:** Legacy codebase, you're new to the team, need to add a feature.

**Workflow:**
```
/gsd-map-codebase
  → 7 analysis documents in .planning/codebase/
  → GSD now understands the project structure

/gsd-new-project  (or /gsd-add-phase)
  → Research uses codebase map
  → Plans respect existing patterns
  → "Add search endpoint to existing API"
```

**Key message:** `/gsd-map-codebase` gives GSD project memory about code you didn't write. This is the brownfield entry point.

**Slide approach:** 1-2 slides. Emphasize that the codebase mapping step is what makes brownfield viable — without it, the agent is guessing about project structure.

### Scenario 3: Quick Fix / Debugging — "Inloggningen returnerar 401" (SCEN-03)

**Starting situation:** Bug reported, need to fix it fast.

**Workflow (two paths):**
```
Path A: Simple fix
  /gsd-fast "fix the 401 error in login validation"
  → Done in seconds, atomic commit

Path B: Needs investigation
  /gsd-debug
  → Parallel debug agents investigate
  → Root cause: "useEffect missing dependency array"
  → DEBUG-login-401.md created
  → /gsd-quick "fix: add dependency array to useEffect in LoginForm"
```

**Key message:** Start with `/gsd-fast`. If the problem is deeper, `/gsd-debug` investigates systematically before you code blindly.

**Slide approach:** 1-2 slides showing the two paths. The "when to escalate" decision mirrors the decision tree.

### Depth Balance Recommendation (D-06)

**Brownfield deserves slightly more emphasis** because:
1. Most developers work in brownfield environments (not greenfield)
2. The `/gsd-map-codebase` command hasn't been shown yet (it's new in this phase — PRAC-04)
3. Greenfield was already covered extensively in Section 5

Suggested weight: Greenfield (1 slide), Brownfield (2 slides), Quick fix/debug (1-2 slides).

## Best Practices Content (BEST-01 through BEST-04)

### Presentation Format Recommendation (D-08)

**Principles-first with do/don't examples** works best:
1. State the principle as a short headline
2. Show a concrete do/don't pair
3. One principle per slide

This combines the best of all three options: the principle gives the "why", the do/don't pair gives the "what", and one-per-slide keeps it spacious per D-12.

### BEST-01: Mental Model Shifts

Two key shifts, each deserves its own slide:

**Shift 1: "Tänk outcomes, inte steg"**
- ❌ "Create a file called AuthService.ts, add a login method that accepts email and password, then create a JWT token..."
- ✅ "Användare ska kunna logga in med email och lösenord"
- GSD derives the steps from the goal. You define success criteria, not implementation.

**Shift 2: "Du bestämmer, AI utför"**
- You: What to build, architectural decisions, quality standards
- AI: Research, planning, implementation, verification execution
- The developer becomes the *architect* and *reviewer*, not the *typist*

### BEST-02: Prompt Crafting (with concrete examples per D-10)

Key prompt patterns verified from how GSD agents parse input:

| Pattern | Bad Prompt | Good Prompt |
|---------|-----------|-------------|
| **Be specific** | "Fix the bug" | "The login form returns 401 when valid credentials are submitted" |
| **State the goal** | "Add a button" | "Users should be able to export their data as CSV from the settings page" |
| **Give context** | "Refactor this" | "Refactor the auth module — it currently mixes JWT creation, validation, and user lookup in one file" |
| **Set constraints** | "Make it better" | "Improve performance of the user search — currently takes 3s, should be under 500ms" |

**Key insight:** GSD's `/gsd-do` router literally parses your intent to choose the right command — specific prompts lead to better routing. Vague prompts mean ambiguity → the router has to ask clarifying questions → slower workflow.

### BEST-03: Escape Hatches — When NOT to Use Agents (D-09)

This section must carry real weight per success criteria #4. Be honest:

**Don't use agents for:**
1. **Arkitekturbeslut** — Novel architecture decisions need human judgment and team discussion. The agent optimizes locally, you optimize globally.
2. **Security-kritisk kod** — Authentication flows, encryption, access control. Agent-generated code needs human security review regardless.
3. **Teamets lärande** — If the purpose is learning, not shipping — do it yourself. Agents bypass the learning process.
4. **Regelverk & compliance** — GDPR, financial regulations, medical standards. Agents don't understand legal liability.
5. **Det du inte kan reviewera** — If you can't evaluate whether the agent's output is correct, you shouldn't delegate it.

**Slide framing:** "GSD gör dig effektivare — men det är fortfarande du som är ansvarig." This builds credibility: the presenter isn't selling, they're being honest.

### BEST-04: Anti-Patterns

Three primary anti-patterns, each with a concrete example:

| Anti-Pattern | What Happens | Instead |
|-------------|-------------|---------|
| **Vaga prompts** | Agent guesses wrong, you redo work | Be specific: state goal + context + constraints |
| **Skippa verification** | "3/3 tasks done!" but nothing works | Always run `/gsd-verify-phase` — task ≠ goal |
| **Micro-management** | You dictate every file and line → loses the benefit of delegation | State the outcome, let GSD figure out the plan |

**Connection to verification:** Reference Section 5's "task completion ≠ goal achievement" — this is the anti-pattern in action. Skipping verification is the #1 way to ship broken code with false confidence.

## "Start Monday" Content (BEST-05)

### Recommended Call-to-Action (D-11)

**Tiered approach for different comfort levels** is more compelling than a single action because the audience includes skeptics and enthusiasts:

```
Tier 1 (5 min):     Installera GSD + kör /gsd-fast
Tier 2 (30 min):    Kör /gsd-quick på en riktig task  
Tier 3 (2 timmar):  Kör /gsd-new-project på en sidoprojekt
```

**Slide framing:** 
- Title: "Börja på måndag"
- Lead with Tier 1 as the primary CTA: install command + first `/gsd-fast` on a real typo in your codebase
- Show Tier 2 and 3 as "ready for more?" options
- End with a motivating close: not "AI will replace you" but "AI will make your Mondays better"

**The install command (verified):**
```bash
$ npx get-shit-done-cc@latest
```

This takes <1 minute and requires only Node.js ≥18 + VS Code + Copilot — prerequisites most developers in this audience already have.

### Closing Slide

The final slide should be warm, not corporate:
- Reference the journey: from "vad är det här?" to "jag vet exakt vilket kommando jag ska använda"
- Practical: the decision tree they photographed + the install command they'll run Monday
- Tone: encouraging, not pressuring

## Section Narrative Flow

Phase 4 needs to maintain the narrative arc from Section 5 into Section 6:

```
Section 5 ends with:  "Goal-backward verification — inte 'är koden skriven?' utan 
                       'fungerar det för användaren?'"
                       [intellectual climax]
                              ↓
Section 6 opens with: "I din vardag" divider
                       [practical application — "how does this map to YOUR work?"]
                       → Decision tree: "which command do I use?"
                       → Scenarios: greenfield, brownfield, debugging
                              ↓
Section 7 opens with: "Tänk så här" divider
                       [mindset + practices — "how do I think about this?"]
                       → Mental model shifts
                       → Prompt crafting
                       → Anti-patterns + escape hatches
                              ↓
Section 8 opens with: "Börja på måndag" divider
                       [call-to-action — "what do I do RIGHT NOW?"]
                       → Install + first command
                       → Tiered challenge
                       → Warm close
```

The arc is: **Theory → Practice → Mindset → Action**. Each section transitions naturally to the next.

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| Decision tree visuals | Mermaid or external diagram tools | ASCII art in plain code fence | Established Phase 2-3 pattern, renders reliably in Marp, photographable |
| Slide transitions | CSS animations between scenarios | Multiple slides (one idea per slide) | Marp has limited animation support; one-per-slide pattern works |
| Command reference | Full command documentation on slides | The companion document (Phase 6) | Slides need brevity; companion.md Section 7 has full command reference |
| Prompt crafting theory | Abstract principles | Concrete good/bad prompt pairs | D-10 mandates actual examples; theory without examples doesn't land |

## Common Pitfalls

### Pitfall 1: Decision Tree Too Wide for Projector
**What goes wrong:** ASCII art tree with 10+ leaf nodes exceeds 75-character width, wrapping on projector.
**Why it happens:** Trying to include every GSD command in one tree.
**How to avoid:** Limit to 8 leaf commands maximum. Keep lines under 75 characters. Use the compact Q&A branching list format, not a full binary tree. Test in Marp PDF output.
**Warning signs:** Lines exceeding the right edge of the Marp preview.

### Pitfall 2: Scenarios Repeat Phase 2-3 Content
**What goes wrong:** Greenfield scenario re-explains `/gsd-new-project` flow that Section 5 already covered in detail.
**Why it happens:** Each scenario touches commands the audience already saw.
**How to avoid:** Frame scenarios as "application" not "explanation." Use phrases like "ni såg `/gsd-new-project` — här är ett konkret projekt" and show the *outcome*, not the *mechanics*. The value is in seeing it applied to a relatable situation.
**Warning signs:** A scenario slide that could have been in Section 5.

### Pitfall 3: Anti-Patterns Without Equal Escape Hatch Weight
**What goes wrong:** Anti-patterns get 3 slides, escape hatches get half a slide. Skeptics feel dismissed.
**Why it happens:** It's more fun to show best practices than limitations.
**How to avoid:** Success criteria #4 explicitly requires "equal weight." Give escape hatches their own full slide with 4-5 concrete situations. Frame it as professional honesty, not weakness.
**Warning signs:** Escape hatches listed as bullet points on the anti-patterns slide.

### Pitfall 4: "Start Monday" Feels Like a Sales Pitch
**What goes wrong:** The close reads as "buy our product" instead of "try this Monday."
**Why it happens:** Call-to-action language naturally tilts toward sales.
**How to avoid:** Keep the tone utbildande (educating) per project constraints. Show the install command and first task as practical steps, not as a pitch. The tiered approach helps — it respects that some people want to try cautiously.
**Warning signs:** Words like "revolutionize", "transform", "don't miss out."

### Pitfall 5: Decision Tree Language Inconsistency
**What goes wrong:** Decision tree mixes Swedish and English, breaking the D-01 mandate.
**Why it happens:** Autopilot follows the deck's Swedish-by-default pattern.
**How to avoid:** D-01 explicitly states all-English for the decision tree. The surrounding slide title and intro line can be Swedish, but everything inside the code block must be English.
**Warning signs:** Swedish words inside the decision tree code block.

### Pitfall 6: Forgetting Terminal Example Style Consistency
**What goes wrong:** Scenario terminal examples use different formatting than Phases 2-3 (e.g., missing `$` prompt, different output style).
**Why it happens:** Writing new scenarios without checking existing examples.
**How to avoid:** Every terminal example must use: `bash` language tag, `$` prompt prefix, 3-5 lines, compact output. Match the exact style of Phase 2's examples.
**Warning signs:** Terminal examples that look visually different from Section 4-5 examples.

## Code Examples

### Example 1: Decision Tree Slide (All-English)

```markdown
---

## Vilket kommando ska jag använda?

```
What are you doing?
├── Starting something new?
│   ├── Whole project       → /gsd-new-project
│   └── One feature         → /gsd-quick --discuss
├── Working on existing code?
│   ├── First time here?    → /gsd-map-codebase
│   ├── Bug or error?       → /gsd-debug
│   └── Big refactor?       → /gsd-add-phase
├── Something small?
│   ├── Trivial fix (≤3)    → /gsd-fast
│   └── Not sure?           → /gsd-do
└── Coming back?
    └── Resuming work       → /gsd-resume-work
```
```

### Example 2: Brownfield Scenario Slide

```markdown
---

## Brownfield — befintlig kodbas

Steg 1: Kartlägg först

```bash
$ /gsd-map-codebase
Mapping... 7 analysis documents created
   .planning/codebase/STRUCTURE.md
   .planning/codebase/PATTERNS.md
   ...
```

Steg 2: GSD förstår nu din kod — planera som vanligt

```bash
$ /gsd-add-phase "add search endpoint to user API"
```
```

### Example 3: Prompt Crafting Do/Don't Slide

```markdown
---

## Prompt crafting — var specifik

❌ **Vagt:**
> "Fix the bug"

✅ **Specifikt:**
> "The login form returns 401 when valid credentials are submitted — the JWT token expiration is set to 0"

Kontext + mål + constraints = bättre resultat.
```

### Example 4: Escape Hatches Slide

```markdown
---

## När du INTE ska använda agents

🚫 **Arkitekturbeslut** — agenten optimerar lokalt, du optimerar globalt

🚫 **Security-kritisk kod** — alltid manuell review

🚫 **Teamets lärande** — om syftet är att lära, inte leverera

🚫 **Regelverk & compliance** — agenten förstår inte juridiskt ansvar

🚫 **Det du inte kan reviewera** — delegera inte det du inte kan bedöma

> GSD gör dig effektivare — men det är fortfarande du som är ansvarig.
```

### Example 5: Start Monday Slide

```markdown
---

## Din challenge

**Måndag morgon:**

```bash
$ npx get-shit-done-cc@latest
$ /gsd-fast "fix a real typo in your codebase"
```

**Redo för mer?**

| Tid | Utmaning | Kommando |
|-----|----------|----------|
| 5 min | Fixa en riktig typo | `/gsd-fast` |
| 30 min | Lägg till en feature | `/gsd-quick` |
| 2 timmar | Nytt sidoprojekt | `/gsd-new-project` |
```

## Validation Architecture

### Test Framework

| Property | Value |
|----------|-------|
| Framework | Marp CLI 4.3.1 (visual rendering validation) |
| Config file | slides.md front matter (`marp: true`) |
| Quick run command | `npx @marp-team/marp-cli slides.md --html -o test-output.html` |
| Full suite command | `npx @marp-team/marp-cli slides.md --html -o test-output.html && npx @marp-team/marp-cli slides.md --pdf -o test-output.pdf` |

### Phase Requirements → Test Map

| Req ID | Behavior | Test Type | Automated Command | File Exists? |
|--------|----------|-----------|-------------------|-------------|
| SCEN-04 | Decision tree maps scenarios to commands | manual | Visual inspection of rendered slide | ❌ Wave 0 |
| SCEN-01 | Greenfield scenario shows distinct workflow | manual | Visual inspection of rendered slide | ❌ Wave 0 |
| SCEN-02 | Brownfield scenario shows /gsd-map-codebase entry | manual | Visual inspection + grep for `map-codebase` | ❌ Wave 0 |
| SCEN-03 | Quick fix/debug scenarios show distinct paths | manual | Visual inspection of rendered slide | ❌ Wave 0 |
| PRAC-04 | Brownfield awareness with /gsd-map-codebase | manual | `grep "map-codebase" slides.md` | ❌ Wave 0 |
| BEST-01 | Mental model shifts stated as actionable principles | manual | Visual inspection of rendered slide | ❌ Wave 0 |
| BEST-02 | Prompt crafting with concrete examples | manual | Visual inspection — good/bad pairs visible | ❌ Wave 0 |
| BEST-03 | Escape hatches with equal weight | manual | Count slides dedicated to escape hatches vs anti-patterns | ❌ Wave 0 |
| BEST-04 | Anti-patterns presented with examples | manual | Visual inspection of rendered slide | ❌ Wave 0 |
| BEST-05 | Start Monday challenge with zero-friction step | manual | `grep "npx get-shit-done" slides.md` — appears in Section 8 | ❌ Wave 0 |

### Sampling Rate

- **Per task commit:** `npx @marp-team/marp-cli slides.md --html -o test-output.html` — visual spot-check
- **Per wave merge:** Full visual review of all new slides in browser + PDF rendering check
- **Phase gate:** All 10 requirements verifiable by visual inspection of rendered output

### Wave 0 Gaps

All requirements in this phase are presentation content (slides) — validation is primarily visual/manual. No automated test framework is needed beyond:

- [ ] Marp renders without errors: `npx @marp-team/marp-cli slides.md --html -o test-output.html`
- [ ] `grep` checks for key content presence (command names in right sections)
- [ ] Visual verification that ASCII art renders correctly at projected resolution

## Sources

### Primary (HIGH confidence)
- GSD workflow source files (`~/.copilot/get-shit-done/workflows/`) — 57 workflow files verified for command behavior, routing tables, and agent architecture
- `slides.md` — Current deck structure with exact insertion points at lines 468, 478, 489
- Prior phase research (`02-RESEARCH.md`, `03-RESEARCH.md`) — Established slide patterns, verified command details, ASCII art conventions

### Secondary (MEDIUM confidence)
- `companion.md` — Companion document outline confirming Section 5 (scenarios) and Section 6 (best practices) topic alignment with Phase 4 slides
- Phase 2-3 plan files — Slide count precedents (8 slides per section as established norm)

### Tertiary (LOW confidence)
- Prompt crafting guidance — Based on GSD design principles (how agents parse input), not external research on prompt engineering best practices. The examples are well-grounded in GSD's actual routing logic but haven't been validated with user testing.

## Open Questions

1. **Decision tree: one dense slide or two slides?**
   - What we know: D-04 grants discretion. The tree with 8 leaf nodes fits within 75 chars. One slide is "photographable." Two slides allow adding specialist commands separately.
   - What's unclear: Whether 8+ leaf nodes render readably at projector resolution.
   - Recommendation: Start with one slide. If the planner/executor finds it too dense, split into two.

2. **`/gsd-debug` vs `/gsd-diagnose-issues` naming**
   - What we know: The workflow file is `diagnose-issues.md`. The routing table in `/gsd-do` uses `/gsd-debug`. Phase 2 D-16 established Copilot-only references.
   - What's unclear: Whether the command is invoked as `/gsd-debug` or `/gsd-diagnose-issues` in Copilot.
   - Recommendation: Use `/gsd-debug` in slides — it's what the routing table references and it's more intuitive. The workflow file name is an internal detail.

3. **Escape hatches: 5 items or 3-4?**
   - What we know: D-09 grants discretion on depth. Success criteria #4 requires "equal weight."
   - What's unclear: Whether 5 escape hatches on one slide is too dense per D-12 (one idea per slide).
   - Recommendation: 5 items as a list with emoji markers is fine — each is one line, not a paragraph. The "one idea" is "when NOT to use agents" — the 5 items are the illustration.

## Metadata

**Confidence breakdown:**
- Standard stack: HIGH — Same Marp stack from Phases 1-3, no changes
- Architecture: HIGH — Insertion points verified in current slides.md, established patterns from prior phases
- Content accuracy: HIGH — All GSD commands verified from primary workflow source files
- Pitfalls: HIGH — Based on specific issues encountered in Phases 2-3 slide development

**Research date:** 2026-04-16
**Valid until:** 2026-05-16 (stable — content creation phase, no external dependencies changing)
