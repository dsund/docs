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

## Känner du igen det här?

"Jag har förklarat arkitekturen tre gånger — i tre olika chattar."

- Ny chat = ny kontext. Varje gång.
- AI:n glömmer beslut du tog igår
- Ingen verification — "3 filer skapade!" men fungerar det?
- Copy-paste av samma prompt, om och om igen

> Ju större uppgiften, desto mer faller isär.

---

## Det som saknas

Verktygen är inte problemet — det som saknas är **struktur runt dem.**

- **Kontext** — varje session börjar från noll. Beslut, arkitektur, progress — borta.
- **Struktur** — ingen plan, ingen ordning. AI:n gör sitt bästa men tappar tråden.
- **Kvalitet** — "tasks klara!" men ingen kollar om målet faktiskt är uppnått.

> Verktygen är kraftfulla. Det som saknas är ett system.

---

## Nästa steg i en bekant resa

```
Manuellt → IDE → Linter → CI → AI-assistent
```

Varje steg automatiserade det tråkiga och lät utvecklaren fokusera på det som spelar roll. AI-assistenter är nästa steg — inte en ersättning, utan en **arbetsfördelning.**

> Det finns ett namn för det här: agent frameworks.

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

## Fem steg — från idé till verifierat resultat

```
  /gsd-new-project
       │
       ▼
  Discuss ──▶ Plan ──▶ Execute ──▶ Verify
  Beslut      Research   Waves      Mål ≠
  & val       + plan     + code     tasks
       │          │          │          │
  CONTEXT.md  PLAN.md   SUMMARY.md  VERIFICATION.md
```

Varje steg producerar artifacts → nästa steg läser dem.

---

## `/gsd-new-project` — det börjar här

```bash
$ /gsd-new-project
Vad vill du bygga? > En REST API för kundhantering
...
Requirements defined: 12 items
Roadmap: 5 phases created
Ready: /gsd-plan-phase 1
```

Djup-intervju → research → requirements → roadmap.
Allt sparas i `.planning/` — redo för nästa steg.

---

## Artifacts — vad som faktiskt sparas

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

Inte TODO-listor — *success criteria* som kan verifieras.

---

## Composable flags — anpassa assistansnivån

Kom ihåg `/gsd-quick` från förra sektionen?

| Flag | Lägger till | När |
|------|-------------|-----|
| `--discuss` | Diskussion före planning | "Jag vet inte alla detaljer" |
| `--research` | Research-agent undersöker | "Jag vet inte bästa sättet" |
| `--full` | Plan-checking + verification | "Det här måste bli rätt" |

Kombinera fritt: `/gsd-quick --discuss --research --full`

---

## GSD glömmer aldrig

```markdown
## Current Position

Phase: 2 of 5
Plan: 1 of 2
Status: Executing
Progress: [████░░░░░░] 35%

Stopped at: JWT middleware implementation
Resume: /gsd-resume-work
```

*3 dagar senare...*

---

## Återuppta exakt där du var

```bash
$ /gsd-resume-work
📍 Phase 2: Auth System — Plan 1, Task 3
   Stopped at: JWT middleware
   Kvar: 2 tasks i Plan 1, sedan Plan 2
```

STATE.md håller koll — du behöver inte komma ihåg.

---

## Hela projektets livscykel

**Starta:** `/gsd-new-project` — skapar allt från scratch

**Pausa & återuppta:** `/gsd-pause-work` → `/gsd-resume-work`

**Kolla status:** `/gsd-progress` — var står projektet?

**Städa upp:** `/gsd-cleanup` — arkivera klara phases

**Byt projekt:** Workspaces isolerar olika projekt

---

## Task completion ≠ Goal achievement

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
  ❌ Wired: RouteGuard importeras inte
  ❌ Functional: Inloggning fungerar inte
────────────────────────
Tasks klara — men målet INTE uppnått.
```

---

## Goal-backward verification

GSD frågar tre saker:

1. Vad måste vara **SANT** för att målet ska vara uppnått?
2. Vad måste **FINNAS** för att det ska vara sant?
3. Vad måste vara **KOPPLAT** för att det ska fungera?

Sedan verifierar den i fyra nivåer:
**Exists** → **Substantive** → **Wired** → **Functional**

> Inte "är koden skriven?" utan "fungerar det för användaren?"

---

<!-- _class: divider -->
<!-- _paginate: skip -->

# I din vardag

<hr>

<!-- Section 6: Scenarios — slides added by Phase 4 -->

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

---

## Greenfield — nytt projekt

```bash
$ /gsd-new-project
Vad vill du bygga? → "En REST API för kundhantering"
✅ 12 requirements defined
✅ 5 phases created
✅ Phase 1 planned and executed
✅ "Kan en användare registrera sig? ✅"
```

Från idé till verifierat resultat — utan att lämna editorn.

---

## Brownfield — kartlägg först

```bash
$ /gsd-map-codebase
Mapping... 7 analysis documents created
   .planning/codebase/ARCHITECTURE.md
   .planning/codebase/CONVENTIONS.md
   .planning/codebase/STRUCTURE.md
   ...
```

GSD förstår nu din kodbas — mönster, konventioner, beroenden.

---

## Brownfield — planera som vanligt

```bash
$ /gsd-add-phase "add search endpoint to user API"
Research uses codebase map → respects existing patterns
✅ Phase planned with 2 plans
```

Kartan gör skillnaden — utan den gissar agenten om din projektstruktur.

---

## Quick fix — `/gsd-fast`

```bash
$ /gsd-fast "fix the 401 error in login validation"
✅ Fixed token expiry check — src/auth.ts
```

Enkelt problem, känt scope → `/gsd-fast` löser det direkt.

---

## Behöver utredning? — `/gsd-debug`

```bash
$ /gsd-debug
✅ Root cause: missing dependency array in useEffect
```

Börja med `/gsd-fast`. Är problemet djupare — `/gsd-debug` utreder systematiskt.

---

## Rätt kommando är halva jobbet

Ni har verktygen. Men agentens resultat beror på hur ni tänker och kommunicerar.

Nästa steg: mindset shifts och best practices.

---

<!-- _class: divider -->
<!-- _paginate: skip -->

# Tänk så här

<hr>

<!-- Section 7: Best Practices — slides added by Phase 4 -->

---

## Tänk outcomes, inte steg

❌ **Steg-för-steg:**
> "Create a file called AuthService.ts, add a login method that accepts email and password, hash with bcrypt, create a JWT token..."

✅ **Outcome:**
> "Användare ska kunna logga in med email och lösenord"

GSD härleder stegen från målet. Du definierar vad som är klart — inte hur.

---

## Du bestämmer, AI utför

**Du:**
- Vad ska byggas
- Arkitekturbeslut
- Kvalitetskrav

**AI:**
- Research och analys
- Planering och implementation
- Verification execution

Utvecklaren blir arkitekt och reviewer — inte typist.

---

## Prompt crafting — var specifik

❌ `"Fix the bug"`
✅ `"The login form returns 401 when valid credentials are submitted"`

❌ `"Add a button"`
✅ `"Users should be able to export their data as CSV from the settings page"`

❌ `"Refactor this"`
✅ `"Refactor the auth module — it mixes JWT creation, validation, and user lookup in one file"`

Kontext + mål + constraints = bättre resultat.

---

## Tre vanliga misstag

**🚫 Vaga prompts** — agenten gissar fel, du gör om arbetet
→ Var specifik: mål + kontext + constraints

**🚫 Skippa verification** — "3/3 tasks done!" men inget fungerar
→ Kör alltid verification — task completion ≠ goal achievement

**🚫 Micro-management** — du dikterar varje fil och rad
→ Beskriv outcome, låt GSD planera vägen dit

---

## När du INTE ska använda agents

🚫 **Arkitekturbeslut** — agenten optimerar lokalt, du optimerar globalt

🚫 **Security-kritisk kod** — alltid manuell review oavsett

🚫 **Teamets lärande** — om syftet är att lära, inte leverera

🚫 **Regelverk & compliance** — agenten förstår inte juridiskt ansvar

🚫 **Det du inte kan reviewera** — delegera inte det du inte kan bedöma

> GSD gör dig effektivare — men det är fortfarande du som är ansvarig.

---

<!-- _class: divider -->
<!-- _paginate: skip -->

# Börja på måndag

<hr>

<!-- Section 8: Getting Started — slides added by Phase 4 -->

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

---

## Tack

Från "vad är det här?" till "jag vet exakt vilket kommando jag ska använda."

Beslutträdet ni fotograferade + installkommandot ni kör på måndag.

Frågor?
