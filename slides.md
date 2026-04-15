---
marp: true
theme: default
paginate: true
size: 16:9
---

<style>
/* Section divider slides — per decision D-04 */
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

/* Lead slides (title slide, closing slide) */
section.lead {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

/* Code blocks — terminal-style for command examples */
pre {
  font-size: 0.85em;
}
code {
  border-radius: 4px;
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

<!-- Section 1: The Problem — slides added by Phase 5 -->

---

<!-- _class: divider -->
<!-- _paginate: skip -->

# Vad finns?

<hr>

<!-- Section 2: Framework Landscape — slides added by Phase 5 -->

---

<!-- _class: divider -->
<!-- _paginate: skip -->

# Hur fungerar det?

<hr>

<!-- Section 3: GSD Mental Model — slides added by Phase 3 -->

---

## GSD — tre byggstenar

**Orchestrator** — koordinerar, bygger aldrig själv

**Specialiserade agents** — var och en expert på sin roll

**Persistent memory** — `.planning/` sparar allt mellan sessioner

> En AI som minns var du var, vad du bestämde, och vad som är kvar.

---

## 18 agents, 4 roller

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

\+ 6 specialister: debugger, codebase-mapper, UI-team m.fl.

---

## Wave-baserad execution

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

Plans inom samma wave körs parallellt. Waves körs i ordning.

---

## `.planning/` — projektets minne

```
.planning/
├── PROJECT.md        ← Vad vi bygger
├── REQUIREMENTS.md   ← Krav + spårbarhet
├── ROADMAP.md        ← Phaser + success criteria
├── STATE.md          ← Var vi är just nu
└── phases/
    ├── 01-foundation/
    │   ├── 01-CONTEXT.md    ← Beslut
    │   ├── 01-PLAN.md       ← Plan
    │   └── 01-SUMMARY.md    ← Resultat
    └── 02-auth-system/
        └── ...
```

Varje phase producerar artifacts. Inget försvinner.

---

<!-- _class: divider -->
<!-- _paginate: skip -->

# Börja enkelt

<hr>

<!-- Section 4: The On-Ramp — slides added by Phase 2 -->

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

---

## `/gsd-fast` — noll overhead

Perfekt för triviala ändringar. Ingen planning, inga subagents.

```bash
$ /gsd-fast "add .env to .gitignore"
✅ Done: Added .env to .gitignore
   Commit: a3f2e1d
   Files: .gitignore
```

≤ 3 file edits → atomic commit → loggat i STATE.md

---

## `/gsd-quick` — med planning

Små tasks med GSD-struktur. Planner + executor som subagents.

```bash
$ /gsd-quick "add dark mode toggle to settings page"
Planning... 3 tasks identified
Executing... ██████████ 3/3
✅ Done — dark mode toggle added
```

Composable: `--discuss` · `--research` · `--full`

---

## `/gsd-do` — smart routing

Beskriv vad du vill göra. GSD väljer rätt kommando.

```bash
$ /gsd-do "refactor the auth system"
Routing to: /gsd-add-phase
Reason: Multi-file refactor needs full phase
```

Aldrig gör jobbet själv — router till rätt specialist.

---

## Full Workflow — hela maskineriet

När uppgiften kräver research, planning och verification.

```bash
$ /gsd-new-project
Vad vill du bygga? > En REST API för kundhantering
Requirements defined: 12 items
Roadmap: 5 phases created
Ready: /gsd-plan-phase 1
```

Phases · milestones · persistent memory · goal-backward verification

---

## Kom igång — förutsättningar

**Du behöver:**
- Node.js ≥18
- VS Code med GitHub Copilot

**Installera GSD:**

```bash
$ npx get-shit-done-cc@latest
```

Klart. Inga andra dependencies.

---

## Ditt första kommando

```bash
$ /gsd-fast "fix the typo in README"
✅ Done — zero setup needed
```

Ingen `.planning/`-mapp behövs.
`/gsd-fast` fungerar direkt — perfekt som första smakprov.

---

## Men om uppgiften är större?

`/gsd-fast` fixar typon.
`/gsd-quick` lägger till en feature.

Men tänk om du ska bygga en hel REST API?
Eller refaktorera ett auth-system?

**Då behöver du hela workflow:en.**

*Nästa: Hela livscykeln →*

---

<!-- _class: divider -->
<!-- _paginate: skip -->

# Hela livscykeln

<hr>

<!-- Section 5: Full Workflow — slides added by Phase 3 -->

---

<!-- _class: divider -->
<!-- _paginate: skip -->

# I din vardag

<hr>

<!-- Section 6: Scenarios — slides added by Phase 4 -->

---

<!-- _class: divider -->
<!-- _paginate: skip -->

# Tänk så här

<hr>

<!-- Section 7: Best Practices — slides added by Phase 4 -->

---

<!-- _class: divider -->
<!-- _paginate: skip -->

# Börja på måndag

<hr>

<!-- Section 8: Getting Started — slides added by Phase 4 -->
