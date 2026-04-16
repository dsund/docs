# Phase 3: Core Payload — Full Workflow - Research

**Researched:** 2026-04-15
**Domain:** Marp slide content — GSD full lifecycle, agent architecture, planning artifacts, persistent memory, goal-backward verification
**Confidence:** HIGH

## Summary

Phase 3 delivers the core intellectual payload of the presentation across two slide sections: Section 3 ("Hur fungerar det?") and Section 5 ("Hela livscykeln"). Where Phase 2's on-ramp section proved GSD is *easy to start*, Phase 3 must prove it's *powerful when you need it*. The audience arrives via the gateway bridge slide ("Men om uppgiften är större? Då behöver du hela workflow:en.") and expects to see the full machinery behind serious projects.

The content divides naturally: Section 3 explains the **mental model** (what GSD is architecturally — agents, orchestrator, how it thinks), while Section 5 walks through the **full lifecycle** (new-project → discuss → plan → execute → verify, with persistent memory tying it all together). This is a conceptual-heavy section compared to Phase 2's terminal-example approach, so the balance should shift toward diagrams, simplified file excerpts, and architectural illustrations — with selective terminal examples only for key moments (e.g., `/gsd-new-project` interactive flow, `/gsd-resume-work` session pickup).

All GSD system details in this research were verified by reading the actual workflow source files (57 workflows in `~/.copilot/get-shit-done/workflows/`), the 18 agent definitions in `~/.copilot/agents/`, and the reference/template files. The verification patterns, wave-based execution model, composable flags, and project lifecycle commands are all documented from primary sources.

**Primary recommendation:** Build ~12-15 slides total across Sections 3 and 5. Section 3 (mental model): ~4-5 slides covering agent architecture and the orchestrator pattern. Section 5 (full lifecycle): ~8-10 slides covering the 5-step workflow, planning artifacts, persistent memory, composable flags, project lifecycle, and goal-backward verification. Use ASCII art diagrams (established Phase 2 pattern) for architecture, and simplified file excerpts for artifacts. End Section 5 with the verification philosophy as the intellectual climax.

<user_constraints>
## User Constraints (from CONTEXT.md)

### Locked Decisions
- **D-01:** Agent's Discretion: Choose the best narrative approach for the 5-step lifecycle (new-project → discuss → plan → execute → verify). Options include step-by-step build-up, single overview + deep-dives, or linear pipeline. Pick what works best for a 60-min presentation flow.
- **D-02:** Agent's Discretion: Composable flags (--discuss, --research, --full) placement — integrate into workflow steps, show on dedicated slide, or reference back to Phase 2's /gsd-quick example. Pick the least repetitive approach.
- **D-03:** Agent's Discretion: Mix of conceptual diagrams and terminal examples. Phase 2 was terminal-heavy; this section can balance conceptual understanding with selective terminal output for key steps.
- **D-04:** Agent's Discretion: How many of the 18 specialized agents to show. Simplified orchestrator pattern is key — show that agents collaborate, not that there are exactly 18 of them.
- **D-05:** Agent's Discretion: Wave-based execution presentation — show the concept of parallel waves without implementation details.
- **D-06:** Agent's Discretion: How to present .planning/ directory files (ROADMAP.md, STATE.md, PLAN.md). Realistic but simplified excerpts preferred — the audience should see what these files look like without reading full content. Per STATE.md blocker: "Artifact examples need to be realistic but simplified."
- **D-07:** Agent's Discretion: Whether to show a file tree or inline code snippets or both.
- **D-08:** Agent's Discretion: How to convey that GSD remembers project state across sessions (STATE.md, /gsd-resume-work, /gsd-progress). This is a key differentiator vs ad-hoc AI usage.
- **D-09:** Agent's Discretion: Project lifecycle management (starting, switching, cleaning up projects) — keep minimal, mention capabilities without deep-diving.
- **D-10:** Agent's Discretion: How to convey "task completion ≠ goal achievement." This is GSD's strongest philosophical point — make it memorable. Options: comparison slide, concrete example, before/after visualization.
- **D-11:** Agent's Discretion: How many verification levels to show (4 levels exist: self-check, automated, goal-backward, human UAT). Showing all 4 may be too much — pick the most impactful.
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

### Deferred Ideas (OUT OF SCOPE)
None — discussion stayed within phase scope
</user_constraints>

<phase_requirements>
## Phase Requirements

| ID | Description | Research Support |
|----|-------------|------------------|
| DEEP-01 | Core workflow overview (new-project → discuss → plan → execute → verify) | Verified full 5-step lifecycle from workflow sources: new-project.md (9 steps: setup → questioning → research → requirements → roadmap), discuss-phase.md (captures decisions for downstream agents), plan-phase.md (research → plan → verify loop, max 3 iterations), execute-phase.md (wave-based parallel execution with subagents), verify-phase.md (goal-backward analysis with 3 verification levels). |
| DEEP-02 | Agent architecture — 18 specialized agents, orchestrator pattern, wave-based execution | Verified 18 agents from `~/.copilot/agents/`: executor, planner, phase-researcher, project-researcher, research-synthesizer, roadmapper, verifier, plan-checker, debugger, codebase-mapper, integration-checker, nyquist-auditor, ui-researcher, ui-checker, ui-auditor, advisor-researcher, assumptions-analyzer, user-profiler. Wave execution: plans grouped by dependency into waves, waves execute sequentially, plans within a wave can run in parallel. |
| DEEP-03 | Planning artifacts walkthrough (.planning/ directory: PROJECT.md, ROADMAP.md, STATE.md) | Verified from this project's own `.planning/` structure and template files. Files include: PROJECT.md (what + constraints + requirements), ROADMAP.md (phased execution plan with success criteria), STATE.md (current position + accumulated context + session continuity), REQUIREMENTS.md (full requirements with traceability), PLAN.md (per-phase executable prompts with must_haves), SUMMARY.md (per-plan completion record). |
| DEEP-04 | Persistent project memory (STATE.md, /gsd-resume-work, /gsd-progress) | Verified from workflow sources: resume-project.md reads STATE.md to restore full context (position, decisions, blockers, session continuity), progress.md analyzes roadmap and routes to next action, pause-work.md creates HANDOFF.json + .continue-here.md for structured handoffs. STATE.md stores: project reference, current position, progress %, decisions, pending todos, blockers, session continuity timestamp. |
| DEEP-05 | Goal-backward verification ("task completion ≠ goal achievement", 4 levels) | Verified from verify-phase.md and verification-patterns.md. The 4 levels: (1) Exists — file present, (2) Substantive — real implementation not placeholder, (3) Wired — connected to rest of system, (4) Functional — actually works when invoked. Goal-backward analysis: derive truths from phase goal → derive artifacts → derive wiring → verify each level. Also: verify-work.md provides human UAT with conversational testing. |
| DEEP-06 | Composable flags pattern (/gsd-quick --discuss --research --full) | Verified from quick.md workflow: `--discuss` adds lightweight discussion before planning, `--research` spawns focused research agent before planning, `--full` enables plan-checking (max 2 iterations) + post-execution verification. Flags are composable: `--discuss --research --full` gives all three. This graduated system is a key differentiator. |
| PRAC-08 | Project lifecycle — hantera .planning/, starta nya projekt, byta mellan projekt, rensa och börja om | Verified commands: /gsd-new-project (initialize), /gsd-new-workspace (multi-repo isolation), /gsd-list-workspaces (show all), /gsd-remove-workspace (cleanup), /gsd-cleanup (archive completed milestone phases), /gsd-complete-milestone (close milestone + evolve PROJECT.md). Workspaces support worktree or clone strategy. |
</phase_requirements>

## Project Constraints (from copilot-instructions.md)

- **GSD Workflow Enforcement:** All repo edits go through GSD commands — no direct edits outside a GSD workflow
- **Language:** Svenska with engelska facktermer (per TERMINOLOGY.md — "phase" not "fas", "workflow" not "arbetsflöde")
- **Format:** Marp markdown, 16:9, default theme, paginate: true
- **Tone:** Utbildande, inte säljande — "hur" rather than "varför"
- **Slide styling:** Section dividers use `<!-- _class: divider -->`, code blocks at 0.85em with 4px border-radius
- **Copilot-only references:** No Claude Code, OpenCode, Gemini, or Codex mentions in slides (D-15)

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

Phase 3 inserts content at TWO locations in `slides.md`:

```
slides.md (current structure)
├── ...
├── Section 3 divider: "Hur fungerar det?"
│   └── <!-- Section 3: GSD Mental Model — slides added by Phase 3 -->
│   └── [INSERT ~4-5 slides here: agent architecture, orchestrator pattern]
├── ...
├── Section 4: "Börja enkelt" (Phase 2 content — 8 slides)
│   └── Gateway bridge: "Men om uppgiften är större?"
├── Section 5 divider: "Hela livscykeln"
│   └── <!-- Section 5: Full Workflow — slides added by Phase 3 -->
│   └── [INSERT ~8-10 slides here: workflow, artifacts, memory, verification]
├── ...
```

**Important narrative note:** The slide deck presentation ORDER is: Section 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8. However, Sections 1-2 will be added in Phase 5. The audience will see Section 3 (mental model) BEFORE Section 4 (on-ramp) BEFORE Section 5 (full workflow). This means:
- Section 3 introduces the *concept* (what GSD is, how agents work)
- Section 4 shows the *easy entry* (start simple, grow complexity)
- Section 5 shows the *full machinery* (when you need the whole thing)

### Recommended Narrative Structure

**Section 3: "Hur fungerar det?" (~4-5 slides)**

Purpose: Give the audience the mental model before seeing any commands. "Before I show you the commands, here's how GSD thinks."

1. **The Big Idea slide** — GSD = orchestrator + specialized agents + project memory. One conceptual sentence, one ASCII art diagram.
2. **Agent Architecture slide** — Show 4-5 agent categories (not all 18). Orchestrator delegates to specialists. ASCII art diagram showing orchestrator → researcher/planner/executor/verifier.
3. **Wave Execution slide** — Plans grouped into waves, waves run in order, parallel within wave. Simple ASCII art timeline.
4. **Planning Directory slide** — `.planning/` as "projektets minne" — file tree showing key files. This primes the audience for the artifact details in Section 5.
5. *(Optional) Composable flags reference* — Could fit here as "GSD anpassar sig" or defer to Section 5.

**Section 5: "Hela livscykeln" (~8-10 slides)**

Purpose: Walk through the full workflow that the gateway bridge promised. "Here's the whole workflow, step by step."

1. **Lifecycle Overview slide** — ASCII art pipeline: new-project → discuss → plan → execute → verify. Single overview showing the complete flow.
2. **New Project slide** — Terminal example of `/gsd-new-project` interactive flow (already teased in Phase 2, now deeper). Show questioning → research → requirements → roadmap.
3. **Planning Artifacts slide** — Show simplified ROADMAP.md and/or STATE.md excerpts. Use realistic but condensed content from this project's own artifacts.
4. **Discuss & Plan slide** — Brief coverage of `/gsd-discuss-phase` (capturing decisions) and `/gsd-plan-phase` (research → plan → verify loop).
5. **Execute slide** — Wave-based execution concept. Orchestrator spawns executor agents. Show the phase → plan → task hierarchy.
6. **Composable Flags slide** — (If not covered in Section 3) Show how `--discuss`, `--research`, `--full` compose on `/gsd-quick`. Reference back to Phase 2's example.
7. **Persistent Memory slide** — STATE.md as session continuity. Terminal example of `/gsd-resume-work` restoring context. Key differentiator vs ad-hoc AI.
8. **Project Lifecycle slide** — Minimal: mention starting, switching, cleaning up. One slide maximum.
9. **Verification Philosophy slide** — "Task completion ≠ Goal achievement." The intellectual climax. Concrete example showing the difference. This should be the most memorable slide.
10. *(Optional) Verification Levels slide* — Show 2-3 of the 4 levels if the philosophy slide needs a follow-up.

### Slide Pattern: Content Slides (established by Phase 2)

```markdown
---

## Slide Title

[One core idea — text, diagram, or code example]

[Optional footer line — summary or transition hint]
```

- No `<!-- _class: ... -->` on content slides
- No `<!-- _paginate: skip -->` on content slides
- `---` separator between slides
- Swedish text with English technical terms

### Slide Pattern: ASCII Art Diagrams (established by Phase 2)

```markdown
```
  [diagram content]
  [use box drawing characters: ─ │ ┌ ┐ └ ┘ ├ ┤ ┬ ┴ ┼]
  [keep lines under 75 characters for projector safety]
```
```

Use plain code fence (no language specifier) to prevent syntax highlighting on diagrams.

### Slide Pattern: File Excerpts (new for Phase 3)

For showing planning artifacts like ROADMAP.md or STATE.md, use `markdown` code fences for syntax highlighting:

```markdown
```markdown
# Roadmap: Mitt API-projekt

## Phases
- [x] Phase 1: Foundation
- [ ] Phase 2: Auth system
- [ ] Phase 3: API endpoints
```
```

Keep excerpts to 5-8 lines maximum. Show the *shape* of the file, not the full content. Use relatable project examples (REST API, not abstract).

### Anti-Patterns to Avoid

- **Information dump:** Don't try to explain all 18 agents — show 4-5 categories
- **Implementation details:** Don't show workflow YAML/markdown internals — show what the user experiences
- **Repetition with Phase 2:** Don't re-show `/gsd-quick` terminal examples — reference them ("ni såg `/gsd-quick` i förra sektionen")
- **Dense artifact slides:** Don't paste full STATE.md — show 5-8 line excerpts that feel authentic
- **Flat verification:** Don't just list 4 levels — make the *philosophy* memorable through a concrete example

## Verified GSD Architecture Details

### The 18 Specialized Agents (grouped for presentation)

The 18 agents naturally group into functional categories. For the presentation, show categories not individual agents:

| Category | Agents | Presentation Label |
|----------|--------|-------------------|
| **Research** | project-researcher, phase-researcher, research-synthesizer, advisor-researcher | "Researchers" — undersöker domänen |
| **Planning** | roadmapper, planner, plan-checker, assumptions-analyzer | "Planners" — skapar och granskar planer |
| **Execution** | executor | "Executor" — bygger koden |
| **Quality** | verifier, integration-checker, nyquist-auditor | "Verifiers" — kontrollerar kvalitet |
| **Specialized** | debugger, codebase-mapper, user-profiler | "Specialists" — felsökning, kodkartläggning |
| **UI** | ui-researcher, ui-checker, ui-auditor | "UI-team" — design och granskning |

**Recommendation for D-04:** Show 4 categories on the architecture slide: Research → Planning → Execution → Verification. Mention "18 specialiserade agents" as a number but don't list them all. The orchestrator pattern (who delegates to whom) matters more than the catalog.

### Orchestrator Pattern (verified)

The orchestrator pattern is consistent across GSD workflows:
1. **Orchestrator loads context** — reads STATE.md, ROADMAP.md, phase config
2. **Orchestrator delegates** — spawns specialized subagents via `Task()` calls
3. **Subagents execute independently** — each gets their own context window, reads their own files
4. **Orchestrator collects results** — checks for completion via filesystem/git state
5. **Orchestrator continues** — next wave/step/phase

Key principle from execute-phase.md: "Orchestrator coordinates, not executes."

### Wave-Based Execution (verified)

From execute-phase.md:
- Plans within a phase are grouped into **waves** based on dependencies
- Waves execute **sequentially** (Wave 1 completes before Wave 2 starts)
- Plans **within a wave** can execute in parallel (if `parallelization: true` in config)
- Each executor agent gets isolated context and commits atomically
- Orchestrator does spot-checks via filesystem and git state to verify completion

**Recommendation for D-05:** Show a simple 2-wave diagram:
```
Wave 1: [Plan A] [Plan B]  ← parallel
         ↓ complete
Wave 2: [Plan C]            ← depends on A & B
```

### The 5-Step Lifecycle (verified from workflow sources)

| Step | Command | What Happens | Key Output |
|------|---------|-------------|------------|
| 1. **Initialize** | `/gsd-new-project` | Deep questioning → research (optional) → requirements → roadmap | PROJECT.md, REQUIREMENTS.md, ROADMAP.md |
| 2. **Discuss** | `/gsd-discuss-phase N` | Surface gray areas → user decides → capture decisions | CONTEXT.md (feeds researcher + planner) |
| 3. **Plan** | `/gsd-plan-phase N` | Research (optional) → create plan → plan-check (up to 3 iterations) | RESEARCH.md, PLAN.md |
| 4. **Execute** | `/gsd-execute-phase N` | Group plans into waves → spawn executor agents → commit atomically | Code changes, SUMMARY.md |
| 5. **Verify** | `/gsd-verify-phase` / `/gsd-verify-work` | Goal-backward analysis (automated) or UAT (human conversational) | VERIFICATION.md or UAT.md |

**Recommendation for D-01:** Use a **single overview slide** showing the pipeline as ASCII art, then **2-3 deep-dive slides** for the most important steps (new-project, artifacts, verify). Don't show all 5 steps in equal depth — the audience doesn't need equal coverage of discuss vs execute.

### Composable Flags (verified from quick.md)

The `/gsd-quick` command supports independently addable flags:

| Flag | What It Adds | When to Use |
|------|-------------|-------------|
| `--discuss` | Lightweight discussion before planning — surfaces assumptions, captures decisions in CONTEXT.md | "Jag vet ungefär vad jag vill men inte alla detaljer" |
| `--research` | Spawns focused research agent before planning — investigates approaches, libraries, pitfalls | "Jag vet inte hur man gör detta bäst" |
| `--full` | Enables plan-checking (max 2 iterations) + post-execution verification | "Det här måste bli rätt — kvalitetsgaranti" |

Flags compose: `--discuss --research --full` gives all three capabilities.

**Recommendation for D-02:** Reference back to Phase 2's `/gsd-quick` slide rather than creating a new terminal example. Show a conceptual slide: "Kom ihåg composable flags?" with a simple matrix showing what each flag adds. This avoids repetition while reinforcing the concept.

### Planning Artifacts (verified from this project + templates)

The `.planning/` directory structure:

```
.planning/
├── PROJECT.md          ← Vad vi bygger + constraints + decisions
├── REQUIREMENTS.md     ← Krav med spårbarhet till phases
├── ROADMAP.md          ← Phaser med success criteria
├── STATE.md            ← Var vi är + minne mellan sessioner
├── config.json         ← GSD-inställningar
├── research/           ← Projekt-level research
│   ├── STACK.md
│   ├── FEATURES.md
│   ├── ARCHITECTURE.md
│   └── PITFALLS.md
└── phases/
    ├── 01-foundation/
    │   ├── 01-CONTEXT.md   ← Beslut från /gsd-discuss
    │   ├── 01-RESEARCH.md  ← Research-resultat
    │   ├── 01-01-PLAN.md   ← Exekverbar plan
    │   └── 01-01-SUMMARY.md ← Vad som byggdes
    └── 02-auth-system/
        └── ...
```

**Recommendation for D-06/D-07:** Show BOTH a file tree (like above, simplified) AND one inline excerpt. The file tree gives shape, the excerpt gives texture. Use this project's own ROADMAP.md as the basis for the excerpt — it's the most relatable example since the audience is literally looking at a presentation built with GSD.

**Realistic excerpt for ROADMAP.md:**

```markdown
## Phases

- [x] Phase 1: Foundation
- [ ] **Phase 2: Auth system** ← du är här
- [ ] Phase 3: API endpoints

### Phase 2: Auth system
**Goal**: Users can log in and access protected routes
**Success Criteria:**
  1. Login form validates credentials
  2. JWT tokens issued on success
  3. Protected routes reject unauthenticated requests
```

**Realistic excerpt for STATE.md:**

```markdown
## Current Position

Phase: 2
Plan: 1 of 2
Status: Executing

Progress: [████░░░░░░] 35%

## Session Continuity

Last session: 2025-06-10
Stopped at: Task 3 of Plan 1 — JWT middleware
```

### Persistent Project Memory (verified)

Three commands maintain session continuity:

| Command | Purpose | What It Does |
|---------|---------|-------------|
| `/gsd-resume-work` | Restore context after break | Reads STATE.md → shows position, decisions, blockers → routes to next action |
| `/gsd-progress` | Check project status | Analyzes roadmap → summarizes what's done/ahead → intelligent routing |
| `/gsd-pause-work` | Save state before leaving | Creates HANDOFF.json + .continue-here.md with full context |

STATE.md is the persistent store. It tracks:
- **Current position** — phase, plan, status, progress %
- **Accumulated context** — decisions, pending todos, blockers/concerns
- **Session continuity** — timestamp, what was interrupted, resume file reference

**Recommendation for D-08:** Show a "before/after" or "session break" scenario:
- Session 1: Working on Phase 2, Task 3... (pause)
- *3 dagar senare*
- Session 2: `/gsd-resume-work` → "Du var på Phase 2, Task 3 — JWT middleware. Det här är kvar att göra..."

This is the most relatable demonstration of persistent memory — every developer has experienced losing context between sessions.

### Project Lifecycle (verified)

| Command | Purpose |
|---------|---------|
| `/gsd-new-project` | Initialize — questioning → research → requirements → roadmap |
| `/gsd-new-workspace` | Isolated workspace with git worktrees or clones |
| `/gsd-list-workspaces` | Show all workspaces with status |
| `/gsd-complete-milestone` | Close milestone, evolve PROJECT.md |
| `/gsd-cleanup` | Archive completed phase directories |
| `/gsd-remove-workspace` | Delete workspace |

**Recommendation for D-09:** One slide maximum. Bullet list format: "GSD hanterar hela projektets livscykel:" followed by 3-4 key capabilities (start, switch, track, clean up). No terminal examples — just capability awareness.

### Goal-Backward Verification (verified)

From verify-phase.md, the core principle:

> **Task completion ≠ Goal achievement**
> A task "create chat component" can be marked complete when the component is a placeholder. The task was done — but the goal "working chat interface" was not achieved.

The goal-backward analysis process:
1. What must be **TRUE** for the goal to be achieved?
2. What must **EXIST** for those truths to hold?
3. What must be **WIRED** for those artifacts to function?

Verification levels from verification-patterns.md:
1. **Exists** — File is present at expected path
2. **Substantive** — Content is real implementation, not placeholder
3. **Wired** — Connected to the rest of the system
4. **Functional** — Actually works when invoked (often requires human)

Additionally, `/gsd-verify-work` provides human UAT with a conversational flow: "Here's what should happen. Does it?"

**Recommendation for D-10:** Use a **concrete example with before/after**:

Before (task-checking): "✅ Login component created. ✅ JWT utility created. ✅ Route guard created. Allt klart!"
After (goal-backward): "Kan en användare faktiskt logga in? → Login component is a placeholder div. JWT utility returns hardcoded token. Route guard is an empty wrapper. *Inget* fungerar."

This makes the "task ≠ goal" distinction visceral and memorable. The audience should feel the *danger* of task-level checking.

**Recommendation for D-11:** Show 2 levels explicitly — goal-backward (automated agent analysis) and human UAT (conversational verification). The "Exists/Substantive/Wired/Functional" framework is the mechanism *behind* goal-backward — mention it briefly but don't deep-dive all 4 sub-levels. The philosophical point matters more than the taxonomy.

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| ASCII art diagrams | Hand-draw complex architecture | Box-drawing characters (─ │ ┌ ┐ └ ┘ ├ ┤) in plain code fences | Marp renders monospace fonts reliably; ASCII art is the established pattern from Phase 2 |
| Mermaid diagrams | Try to get Mermaid rendering in Marp | Static ASCII art or pre-rendered images | Marp has no native Mermaid support; pre-rendering adds build complexity |
| Slide transitions/animations | CSS animations for progressive reveals | Multiple slides (one idea per slide) | Marp has limited animation support; the "one idea per slide" pattern achieves the same effect |
| File content excerpts | Invent generic project examples | Use this project's own `.planning/` files as templates | The audience is looking at a presentation *built with GSD* — self-referential examples feel authentic |

**Key insight:** This phase is about *information design* not *technology*. The hard part is simplifying complex architecture into scannable slides, not building anything new. Every slide should pass the "back of the room" test: can someone 15 meters away grasp the main idea?

## Common Pitfalls

### Pitfall 1: Information Overload on Agent Architecture
**What goes wrong:** Showing all 18 agents overwhelms the audience. They stop listening.
**Why it happens:** The builder's pride — GSD has 18 agents and that's impressive. But the audience doesn't need a catalog.
**How to avoid:** Show 4 functional categories (research, plan, execute, verify) + the orchestrator. Mention "18 specialiserade agents" as a number but visualize only the pattern.
**Warning signs:** If a slide has more than 6 items in a list, it's too dense.

### Pitfall 2: Repeating Phase 2 Content
**What goes wrong:** Re-showing `/gsd-quick` examples or composable flags in full when Phase 2 already covered them.
**Why it happens:** Phase 3 requirements include DEEP-06 (composable flags) which overlaps with PRAC-03.
**How to avoid:** Use "recall" language: "Kom ihåg `/gsd-quick` från förra sektionen?" then show what's NEW (the conceptual matrix of what each flag adds, not another terminal example).
**Warning signs:** If you're copying content that already exists in Section 4, you're repeating.

### Pitfall 3: Generic Planning Artifact Examples
**What goes wrong:** Using placeholder content like "TODO app" or "Example project" for ROADMAP.md excerpts. Feels fake.
**Why it happens:** Easier to invent generic content than to simplify real content.
**How to avoid:** Use THIS PROJECT's own `.planning/` files as the template, translated to a relatable developer scenario (REST API project). The audience should think "oh, that's what real GSD files look like."
**Warning signs:** If the artifact excerpt contains "TODO" or "Example" or "Lorem ipsum" — it's a placeholder.

### Pitfall 4: Making Verification Boring
**What goes wrong:** Listing 4 verification levels as a bullet list. The audience nods politely but doesn't *feel* why it matters.
**Why it happens:** Verification is abstract. Lists are safe.
**How to avoid:** Lead with the PROBLEM (a concrete example where task-checking passed but the feature was broken), then show how goal-backward analysis catches it. Make the audience feel the danger first.
**Warning signs:** If the verification slide doesn't have a concrete example, it won't be memorable.

### Pitfall 5: Narrative Disconnection Between Sections 3 and 5
**What goes wrong:** Section 3 (mental model) and Section 5 (full workflow) feel like separate presentations with Section 4 awkwardly in between.
**Why it happens:** They ARE separated by Section 4 in the slide deck. The narrative thread needs to be intentional.
**How to avoid:** Section 3 should end with a "nu vet ni hur GSD tänker — i nästa sektion ser ni hur ni börjar" forward reference. Section 5 should open by fulfilling the gateway bridge promise from Section 4. The mental model → on-ramp → full workflow arc should feel like chapters, not disconnected talks.
**Warning signs:** If removing Section 4 would make Sections 3 and 5 feel more coherent, the narrative threading is weak.

### Pitfall 6: Slide Density — Too Much Text Per Slide
**What goes wrong:** Packing multiple concepts on one slide because "they're related."
**Why it happens:** There's a lot of content to cover and a desire to keep slide count manageable.
**How to avoid:** Follow D-12 strictly: one idea per slide. 12-15 slides for Phase 3 is fine — at ~2 minutes per slide, that's 24-30 minutes of the ~60 minute presentation, appropriate for the core content sections.
**Warning signs:** If you can't describe what a slide is about in one sentence, it has too many ideas.

## Code Examples

### ASCII Art: Agent Architecture Diagram

Recommended pattern for the orchestrator slide:

```
  ┌─────────────────────────────────────────┐
  │            ORCHESTRATOR                  │
  │     Koordinerar — bygger aldrig själv    │
  └────┬──────┬──────────┬──────────┬───────┘
       │      │          │          │
       ▼      ▼          ▼          ▼
  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐
  │Research│ │Planning│ │Execute │ │Verify  │
  │  (4)   │ │  (4)   │ │  (1)   │ │  (3)   │
  └────────┘ └────────┘ └────────┘ └────────┘
  Undersöker  Skapar     Bygger    Kontrollerar
  domänen     planer     koden     kvalitet
```

Numbers in parentheses show how many agents per category. Total = 12 of the 18 (the remaining 6 are specialists: debugger, codebase-mapper, user-profiler, and UI-team of 3).

### ASCII Art: Lifecycle Pipeline

```
  /gsd-new-project
       │
       ▼
  ┌─────────┐   ┌─────────┐   ┌─────────┐   ┌─────────┐
  │ Discuss  │──▶│  Plan   │──▶│ Execute │──▶│ Verify  │
  │ Beslut   │   │Research │   │  Waves  │   │ Mål ≠   │
  │ & val    │   │ + plan  │   │  + code │   │ tasks   │
  └─────────┘   └─────────┘   └─────────┘   └─────────┘
       │              │              │              │
  CONTEXT.md    PLAN.md +      SUMMARY.md    VERIFICATION.md
                RESEARCH.md
```

### ASCII Art: Wave Execution

```
  Phase 2: Auth System
  ────────────────────

  Wave 1    [Plan A: Models]  [Plan B: Utils]
            ────────────────  ───────────────
                    ↓ klart

  Wave 2    [Plan C: Routes + middleware]
            ─────────────────────────────
                    ↓ klart

  Verify    Goal-backward: "Kan en användare logga in?"
```

### File Excerpt: ROADMAP.md (simplified for slide)

```markdown
## Phases

- [x] Phase 1: Foundation
- [ ] **Phase 2: Auth** ← du är här
- [ ] Phase 3: API endpoints

### Phase 2: Auth
**Goal**: Användare kan logga in
**Success Criteria:**
  1. Login-formulär validerar credentials
  2. JWT-tokens utfärdas vid lyckad inloggning
  3. Skyddade routes avvisar oautentiserade requests
```

### File Excerpt: STATE.md (simplified for slide)

```markdown
## Current Position

Phase: 2 of 5
Plan: 1 of 2
Status: Executing

Progress: [████░░░░░░] 35%

## Session Continuity

Stopped at: JWT middleware implementation
Resume: /gsd-resume-work
```

### Terminal Example: /gsd-resume-work

```bash
$ /gsd-resume-work
📍 Phase 2: Auth System — Plan 1, Task 3
   Last session: 3 dagar sedan
   Stopped at: JWT middleware
   Kvar: 2 tasks i Plan 1, sedan Plan 2
```

### Verification Contrast Example

**Task-checking (farligt):**
```
✅ LoginComponent.tsx skapad
✅ jwt-utils.ts skapad
✅ RouteGuard.tsx skapad
────────────────────────
3/3 tasks klara! 🎉
```

**Goal-backward (GSD):**
```
Goal: "Användare kan logga in"
  ✅ Exists: Alla filer finns
  ❌ Substantive: LoginComponent returnerar <div/>
  ❌ Wired: RouteGuard importeras inte i App.tsx
  ❌ Functional: Inloggning fungerar inte
────────────────────────
Tasks klara — men målet INTE uppnått.
```

## State of the Art

| Old Approach | Current Approach | When Changed | Impact |
|--------------|------------------|--------------|--------|
| Ad-hoc AI prompting | Structured agent frameworks (GSD, BMAD) | 2024-2025 | Persistent memory, verification, project lifecycle |
| "It compiled = done" | Goal-backward verification | GSD architecture decision | Catches placeholder/stub implementations |
| Manual context restoration | STATE.md + /gsd-resume-work | GSD architecture decision | Zero-cost session continuity |
| One-shot AI responses | Orchestrator + specialized agents | 2024-2025 | Each agent optimized for its role, fresh context windows |

## Open Questions

1. **Section 3 vs Section 5 slide count balance**
   - What we know: Phase 3 needs ~12-15 slides total, split across two sections
   - What's unclear: Exactly how many for Section 3 (mental model) vs Section 5 (lifecycle)
   - Recommendation: 4-5 for Section 3, 8-10 for Section 5. Section 5 has more content and is the core promise fulfillment. Section 3 is setup/context.

2. **Self-referential examples or generic project?**
   - What we know: Using this project's own .planning/ files as examples is authentic but meta
   - What's unclear: Will "a presentation about GSD, built with GSD" confuse the audience or impress them?
   - Recommendation: Use a generic REST API project scenario for artifact examples. It's more relatable. Reference that GSD built this presentation only if it fits naturally (e.g., a brief mention).

3. **Composable flags — Section 3 or Section 5?**
   - What we know: Flags are already mentioned in Phase 2's `/gsd-quick` slide ("Composable: `--discuss` · `--research` · `--full`")
   - What's unclear: Where to show the deeper explanation — Section 3 (as part of "how GSD adapts") or Section 5 (as part of the workflow)
   - Recommendation: Section 5, integrated into the workflow discussion. "När du kör `/gsd-quick` kan du lägga till..." — this avoids repetition and puts flags in context where they make sense.

## Validation Architecture

### Test Framework
| Property | Value |
|----------|-------|
| Framework | PowerShell string matching (same as Phase 2) |
| Config file | None — inline verification commands |
| Quick run command | `powershell -Command "$c = Get-Content slides.md -Raw; ..."` |
| Full suite command | Same as quick run — all checks in one pass |

### Phase Requirements → Test Map
| Req ID | Behavior | Test Type | Automated Command | File Exists? |
|--------|----------|-----------|-------------------|-------------|
| DEEP-01 | Core workflow overview slides exist in Section 5 | automated | `$c -match 'new-project.*discuss.*plan.*execute.*verify' -or ($c -match 'livscykeln' -and $c -match 'discuss' -and $c -match 'verify')` | ❌ Wave 0 |
| DEEP-02 | Agent architecture slide exists in Section 3 | automated | `$c -match 'orchestrator' -and $c -match 'agents'` | ❌ Wave 0 |
| DEEP-03 | Planning artifacts slide(s) with .planning/ examples | automated | `$c -match '\.planning/' -and $c -match 'ROADMAP' -and $c -match 'STATE'` | ❌ Wave 0 |
| DEEP-04 | Persistent memory slide with resume-work | automated | `$c -match 'resume-work' -or $c -match 'projektminne' -or $c -match 'session'` | ❌ Wave 0 |
| DEEP-05 | Verification slide with goal-backward concept | automated | `$c -match 'task completion.*goal' -or ($c -match 'Task.*klara' -and $c -match 'mål.*uppnått')` | ❌ Wave 0 |
| DEEP-06 | Composable flags shown in context | automated | `$c -match '--discuss' -and $c -match '--research' -and $c -match '--full'` already in Phase 2 content; Phase 3 adds deeper context | ✅ Partial |
| PRAC-08 | Project lifecycle mentioned | automated | `$c -match 'new-project' -and ($c -match 'cleanup' -or $c -match 'livscykel' -or $c -match 'workspace')` | ❌ Wave 0 |

### Sampling Rate
- **Per task commit:** `powershell -Command "$c = Get-Content slides.md -Raw; [run relevant checks]"`
- **Per wave merge:** Full suite — all requirement checks in one pass
- **Phase gate:** Full suite green + human visual verification before `/gsd-verify-work`

### Wave 0 Gaps
- [ ] No existing test infrastructure for Phase 3 checks — all verification commands are inline PowerShell
- [ ] Human visual verification (Marp preview) is required as final gate — cannot be fully automated

*(Note: This matches Phase 2's validation approach — inline PowerShell checks + human Marp preview)*

## Sources

### Primary (HIGH confidence)
- `~/.copilot/get-shit-done/workflows/new-project.md` — Full lifecycle initialization, 9 steps, 1250 lines
- `~/.copilot/get-shit-done/workflows/discuss-phase.md` — Decision capture for downstream agents
- `~/.copilot/get-shit-done/workflows/plan-phase.md` — Research → plan → verify loop
- `~/.copilot/get-shit-done/workflows/execute-phase.md` — Wave-based parallel execution, orchestrator pattern
- `~/.copilot/get-shit-done/workflows/verify-phase.md` — Goal-backward verification, 3 truth levels
- `~/.copilot/get-shit-done/workflows/verify-work.md` — Human UAT, conversational testing
- `~/.copilot/get-shit-done/workflows/quick.md` — Composable flags (--discuss, --research, --full)
- `~/.copilot/get-shit-done/workflows/resume-project.md` — Session continuity from STATE.md
- `~/.copilot/get-shit-done/workflows/progress.md` — Project status + intelligent routing
- `~/.copilot/get-shit-done/workflows/pause-work.md` — Structured handoff files
- `~/.copilot/get-shit-done/workflows/cleanup.md` — Milestone phase archival
- `~/.copilot/get-shit-done/references/verification-patterns.md` — 4 verification levels
- `~/.copilot/agents/*.agent.md` — 18 specialized agent definitions
- `.planning/` directory of this project — real-world artifact examples

### Secondary (MEDIUM confidence)
- Phase 2 PLAN.md and SUMMARY.md — established slide patterns and conventions
- TERMINOLOGY.md — language policy verification

### Tertiary (LOW confidence)
- None — all findings verified from primary sources

## Metadata

**Confidence breakdown:**
- Standard stack: HIGH — same as Phase 2, no changes
- Architecture: HIGH — all GSD details verified from source files
- Content design: HIGH — patterns established by Phase 2, agent architecture verified
- Pitfalls: HIGH — based on real presentation design experience and Phase 2 learnings

**Research date:** 2026-04-15
**Valid until:** 2026-05-15 (stable — Marp and GSD architecture unlikely to change)
