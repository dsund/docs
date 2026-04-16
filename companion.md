# Arbeta effektivt med AI Agent Frameworks — GSD

> Kompletterande dokument till presentationen. Kan läsas standalone.

## 1. Introduktion

### Problemet med ostrukturerad AI-assistans

"Jag har förklarat arkitekturen tre gånger — i tre olika chattar."

Det här är vardagen för utvecklare som använder AI-assistenter utan struktur. Du öppnar en ny chat, beskriver systemet, fattar beslut, bygger en lösning — och nästa dag börjar du om från noll. Kontexten är borta. Besluten är borta. Progressen existerar bara i dina egna anteckningar, om du ens hann skriva några.

Problemet handlar inte om att verktygen är dåliga. Copilot, ChatGPT och andra AI-assistenter är remarkabelt kapabla. Problemet är att de saknar tre fundamentala egenskaper som krävs för att hantera riktigt arbete:

**Kontext** — varje session börjar från noll. De beslut du tog igår, den arkitektur du valde förra veckan, den progress du gjorde i morse — allt är borta när du startar en ny chat. Du kompenserar med copy-paste av prompts, men det skalas inte.

**Struktur** — det finns ingen plan, ingen ordning, ingen nedbrytning av arbetet. AI:n gör sitt bästa med det du ger den just nu, men den har ingen uppfattning om helheten. Den tappar tråden mitt i komplexa uppgifter, eller levererar delar som inte hänger ihop.

**Kvalitet** — "3 tasks klara!" Men fungerar det? AI:n rapporterar att filer skapats och kod skrivits, men ingen kontrollerar om det faktiska målet är uppnått. En login-komponent kan vara "klar" utan att en enda användare faktiskt kan logga in.

Det här är inte unikt. Om vi zoomar ut ser vi ett bekant mönster:

```
Manuellt → IDE → Linter → CI → AI-assistent
```

Varje steg i den kedjan automatiserade det tråkiga och lät utvecklaren fokusera på det som spelar roll. IDE:n ersatte inte utvecklaren — den gav bättre verktyg. Lintern fångade misstag automatiskt. CI testade vid varje push. AI-assistenten är nästa steg i samma resa — inte en ersättning, utan en arbetsfördelning.

> Verktygen är kraftfulla. Det som saknas är ett system.

Det finns ett namn för lösningen: agent frameworks.

### Vad är ett agent framework?

Ett AI agent framework är ett system som ger en AI-assistent fyra egenskaper som den annars saknar:

```
┌──────────────────────────────────────┐
│           AGENT FRAMEWORK            │
│                                      │
│  LLM            Instruktioner        │
│  (hjärnan)      (hur den jobbar)     │
│                                      │
│  Verktyg        Minne                │
│  (vad den kan)  (vad den kommer      │
│                  ihåg)               │
└──────────────────────────────────────┘
```

**LLM (hjärnan)** — den stora språkmodellen som driver resonemang, kodgenerering och beslutsfattande. Det här är det du redan använder i Copilot eller ChatGPT. Utan de andra tre komponenterna är LLM:en begränsad till det du ger den i varje enskild prompt.

**Instruktioner (hur den jobbar)** — strukturerade regler för hur AI:n ska arbeta. Istället för att du manuellt promptar "skriv tester först" eller "committa varje ändring separat" varje gång, har ett framework inbyggda workflows som säkerställer att arbetet följer beprövade mönster.

**Verktyg (vad den kan)** — möjligheten att läsa filer, skriva kod, köra kommandon, söka i kodbasen och interagera med utvecklingsmiljön. Det är skillnaden mellan att ge råd och att faktiskt göra jobbet.

**Minne (vad den kommer ihåg)** — persistent lagring av beslut, arkitektur, progress och kontext mellan sessioner. Det här är den kritiska komponenten som saknas i vanliga AI-chattar. Med minne kan en AI-assistent fortsätta där den slutade — nästa dag, nästa vecka, eller efter en semester.

Utan framework: en AI-chat med copy-paste. Du ger kontext, får svar, kopierar kod, förlorar allt nästa session.

Med framework: en strukturerad assistent som minns vad du bygger, vilka beslut du tagit, var du är i processen, och vad som återstår. Den kan ta vid där den slutade och hålla ihop komplexa projekt över tid.

Skillnaden är som mellan att anteckna i ett block vs att använda ett projekthanteringsverktyg. Båda fungerar — men bara ett av dem skalas.

## 2. GSD i korthet

### Arkitektur: orchestrator + agents

GSD (Get Shit Done) är ett agent framework byggt för Copilot. Det bygger på tre grundstenar:

**Orchestrator** — koordinerar arbetet men bygger aldrig själv. Tänk projektledare: den vet vad som ska göras, i vilken ordning, och vem som ska göra det — men den skriver inte koden. Orchestratorn läser planer, fördelar uppgifter till specialiserade agents, och samlar in resultat.

**Specialiserade agents** — 18 stycken, var och en expert på sin roll. Istället för en generalist som gör allt medelmåttigt har GSD specialister som är optimerade för sin specifika uppgift.

**Persistent memory** — `.planning/`-mappen sparar allt mellan sessioner. Beslut, planer, resultat, progress — inget försvinner.

Agenterna är organiserade i fyra roller:

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

**Research-agents (4 st)** undersöker domänen innan arbetet börjar. De kartlägger vilka bibliotek som finns, vilka mönster som passar, vilka fallgropar som finns. Det är skillnaden mellan att gissa sig fram och att fatta informerade beslut.

**Planning-agents (4 st)** skapar detaljerade planer med tasks, beroendegrafar och waves. En plan i GSD är inte en TODO-lista — det är en execution-plan med tydliga acceptanskriterier och verifierbara mål.

**Execute-agent (1 st)** implementerar planen task för task. Varje task resulterar i en atomic commit. Agenten följer planen men har regler för att hantera avvikelser — buggar fixas automatiskt, medan arkitekturbeslut eskaleras till dig.

**Verify-agents (3 st)** utför goal-backward verification. De kontrollerar inte bara att tasks är utförda utan att det faktiska målet är uppnått — mer om det i Section 4.

Utöver dessa finns 6 specialister: debugger, codebase-mapper, UI-team (researcher, checker, auditor), och integration-checker. De aktiveras vid behov.

Plans inom samma wave körs parallellt. Waves körs i ordning. Det betyder att oberoende arbete sker samtidigt medan beroende arbete väntar tills föregående steg är klart:

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

### .planning/ — projektets minne

Hjärtat i GSD:s minnesförmåga är `.planning/`-mappen. Den skapas automatiskt när du startar ett projekt och innehåller alla artifacts som produceras under projektets gång:

```
.planning/
├── PROJECT.md        ← Vad vi bygger — vision, constraints, core value
├── REQUIREMENTS.md   ← Alla krav med spårbarhet till phases
├── ROADMAP.md        ← Phases med success criteria och beroenden
├── STATE.md          ← Var projektet är just nu — progress, beslut
└── phases/
    ├── 01-foundation/
    │   ├── 01-CONTEXT.md    ← Beslut från diskussionsfasen
    │   ├── 01-RESEARCH.md   ← Domänresearch
    │   ├── 01-PLAN.md       ← Executionsplan med tasks
    │   ├── 01-SUMMARY.md    ← Resultat efter execution
    │   └── 01-VERIFICATION.md ← Goal-backward verification
    └── 02-auth-system/
        └── ...
```

**PROJECT.md** definierar vad du bygger — vision, constraints, core value. Det är det dokument som alla agents refererar till för att förstå projektets syfte.

**REQUIREMENTS.md** innehåller alla krav med spårbarhet till vilken phase som adresserar dem. Det säkerställer att inget krav faller mellan stolarna.

**ROADMAP.md** bryter ner projektet i phases med success criteria och beroenden. Varje phase har ett tydligt mål som kan verifieras.

**STATE.md** är det dokument som gör session-persistens möjlig. Det håller koll på var projektet är just nu: vilken phase, vilken plan, vilken task. Det är det som gör att du kan stänga VS Code, komma tillbaka nästa vecka, och GSD fortsätter exakt där du slutade.

Varje phase producerar sin egen uppsättning artifacts. Inget försvinner — du kan alltid gå tillbaka och se vad som bestämdes och varför.

### Kärnprincip: du bestämmer, GSD strukturerar

GSD bygger på en tydlig arbetsfördelning:

**Du bestämmer:**
- Vad ska byggas
- Arkitekturbeslut
- Kvalitetskrav

**AI utför:**
- Research och analys
- Planering och implementation
- Verification execution

Utvecklaren blir arkitekt och reviewer — inte typist. Du definierar målet och granskar resultatet. Allt däremellan — research, planering, kodgenerering, testning — hanterar GSD.

Det här är inte samma sak som att ge upp kontroll. Tvärtom — det betyder att du fokuserar på de beslut som faktiskt kräver mänskligt omdöme: arkitektur, affärslogik, kvalitetsnivå, och prioriteringar. De mekaniska delarna — att skriva boilerplate, sätta upp tester, strukturera commits — delegeras till agenter som är bra på just det.

> Utvecklaren blir arkitekt och reviewer — inte typist.

## 3. Kom igång — On-Ramp

Du behöver inte använda hela GSD-maskineriet från dag ett. GSD erbjuder en graderad komplexitetsstege — börja med det enklaste kommandot och flytta uppåt när behoven växer.

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

### Förutsättningar och installation

**Du behöver:**
- Node.js ≥18
- VS Code med GitHub Copilot

**Installera GSD:**

```bash
$ npx get-shit-done-cc@latest
```

Klart. Inga andra dependencies. GSD installeras som Copilot skills och fungerar direkt i terminalen.

**Ditt första kommando:**

```bash
$ /gsd-fast "fix the typo in README"
✅ Done — zero setup needed
```

Ingen `.planning/`-mapp behövs. `/gsd-fast` fungerar direkt — perfekt som första smakprov.

### /gsd-fast — triviala tasks

`/gsd-fast` är det enklaste sättet att använda GSD. Ge den en kort beskrivning av vad du vill göra, så fixar den det direkt — utan planning, utan subagents, utan `.planning/`-mapp.

```bash
$ /gsd-fast "add .env to .gitignore"
✅ Done: Added .env to .gitignore
   Commit: a3f2e1d
   Files: .gitignore
```

Ytterligare ett exempel — uppdatera en dependency-version:

```bash
$ /gsd-fast "bump express from 4.18 to 4.21 in package.json"
✅ Done: Updated express version
   Commit: b7c4f2a
   Files: package.json
```

**Begränsningar:** Max 3 filändringar per anrop. Om uppgiften kräver mer, föreslår GSD automatiskt `/gsd-quick` istället. Varje ändring resulterar i en atomic commit, och om `.planning/` finns loggas den i STATE.md.

**När du ska använda det:**
- Typos och småfixar
- Config-ändringar (lägga till i `.gitignore`, uppdatera en env-variabel)
- Du vet exakt vad som behöver göras
- Det skulle ta dig 2 minuter att göra manuellt

### /gsd-do — smart routing

Ibland vet du vad du vill uppnå men inte vilket GSD-kommando som passar. `/gsd-do` löser det — beskriv vad du vill göra så väljer GSD rätt kommando åt dig.

```bash
$ /gsd-do "refactor the auth system"
Routing to: /gsd-add-phase
Reason: Multi-file refactor needs full phase
```

Ett enklare fall routas automatiskt till `/gsd-fast`:

```bash
$ /gsd-do "add a comment to the config file"
Routing to: /gsd-fast
Reason: Single-file change, trivial scope
```

`/gsd-do` gör aldrig jobbet själv — den analyserar din beskrivning och delegerar till rätt specialist. Det är ingångspunkten för den som vill beskriva arbetet naturligt utan att lära sig alla kommandon först.

**När du ska använda det:**
- Du vet inte vilket kommando som passar
- Du vill beskriva arbetet med egna ord
- Du är ny med GSD och vill låta systemet guida dig

### /gsd-quick — tasks med planering

`/gsd-quick` är för uppgifter som är för stora för `/gsd-fast` men inte kräver ett helt projekt. Den ger dig GSD:s struktur — planner + executor som subagents — utan overhead:en av research, phases och milestones.

```bash
$ /gsd-quick "add dark mode toggle to settings page"
Planning... 3 tasks identified
Executing... ██████████ 3/3
✅ Done — dark mode toggle added
```

Det som gör `/gsd-quick` kraftfull är de composable flags som låter dig anpassa assistansnivån:

| Flag | Lägger till | När |
|------|-------------|-----|
| `--discuss` | Diskussion före planning | "Jag vet inte alla detaljer" |
| `--research` | Research-agent undersöker | "Jag vet inte bästa sättet" |
| `--full` | Plan-checking + verification | "Det här måste bli rätt" |

Kombinera fritt efter behov:

```bash
$ /gsd-quick --discuss --research "add OAuth2 login"
Discussing... 3 questions asked
Researching... Best practices for OAuth2 with PKCE
Planning... 5 tasks identified
Executing... ██████████ 5/5
Verifying... Goal check passed ✅
```

Med `--discuss` ställer GSD frågor innan den planerar — bra när du inte har alla detaljer klara. Med `--research` undersöker en research-agent domänen först — bra när du inte vet bästa sättet att implementera något. Med `--full` lägger GSD till plan-checking (granskar planen innan execution) och verification (kontrollerar att målet uppnåddes).

**När du ska använda det:**
- Lägga till en ny feature
- Liten refaktorering
- Allt som är större än 3 filändringar men inte ett helt projekt

### Vilken ska jag välja? (beslutsträd)

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

Börja till vänster (enklare). Flytta höger (mer struktur) när du behöver mer. Du kan alltid börja med `/gsd-fast` eller `/gsd-do` och låta GSD föreslå ett mer strukturerat alternativ om uppgiften visar sig vara större än du trodde.

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
