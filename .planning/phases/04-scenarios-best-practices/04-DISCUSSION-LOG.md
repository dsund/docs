# Phase 4: Scenarios & Best Practices - Discussion Log

> **Audit trail only.** Do not use as input to planning, research, or execution agents.
> Decisions are captured in CONTEXT.md — this log preserves the alternatives considered.

**Date:** 2026-04-16
**Phase:** 04-scenarios-best-practices
**Areas discussed:** Decision tree format, Scenario depth & structure, Best practices & anti-patterns tone, "Start Monday" challenge

---

## Decision Tree Format

| Option | Description | Selected |
|--------|-------------|----------|
| ASCII flowchart | Branching yes/no paths (consistent with Phase 3 diagrams) | |
| Question-answer list | "Behöver du research? → /gsd-quick --research" (scannable) | |
| Table matrix | Situations as rows, commands as columns (compact) | |
| You decide | Pick what works best for a slide deck | ✓ |

**User's choice:** Agent's discretion — pick the best format for a slide deck
**Notes:** None

---

| Option | Description | Selected |
|--------|-------------|----------|
| Swedish situations, English commands | "Fixar en typo? → /gsd-fast" (consistent with deck) | |
| All English | Universal and terse | ✓ |
| You decide | Follow established pattern | |

**User's choice:** All English — keeps it universal and terse
**Notes:** Breaks from Swedish pattern specifically for the decision tree — makes it more "photographable"

---

| Option | Description | Selected |
|--------|-------------|----------|
| Quick commands only | Mirrors command spectrum (/gsd-fast, /gsd-quick, /gsd-do, full) | |
| Include specialist commands | /gsd-debug, /gsd-map-codebase, /gsd-insert-phase — full toolkit | ✓ |
| Quick + separate specialist slide | Overview tree + specialist reference | |

**User's choice:** Include specialist commands too — shows the full toolkit
**Notes:** Decision tree goes beyond Phase 2's spectrum to cover the complete command set

---

| Option | Description | Selected |
|--------|-------------|----------|
| One dense slide | The "cheat sheet" people photograph | |
| Split: overview + follow-ups | Multiple slides with branches expanded | |
| You decide | Based on how many commands need to fit | ✓ |

**User's choice:** Agent's discretion based on command count
**Notes:** None

---

## Scenario Depth & Structure

| Option | Description | Selected |
|--------|-------------|----------|
| Command highlights | Show commands + 2-3 line terminal snippet per scenario | |
| Before/after contrast | "Without GSD" vs "With GSD" | |
| Mini-walkthrough | Step-by-step, 2-3 slides each | |
| You decide | Pick best format for 60-min presentation | ✓ |

**User's choice:** Agent's discretion
**Notes:** None

---

| Option | Description | Selected |
|--------|-------------|----------|
| Equal weight | Same depth for all three scenarios | |
| Greenfield deepest | Shows full workflow best | |
| Brownfield deepest | Most relevant for teams with existing code | |
| You decide | Based on audience needs | ✓ |

**User's choice:** Agent's discretion
**Notes:** None

---

| Option | Description | Selected |
|--------|-------------|----------|
| Generic | "REST API", "legacy refactor" (relatable to everyone) | ✓ |
| Developer-tool adjacent | Close to audience's daily work | |
| You decide | | |

**User's choice:** Generic scenarios — relatable to any developer
**Notes:** None

---

## Best Practices & Anti-Patterns Tone

| Option | Description | Selected |
|--------|-------------|----------|
| Side-by-side do/don't | Concrete good vs bad examples | |
| Principles first | State mindset shift, then illustrate | |
| Anti-pattern gallery | Lead with what goes wrong | |
| You decide | | ✓ |

**User's choice:** Agent's discretion
**Notes:** None

---

| Option | Description | Selected |
|--------|-------------|----------|
| 1 slide | Brief mention with examples | |
| 2-3 slides | Honest treatment showing when manual is better | |
| You decide | | ✓ |

**User's choice:** Agent's discretion — but success criteria require real weight for credibility
**Notes:** None

---

| Option | Description | Selected |
|--------|-------------|----------|
| Concrete prompt examples | Show actual good/bad prompts | ✓ |
| General principles | "Be specific", "State the goal" | |
| You decide | | |

**User's choice:** Concrete prompt examples — show actual good/bad prompts
**Notes:** "Fix the bug" vs "The login form returns 401 when valid credentials are submitted"

---

## "Start Monday" Challenge

| Option | Description | Selected |
|--------|-------------|----------|
| /gsd-fast something | Lowest bar, proves tool works | |
| Pick a real backlog task + /gsd-quick | More commitment, more meaningful | |
| Install GSD + run one command | Installation as explicit step | |
| You decide | Pick most compelling close | ✓ |

**User's choice:** Agent's discretion
**Notes:** None

---

| Option | Description | Selected |
|--------|-------------|----------|
| Single action | One clear "do this" message | |
| Tiered | 3 levels matching comfort | |
| You decide | | ✓ |

**User's choice:** Agent's discretion
**Notes:** None

## Agent's Discretion

- Decision tree visual format (ASCII flowchart, table, Q&A list) — D-03
- Decision tree slide count (one dense or multiple) — D-04
- Scenario structure and format — D-05
- Scenario depth balance — D-06
- Best practices presentation style — D-08
- Escape hatches depth — D-09
- "Start Monday" challenge specifics — D-11

## Deferred Ideas

None — discussion stayed within phase scope
