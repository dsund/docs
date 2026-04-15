# Feature Landscape

**Domain:** Developer education presentation — AI agent framework (GSD)
**Format:** 45-minute presentation + companion markdown document
**Researched:** 2025-01-27
**Confidence:** HIGH (based on primary source analysis of GSD v1.29.0 internals + domain expertise in developer education)

---

## Table Stakes

Features the audience expects. Missing any of these = presentation feels incomplete or confusing.

### Content Areas

| Content Area | Why Expected | Complexity | Notes |
|---|---|---|---|
| **Problem statement: why agent frameworks exist** | Audience needs the "why" before the "how" — especially for skeptics | Low | Context window limits, consistency across sessions, quality gates, project memory. 3-5 min max. |
| **What is an AI agent framework (conceptual)** | Mixed audience needs shared vocabulary before deep-dive | Low | Agent = LLM + instructions + tools + memory. Framework = orchestrated agents with defined workflow. |
| **GSD core workflow overview** | Central thesis of the talk — what GSD actually does | Med | new-project → discuss → plan → execute → verify. The "happy path" diagram. |
| **Getting started / on-ramp** | "How do I start?" is the first practical question | Low | Installation (`npx get-shit-done-cc@latest`), first command, what happens. |
| **Command spectrum (graduated complexity)** | Key usability concept — show that adoption isn't all-or-nothing | Med | `/gsd-fast` → `/gsd-quick` → `/gsd-do` → `/gsd-new-project`. The "ramp" from trivial to full workflow. |
| **Planning artifacts (`.planning/` directory)** | Audience needs to understand what GSD produces and why | Med | PROJECT.md, ROADMAP.md, STATE.md, phases/, config.json. This IS the project memory. |
| **Practical scenarios** | Developers learn by recognizing their own work in examples | Med | Greenfield project, brownfield/existing codebase, quick fix, debugging. At least 3 scenarios. |
| **Best practices for working with agents** | Actionable takeaway — what do they DO differently Monday morning | Med | Be specific about goals, let the framework handle planning, trust the workflow, when to intervene. |
| **Live-looking command examples** | Devs trust what they can type. Show actual terminal output, not abstract diagrams. | Low | Use code blocks with realistic prompts and outputs in both slides and companion doc. |
| **Actionable next steps** | "What do I do Monday morning?" is the question that converts understanding into adoption. | Low | Final slide(s) with exact first steps to try. Lowest-friction possible. |

### Presentation Mechanics

| Feature | Why Expected | Complexity | Notes |
|---|---|---|---|
| **Clear slide structure with visual hierarchy** | 45 min = ~30-35 slides max. Audience needs visual anchors. | Med | Marp-format slides. Use section dividers, progressive reveals. |
| **Companion document (wiki/repo-friendly)** | Standalone reference after the talk. The "textbook" that outlives the presentation. | Med | Deeper than slides — includes command reference, full scenarios, links. |
| **Swedish text with English terms preserved** | Language policy from project context — audience is Swedish devs | Low | "phase" not "fas", "roadmap" not "vägkarta". Natural svengelska throughout. |

---

## Differentiators

Content that elevates this presentation from "yet another tool walkthrough" to something developers remember and act on.

### Conceptual Differentiators

| Content Area | Value Proposition | Complexity | Notes |
|---|---|---|---|
| **The command spectrum as adoption strategy** | Shows agent frameworks aren't binary (all-in vs none). Start with `/gsd-fast`, grow to `/gsd-new-project`. This is GSD's killer UX insight. | Med | **Key slide.** Visual spectrum: `/gsd-fast` (≤3 edits, no planning, no subagents) → `/gsd-quick` (planner + executor, composable flags `--discuss --research --full`) → `/gsd-do` (smart router, natural language dispatch to 40+ commands) → `/gsd-new-project` (full workflow: questioning → research → requirements → roadmap → phases). Each step adds structure, not complexity. |
| **"Task completion ≠ Goal achievement" philosophy** | Reframes how developers think about AI output quality. GSD's verifier checks if the GOAL was met, not just if tasks were marked done. | Med | GSD's verification uses goal-backward analysis: (1) What must be TRUE for the goal? (2) What must EXIST for those truths? (3) What must be WIRED for artifacts to function? Then checks 4 levels: Exists → Substantive → Wired → Functional. Most AI tools stop at "task done." GSD asks "does it actually work?" |
| **Persistent project memory (STATE.md)** | Solves the "new context window = amnesia" problem. GSD remembers decisions, accumulated context, performance metrics across sessions. | Med | STATE.md = project memory. `/gsd-resume-work` and `/gsd-progress` restore context. Decisions persist, velocity tracked, todos preserved. `.planning/` directory IS the project's institutional memory. |
| **Agent specialization vs persona simulation** | GSD vs BMAD conceptual distinction. GSD uses workflow-centric agents (researcher, planner, executor, verifier). BMAD uses persona agents (PM, Architect, Dev, QA). GSD's approach: agents do ONE thing well with strict scope guardrails. | High | Critical comparison point. GSD has 18 agent types, each named by function (gsd-executor, gsd-verifier, gsd-plan-checker, gsd-nyquist-auditor), not by pretending to be humans. Each agent has defined tool access, downstream awareness, and explicit scope boundaries. |
| **Orchestrator pattern: "coordinates, not executes"** | Design principle that makes GSD scale. The orchestrator spawns agents, manages wave-based parallel execution, tracks state — but never writes code itself. | Med | Parallels to microservice orchestration. Execute-phase groups plans into waves by dependency, runs independent plans in parallel, then sequences waves. Devs who understand choreography vs orchestration will recognize this instantly. |

### Structural Differentiators

| Content Area | Value Proposition | Complexity | Notes |
|---|---|---|---|
| **GSD vs BMAD comparison** | Gives the audience a frame of reference — not to sell GSD but to show different philosophies exist | High | See detailed comparison table in section below. 2-3 slides max. |
| **The composable flags pattern** | `/gsd-quick --discuss --research --full` — dial quality up without changing commands. Shows thoughtful UX design. | Low | One command, four quality levels. Default: fast path. Add `--discuss` for clarification → captures decisions in CONTEXT.md. Add `--research` for investigation → spawns researcher agent. Add `--full` for plan-checking + verification. All composable. |
| **Brownfield awareness** | Most teams have existing code. `/gsd-map-codebase` creates structured understanding: 7 focused documents covering stack, architecture, structure, conventions, testing, integrations, concerns. | Med | Greenfield gets all the attention, but brownfield is where most real work happens. GSD auto-detects existing code and offers mapping before planning. Show how this changes the planning quality. |
| **Phase insertion and roadmap adaptation** | Real projects change mid-flight. `/gsd-insert-phase 7 "Critical fix"` creates Phase 7.1 — urgent work slotted in without disrupting numbering. | Low | Small feature, big mindset shift: the roadmap isn't frozen. Also: `/gsd-add-phase`, `/gsd-remove-phase` for full roadmap management. |
| **Cross-AI review** | `/gsd-review --phase 3 --all` invokes Gemini, Claude, Codex independently to review plans. Multi-AI peer review before execution. | Low | Mind-expanding concept. Feed reviews back into planning: `/gsd-plan-phase N --reviews`. Not day-one usage but shows GSD's philosophy of quality gates. |
| **Autonomous mode** | `/gsd-autonomous` drives all remaining phases: discuss → plan → execute for each, pausing only for explicit user decisions. | Low | Shows the end-game: trust the framework enough to let it run. Good for "where is this heading?" framing. |

### Pedagogical Differentiators

| Content Area | Value Proposition | Complexity | Notes |
|---|---|---|---|
| **"Skeptics to practitioners" arc** | Structure the talk as a journey from doubt to understanding. Open with skeptics' concerns, answer them through the content. | Med | Audience explicitly includes AI-skeptics (per PROJECT.md). Don't dismiss their concerns — address them structurally. Each section should answer an implicit skeptic question. |
| **Mental model shifts (not just tool features)** | Teach HOW to think about AI-assisted development, not just which buttons to press | High | Key shifts: (1) Think in outcomes, not steps — tell the agent WHAT, not HOW. (2) Your job is decisions, AI's job is execution. (3) Planning is the highest-leverage moment — deep questioning at new-project means better everything downstream. (4) Verification is non-negotiable — trust but verify. |
| **The "start Monday" challenge** | End with something they can literally do tomorrow morning | Low | `/gsd-fast "fix that typo"` — under 30 seconds. No project initialization required. Zero-friction first experience. |
| **Escape hatches: when NOT to use agents** | Builds trust. "This tool has limits and here's when to do it manually." | Low | Shows maturity, not blind advocacy. Earns credibility with skeptics. Examples: exploratory prototyping, pair programming with humans, security-critical code review. |
| **Anti-patterns section** | "Here's what NOT to do" builds credibility. Shows real-world experience with the tools. | Low | Vague prompts ("fix the code"), skipping verification, micro-managing agent execution, over-automating before understanding the workflow. |

---

## Anti-Features

Topics to deliberately NOT cover. Including these would dilute the message, waste time, or confuse the audience.

| Anti-Feature | Why Avoid | What to Do Instead |
|---|---|---|
| **GSD internals (gsd-tools.cjs, bin/ architecture, template system)** | Audience is users, not contributors. Internal implementation creates noise, not understanding. GSD has 18 agent types and complex orchestration — none of which users need to see. | Show user-facing commands and artifacts. Reference that there's a CLI toolchain "under the hood" without opening the hood. |
| **Every single /gsd-* command** | GSD has 40+ commands. Listing them all = death by bullet points. The help reference is 500+ lines. | Cover the 6-8 most important commands in depth. Mention `/gsd-help` for the full reference. Put command catalog in companion doc. |
| **AI model pricing and token economics** | Changes constantly, is vendor-specific, and distracts from the workflow education | Mention model profiles (quality/balanced/budget/inherit) as a one-liner. Point to docs for specifics. |
| **Live coding demo or scripted walkthrough** | Out of scope per PROJECT.md. Also risky in 45 min — live demos eat time unpredictably and can fail publicly. | Use annotated terminal output as static slides. Show realistic command/response pairs. The companion doc can include full session transcripts. |
| **Comprehensive BMAD tutorial** | This isn't a comparison talk — it's a GSD education talk. Deep BMAD coverage shifts focus. | 2-3 slides maximum. "Here's how BMAD approaches it, here's how GSD approaches it, here's why we chose GSD." |
| **Company-specific examples** | Per PROJECT.md — keep scenarios generic so anyone can relate. Avoids internal politics. | Use universal developer scenarios: "du bygger en ny API", "du fixar en bugg i legacy-kod", "du ska refaktorera auth-systemet". |
| **Prompt engineering deep-dive** | Separate topic entirely. GSD's philosophy is that the framework handles prompt engineering for you via structured workflows. | Brief best practices slide. How to describe goals, how to answer GSD's questions well. Not a prompt engineering course. |
| **Competing framework catalog** | Listing Cursor Rules, Windsurf, Roo Code, Aider etc. turns this into a market survey and overwhelms | Acknowledge the landscape exists. Use BMAD as the single comparison point because it represents a fundamentally different approach (persona-based vs workflow-based). |
| **Video/voiceover material** | Out of scope per PROJECT.md | Slides + companion doc are the deliverables. |
| **Configuration/setup tutorial** | 45 minutes isn't enough for both "how to install" and "how to use". Pick usage. | One slide with install command. Link to setup docs as appendix in companion doc. |
| **Hype/sales language** | Audience includes skeptics. "AI will revolutionize everything" will lose them instantly. | Factual, pragmatic tone. "This saves me time on X" not "this changes everything." Let the workflow speak for itself. |

---

## Feature Dependencies

```
Problem statement (why frameworks exist)
  └── What is an agent framework (conceptual vocabulary)
       ├── GSD vs BMAD comparison (two different philosophies)
       │    └── Why GSD for this team (bridges to the deep-dive)
       ├── Agent specialization concept
       │    └── GSD agent types (researcher, planner, executor, verifier)
       │         └── Orchestrator pattern ("coordinates, not executes")
       └── Core workflow overview (new-project → discuss → plan → execute → verify)
            ├── Command spectrum (graduated complexity)
            │    ├── /gsd-fast (trivial inline tasks, ≤3 edits)
            │    ├── /gsd-quick (planner + executor, composable flags)
            │    │    └── Composable flags (--discuss, --research, --full)
            │    ├── /gsd-do (smart router, natural language dispatch)
            │    └── /gsd-new-project (full workflow with research)
            ├── Planning artifacts (.planning/ structure)
            │    ├── STATE.md as project memory
            │    ├── ROADMAP.md as living plan
            │    └── Phase directories with PLAN.md / SUMMARY.md
            ├── Practical scenarios
            │    ├── Greenfield project (new-project → plan → execute)
            │    ├── Brownfield/existing code (map-codebase → new-milestone)
            │    ├── Quick fix (gsd-fast or gsd-quick)
            │    └── Phase insertion (mid-flight roadmap changes)
            └── Verification philosophy
                 └── "Task completion ≠ Goal achievement"
                      └── 4-level check: Exists → Substantive → Wired → Functional

Best practices & mental model shifts
  └── Anti-patterns (what NOT to do)
       └── "Start Monday" challenge (actionable close)
```

**Key dependency insight:** The comparison section MUST come before the GSD deep-dive. Without the taxonomy (persona-based vs workflow-based), the audience can't place GSD in their mental model. But the comparison must be brief enough that it doesn't steal focus from the GSD education.

**Second insight:** The command spectrum should come AFTER the full workflow overview. Audience needs to understand the "full picture" first, then see how GSD lets you enter at any level of complexity. This creates a "oh, I don't HAVE to do all that" relief moment.

---

## Presentation Flow Recommendation

Based on dependencies and the 45-minute constraint:

### Block 1: The Why (8-10 min)
1. **Problem statement** — What breaks when you just chat with AI? (context loss, inconsistency, no verification)
2. **What is an agent framework** — Shared vocabulary: agents, workflows, orchestration, memory
3. **Landscape overview** — BMAD (persona approach) vs GSD (workflow approach), 2-3 slides max

### Block 2: The What — GSD Deep-Dive (15-18 min)
4. **Core workflow** — new-project → discuss → plan → execute → verify (the "happy path" diagram)
5. **Agent types** — Researcher, Planner, Executor, Verifier — what each does, why specialized, how they collaborate
6. **Planning artifacts** — What gets created, what STATE.md remembers, why `.planning/` matters
7. **Verification philosophy** — "Task completion ≠ Goal achievement", goal-backward analysis

### Block 3: The How — Practical Usage (12-15 min)
8. **Command spectrum** — Start light, grow heavy: `/gsd-fast` → `/gsd-quick` → `/gsd-do` → `/gsd-new-project`
9. **Composable quality flags** — `--discuss`, `--research`, `--full` — dial quality up on demand
10. **Scenarios walkthrough** — Greenfield, brownfield, quick fix, debugging (2-3 min each)

### Block 4: The Mindset (5-7 min)
11. **Mental model shifts** — Think in outcomes, your job = decisions, planning = leverage, verify always
12. **Best practices & anti-patterns** — How to think, what to avoid, when NOT to use agents
13. **"Start Monday" challenge** — Install + `/gsd-fast "fix that README typo"` = done in 30 seconds

---

## MVP Recommendation

Prioritize these content areas if time runs short:

1. **Command spectrum** — The single most unique GSD concept. If they remember one thing, this is it. The graduated adoption path from zero to full workflow.
2. **Core workflow diagram** — The "poster" they can pin up. new-project → discuss → plan → execute → verify.
3. **Problem statement** — Without the "why", nothing else matters. Especially for skeptics.
4. **One practical scenario end-to-end** — At least one walkthrough showing GSD in action on a recognizable task.
5. **"Start Monday" challenge** — Zero-friction starting point drives actual adoption.

Defer if pressed for time:
- **Cross-AI review** (`/gsd-review`): Cool but niche. Save for follow-up session.
- **Autonomous mode**: Important concept but not day-one knowledge.
- **Phase insertion**: Important but not introductory material.
- **Model profiles**: Reference material, not presentation material.
- **Brownfield deep-dive**: Important but can be separate lunch-and-learn.

---

## Key Comparison: GSD vs BMAD

For the comparison slides (2-3 slides max):

| Dimension | GSD (Get Shit Done) | BMAD Method |
|---|---|---|
| **Philosophy** | Workflow-centric: orchestrate specialized agents through defined phases | Persona-centric: simulate a development team through AI role-play |
| **Agent naming** | By function: gsd-researcher, gsd-planner, gsd-executor, gsd-verifier | By role: Product Manager, Architect, Developer, QA |
| **Agent count** | 18 specialized agents (executor, verifier, plan-checker, nyquist-auditor, etc.) | ~5-6 persona agents |
| **Primary artifact** | Executable PLAN.md files with task-level granularity + VERIFICATION.md | Strategic documents (PRD, Architecture doc, User Stories) |
| **Workflow control** | Framework enforces: discuss → research → plan → execute → verify | User drives conversation between personas manually |
| **Scope management** | Strict guardrails: "Does this clarify HOW to implement or add NEW capability?" | Emergent through persona dialogue |
| **Memory** | STATE.md + `.planning/` directory = persistent cross-session project memory | Session-bound conversation history |
| **Entry point** | Graduated: `/gsd-fast` (30 sec) through `/gsd-new-project` (full workflow) | Typically starts with PM persona to create PRD |
| **Verification** | Automated goal-backward verification: Exists → Substantive → Wired → Functional | QA persona reviews conversationally |
| **Parallelization** | Wave-based parallel execution: independent plans run simultaneously | Sequential persona conversations |

**Key takeaway for slides:** Neither is "better." BMAD excels at strategic thinking and collaborative document generation. GSD excels at execution management, quality verification, and graduated adoption. GSD was chosen for this team because the primary need is **executing work reliably with quality gates**, not generating strategy documents. (BMAD comparison is MEDIUM confidence — core concepts are well-established but specific BMAD features may have evolved. Validate before presentation.)

---

## Sources

- **GSD Framework v1.29.0** — Primary source: full analysis of all workflow files (new-project.md, quick.md, fast.md, do.md, execute-phase.md, verify-phase.md, discuss-phase.md, research-phase.md, autonomous.md, help.md, transition.md, plan-phase.md), all 18 agent definitions, template system, references (model-profiles.md, verification-patterns.md), and CLI tooling. **HIGH confidence.**
- **GSD Help Reference** — Complete command catalog: 40+ commands across project init, phase planning, execution, debugging, milestone management, session management, review, shipping. **HIGH confidence.**
- **BMAD Method** — Based on training data knowledge of persona-based AI development framework. **MEDIUM confidence** — core concepts verified through multiple training sources but specific features may have evolved since training cutoff. Comparison is directionally correct but should be validated before presentation delivery.
- **Developer education presentation patterns** — Based on established principles: progressive disclosure, skeptic-to-practitioner narrative arc, cognitive load management, concrete-before-abstract pedagogy. **MEDIUM confidence** for general principles, **HIGH confidence** for structural recommendations.
