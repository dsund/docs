# Domain Pitfalls

**Domain:** Developer education presentations about AI agent frameworks (GSD)
**Audience:** Mixed developer team — AI skeptics through early adopters
**Format:** 45-minute presentation by Tech Lead to own team
**Researched:** 2025-07-11

---

## Critical Pitfalls

Mistakes that undermine the entire presentation's goals — causing rejection, distrust, or misaligned expectations.

---

### Pitfall 1: The "Magic Show" Effect

**What goes wrong:** The presenter shows only impressive, cherry-picked workflows where the AI produces perfect code on the first try. The audience leaves thinking it either (a) always works this well (disappointment follows) or (b) it's staged/unrealistic (credibility destroyed).

**Why it happens:** Presenters naturally want to showcase the best case. Training material and demos tend to use ideal scenarios. The temptation is to show a "wow" moment — a full feature built in 2 minutes — because it's dramatic.

**Consequences:**
- Enthusiasts try it, hit first friction, and conclude "it doesn't work like in the demo"
- Skeptics smell the cherry-picking and dismiss the entire tool
- Trust in the presenter (Tech Lead) is damaged — "you sold us something"

**Warning signs:**
- Every example in the slides produces perfect output
- No mention of iteration, correction, or failed attempts
- The word "just" appears frequently ("you just run this command")

**Prevention:**
- Show the **realistic flow**: prompt → output → review → adjust → better output
- Include at least one "here's what it got wrong and how you course-correct" example
- Frame it as collaboration, not magic: "you're directing an agent, not pressing a button"
- Use language like "typically" and "in my experience" rather than absolutes

**Relevant section:** GSD deep-dive, scenarion, best practices

---

### Pitfall 2: Ignoring the "Am I Being Replaced?" Elephant

**What goes wrong:** The presentation enthusiastically shows how AI can write code, generate architecture, and handle entire workflows — without ever addressing the unspoken fear that this technology threatens developers' livelihoods and professional identity.

**Why it happens:** The presenter (as Tech Lead and early adopter) has already resolved this tension internally. They genuinely see AI as augmentation. They forget that others haven't gone through that mental journey yet.

**Consequences:**
- Skeptics become actively hostile — arms-crossed resistance
- Even enthusiasts may feel uneasy but won't voice it publicly
- The team may adopt the tool superficially but resist integrating it into real workflow
- Presentationen upplevs som "management pushing AI on us"

**Warning signs:**
- No section addressing developer role evolution
- AI is positioned as doing the developer's job rather than amplifying it
- Phrases like "the AI builds this for you" instead of "you direct the AI to build this"
- No acknowledgment that this changes how work feels

**Prevention:**
- Address it head-on in the first 5 minutes: "Let's talk about what this means for us as developers"
- Position explicitly: AI handles the tedious parts (boilerplate, repetition, research) so you focus on the hard parts (design decisions, trade-offs, domain logic)
- Show that the developer is always the decision-maker — the AI proposes, the developer disposes
- Use the word "du" frequently in examples — "du bestämmer", "du reviewar", "du kör"
- Emphasize that understanding code is MORE important with AI, not less — you need to evaluate what it produces

**Relevant section:** Introduktion (varför AI agent frameworks), best practices

---

### Pitfall 3: Skipping the On-Ramp — Going Full Workflow First

**What goes wrong:** The presentation leads with the complete GSD lifecycle (new-project → plan → execute) — a complex, multi-step process with phases, roadmaps, milestones, and agents. The audience, especially those who've never used AI coding tools, feels overwhelmed and concludes "this is too complicated for me."

**Why it happens:** The full workflow is the most impressive and differentiated feature. It's what makes GSD interesting compared to basic Copilot autocomplete. The presenter wants to show the full power.

**Consequences:**
- 70% of the audience mentally checks out before seeing the easy entry points
- Developers don't try it after the presentation because the perceived effort is too high
- The "start small" commands (`/gsd-quick`, `/gsd-fast`, `/gsd-do`) feel like afterthoughts
- You lose the most important group: the curious-but-cautious middle

**Warning signs:**
- Full workflow appears in the first half of the presentation
- Light commands are mentioned late or briefly ("oh, and you can also do...")
- Slides show complex phase diagrams before showing a simple one-shot command
- No "try this tomorrow morning" moment in the first 15 minutes

**Prevention:**
- Structure as a **spectrum**: start with the simplest possible interaction, then layer up
- Recommended flow: `/gsd-do` (one-shot) → `/gsd-quick` / `/gsd-fast` (structured but light) → full project workflow
- Give the audience a "you can try THIS right now" within the first 10 minutes
- Position the full workflow as "when you're ready" — an evolution, not a prerequisite
- The key insight: most daily usage is quick commands, not full project orchestration

**Relevant section:** On-ramp (denna sektion ska komma FÖRE full workflow i presentationen)

---

### Pitfall 4: The Enthusiast's Bias — Preaching to Non-Converts

**What goes wrong:** The presentation's tone, examples, and framing assume the audience already believes AI coding tools are valuable. It optimizes for the 20% enthusiasts while alienating the 60% curious-middle and 20% skeptics.

**Why it happens:** The presenter is a convinced user. They spend time in communities where AI-assisted development is the norm. Their mental model of "normal" is already shifted.

**Consequences:**
- Skeptics feel unheard and dig in harder
- The curious middle doesn't get their "why should I care?" answered
- The presentation feels like evangelism rather than education
- Team adoption is low because only the already-convinced adopt

**Warning signs:**
- No acknowledgment that skepticism is rational and healthy
- Examples don't address common objections ("but what about code quality?", "what about security?", "what about understanding my codebase?")
- Enthusiastic language throughout ("amazing", "incredible", "game-changer")
- No section that honestly discusses limitations

**Prevention:**
- Open by validating skepticism: "If you're skeptical, good. You should be. Let me show you what's actually useful and where the limits are."
- Address the top 3 skeptic concerns explicitly: quality, understanding, trust
- Use measured, technical language — not marketing language
- Include a "limitations and when NOT to use this" section
- Show the tool earning trust through results, not through claims
- Let the audience draw their own conclusions from what you show

**Relevant section:** Introduktion, best practices, entire presentation tone

---

### Pitfall 5: The "It Just Works" Omission — Hiding Failure Modes

**What goes wrong:** The presentation never shows what happens when the AI produces bad output, misunderstands the task, or goes off in the wrong direction. Developers who then encounter these inevitable situations feel betrayed or conclude the tool is broken.

**Why it happens:** Showing failure feels counterproductive — "why show it failing?" But hiding failure is far more damaging than showing it and demonstrating recovery.

**Consequences:**
- Developers abandon the tool at first failure ("it doesn't work")
- No mental model for how to debug or redirect the AI
- Unrealistic expectations → frustration → rejection
- Lost opportunity to teach the most valuable skill: guiding AI when it's wrong

**Warning signs:**
- Every example flows linearly from prompt to perfect result
- No mention of reviewing output critically
- No guidance on what to do when output is wrong
- No mention of common failure patterns (hallucinated APIs, wrong assumptions, over-engineering)

**Prevention:**
- Dedicate a "when things go wrong" section — normalize it
- Show the correction loop: "The AI generated X. That's not what I wanted because Y. Here's how I adjust..."
- Teach the audience to expect ~80% right, 20% needs adjustment (realistic framing)
- Explain WHY it fails (context window limits, ambiguous instructions, missing context) so developers understand the mechanism
- Frame debugging AI output as a skill to develop, not a defect of the tool

**Relevant section:** Best practices, scenarion

---

## Moderate Pitfalls

Mistakes that reduce presentation effectiveness but don't cause outright rejection.

---

### Pitfall 6: The Framework Comparison Trap

**What goes wrong:** The presentation spends too long comparing GSD vs BMAD vs other frameworks, turning an educational session into a confusing landscape survey. The audience leaves knowing about five frameworks but feeling confident in none.

**Why it happens:** The presenter wants to show they've done their homework and that GSD was chosen deliberately. Comparison feels fair and balanced. But for an audience that hasn't used ANY framework, comparing three unfamiliar things is cognitive overload.

**Prevention:**
- Limit comparison to 2-3 slides maximum, early in the presentation
- Frame it as "why we chose GSD" not "here are all your options"
- Use a simple table: framework → approach → our choice (GSD) because [one-liner]
- If someone asks about alternatives, answer it — but don't front-load the comparison
- The audience needs to learn ONE tool well, not know about five tools vaguely

**Warning signs:**
- More than 5 minutes on framework comparison
- Audience asks "so which one should we use?" after the comparison section
- Multiple complex comparison matrices

**Relevant section:** Kort jämförelse (keep it kort)

---

### Pitfall 7: Theory-Heavy, Practice-Light Imbalance

**What goes wrong:** The presentation spends most of its time on architecture diagrams, agent roles, phase definitions, and conceptual models — but very little on "here's what you type and here's what happens."

**Why it happens:** Architecture is interesting to explain. It feels like deeper content. And the presenter genuinely understands the system better at the architecture level. But the audience needs "what do I do Monday morning?" more than "how does the agent orchestration work internally?"

**Prevention:**
- Apply the 30/70 rule: 30% conceptual framework, 70% practical usage
- Every concept slide should be followed by a "what this looks like in practice" slide
- Use real terminal output / command examples as primary content
- Architecture is "nice to know" — practical usage is "need to know"
- Ask yourself for each slide: "Does this help someone USE the tool tomorrow?"

**Warning signs:**
- Multiple slides of system diagrams without corresponding usage examples
- The word "architecture" appears more than 3 times in slides
- No concrete command + output examples in the first 15 minutes

**Relevant section:** GSD deep-dive (balance architecture with practical examples)

---

### Pitfall 8: Not Showing the Spectrum of Use Cases

**What goes wrong:** The presentation focuses on one type of usage — typically either "quick fixes" OR "full project workflows" — missing the spectrum of how developers actually integrate AI tools into daily work.

**Why it happens:** It's easier to tell one coherent story than to show a spectrum. And the presenter tends to favor the mode they personally use most.

**Consequences:**
- Developers who do mostly maintenance/debugging don't see how the tool fits their work
- Developers on greenfield projects don't realize the tool scales up to full orchestration
- The tool is adopted for only one use case when it could serve many

**Prevention:**
- Explicitly map the spectrum with concrete examples:
  - **Quick fix**: "Fixa den här TypeScript-errorn" → `/gsd-do`
  - **Small task**: "Lägg till input validation på det här formuläret" → `/gsd-quick`
  - **Feature**: "Bygg en ny API endpoint med tester" → `/gsd-fast`
  - **Full project**: "Nytt microservice-projekt från scratch" → `/gsd-new-project`
- Map each scenario to a developer persona the audience recognizes
- Show that most daily usage is on the lighter end of the spectrum

**Warning signs:**
- Only one type of scenario is shown
- No mapping between task size and appropriate tool/command

**Relevant section:** Scenarion, On-ramp

---

### Pitfall 9: Prompt Crafting as Afterthought

**What goes wrong:** The presentation shows what commands to run but barely discusses HOW to write good prompts/instructions to get quality results. Developers then write vague prompts, get poor output, and blame the tool.

**Why it happens:** Prompt crafting feels like a "soft skill" — less tangible than showing commands and workflows. It's also harder to teach in slides because it requires nuance and examples.

**Consequences:**
- Developers write prompts like "fix the bug" instead of "the login form submits but the password validation in AuthService.validateCredentials() isn't checking minimum length — add the check and update the unit test"
- Poor prompts → poor output → "this tool is useless"
- The single biggest determinant of tool effectiveness is undertaught

**Prevention:**
- Dedicate a full section to "hur man promptar för bäst resultat"
- Show side-by-side: vague prompt → poor result vs. specific prompt → good result
- Teach the key principles: be specific, provide context, state constraints, describe expected output
- Give a "prompt template" they can reuse: [What] + [Where] + [Constraints] + [Expected behavior]
- Emphasize: "The quality of what you get out is directly proportional to the quality of what you put in"

**Warning signs:**
- Example prompts are suspiciously well-crafted without explaining why
- No "bad prompt vs good prompt" comparison
- Prompt crafting covered in one slide or less

**Relevant section:** Best practices (ska vara ett av de tyngsta avsnitten)

---

### Pitfall 10: The "Trust Me" Problem — No Verification Pattern

**What goes wrong:** The presentation shows developers using AI output without discussing HOW to verify it. This either creates blind-trust adopters (dangerous) or reinforces skeptics' fears ("see, no one reviews AI code").

**Why it happens:** Showing verification slows down the demo and makes it less impressive. It's also implicit for the experienced presenter — they always review output — but they forget to make it explicit.

**Prevention:**
- Make review a VISIBLE part of every workflow shown
- Show the verification pattern: generate → read → understand → test → integrate
- Emphasize: "You are the reviewer. AI is the author. You own the merge."
- Address code quality explicitly: "AI-generated code should meet the same review standards as human code"
- Mention specific things to check: edge cases, error handling, security patterns, naming conventions

**Warning signs:**
- Examples go directly from AI output to "done!"
- No mention of code review, testing, or verification
- No discussion of who is responsible for AI-generated code

**Relevant section:** Best practices, full workflow

---

## Minor Pitfalls

Mistakes that cause friction or missed opportunities but are recoverable.

---

### Pitfall 11: Language Inconsistency Creating Cognitive Friction

**What goes wrong:** The presentation inconsistently mixes Swedish and English — sometimes translating terms, sometimes not — creating confusion about terminology. One slide says "fas" and the next says "phase."

**Why it happens:** The language policy (Swedish with English terms) requires deliberate attention. In natural speech and writing, it's easy to slip between conventions.

**Prevention:**
- Create a terminology reference BEFORE building slides
- Rule: if it's a GSD/technical concept, use English (phase, roadmap, milestone, agent, workflow, prompt)
- Rule: if it's a natural language sentence, use Swedish ("I den här phasen gör vi...")
- Review all slides specifically for terminology consistency
- When introducing an English term for the first time, briefly clarify: "en milestone — alltså en leverabel delmål"

**Relevant section:** Entire presentation, especially GSD deep-dive

---

### Pitfall 12: No "What to Do Monday Morning" Close

**What goes wrong:** The presentation ends with a summary or Q&A but doesn't give the audience a concrete, low-friction next step they can take immediately.

**Why it happens:** Standard presentation structure ends with summary + questions. But developer education presentations need an ACTION close, not a SUMMARY close.

**Prevention:**
- End with "Tre saker du kan göra imorgon":
  1. A zero-setup first try (e.g., "Öppna terminalen och kör `/gsd-do 'förklara vad den här funktionen gör' i ett projekt du jobbar i`")
  2. A resource to bookmark (wiki doc, cheat sheet)
  3. Who to ask for help (the presenter / a channel)
- Make the first step so small it feels absurd NOT to try it
- Consider a one-page "cheat sheet" handout with commands and examples

**Warning signs:**
- Last slide is "Questions?" with no preceding action slide
- No mention of next steps or where to go from here
- No resources shared

**Relevant section:** Presentation close (should be designed explicitly as an action trigger)

---

### Pitfall 13: Ignoring the Brownfield Reality

**What goes wrong:** All examples show greenfield scenarios — new projects, new features, clean codebases. But most developers spend most of their time in existing, messy codebases. They leave thinking "cool, but my codebase is a mess, so this won't work."

**Why it happens:** Greenfield examples are cleaner and produce more impressive results. It's genuinely harder to demo AI tools on complex existing codebases.

**Prevention:**
- Include at least 2 scenarios in existing/messy codebases: debugging, refactoring, adding features to legacy code
- Show how GSD handles context — it reads your existing code, understands patterns, works within constraints
- Frame brownfield as the PRIMARY use case: "Det här är vad du mest troligt kommer använda det till"
- Address common brownfield concerns: "Can it understand our codebase?" → show how context works

**Warning signs:**
- All code examples start from scratch
- No mention of existing projects, legacy code, or adding to existing features
- No debugging or refactoring scenarios

**Relevant section:** Scenarion (brownfield should come before greenfield in presentation order)

---

### Pitfall 14: Presenting at One Technical Level

**What goes wrong:** The presentation assumes one level of AI tool experience — typically either too basic (boring the enthusiasts) or too advanced (losing the newcomers).

**Why it happens:** With a 45-minute time constraint, it's hard to serve multiple levels. The presenter naturally gravitates toward their own level.

**Prevention:**
- Use a **layered approach**: each topic starts with the essential (everyone needs this), then goes deeper (for the curious)
- Signal transitions: "Det här var grunderna — nu ska vi titta lite djupare för er som vill förstå mer"
- Make sure enthusiasts learn at least 2-3 things they didn't know (advanced tips, edge cases, power-user patterns)
- Make sure newcomers never feel lost for more than 30 seconds — anchor frequently to practical examples

**Warning signs:**
- A third of the audience looks bored while another third looks confused
- No differentiation between "need to know" and "nice to know" content

**Relevant section:** Entire presentation structure

---

### Pitfall 15: Not Acknowledging What the AI Can't See

**What goes wrong:** The presentation doesn't address the boundaries of AI context — what the tool can and cannot access, understand, or know about. Developers then expect the AI to know about their deployment pipeline, production data, internal APIs, or business domain without being told.

**Why it happens:** Context limitations are a "downer" topic. The presenter wants to focus on capabilities.

**Prevention:**
- Have a brief "what the AI knows and doesn't know" section
- Explain context boundaries: it sees your code, your project structure, your prompt — not your production environment, not your team's unwritten conventions, not your business domain (unless you tell it)
- Frame this as empowering, not limiting: "Du styr vad AI:n vet — ju mer context du ger, desto bättre resultat"
- Connect this back to prompt crafting: "This is why good prompts include context"

**Warning signs:**
- No mention of context windows, context limitations, or what the AI can access
- Developers asking "can it see our database?" type questions with surprise at the answer

**Relevant section:** GSD deep-dive, best practices

---

## Phase-Specific Warnings

Mapped to the project's required sections from PROJECT.md.

| Presentation Section | Likely Pitfall | Severity | Mitigation |
|---|---|---|---|
| **Introduktion** (varför AI agent frameworks) | Pitfall 2: Ignoring "Am I being replaced?" | Critical | Address head-on in first 5 minutes. Validate concerns. Position as augmentation. |
| **Introduktion** | Pitfall 4: Enthusiast bias in framing | Critical | Open by validating skepticism. Use measured language. |
| **Kort jämförelse** (GSD vs others) | Pitfall 6: Framework comparison trap | Moderate | Max 2-3 slides. "Why we chose GSD" framing, not landscape survey. |
| **GSD deep-dive** (arkitektur, workflow) | Pitfall 7: Theory-heavy, practice-light | Moderate | 30/70 rule. Every concept → practical example. |
| **GSD deep-dive** | Pitfall 1: Magic show effect | Critical | Show realistic flow including iteration and correction. |
| **On-ramp** (quick/fast/do) | Pitfall 3: Skipping the on-ramp | Critical | This section MUST come before full workflow. Start with `/gsd-do`. |
| **Full workflow** (project lifecycle) | Pitfall 8: Not showing the spectrum | Moderate | Frame as the "top end" of a spectrum already introduced. |
| **Scenarion** (greenfield, brownfield, debugging) | Pitfall 13: Ignoring brownfield | Minor | Lead with brownfield/debugging. Greenfield last. |
| **Scenarion** | Pitfall 5: Hiding failure modes | Critical | Include a scenario where AI gets it wrong + correction. |
| **Best practices** (prompting, tänkande) | Pitfall 9: Prompt crafting as afterthought | Moderate | Make this a major section. Show bad vs good prompts. |
| **Best practices** | Pitfall 10: No verification pattern | Moderate | Make review explicit in every workflow. |
| **Best practices** | Pitfall 15: Not acknowledging context limits | Minor | Include "what the AI knows/doesn't know" subsection. |
| **Closing** | Pitfall 12: No action close | Minor | End with "3 things to do tomorrow" not just "Questions?" |
| **Throughout** | Pitfall 11: Language inconsistency | Minor | Create terminology reference before building slides. |
| **Throughout** | Pitfall 14: Presenting at one level | Minor | Layered approach: essentials → deeper. Signal transitions. |

---

## Meta-Pitfall: The Presenter's Own Journey as Blind Spot

One overarching risk deserves special attention: **the presenter has already completed their own adoption journey**. They've moved from curiosity → experimentation → competence → advocacy. Every pitfall above stems partly from this: the presenter unconsciously skips the stages they've already passed through.

**Prevention:** Before finalizing the presentation, have someone who HASN'T used GSD review the slides and flag every point where they'd think "wait, what?" or "why should I care?" or "that seems too good to be true." The presentation should take the audience on the same journey the presenter already completed — not start where the presenter currently is.

---

## Pitfall Severity Summary

| Severity | Count | Key Theme |
|---|---|---|
| **Critical** | 5 | Credibility, trust, and adoption barriers |
| **Moderate** | 5 | Effectiveness and learning outcomes |
| **Minor** | 5 | Polish, completeness, and missed opportunities |

## Sources

- Developer advocacy and education patterns (HIGH confidence — well-established domain)
- AI tool adoption research and community patterns 2024-2025 (MEDIUM confidence — based on training data, rapidly evolving field)
- Presentation design for mixed technical audiences (HIGH confidence — established pedagogy)
- Change management patterns in engineering teams (HIGH confidence — established domain)

**Confidence note:** These pitfalls are synthesized from extensive patterns in developer advocacy, technical education, and AI tool adoption. The specific manifestations for AI agent frameworks like GSD are informed by general AI tool adoption patterns rather than GSD-specific case studies (which don't exist at scale yet). Confidence is HIGH for the patterns, MEDIUM for their specific expression in the GSD context.
