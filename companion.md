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

`/gsd-fast` och `/gsd-quick` räcker långt — men ibland är uppgiften för stor. Du ska bygga en hel applikation, refaktorera ett system, eller leverera en feature som spänner över flera moduler. Då behöver du hela maskineriet: research, planning, execution och verification.

### /gsd-new-project — från idé till roadmap

Allt börjar med en idé. `/gsd-new-project` tar den från en mening till en fullständig projektplan genom fem steg:

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

Varje steg producerar artifacts som nästa steg läser. Kedjan är inte linjär i praktiken — du kan gå tillbaka och revidera — men flödet ger struktur åt arbetet.

```bash
$ /gsd-new-project
Vad vill du bygga? > En REST API för kundhantering
...
Requirements defined: 12 items
Roadmap: 5 phases created
Ready: /gsd-plan-phase 1
```

**Discuss** — GSD genomför en djupintervju om vad du vill bygga. Den ställer frågor om scope, constraints, teknikval och kvalitetskrav. Svaren sparas i CONTEXT.md så att alla efterföljande agents har samma förståelse.

**Plan** — research-agents undersöker domänen (bibliotek, mönster, fallgropar) och planning-agents skapar detaljerade planer med tasks, beroenden och waves. Resultatet är PLAN.md — en executionsplan, inte en TODO-lista.

**Execute** — executor-agenten implementerar planen task för task. Varje task resulterar i en atomic commit. Plans inom samma wave körs parallellt, waves körs i ordning.

**Verify** — verify-agents kontrollerar att det faktiska målet är uppnått, inte bara att tasks är avbockade. Resultatet sparas i VERIFICATION.md.

### Phase lifecycle: plan → execute → verify

Varje phase i roadmappen har ett tydligt mål och verifierbara success criteria — inte TODO-listor:

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

Success criteria formuleras som påståenden som kan vara sanna eller falska. Det är det som gör verification möjlig — "kan en användare logga in?" har ett definitivt svar.

Inom varje phase organiseras arbetet i waves:

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

Plans som inte beror på varandra körs parallellt i samma wave. Plans med beroenden placeras i senare waves. Resultatet: snabbare execution utan att kompromissa med ordning.

### Projektminne: STATE.md och /gsd-resume-work

Det som skiljer GSD från en vanlig AI-chat är att inget försvinner. STATE.md håller koll på exakt var projektet befinner sig:

```markdown
## Current Position

Phase: 2 of 5
Plan: 1 of 2
Status: Executing
Progress: [████░░░░░░] 35%

Stopped at: JWT middleware implementation
Resume: /gsd-resume-work
```

Tre dagar senare öppnar du VS Code igen:

```bash
$ /gsd-resume-work
📍 Phase 2: Auth System — Plan 1, Task 3
   Stopped at: JWT middleware
   Kvar: 2 tasks i Plan 1, sedan Plan 2
```

STATE.md håller koll — du behöver inte komma ihåg. Det fungerar oavsett om det gått tre timmar eller tre veckor. Varje decision som tagits, varje fil som skapats, varje avvikelse som hanterats — allt finns dokumenterat i `.planning/`-strukturen.

### Milestones och arkivering

GSD hanterar inte bara enskilda phases utan hela projektets livscykel:

**Starta:** `/gsd-new-project` — skapar allt från scratch: PROJECT.md, REQUIREMENTS.md, ROADMAP.md, STATE.md.

**Pausa & återuppta:** `/gsd-pause-work` → `/gsd-resume-work` — spara och återställ kontext exakt.

**Kolla status:** `/gsd-progress` — var står projektet? Vilka phases är klara? Vad återstår?

**Städa upp:** `/gsd-cleanup` — arkivera klara phases för att hålla `.planning/` rent.

**Byt projekt:** Workspaces isolerar olika projekt i samma repo. Varje workspace har sin egen `.planning/`-struktur.

Milestones grupperar phases i versionerade leveranser (v1, v2). När en milestone är klar kan du köra retrospektiv, arkivera, och starta nästa.

### Goal-backward verification

Det här är kanske GSD:s viktigaste koncept. Traditionell task-checking ser ut så här:

```
✅ LoginComponent.tsx skapad
✅ jwt-utils.ts skapad
✅ RouteGuard.tsx skapad
────────────────────────
3/3 tasks klara! 🎉
```

Allt ser bra ut — men fungerar det? GSD:s goal-backward verification ställer tre frågor:

1. Vad måste vara **SANT** för att målet ska vara uppnått?
2. Vad måste **FINNAS** för att det ska vara sant?
3. Vad måste vara **KOPPLAT** för att det ska fungera?

Sedan verifierar den i fyra nivåer:

```
Goal: "Användare kan logga in"
  ✅ Exists: Alla filer finns
  ❌ Substantive: LoginComponent returnerar <div/>
  ❌ Wired: RouteGuard importeras inte
  ❌ Functional: Inloggning fungerar inte
────────────────────────
Tasks klara — men målet INTE uppnått.
```

**Exists** — finns filerna? Enklaste kontrollen. Nästan alltid "ja" men säger inget om kvalitet.

**Substantive** — har filerna meningsfullt innehåll? En komponent som returnerar `<div/>` klarar Exists men inte Substantive.

**Wired** — är komponenterna kopplade till varandra? Importeras RouteGuard i rätt routes? Anropas login-API:et från formuläret?

**Functional** — fungerar det faktiskt? Kan en användare logga in end-to-end?

> Inte "är koden skriven?" utan "fungerar det för användaren?"

Det här är skillnaden mellan "tasks done" och "goal achieved" — och det är anledningen till att GSD fångar problem som andra AI-assistenter missar.

### Phase insertion — `/gsd-insert-phase`

Du är mitt i Phase 3 av ett API-projekt. Under implementation inser du att du behöver en databasmigrering innan API-endpoints kan fungera. Att starta om hela projektet vore slöseri — allt du gjort hittills är korrekt.

```bash
$ /gsd-insert-phase "database migration setup" --before 3
✅ Phase 2.1 inserted: Database Migration
   Roadmap updated — Phase 3 becomes Phase 4
   Ready: /gsd-plan-phase 2.1
```

GSD numrerar om roadmappen automatiskt och bevarar alla befintliga artifacts. Dina färdiga phases påverkas inte — Phase 1 och 2 är fortfarande klara. Den nya phase:en får ett decimalnummer (2.1) som placerar den i rätt ordning.

Det här är inte ovanligt i riktiga projekt. Requirements förändras, du upptäcker saknade steg, teamet beslutar att utöka scope. Istället för att starta om eller hacka runt problemet ger `/gsd-insert-phase` ett strukturerat sätt att anpassa planen.

**När du behöver det:**
- Du upptäcker ett saknat steg mitt i arbetet
- En extern dependency kräver förberedelse du inte planerade
- Scope utökas — en ny requirement behöver eget steg

### Autonomous mode — `/gsd-autonomous`

När du har kört GSD genom ett par projekt och litar på workflow:en finns nästa steg: autonomous mode.

Istället för att starta varje phase manuellt — plan, execute, verify, plan nästa — låter du GSD köra igenom hela pipeline:n utan att stanna mellan stegen:

```bash
$ /gsd-autonomous
Phase 1: Foundation ████████████ ✅
Phase 2: Auth       ████████████ ✅
Phase 3: API        ████████░░░░ executing...
```

GSD hanterar diskussion, planning, execution och verification för varje phase automatiskt. Om verification hittar problem skapar den gap-closure plans och kör om. Du kan göra annat under tiden och granska resultatet när det är klart.

**Viktigt:** Autonomous mode är inte för varje projekt. Det kräver:
- Tydliga requirements och väldefinierade phases
- Erfarenhet av GSD:s workflow — du vet vad du kan förvänta dig
- Tillit till att verification fångar problem

Tänk på det som skillnaden mellan att köra manuell växel och automat. Båda fungerar — men automat passar bäst när vägen är rak och du har kört den förut.

**När du ska använda det:**
- Projektet har tydliga requirements och phases
- Du har erfarenhet av GSD:s workflow och litar på verification
- Du vill köra en hel pipeline medan du gör annat

## 5. Scenarion

Olika situationer kräver olika GSD-kommandon. De här scenarierna visar vilka kommandon du ska välja i de vanligaste situationerna du möter som utvecklare.

### Greenfield-projekt

Du ska bygga något helt nytt — en REST API, en webbapp, en CLI-tool. Inget befintligt code att ta hänsyn till.

```bash
$ /gsd-new-project
Vad vill du bygga? → "En REST API för kundhantering"
✅ 12 requirements defined
✅ 5 phases created
✅ Phase 1 planned and executed
✅ "Kan en användare registrera sig? ✅"
```

Flödet för greenfield:
1. **`/gsd-new-project`** — definiera vision, requirements, roadmap
2. **`/gsd-plan-phase 1`** — planera första phase:en (eller låt GSD göra det automatiskt)
3. **`/gsd-execute-phase 1`** — bygg det
4. **`/gsd-verify-work`** — verifiera att phase-målet är uppnått
5. Fortsätt med Phase 2, 3, etc.

Från idé till verifierat resultat — utan att lämna editorn. Varje phase bygger på den föregående, och verification säkerställer att ingenting faller mellan stolarna.

### Brownfield: ny feature i befintlig kodbas

Du ska lägga till en feature i ett befintligt projekt. Koden är redan skriven av andra (eller av dig, för länge sedan). Du behöver förstå mönster, konventioner och beroenden innan du börjar.

```bash
$ /gsd-map-codebase
Mapping... 7 analysis documents created
   .planning/codebase/ARCHITECTURE.md
   .planning/codebase/CONVENTIONS.md
   .planning/codebase/STRUCTURE.md
   ...
```

`/gsd-map-codebase` skapar en kartläggning av den befintliga kodbasen. GSD analyserar arkitektur, kodkonventioner, filstruktur och beroenden. Det här blir grunden för alla efterföljande beslut.

```bash
$ /gsd-add-phase "add search endpoint to user API"
Research uses codebase map → respects existing patterns
✅ Phase planned with 2 plans
```

Med kartan som grund respekterar GSD befintliga mönster. Om projektet använder en viss mappstruktur, namnkonvention eller error-handling-strategi följer den nya koden samma stil.

> Kartan gör skillnaden — utan den gissar agenten om din projektstruktur.

### Buggfixar och debugging

En 401-error dyker upp i login-validationen. Hur du hanterar det beror på hur väl du förstår problemet.

**Enkelt problem, känt scope** — du vet var felet är:

```bash
$ /gsd-fast "fix the 401 error in login validation"
✅ Fixed token expiry check — src/auth.ts
```

**Komplext problem, behöver utredning** — du vet inte vad som orsakar det:

```bash
$ /gsd-debug
✅ Root cause: missing dependency array in useEffect
```

`/gsd-debug` utreder systematiskt. Den formulerar hypoteser, testar dem, och spårar sig fram till grundorsaken. Den hanterar sin egen session med checkpoints, så att du kan avbryta och återuppta.

Tumregel: börja med `/gsd-fast`. Är problemet djupare än du trodde — byt till `/gsd-debug`.

### Quick fixes och config-ändringar

Inte allt arbete är features eller buggar. Ibland behöver du bara:

```bash
$ /gsd-fast "add NODE_ENV=production to .env.example"
✅ Done: Updated .env.example
   Commit: c4d8e2f
   Files: .env.example
```

```bash
$ /gsd-fast "update the copyright year to 2026 in LICENSE"
✅ Done: Updated LICENSE
   Commit: f1a9b3c
   Files: LICENSE
```

Config-ändringar, typos, dependency-uppdateringar, `.gitignore`-tillägg — allt som tar under 2 minuter manuellt och berör max 3 filer. `/gsd-fast` är det rätta verktyget. Använd inte full workflow för en typo.

## 6. Best Practices

Att ha rätt verktyg är halva jobbet — den andra halvan är hur du tänker och kommunicerar med agenten. De här principerna hjälper dig att få ut mest möjligt av GSD.

### Tänk i outcomes

❌ **Steg-för-steg:**
> "Create a file called AuthService.ts, add a login method that accepts email and password, hash with bcrypt, create a JWT token..."

✅ **Outcome:**
> "Användare ska kunna logga in med email och lösenord"

Varför fungerar outcomes bättre? GSD härleder stegen från målet. Planning-agenten undersöker domänen, väljer libraries, bryter ner i tasks — och gör det ofta bättre än du själv hade gjort, för den har tillgång till research och mönsterigenkänning.

Du definierar vad "klart" ser ut. GSD planerar vägen dit.

Ytterligare ett exempel:

❌ `"Move all auth functions from utils.ts into a new auth/ folder with separate files for jwt.ts, password.ts, and middleware.ts"`

✅ `"Refactor the auth module — it mixes JWT creation, validation, and user lookup in one file"`

Det första dikterar implementationen. Det andra beskriver problemet och låter GSD hitta den bästa lösningen — som kanske ser helt annorlunda ut än vad du föreställde dig.

### Trust but verify

Lita på att GSD gör jobbet — men kör alltid verification.

Det är frestande att se "3/3 tasks done!" och gå vidare. Men som vi såg i Section 4: task completion ≠ goal achievement. En login-komponent kan vara "klar" utan att en enda användare kan logga in.

Praktiska råd:
- Använd `/gsd-verify-work` efter varje phase
- Använd `--full` flaggan på `/gsd-quick` för viktig kod
- Granska VERIFICATION.md — den visar exakt vad som kontrollerades och vad som passerade

Verification kostar lite extra tid men sparar mångdubbelt i omarbete. Det är skillnaden mellan att tro att det fungerar och att veta.

### Prompt crafting — var specifik

❌ `"Fix the bug"`
✅ `"The login form returns 401 when valid credentials are submitted"`

❌ `"Add a button"`
✅ `"Users should be able to export their data as CSV from the settings page"`

❌ `"Refactor this"`
✅ `"Refactor the auth module — it mixes JWT creation, validation, and user lookup in one file"`

❌ `"Make it faster"`
✅ `"The dashboard loads in 4 seconds — optimize database queries to bring it under 1 second"`

Formeln: **Kontext + mål + constraints = bättre resultat.**

GSD fungerar bäst när den förstår VAD du vill uppnå, VARFÖR det behövs, och vilka BEGRÄNSNINGAR som gäller. Ju mer specifik du är om problemet, desto bättre blir lösningen.

### Tre vanliga misstag

**🚫 Vaga prompts** — agenten gissar fel, du gör om arbetet.

Hur det ser ut: `"Fix the thing"` → agenten ändrar fel fil → du korrigerar → den ändrar fel sak → du ger upp och gör det manuellt.

Hur du undviker det: beskriv problemet specifikt. Vad händer? Vad borde hända? Var i koden finns problemet?

**🚫 Skippa verification** — "3/3 tasks done!" men inget fungerar.

Hur det ser ut: du ser gröna bockar och går vidare. Nästa phase bygger på kod som inte fungerar. Problem ackumuleras tills allt kollapsar.

Hur du undviker det: kör `/gsd-verify-work` eller använd `--full`. De 30 sekunder det tar sparar timmar av debugging.

**🚫 Micro-management** — du dikterar varje fil och rad.

Hur det ser ut: du skriver en 500-ord prompt som specificerar filnamn, imports, funktionsnamn och implementation. GSD gör exakt det du sa — men missar en bättre lösning.

Hur du undviker det: beskriv outcome, inte steg. Låt GSD:s planning-agent bestämma implementationen. Du kan alltid granska och justera efteråt.

### När du INTE ska använda GSD

🚫 **Arkitekturbeslut** — agenten optimerar lokalt, du optimerar globalt. Fundamentala arkitekturval (monolith vs microservices, databasval, API-design) kräver mänskligt omdöme.

🚫 **Security-kritisk kod** — alltid manuell review oavsett. Auth, kryptering, betalningshantering — lita inte blint på genererad kod.

🚫 **Teamets lärande** — om syftet är att lära, inte leverera. Att delegera till AI när du borde förstå koden motverkar långsiktig kompetensuppbyggnad.

🚫 **Regelverk & compliance** — agenten förstår inte juridiskt ansvar. GDPR, PCI-DSS, branschspecifika krav kräver mänsklig expertis.

🚫 **Det du inte kan reviewera** — delegera inte det du inte kan bedöma. Om du inte kan avgöra om koden är korrekt bör du inte använda AI för att skriva den.

> GSD gör dig effektivare — men det är fortfarande du som är ansvarig.

### Gradvis adoption

Du behöver inte gå all-in dag ett. Börja smått och bygg tillit:

| Tid | Utmaning | Kommando |
|-----|----------|----------|
| 5 min | Fixa en riktig typo i din kodbas | `/gsd-fast` |
| 30 min | Lägg till en liten feature | `/gsd-quick` |
| 2 timmar | Starta ett nytt sidoprojekt | `/gsd-new-project` |

Vecka 1: använd bara `/gsd-fast` för triviala fixar. Lär dig hur commits ser ut, hur STATE.md uppdateras, hur det känns.

Vecka 2: prova `/gsd-quick` för en riktig feature. Se hur planning fungerar, granska planen innan execution.

Vecka 3+: kör ett riktigt projekt med `/gsd-new-project`. Nu har du tillräckligt med erfarenhet för att utvärdera resultaten och justera workflow:en.

### Cross-AI review — `/gsd-review`

Du har låtit Copilot bygga en auth-modul genom GSD. Koden fungerar, verification passerar — men du vill ha en second opinion. Kanske en annan AI ser mönster eller problem som Copilot missade.

```bash
$ /gsd-review
Reviewing Phase 2: Auth System
Reviewer 1 (Claude): 3 concerns, 2 suggestions
Reviewer 2 (GPT-4): 1 concern, 4 suggestions
✅ Consensus: 2 shared concerns identified
```

`/gsd-review` använder en annan AI-modell för att granska arbetet som den primära agenten utfört — som en code review fast med olika AI-perspektiv. Flera reviewers ger oberoende feedback som syntetiseras till konsensus.

Olika AI-modeller har olika styrkor och blinda fläckar. Cross-review fångar problem som en enda modell kan missa — precis som mänsklig code review fungerar bättre med flera ögon.

**När du ska använda det:**
- Kritisk kod — auth, betalningar, datahantering
- Du vill validera arkitekturbeslut från en annan vinkel
- Du har tid för en extra kvalitetskontroll och vill maximera confidence

## 7. Referens

### Kommandoöversikt

De viktigaste GSD-kommandona — från enklaste till mest avancerade.

| Kommando | Beskrivning | När? |
|----------|-------------|------|
| `/gsd-fast` | Snabbfix utan planning — atomic commit | Triviala ändringar (≤3 filer) |
| `/gsd-quick` | Task med planner + executor, composable flags | Ny feature, liten refaktor |
| `/gsd-do` | Smart routing — väljer rätt kommando åt dig | Du vet inte vilket kommando du behöver |
| `/gsd-new-project` | Nytt projekt med full workflow | Greenfield — helt nytt projekt |
| `/gsd-plan-phase` | Planerar en phase med tasks och waves | Nästa phase i roadmap ska planeras |
| `/gsd-execute-phase` | Exekverar en planerad phase | Phase är planerad, redo att bygga |
| `/gsd-verify-work` | Goal-backward verification av phase | Phase exekverad, mål ska verifieras |
| `/gsd-resume-work` | Återuppta arbete efter paus | Du kommer tillbaka till ett projekt |
| `/gsd-progress` | Visa projektets status | Snabb koll — var står vi? |
| `/gsd-map-codebase` | Kartlägger befintlig kodbas | Brownfield — innan du börjar ändra |
| `/gsd-debug` | Systematisk buggutredning | Komplext problem som kräver analys |
| `/gsd-insert-phase` | Lägg till en phase mitt i roadmap | Saknat steg upptäckt under arbete |
| `/gsd-review` | Cross-AI review av utfört arbete | Kritisk kod — vill ha second opinion |
| `/gsd-autonomous` | Kör hela pipeline:n utan stopp | Erfaren användare, tydligt scope |

Alla kommandon körs i Copilot Chat. Composable flags (`--discuss`, `--research`, `--full`) fungerar med `/gsd-quick`.

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
        ├── 01-CONTEXT.md       # Beslut från /gsd-discuss-phase
        ├── 01-RESEARCH.md      # Domänresearch från /gsd-research-phase
        ├── 01-PLAN.md          # Executionsplan med tasks
        ├── 01-SUMMARY.md       # Resultat efter execution
        └── 01-VERIFICATION.md  # Goal-backward verification
```

Varje phase producerar sin egen uppsättning artifacts. Inget försvinner — du kan alltid gå tillbaka och se vad som bestämdes och varför. Det här är det som skiljer GSD från en vanlig AI-chat: persistent memory som överlever sessioner, dagar och veckor.

### Länkar och resurser

- **Installera GSD:** `npx get-shit-done-cc@latest`
- **GitHub Copilot:** VS Code med GitHub Copilot-extension
- **Terminologi:** Se `TERMINOLOGY.md` i projektets rot för svensk/engelsk termreferens

## Appendix

### GSD vs BMAD — kortjämförelse

GSD och BMAD är båda AI agent frameworks — men de löser olika problem med olika filosofier.

| Dimension | GSD | BMAD |
|-----------|-----|------|
| **Filosofi** | Workflow-centric — strukturerad execution pipeline | Persona-based — specialiserade roller (PM, Architect, Dev) |
| **Agents** | Researcher, Planner, Executor, Verifier — funktionsroller | PM, Architect, Developer, QA — yrkesroller |
| **Styrka** | Execution + verification — bygger och kontrollerar | Strategi + dokumentation — planerar och dokumenterar |
| **Workflow** | Linjär pipeline: discuss → plan → execute → verify | Rollbaserade handoffs: varje persona bidrar med sin expertis |
| **Bäst för** | Projekt där execution och kvalitetskontroll är kritiskt | Projekt där strategisk planering och dokumentation är viktigast |

Det här är inte en tävling. GSD och BMAD löser olika problem — som en skruvmejsel och en hammare. GSD utmärker sig när du behöver strukturerad execution med inbyggda kvalitetsgrindar: bygga kod, verifiera att den fungerar, hantera avvikelser automatiskt.

BMAD utmärker sig när du behöver strategisk planering och grundlig dokumentation: definiera arkitektur, kartlägga stakeholders, skapa omfattande design-docs innan en rad kod skrivs.

Vi valde GSD — execution med kvalitetskontroll. Det passade vårt behov: utvecklare som vill bygga saker effektivt, med förtroende för att resultatet faktiskt fungerar. Men om ditt projekt kräver djup strategisk planering och dokumentation först, kan BMAD vara ett bättre val.
