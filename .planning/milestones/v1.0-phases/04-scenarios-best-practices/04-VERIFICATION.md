---
phase: 04-scenarios-best-practices
verified: 2026-04-16T08:30:00Z
status: passed
score: 10/10 must-haves verified
---

# Phase 4: Scenarios & Best Practices — Verification Report

**Phase Goal:** Audience can map their real-world situations to specific GSD commands, with clear guidance on mindset shifts, prompt crafting, anti-patterns, and a concrete next step to take Monday morning
**Verified:** 2026-04-16T08:30:00Z
**Status:** passed
**Re-verification:** No — initial verification

## Goal Achievement

### Observable Truths

| # | Truth | Status | Evidence |
|---|-------|--------|----------|
| 1 | Developer can look at decision tree and identify the right GSD command for their situation | ✓ VERIFIED | Lines 472–488: ASCII tree with 4 top-level branches, 8 command leaf nodes, all-English inside code fence |
| 2 | Greenfield scenario shows /gsd-new-project as full workflow entry point | ✓ VERIFIED | Lines 492–503: bash terminal example showing `/gsd-new-project` flow from idea to verified result |
| 3 | Brownfield scenario introduces /gsd-map-codebase as the distinct brownfield entry point | ✓ VERIFIED | Lines 507–519: dedicated slide "Brownfield — kartlägg först" with `/gsd-map-codebase` terminal example |
| 4 | Quick fix/debugging scenario shows two distinct paths: /gsd-fast for trivial and /gsd-debug for investigation | ✓ VERIFIED | Lines 534–552: two separate slides — "Quick fix — `/gsd-fast`" and "Behöver utredning? — `/gsd-debug`" |
| 5 | Decision tree content is entirely in English (exception to Swedish deck pattern) | ✓ VERIFIED | Code block lines 475–488 contain zero Swedish words; all labels/questions in English |
| 6 | Mental model shifts are stated as actionable principles with concrete do/don't examples | ✓ VERIFIED | Lines 575–599: two slides with ❌/✅ pairs ("Steg-för-steg" vs "Outcome", "Du" vs "AI" role split) |
| 7 | Prompt crafting guidance includes at least 3 concrete good/bad prompt pairs | ✓ VERIFIED | Lines 605–613: exactly 3 ❌/✅ pairs with concrete prompts (bug fix, button, refactor) |
| 8 | Escape hatches (when NOT to use agents) receive their own full slide with equal weight to anti-patterns | ✓ VERIFIED | Lines 631–643: dedicated slide "När du INTE ska använda agents" with 5 🚫 items and blockquote close |
| 9 | Anti-patterns reference the verification philosophy from Section 5 (task ≠ goal) | ✓ VERIFIED | Line 624: "task completion ≠ goal achievement" — mirrors Section 5 heading at line 420 |
| 10 | Start Monday challenge offers a zero-friction first step with install command and tiered options | ✓ VERIFIED | Lines 658–673: bash fence with `npx get-shit-done-cc@latest`, tiered table (5min/30min/2h) |

**Score:** 10/10 truths verified

### Required Artifacts

| Artifact | Expected | Status | Details |
|----------|----------|--------|---------|
| `slides.md` Section 6 | Decision tree + scenario content slides (7 slides) | ✓ VERIFIED | 7 slides: decision tree, greenfield, brownfield×2, gsd-fast, gsd-debug, bridge |
| `slides.md` Section 7 | Best practices content slides (5 slides) | ✓ VERIFIED | 5 slides: outcomes, role split, prompt crafting, anti-patterns, escape hatches |
| `slides.md` Section 8 | Start Monday + closing slides (2 slides) | ✓ VERIFIED | 2 slides: "Din challenge" with install+table, "Tack" closing |

All artifacts exist (Level 1), contain substantive content (Level 2), and are wired into the deck's slide flow (Level 3).

### Key Link Verification

| From | To | Via | Status | Details |
|------|----|-----|--------|---------|
| Section 6 decision tree | Commands in Sections 4–5 | Command name references | ✓ WIRED | All 8 commands appear earlier: gsd-fast (L199), gsd-quick (L214), gsd-do (L229), gsd-new-project (L327), gsd-resume-work (L396), gsd-add-phase (L230), gsd-map-codebase (new in S6), gsd-debug (new in S6) |
| Brownfield scenario | /gsd-map-codebase workflow | Terminal example | ✓ WIRED | Line 510: `$ /gsd-map-codebase` with plausible output showing 7 analysis documents |
| Section 7 anti-patterns | Section 5 verification philosophy | "task completion ≠ goal achievement" | ✓ WIRED | Line 624 references same concept as Section 5 line 420 |
| Section 8 install command | Section 4 installation slide | Same npx install command | ✓ WIRED | Line 663 `npx get-shit-done-cc@latest` matches Section 4 line 263 exactly |

### Data-Flow Trace (Level 4)

Not applicable — this is a static Marp presentation deck, not a dynamic data-rendering application. Content is authored text, not fetched/rendered data.

### Behavioral Spot-Checks

Step 7b: SKIPPED — Marp slide deck is static content; no runnable entry points to test. Marp rendering is a visual-only check (see Human Verification).

### Requirements Coverage

| Requirement | Source Plan | Description | Status | Evidence |
|-------------|------------|-------------|--------|----------|
| SCEN-04 | 04-01 | Decision tree — "vilket kommando ska jag använda?" | ✓ SATISFIED | Lines 472–488: decision tree with 8 command endpoints |
| SCEN-01 | 04-01 | Greenfield — full workflow från idé till implementation | ✓ SATISFIED | Lines 492–503: `/gsd-new-project` terminal walkthrough |
| SCEN-02 | 04-01 | Brownfield — jobba med befintlig kodbas | ✓ SATISFIED | Lines 507–530: two slides — mapping then adding features |
| SCEN-03 | 04-01 | Quick fix / debugging — `/gsd-fast` och `/gsd-debug` | ✓ SATISFIED | Lines 534–552: two separate slides for each path |
| PRAC-04 | 04-01 | Brownfield awareness — `/gsd-map-codebase` för befintlig kod | ✓ SATISFIED | Lines 507–519: dedicated brownfield mapping slide |
| BEST-01 | 04-02 | Mental model shifts — tänk outcomes inte steg | ✓ SATISFIED | Lines 575–599: two slides with ❌/✅ actionable principles |
| BEST-02 | 04-02 | Prompt crafting — hur man pratar med agents | ✓ SATISFIED | Lines 603–614: three concrete good/bad prompt pairs |
| BEST-03 | 04-02 | Escape hatches — när man INTE ska använda agents | ✓ SATISFIED | Lines 631–643: full slide with 5 situations + blockquote |
| BEST-04 | 04-02 | Anti-patterns — vaga prompts, skippa verification, micro-management | ✓ SATISFIED | Lines 618–628: three anti-patterns with guidance |
| BEST-05 | 04-02 | "Start Monday" challenge — konkret nästa steg | ✓ SATISFIED | Lines 658–673: install command + tiered challenge table |

**Orphaned requirements:** None. All 10 Phase 4 IDs in REQUIREMENTS.md traceability table are claimed by plans 04-01 and 04-02.

### Anti-Patterns Found

| File | Line | Pattern | Severity | Impact |
|------|------|---------|----------|--------|
| — | — | — | — | No anti-patterns detected |

- **TODO/FIXME/PLACEHOLDER scan:** Only match at line 357 ("Inte TODO-listor") is narrative text in Section 5, not a development placeholder. No Phase 4 content contains placeholders.
- **`_class` on content slides:** Zero occurrences. All `_class: divider` directives (lines 461, 564, 647) are on section divider slides only. ✓
- **Empty implementations:** Not applicable to static markdown content.
- **Stub patterns:** All slides contain substantive content — no `<div>Placeholder</div>` equivalents.

### Human Verification Required

### 1. Visual Rendering of Decision Tree

**Test:** Open slides.md in VS Code with Marp extension, navigate to "Vilket kommando ska jag använda?" slide
**Expected:** Box-drawing characters (├── │ └──) render correctly at slide viewport size, all 8 commands readable without horizontal scrolling
**Why human:** Character rendering depends on font and viewport — can't verify visually with grep

### 2. Slide Layout Density

**Test:** Navigate through all 14 Phase 4 content slides in Marp preview
**Expected:** Each slide follows one-idea-per-slide (D-12) — no overflow, no cramped text, spacious layout
**Why human:** Content density vs. viewport is a visual judgment

### 3. Narrative Flow Across Sections 6→7→8

**Test:** Read slides 6 through 8 as a continuous presentation
**Expected:** Natural transition from "which command" (S6) → "how to think" (S7) → "start now" (S8). Bridge slide (line 556) connects S6 to S7. Closing slide (line 677) provides satisfying end.
**Why human:** Narrative coherence requires reading comprehension, not pattern matching

### 4. Tone Verification — Utbildande, inte säljande

**Test:** Read Section 8 "Din challenge" and "Tack" slides
**Expected:** Educational tone. No "revolutionize", "transform", or sales-y language. The call-to-action feels like an invitation, not a pitch.
**Why human:** Tone is subjective — requires native Swedish comprehension

### Gaps Summary

No gaps found. All 10 observable truths verified. All 10 requirements satisfied. All key links wired. All artifacts substantive. Phase 4 adds 14 content slides across Sections 6 (7 slides), 7 (5 slides), and 8 (2 slides) — the decision tree, scenarios, best practices, and Start Monday challenge are complete and well-integrated into the deck's narrative arc.

---

_Verified: 2026-04-16T08:30:00Z_
_Verifier: the agent (gsd-verifier)_
