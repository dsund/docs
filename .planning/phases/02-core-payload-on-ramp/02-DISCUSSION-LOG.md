# Phase 2: Core Payload — On-Ramp - Discussion Log

> **Audit trail only.** Do not use as input to planning, research, or execution agents.
> Decisions are captured in CONTEXT.md — this log preserves the alternatives considered.

**Date:** 2026-04-15
**Phase:** 02-core-payload-on-ramp
**Areas discussed:** Command spectrum visual, Terminal examples, Getting started/installation, Slide density & narrative arc

---

## Command Spectrum Visual

| Option | Description | Selected |
|--------|-------------|----------|
| Horizontal progression | Left-to-right arrow/scale with labels (like a "complexity dial") | ✓ |
| Stacked comparison table | Rows for each command with columns: name, when to use, what it does, overhead | |
| Visual pyramid/ladder | Simple at bottom, complex at top, each level builds on previous | |
| You decide | Pick what works best for slides | |

**User's choice:** Horizontal progression — left-to-right arrow/scale
**Notes:** None

| Option | Description | Selected |
|--------|-------------|----------|
| Minimal | Command name + one-liner description per level | |
| Medium | Command name + description + "use when" hint per level | ✓ |
| Rich | Command name + description + use-when + example scenario per level | |

**User's choice:** Medium detail per level
**Notes:** None

| Option | Description | Selected |
|--------|-------------|----------|
| One spectrum slide only | Keep it punchy, details come in follow-up slides | ✓ |
| Spectrum + one follow-up | Slightly deeper breakdown on second slide | |
| Spectrum + individual breakdown | One slide per command level (4 slides total) | |

**User's choice:** One spectrum slide only
**Notes:** None

| Option | Description | Selected |
|--------|-------------|----------|
| ASCII art | Pure markdown, works everywhere, terminal-native feel | ✓ |
| Marp HTML/CSS | Styled boxes with arrows, slightly richer | |

**User's choice:** ASCII art — terminal-native feel
**Notes:** None

---

## Terminal Examples

| Option | Description | Selected |
|--------|-------------|----------|
| Plausible but invented | Generic "todo app" or similar simple context | |
| GSD-meta | Self-referential — GSD building this presentation | |
| Relatable dev scenario | "Fix a bug", "add a feature", something any developer recognizes | ✓ |

**User's choice:** Relatable dev scenarios
**Notes:** None

| Option | Description | Selected |
|--------|-------------|----------|
| Compact | 3-5 lines: prompt + command + key output line only | ✓ |
| Medium | 5-10 lines: realistic output snippet + result | |
| Verbose | 10+ lines: full realistic terminal output | |

**User's choice:** Compact — 3-5 lines, readable from the back
**Notes:** None

| Option | Description | Selected |
|--------|-------------|----------|
| Just /gsd-fast and /gsd-quick | The two extremes of the on-ramp | |
| Three examples | /gsd-fast, /gsd-quick, /gsd-do (skip full workflow) | |
| One per spectrum level | Including full workflow tease | ✓ |

**User's choice:** One per spectrum level including full workflow tease
**Notes:** None

| Option | Description | Selected |
|--------|-------------|----------|
| Standard $ prompt | Clean and universal | ✓ |
| copilot> styled prompt | Makes it clear it's inside the Copilot CLI | |

**User's choice:** Standard $ prompt
**Notes:** None

---

## Getting Started / Installation

| Option | Description | Selected |
|--------|-------------|----------|
| One-liner only | Show the install command, assume they'll figure it out | |
| One-liner + first command | Install + run /gsd-fast to show instant payoff | |
| Step-by-step | Prerequisites, install, verify, first command (2+ slides) | ✓ |

**User's choice:** Step-by-step — 2+ slides with full install walkthrough
**Notes:** None

| Option | Description | Selected |
|--------|-------------|----------|
| Before command spectrum | "Here's how to get it, now here's what you can do" | |
| After command spectrum | "Here's what you CAN do, now let's set it up" | |
| You decide | Agent picks what flows best | ✓ |

**User's choice:** You decide — agent's discretion on ordering
**Notes:** None

| Option | Description | Selected |
|--------|-------------|----------|
| Copilot CLI only | GitHub Copilot Extensions | ✓ |
| Claude Code only | CLAUDE.md skills | |
| Both side by side | Show it works with either | |

**User's choice:** Copilot CLI only
**Notes:** None

---

## Slide Density & Narrative Arc

| Option | Description | Selected |
|--------|-------------|----------|
| Spacious | One idea per slide, more slides, easier to follow | ✓ |
| Dense | Fewer slides with more content each | |
| Mixed | Spacious for key visuals, dense for explanatory slides | |

**User's choice:** Spacious — one idea per slide
**Notes:** None

| Option | Description | Selected |
|--------|-------------|----------|
| ~8-10 slides | Comfortable pacing for a 10-12 min section | |
| ~5-7 slides | Keep it tight, more time for other sections | |
| ~12-15 slides | Really spread out, each point gets room to breathe | |
| You decide | Agent picks appropriate count | ✓ |

**User's choice:** You decide — agent's discretion
**Notes:** None

| Option | Description | Selected |
|--------|-------------|----------|
| Gateway tease | "But what if your task is bigger? That's the full workflow..." | ✓ |
| Recap/summary slide | Section summary before transition | |
| Let divider handle it | Last example flows into divider slide | |

**User's choice:** Gateway tease — bridges to Phase 3
**Notes:** None

---

## Agent's Discretion

- Installation slide ordering (before or after command spectrum)
- Total slide count for Section 4

## Deferred Ideas

None — discussion stayed within phase scope
