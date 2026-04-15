# Architecture Patterns: GSD Presentation

**Domain:** Developer education / technical presentation (45-minute slot)
**Researched:** 2025-07-17
**Overall confidence:** HIGH — presentation architecture principles are well-established; GSD-specific content verified against actual framework source

## Recommended Presentation Architecture

### Narrative Arc: "The Ladder"

The presentation follows a **progressive complexity** arc — not a sales pitch arc. This is critical for a mixed audience of skeptics and early adopters.

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  Pain Recognition ──► Quick Win ──► Deeper Power ──►    │
│  "You know this"    "This easy"   "Goes further"        │
│                                                         │
│            ──► Mental Model ──► Your Scenarios ──►      │
│              "How to think"    "Your daily work"        │
│                                                         │
│                          ──► Monday Morning Action      │
│                             "Start here"                │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

**Why this arc, not "features tour":** A feature parade loses skeptics at slide 3. The ladder arc hooks with shared pain, proves value with the simplest possible example, then earns permission to go deeper. Early adopters stay engaged because each rung adds depth they haven't explored.

### Audience Strategy

| Audience Segment | Hook | Sustained By | Converted By |
|------------------|------|--------------|--------------|
| Skeptics | Pain recognition (Section 1) | Minimal "why", fast to "how" | Quick win — /gsd-fast in 30 seconds |
| Curious | Framework positioning (Section 2) | Seeing progressive complexity | Mental model click — agents concept |
| Early Adopters | Deep-dive (Section 5) | Architecture details, advanced flags | Scenarios they haven't tried yet |

---

## Section Architecture (8 sections, 45 minutes)

### Section 1: The Problem — "Var är vi idag?" (5 min)

**Purpose:** Shared pain recognition. Establish that raw AI assistance plateaus.

**Content:**
- AI coding tools progression: autocomplete → chat → inline edit → agent mode
- The ceiling: context loss between sessions, no structured approach, repeating yourself
- The gap between "impressive demo" and "daily workflow tool"
- Frame: "Frameworks solve the gap between chatbot and engineering partner"

**Slide budget:** 4-5 slides
**Tone:** Observational, not selling. "You've probably experienced..."
**Key slide:** Before/after — unstructured AI chat vs structured framework output

**Information dependencies:** None — this is the foundation.

**Anti-pattern to avoid:** Don't list AI tool problems for 5 minutes. Show ONE relatable scenario (e.g., asking AI to build something, it loses context at step 4, you re-explain everything), then move on.

---

### Section 2: Framework Landscape — "Vad finns?" (3 min)

**Purpose:** Position GSD in context. Legitimize the category. Brief — not a comparison talk.

**Content:**
- One slide: spectrum from prompt engineering → agent frameworks → orchestrated workflows
- GSD vs BMAD positioning (2 sentences each, not a feature matrix)
- Key insight: frameworks structure the conversation between developer and AI — you provide intent, framework provides process

**Slide budget:** 2-3 slides
**Tone:** Contextual. "Here's the landscape, here's where GSD sits."

**Information dependencies:** Section 1 (why frameworks exist).

**Anti-pattern to avoid:** Don't turn this into a 10-minute comparison. The audience doesn't need to evaluate alternatives — they need enough context to understand the category. If they want comparison, point to a resource. This section must stay at 3 minutes max.

---

### Section 3: GSD Mental Model — "Hur fungerar det?" (5 min)

**Purpose:** Give the audience a conceptual framework before showing commands. Without the mental model, commands feel like magic incantations.

**Content:**
- GSD = orchestrator with specialized agents (researcher, planner, executor, verifier)
- The core loop: You describe intent → GSD structures the work → agents execute → you verify
- The `.planning/` directory: project memory that survives between sessions
- Key principle: **you're always in control** — GSD proposes, you approve, agents execute
- Visual: the agent architecture diagram (orchestrator → spawns → agents → produce artifacts)

**Slide budget:** 4-5 slides
**Tone:** Explanatory. "Think of it as..."
**Key slide:** Architecture diagram — orchestrator in center, agent types around it, artifacts below

**Information dependencies:** Section 2 (what frameworks are).

**Design note:** This section is where skeptics either lean in or check out. The "you're always in control" message is critical. Show that GSD doesn't "take over" — it structures your intent into executable plans that you can inspect, modify, and approve.

---

### Section 4: The On-Ramp — "Börja enkelt" (8 min) ⭐ CORE SECTION

**Purpose:** Lowest-friction entry point. Show that you can get value in 30 seconds without understanding the full system.

**Content — progressive complexity ladder:**

**Rung 1: `/gsd-fast` (2 min)**
- Zero overhead — no planning files, no subagents
- Example: `"/gsd-fast fix the typo in README"` → atomic commit, done
- Scope: ≤3 file edits, trivial tasks
- Message: "If this is all you ever use, you're already ahead"

**Rung 2: `/gsd-do` (2 min)**
- Smart router — describe what you want in plain language
- GSD figures out which command to run
- Example: `"/gsd-do I need to refactor the auth module"` → routes to /gsd-quick
- Message: "Don't memorize commands — just describe what you need"

**Rung 3: `/gsd-quick` (3 min)**
- Small tasks with actual planning structure
- Spawns planner + executor, creates PLAN.md and SUMMARY.md
- Composable flags: `--discuss`, `--research`, `--full`
- Example: `"/gsd-quick --research add caching to the API layer"`
- Message: "When a task needs thinking before doing"

**Rung 4: Teaser of full workflow (1 min)**
- "But when you're building something bigger, there's a full lifecycle..."
- Bridge to Section 5

**Slide budget:** 8-10 slides (more slides here, moved through faster — command examples)
**Tone:** Practical, demonstrative. "Here's exactly what you type."
**Key slide:** The complexity ladder visual — 4 rungs, each with command + when to use it

**Information dependencies:** Section 3 (agent concept, .planning/ directory concept).

**Why this is the core section:** This is where skeptics convert. They see that the lowest rung costs nothing — no setup, no ceremony, just `/gsd-fast "fix the thing"`. The on-ramp makes adoption feel safe: start small, graduate when ready.

---

### Section 5: Full Workflow — "Hela livscykeln" (12 min) ⭐ DEEPEST SECTION

**Purpose:** Show the complete project lifecycle for non-trivial work.

**Content — lifecycle walkthrough:**

**5a: Project initialization (4 min)**
- `/gsd-new-project`: one command → questioning → research → requirements → roadmap
- The deep questioning phase: GSD asks YOU what you want (not the other way around)
- Research: 4 parallel researcher agents investigate the domain
- Output: PROJECT.md, REQUIREMENTS.md, ROADMAP.md, STATE.md
- Show: what a ROADMAP.md looks like (phases with scope and success criteria)

**5b: Phase lifecycle (5 min)**
- `/gsd-discuss-phase` → `/gsd-plan-phase` → `/gsd-execute-phase`
- Optional steps: discuss (capture your vision), research (investigate approaches)
- Plan: concrete tasks, verification criteria, file-level scope
- Execute: wave-based parallel execution, agents do the work
- Verify: automated checks, UAT with `/gsd-verify-work`
- Show: what a PLAN.md and SUMMARY.md look like

**5c: Project memory & continuity (3 min)**
- STATE.md: the project's memory across sessions
- `/gsd-resume-work`: pick up exactly where you left off
- `/gsd-progress`: visual progress bar, intelligent next-action routing
- Milestones: `/gsd-complete-milestone` → archive → `/gsd-new-milestone`
- Key insight: context survives between sessions — no more re-explaining

**Slide budget:** 10-12 slides
**Tone:** Walk-through. Show artifacts, show the flow.
**Key slides:**
- Lifecycle diagram: new-project → plan → execute → verify → complete
- Real ROADMAP.md snippet (redacted/simplified)
- The `.planning/` directory tree

**Information dependencies:** Section 3 (agent model), Section 4 (graduated from on-ramp to "what's beyond quick?").

**Pacing note:** This is the densest section. Use the lifecycle diagram as a visual anchor — keep returning to it to show "we're here now." Don't try to cover every command — cover the core loop and mention that commands like `/gsd-debug`, `/gsd-ship`, `/gsd-review` exist for specific needs.

---

### Section 6: Scenarios — "I din vardag" (7 min)

**Purpose:** Make it real. Map GSD commands to the audience's actual work patterns.

**Content — decision tree:**

| Scenario | Entry Point | Why |
|----------|-------------|-----|
| Fix a typo / config change | `/gsd-fast` | Trivial, no planning needed |
| Small bug fix (known cause) | `/gsd-quick` | Needs a plan but not research |
| Feature with unclear approach | `/gsd-quick --research` | Research before building |
| Add feature to existing project | `/gsd-quick --full` or new milestone | Depends on scope |
| New project from scratch | `/gsd-new-project` | Full lifecycle |
| Brownfield: new milestone on existing codebase | `/gsd-map-codebase` → `/gsd-new-milestone` | Map first, then plan |
| Mysterious bug, no idea where | `/gsd-debug` | Scientific method debugging |
| Capture an idea for later | `/gsd-note` or `/gsd-plant-seed` | Zero friction capture |

**Slide budget:** 5-6 slides
**Tone:** Recognition-based. "If you're doing X, use Y."
**Key slide:** Decision flowchart — complexity on Y-axis, GSD command on each branch

**Information dependencies:** Sections 4 AND 5 (audience must know both on-ramp and full workflow to understand the routing).

**Engagement note:** This is where the audience maps GSD to their own work. Ask rhetorical questions: "Hur ofta sitter ni med en bugg och bara vill att AI ska fixa den? `/gsd-fast`." This section resets attention after the dense Section 5.

---

### Section 7: Best Practices — "Tänk så här" (3 min)

**Purpose:** Mindset shift. Not just "what to type" but "how to think."

**Content:**
- **Think in outcomes, not steps:** "Jag vill ha en auth-modul med JWT" not "Skapa en fil som heter..."
- **Trust but verify:** The verification loop exists for a reason — review PLAN.md before executing
- **Start with /gsd-fast, graduate up:** Don't jump to full workflow for everything
- **When NOT to use GSD:** Creative exploration, pair-programming style work, tiny edits where git commit is enough
- **The skeptic's challenge:** Use `/gsd-fast` for one week — 5 tasks. Then decide.

**Slide budget:** 3-4 slides
**Tone:** Coaching. "In my experience..."
**Key slide:** The anti-patterns — "Don't do this" list

**Information dependencies:** Sections 4, 5, 6 (all practical content).

---

### Section 8: Getting Started — "Börja på måndag" (2 min)

**Purpose:** Call to action. Remove friction between "this looks interesting" and "I'll try it."

**Content:**
- GSD is already installed (via Copilot CLI skills) — no setup needed
- First command to try: `/gsd-fast "add X to Y"` (literally anything)
- Second command: `/gsd-help` to see the full reference
- Resources: where to find docs, how to get help
- Q&A prompt

**Slide budget:** 2-3 slides
**Tone:** Encouraging, concrete. "On Monday, open your terminal and type..."
**Key slide:** "Ditt första kommando" — one big command on screen

**Information dependencies:** Everything prior. This is the capstone.

---

## Time Allocation Summary

| # | Section | Time | % of Total | Slides | Purpose |
|---|---------|------|------------|--------|---------|
| 1 | The Problem | 5 min | 11% | 4-5 | Pain recognition |
| 2 | Framework Landscape | 3 min | 7% | 2-3 | Context positioning |
| 3 | GSD Mental Model | 5 min | 11% | 4-5 | Conceptual foundation |
| 4 | The On-Ramp ⭐ | 8 min | 18% | 8-10 | Low-friction entry |
| 5 | Full Workflow ⭐ | 12 min | 27% | 10-12 | Deep capability |
| 6 | Scenarios | 7 min | 15% | 5-6 | Real-world mapping |
| 7 | Best Practices | 3 min | 7% | 3-4 | Mindset & tips |
| 8 | Getting Started | 2 min | 4% | 2-3 | Call to action |
| | **Total** | **45 min** | **100%** | **38-48** | |

**Balance check:**
- "Why" content (Sections 1-2): 8 min / 18% ✓ (minimal, as required)
- "How" content (Sections 3-6): 32 min / 71% ✓ (dominant, as required)
- "What next" content (Sections 7-8): 5 min / 11% ✓ (actionable close)

---

## Information Dependency Graph

```
Section 1 (Problem)
    │
    ▼
Section 2 (Landscape)
    │
    ▼
Section 3 (Mental Model) ◄── Critical gate: audience must grasp
    │                         agents + .planning/ before commands
    ▼
Section 4 (On-Ramp) ◄──── Core conversion moment
    │
    ▼
Section 5 (Full Workflow) ◄── Deepest content, builds on on-ramp
    │
    ├───────────┐
    ▼           ▼
Section 6    Section 7
(Scenarios)  (Best Practices)
    │           │
    └─────┬─────┘
          ▼
    Section 8 (Getting Started)
```

**Hard dependencies (cannot reorder):**
- Section 3 before Section 4 (need mental model before commands)
- Section 4 before Section 5 (on-ramp before full workflow — progressive complexity)
- Sections 4+5 before Section 6 (scenarios reference both levels)

**Soft dependencies (could theoretically move):**
- Section 1 could be shortened to 2 min if audience is pre-sold
- Section 2 could be cut entirely for an audience that already knows about agent frameworks
- Section 7 could merge into Section 6 as inline tips

---

## Attention Curve Management

```
Attention
  ▲
  │   ┌─┐
  │   │1│ ┌───┐         ┌──────┐          ┌────┐
  │   │ │ │ 3 │  ┌────┐ │  5a  │  ┌─────┐ │ 6  │  ┌─┐
  │   │ │ │   │  │ 4  │ │      │  │ 5c  │ │    │  │8│
  │   │ │ │   │  │    │ │      │  │     │ │    │  │ │
  │  ─┤ ├─┤   ├──┤    ├─┤      ├──┤     ├─┤    ├──┤ ├──
  │   │ │ │   │  │    │ │      │  │     │ │    │  │ │
  │   │ │ │   │  │    │ │  5b  │  │     │ │    │  │ │
  │   └─┘ └───┘  └────┘ └──────┘  └─────┘ └────┘  └─┘
  │  1   2   3      4      5a  5b   5c      6   7   8
  └──────────────────────────────────────────────────────►
  0    5    8   13    21      27  30   37  40  42  45 min
```

**Planned attention resets:**
- **Minute 0:** Opening hook — relatable pain scenario (high engagement)
- **Minute 8→13:** Transition from abstract (landscape) to concrete (mental model) — visual diagram resets attention
- **Minute 13→21:** On-ramp commands — each command is a mini-demo, natural engagement
- **Minute 27:** Mid-deep-dive attention dip — counter with artifact walkthrough (show real PLAN.md)
- **Minute 30→37:** Scenarios = recognition-based engagement ("oh, I do that!")
- **Minute 42:** Call to action — future-oriented, inherently engaging

---

## Document Architecture (Wiki/Repo Companion)

The markdown companion document mirrors the presentation but serves a different purpose: **reference after the talk, not narrative during it.**

### Document Structure

```
gsd-presentation.md (or similar)
├── 1. Introduktion
│   ├── Problemet med ostrukturerad AI-assistans
│   └── Vad är ett agent framework?
├── 2. GSD i korthet
│   ├── Arkitektur: orchestrator + agents
│   ├── .planning/ — projektets minne
│   └── Kärnprincip: du bestämmer, GSD strukturerar
├── 3. Kom igång — On-Ramp
│   ├── /gsd-fast — triviala tasks
│   ├── /gsd-do — smart routing
│   ├── /gsd-quick — tasks med planering
│   └── Vilken ska jag välja? (beslutsträd)
├── 4. Full Workflow
│   ├── /gsd-new-project — från idé till roadmap
│   ├── Phase lifecycle: plan → execute → verify
│   ├── Projektminne: STATE.md och /gsd-resume-work
│   └── Milestones och arkivering
├── 5. Scenarion
│   ├── Greenfield-projekt
│   ├── Brownfield: ny feature i befintlig kodbas
│   ├── Buggfixar och debugging
│   └── Quick fixes och config-ändringar
├── 6. Best Practices
│   ├── Tänk i outcomes
│   ├── Trust but verify
│   ├── När du INTE ska använda GSD
│   └── Gradvis adoption
├── 7. Referens
│   ├── Kommandoöversikt (alla /gsd-* kommandon)
│   ├── .planning/ filstruktur
│   └── Länkar och resurser
└── Appendix
    └── GSD vs BMAD — kortjämförelse
```

**Key difference from slides:** The document includes full command references, longer examples, and the comparison appendix that was deliberately kept brief in the presentation. A developer reading this after the talk can use it as a reference.

---

## Patterns to Follow

### Pattern 1: Progressive Disclosure in Technical Education
**What:** Introduce concepts at the simplest level first, add complexity only when the audience has absorbed the prior level.
**When:** Always, for mixed-audience technical content.
**Application:** The on-ramp ladder (/gsd-fast → /gsd-do → /gsd-quick → full workflow) IS progressive disclosure. Each section builds one level of complexity.

### Pattern 2: Concrete Before Abstract
**What:** Show the command/output before explaining the architecture behind it.
**When:** Whenever introducing a new concept.
**Application:** In Section 3, show a `/gsd-fast "fix typo"` command and its result BEFORE explaining the agent architecture. Let the audience see value, then explain mechanism. Exception: Section 3 intentionally goes abstract-first because the mental model is needed to make sense of the command flags in Section 4.

### Pattern 3: The "Permission Ramp"
**What:** Each section earns the audience's permission to go deeper. You can't take 12 minutes on full workflow (Section 5) without first proving value with the 30-second on-ramp (Section 4).
**When:** Any technical talk where depth varies.
**Application:** Section 4 → Section 5 transition. If the audience doesn't buy the on-ramp, the deep-dive lands flat.

### Pattern 4: Decision Tree as Takeaway
**What:** A flowchart or matrix that maps audience situations to recommended actions.
**When:** Tool adoption presentations.
**Application:** Section 6's scenario table. This is the slide people photograph/screenshot. Design it to be self-contained.

---

## Anti-Patterns to Avoid

### Anti-Pattern 1: The Feature Parade
**What:** Listing every GSD command with a slide each.
**Why bad:** GSD has 40+ commands. A parade kills attention and makes the tool feel overwhelming — the exact opposite of the on-ramp message.
**Instead:** Cover 6-8 commands in depth (fast, do, quick, new-project, plan-phase, execute-phase, progress, debug). Mention others exist. Point to /gsd-help.

### Anti-Pattern 2: The Apology Tour
**What:** "I know some of you are skeptical about AI tools..."
**Why bad:** Patronizing. Highlights division instead of shared interest.
**Instead:** Lead with pain everyone shares. Let the tool prove itself through the on-ramp demo. Skeptics convert through evidence, not reassurance.

### Anti-Pattern 3: The Deep Internals Dive
**What:** Explaining how GSD's agent spawning works, wave-based execution internals, model profiles, etc.
**Why bad:** The audience is users, not contributors. Internals are fascinating to builders but irrelevant to adopters.
**Instead:** Stay at the "what it does for you" level. One architecture diagram is enough. The agent concept matters; the agent implementation doesn't.

### Anti-Pattern 4: The Sales Pitch Tone
**What:** "GSD is amazing, it will transform your workflow, you'll never go back."
**Why bad:** Developers have finely-tuned BS detectors. Hype backfires with technical audiences.
**Instead:** "Here's what it does. Try it. Form your own opinion." Let the on-ramp demo be the argument.

---

## Slide Design Principles (Marp-Specific)

| Principle | Rationale |
|-----------|-----------|
| Dark theme, monospace for code | Developer-familiar visual language |
| One idea per slide | 45 min = fast pacing, no time for dense slides |
| Command examples: full-bleed code blocks | Commands must be readable from the back row |
| Diagrams: simple boxes and arrows | Not UML — Marp's markdown-native diagrams or simple ASCII |
| Swedish body text, English commands/terms | Match the svengelska policy from PROJECT.md |
| Section divider slides | Clear visual breaks between sections (numbered, titled) |

---

## Build Order for Materials

The materials should be built in this order — **payload first, framing second:**

| Build Order | Section | Rationale |
|-------------|---------|-----------|
| 1st | Section 4: On-Ramp | Core value proposition. If this section doesn't land, nothing else matters. Build and polish first. |
| 2nd | Section 5: Full Workflow | Main content mass. Needs artifact examples (ROADMAP, PLAN, etc.) that take time to craft. |
| 3rd | Section 6: Scenarios | Ties sections 4+5 together. Can't write good scenarios without knowing what was covered. |
| 4th | Section 3: Mental Model | Architecture diagram and agent explanation. Easier to write when you know exactly what concepts sections 4+5 need pre-loaded. |
| 5th | Section 1: The Problem | The hook. Easier to write a sharp opening when you know the payload it's setting up. |
| 6th | Section 2: Landscape | Brief context framing. Write last for slides — it's a thin section. |
| 7th | Section 7: Best Practices | Emerges naturally from sections 4+5+6. |
| 8th | Section 8: Getting Started | Simple call-to-action. Build last. |
| Last | Companion document | Expand slides into full reference after the presentation narrative is locked. |

**Rationale:** Writing the opening first is tempting but wrong — you don't know what you're setting up yet. Writing Section 4 first forces you to crystallize the core message: "you can start in 30 seconds." Everything else flows from there.

---

## Scalability Considerations

| Concern | 30-min slot | 45-min slot (target) | 60-min slot |
|---------|-------------|---------------------|-------------|
| Sections 1-2 | Merge into 3 min | 8 min | 10 min |
| On-ramp (4) | 5 min, skip /gsd-do | 8 min | 10 min + live examples |
| Full workflow (5) | 8 min, cut 5c | 12 min | 18 min + live demo |
| Scenarios (6) | 3 min, matrix only | 7 min | 10 min + audience Q&A |
| Best practices (7-8) | 2 min combined | 5 min | 7 min + discussion |
| Q&A | Skip or 2 min | End of Section 8 | Dedicated 5 min |

**Flexibility buffers:** If running long, cut Section 2 (landscape) to 1 slide. If running short, expand Section 6 scenarios with audience interaction.

---

## Sources

- GSD framework source: `~/.copilot/get-shit-done/workflows/` (verified against actual workflow definitions)
- GSD help reference: `~/.copilot/get-shit-done/workflows/help.md` (command reference verified)
- Presentation architecture: Established patterns from technical education — progressive disclosure, concrete-before-abstract, attention curve management (HIGH confidence — stable domain knowledge)
- Marp slide framework: Markdown-based presentation tool (verified in PROJECT.md as chosen format)
