# Technology Stack

**Project:** GSD-presentation (AI Agent Framework Education)
**Researched:** 2026-04-15
**Primary source confidence:** MEDIUM (npm registry verified versions + training data; no external search APIs available)

---

## Recommended Stack

### Presentation Engine

| Technology | Version | Purpose | Why | Confidence |
|------------|---------|---------|-----|------------|
| **Marp CLI** | 4.3.1 | Slide generation (HTML, PDF, PPTX) | Markdown-native, Git-friendly, zero build pipeline. PROJECT.md mandates Marp — and it's the right call. | HIGH |
| **Marp Core** | 4.3.0 | Rendering engine (used by CLI) | Comes with CLI, provides themes + syntax extensions | HIGH |
| **Marp for VS Code** | latest | Live preview while authoring | Instant feedback loop, same tool the presenters already use | HIGH |

**Rationale:** Marp is the right tool because this project values *content over tooling*. The slides are a communication vehicle, not a product. Marp lets you write markdown and get professional slides. No React, no Vue, no build step. `marp slides.md --pdf` and you're done.

### Authoring & Tooling

| Technology | Version | Purpose | Why | Confidence |
|------------|---------|---------|-----|------------|
| **VS Code** | current | Authoring environment | Team already uses it; Marp extension provides live preview | HIGH |
| **Git** | current | Version control for all content | Markdown diffs are readable; enables collaboration on content | HIGH |
| **Node.js** | ≥18 LTS | Runtime for Marp CLI | Required by marp-cli; team already has it | HIGH |

### Theme & Styling

| Technology | Purpose | Why | Confidence |
|------------|---------|-----|------------|
| **Marp built-in `default` theme** | Base styling | Clean, readable, works well for technical content. Start here. | HIGH |
| **Custom CSS overrides** | Brand colors, font sizing, code block styling | Marp supports `<!-- theme: custom -->` with CSS files. Keep minimal. | HIGH |
| **highlight.js** (bundled in Marp Core) | Code syntax highlighting | Already included — no extra setup. Supports all relevant languages. | HIGH |

### Content Format

| Format | Purpose | Why | Confidence |
|--------|---------|-----|------------|
| **Marp Markdown (.md)** | Slide deck (~45 min) | `---` separators, directives, image sizing. One file = one deck. | HIGH |
| **Standard Markdown (.md)** | Long-form reference document | Wiki/repo-friendly. No special tooling needed to read. | HIGH |

---

## Alternatives Considered

| Category | Recommended | Alternative | Why Not Alternative |
|----------|-------------|-------------|---------------------|
| **Slide engine** | **Marp** | **reveal.js** (v6.0.1, updated 2026-04-11) | reveal.js is HTML-first with markdown plugin. More powerful (fragments, transitions, plugins) but heavier. Requires HTML boilerplate, JS config, local server. Overkill for a content-focused 45-min talk. |
| **Slide engine** | **Marp** | **Slidev** (v52.14.2, updated 2026-04-05) | Slidev is Vue-powered with many features (Monaco editor, animations, recording). Developer-friendly but opinionated runtime. Requires `npm run dev` workflow, has its own component ecosystem. Too much tooling complexity for a presentation that needs to be *written and maintained*, not *developed*. |
| **Slide engine** | **Marp** | **Google Slides / PowerPoint** | Not version-controllable. Binary format = no diffs. Can't be authored alongside code in VS Code. Violates project constraints. |
| **Styling** | **CSS overrides** | **Full custom Marp theme** | A full theme (`@theme` directive with separate CSS file) is warranted only if you're creating multiple decks with shared branding. For one presentation, inline overrides in a `<style>` block within the markdown are sufficient and simpler. |
| **Diagrams** | **Text/ASCII + Marp images** | **Mermaid integration** | Marp doesn't natively render Mermaid in slides. You'd need to pre-render diagrams to images. For this presentation's architecture diagrams, static images or well-formatted text blocks are simpler and more reliable. |

---

## AI Agent Frameworks to Cover in Presentation

This is the *content domain*, not the *tooling stack*. These are the frameworks and tools the presentation will teach about.

### Primary Focus: GSD (Get Shit Done)

| Aspect | Details | Confidence |
|--------|---------|------------|
| **What** | Structured AI agent framework for Copilot CLI | HIGH |
| **Architecture** | Orchestrator → specialized agents (researcher, planner, executor, verifier) | HIGH |
| **Entry points** | `/gsd-quick` (one-off), `/gsd-fast` (skip planning), `/gsd-do` (direct), full workflow (`/gsd-new-project`) | HIGH |
| **Key concepts** | Phases, milestones, roadmaps, skills, agent orchestration, research-before-build | HIGH |
| **Lifecycle** | Research → Plan → Execute → Verify (per phase) | HIGH |
| **Differentiator** | Structured methodology, not just "ask AI to code" — project management built in | HIGH |

### Framework Comparison Candidates

The presentation needs a **brief** comparison (PROJECT.md: "kort jämförelse"). Cover enough to give context, not enough to confuse.

| Framework | Category | What to say | Depth | Confidence |
|-----------|----------|-------------|-------|------------|
| **BMAD** | Structured methodology | Persona-driven (architect, developer, PM personas). More documentation-heavy than GSD. Similar philosophy of "structure before code" but different execution model. | 2-3 slides | MEDIUM |
| **Aider** | CLI coding assistant | Pair-programming model. Git-aware with auto-commits. Works with multiple LLMs. No project lifecycle — it's a coding partner, not a methodology. Good for comparison: "tool vs framework" distinction. | 1-2 slides | HIGH |
| **Claude Code** | Terminal-based AI agent | Anthropic's coding agent. Deep codebase understanding. Can plan + execute multi-step tasks autonomously. Growing rapidly in 2025-2026. Represents the "raw agent" approach without imposed structure. | 1-2 slides | HIGH |
| **Cursor Agent** | IDE-integrated agent | Agent mode inside Cursor IDE. Composer for multi-file changes. Tight IDE integration is its strength. Represents the "IDE-native" approach. | 1 slide | HIGH |
| **GitHub Copilot (Agent Mode)** | IDE-integrated agent | VS Code integrated. MCP support. Extensible via skills — GSD runs ON TOP of Copilot. Important to show the relationship: Copilot is the platform, GSD is the methodology layer. | 1-2 slides | HIGH |
| **Windsurf (Codeium)** | IDE-integrated agent | Cascade for multi-step flows. | ½ slide (mention only) | MEDIUM |

### Conceptual Framework for the Comparison

The presentation should organize comparisons along these axes:

1. **Tool vs Framework vs Methodology**
   - *Tool:* Aider, Claude Code — write code when asked
   - *IDE Agent:* Cursor, Copilot Agent — integrated into editor workflow
   - *Methodology/Framework:* GSD, BMAD — structured approach to using AI agents

2. **Autonomy Spectrum**
   - *Pair programming:* Aider (human drives, AI assists)
   - *Agent mode:* Claude Code, Cursor (AI plans and executes, human reviews)
   - *Orchestrated:* GSD (structured lifecycle with multiple specialized agents)

3. **When to use what**
   - Quick fix → raw agent (Claude Code, Copilot)
   - Feature work → GSD light (`/gsd-quick`, `/gsd-fast`)
   - Greenfield project → GSD full workflow
   - Exploration/debugging → Aider or Claude Code

---

## Marp Configuration Guide

### Minimal Slide Deck Structure

```markdown
---
marp: true
theme: default
paginate: true
header: 'AI Agent Frameworks — GSD'
footer: '[Team Name] 2026'
---

# Slide Title

Content here

---

# Next Slide

More content
```

### Key Marp Directives

| Directive | Scope | Purpose | Example |
|-----------|-------|---------|---------|
| `marp: true` | Global | Enable Marp rendering | Front matter |
| `theme:` | Global | Set theme (default, gaia, uncover) | `theme: default` |
| `paginate:` | Global/Local | Show slide numbers | `paginate: true` |
| `header:` / `footer:` | Global/Local | Persistent header/footer text | `header: 'Title'` |
| `class:` | Local | Apply CSS class to specific slide | `<!-- _class: lead -->` |
| `backgroundColor:` | Local | Slide background color | `<!-- _backgroundColor: #1a1a2e -->` |
| `backgroundImage:` | Local | Slide background image | `<!-- _backgroundImage: url(bg.png) -->` |
| `color:` | Local | Text color override | `<!-- _color: white -->` |

**Note:** Underscore prefix (`_`) makes directive local to current slide only. Without underscore, it applies to current and all subsequent slides.

### Custom Styling (Inline)

```markdown
---
marp: true
theme: default
style: |
  section {
    font-family: 'Segoe UI', sans-serif;
  }
  h1 {
    color: #2d3748;
  }
  code {
    background-color: #f7fafc;
    padding: 2px 6px;
    border-radius: 4px;
  }
  section.lead h1 {
    font-size: 2.5em;
    text-align: center;
  }
---
```

### Output Commands

```bash
# Install Marp CLI
npm install -g @marp-team/marp-cli

# Generate PDF
marp slides.md --pdf

# Generate HTML (self-contained, shareable)
marp slides.md --html

# Generate PPTX (for those who insist)
marp slides.md --pptx

# Live preview server (for authoring)
marp slides.md --preview

# Watch mode (auto-regenerate on save)
marp slides.md --pdf --watch
```

---

## Installation

```bash
# Presentation tooling (global install for convenience)
npm install -g @marp-team/marp-cli@4.3.1

# VS Code extension (install from marketplace)
# Extension ID: marp-team.marp-vscode
```

No other packages needed. This is a markdown project, not a software project.

---

## What NOT to Include

| Excluded Tool/Approach | Why |
|------------------------|-----|
| **Slidev** | Adds Vue.js runtime dependency, requires `npm run dev` workflow, overkill for content delivery |
| **reveal.js** | HTML-first approach fights the "markdown-native" requirement; adds server dependency for presenting |
| **Mermaid.js** | No native Marp support; pre-rendering adds build complexity for minimal diagram needs |
| **Custom Marp theme package** | One presentation doesn't justify a reusable theme package; inline `style` block is sufficient |
| **PDF-from-browser** | Marp CLI handles PDF generation natively; no need for Puppeteer/Chrome workarounds |
| **AI-generated slides** | Content must be curated by the Tech Lead; AI can assist drafting but the structure/narrative needs human editorial control |

---

## Sources

| Source | Type | What it confirmed |
|--------|------|-------------------|
| npm registry (`npm view @marp-team/marp-cli`) | Package metadata | Version 4.3.1, last updated 2026-03-16, MIT license |
| npm registry (`npm view @marp-team/marp-core`) | Package metadata | Version 4.3.0, dependencies (highlight.js, KaTeX, etc.) |
| npm registry (`npm view reveal.js`) | Package metadata | Version 6.0.1, last updated 2026-04-11 |
| npm registry (`npm view @slidev/cli`) | Package metadata | Version 52.14.2, last updated 2026-04-05 |
| Training data (2024-2025) | Framework knowledge | AI agent framework landscape, GSD architecture, tool comparisons |

**Confidence note:** Marp versions and activity are HIGH confidence (verified via npm). AI agent framework details are MEDIUM confidence (training data, not independently verified against current state). The landscape is fast-moving; specific features of Claude Code, Cursor, etc. may have evolved since training cutoff.
