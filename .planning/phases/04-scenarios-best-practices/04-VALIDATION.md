---
phase: 4
slug: scenarios-best-practices
status: draft
nyquist_compliant: false
wave_0_complete: false
created: 2026-04-16
---

# Phase 4 — Validation Strategy

> Per-phase validation contract for feedback sampling during execution.

---

## Test Infrastructure

| Property | Value |
|----------|-------|
| **Framework** | Marp CLI (markdown presentation) |
| **Config file** | none — slides.md is the deliverable |
| **Quick run command** | `grep -c "^---$" slides.md` (slide count check) |
| **Full suite command** | `npx @marp-team/marp-cli slides.md --html -o /dev/null 2>&1` |
| **Estimated runtime** | ~5 seconds |

---

## Sampling Rate

- **After every task commit:** Run `grep -c "^---$" slides.md` (verify slide count increases)
- **After every plan wave:** Run full Marp build to verify no rendering errors
- **Before `/gsd-verify-work`:** Full suite must be green
- **Max feedback latency:** 5 seconds

---

## Per-Task Verification Map

| Task ID | Plan | Wave | Requirement | Test Type | Automated Command | File Exists | Status |
|---------|------|------|-------------|-----------|-------------------|-------------|--------|
| 04-01-01 | 01 | 1 | SCEN-01 | content | `grep -c "decision tree\|flowchart" slides.md` | ✅ | ⬜ pending |
| 04-01-02 | 01 | 1 | SCEN-02 | content | `grep "gsd-new-project" slides.md` | ✅ | ⬜ pending |
| 04-01-03 | 01 | 1 | SCEN-03 | content | `grep "gsd-map-codebase" slides.md` | ✅ | ⬜ pending |
| 04-01-04 | 01 | 1 | SCEN-04 | content | `grep "gsd-debug\|gsd-fast" slides.md` | ✅ | ⬜ pending |
| 04-02-01 | 02 | 1 | BEST-01 | content | `grep -i "mental model\|mindset" slides.md` | ✅ | ⬜ pending |
| 04-02-02 | 02 | 1 | BEST-02 | content | `grep -i "prompt" slides.md` | ✅ | ⬜ pending |
| 04-02-03 | 02 | 1 | BEST-03 | content | `grep -i "anti-pattern" slides.md` | ✅ | ⬜ pending |
| 04-02-04 | 02 | 1 | BEST-04 | content | `grep -i "escape\|when not" slides.md` | ✅ | ⬜ pending |
| 04-02-05 | 02 | 1 | BEST-05 | content | `grep -i "Monday\|Start Monday" slides.md` | ✅ | ⬜ pending |
| 04-03-01 | 03 | 1 | PRAC-04 | content | `grep "gsd-map-codebase" slides.md` | ✅ | ⬜ pending |

*Status: ⬜ pending · ✅ green · ❌ red · ⚠️ flaky*

---

## Wave 0 Requirements

*Existing infrastructure covers all phase requirements.*

---

## Manual-Only Verifications

| Behavior | Requirement | Why Manual | Test Instructions |
|----------|-------------|------------|-------------------|
| Decision tree is photographable at projector resolution | SCEN-01 | Visual layout check | Preview slide at 1920x1080, verify tree fits single slide |
| Slide transitions flow naturally | ALL | Presentation flow | Read slides in sequence, verify logical progression |

---

## Validation Sign-Off

- [ ] All tasks have automated verify or Wave 0 dependencies
- [ ] Sampling continuity: no 3 consecutive tasks without automated verify
- [ ] Wave 0 covers all MISSING references
- [ ] No watch-mode flags
- [ ] Feedback latency < 5s
- [ ] `nyquist_compliant: true` set in frontmatter

**Approval:** pending
