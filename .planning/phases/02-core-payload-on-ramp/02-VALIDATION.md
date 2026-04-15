---
phase: 02
slug: core-payload-on-ramp
status: draft
nyquist_compliant: false
wave_0_complete: false
created: 2026-04-15
---

# Phase 02 — Validation Strategy

> Per-phase validation contract for feedback sampling during execution.

---

## Test Infrastructure

| Property | Value |
|----------|-------|
| **Framework** | Manual visual inspection (Marp slides) |
| **Config file** | slides.md (Marp front matter) |
| **Quick run command** | `npx @marp-team/marp-cli slides.md --html -o slides.html && start slides.html` |
| **Full suite command** | `npx @marp-team/marp-cli slides.md --html -o slides.html && start slides.html` |
| **Estimated runtime** | ~5 seconds |

---

## Sampling Rate

- **After every task commit:** Visual check of modified slides in browser
- **After every plan wave:** Full slide deck render and review
- **Before `/gsd-verify-work`:** Full suite must render cleanly
- **Max feedback latency:** 5 seconds

---

## Per-Task Verification Map

| Task ID | Plan | Wave | Requirement | Test Type | Automated Command | File Exists | Status |
|---------|------|------|-------------|-----------|-------------------|-------------|--------|
| 02-01-01 | 01 | 1 | SLIDE-03 | visual | `grep "gsd-fast" slides.md` | ✅ | ⬜ pending |
| 02-01-02 | 01 | 1 | SLIDE-04 | visual | `grep '^\$' slides.md` | ✅ | ⬜ pending |
| 02-01-03 | 01 | 1 | PRAC-01 | visual | `grep -i "install" slides.md` | ✅ | ⬜ pending |
| 02-01-04 | 01 | 1 | PRAC-02 | visual | `grep "gsd-fast" slides.md` | ✅ | ⬜ pending |
| 02-01-05 | 01 | 1 | PRAC-03 | visual | `grep "gsd-quick" slides.md` | ✅ | ⬜ pending |

*Status: ⬜ pending · ✅ green · ❌ red · ⚠️ flaky*

---

## Wave 0 Requirements

Existing infrastructure covers all phase requirements. Marp CLI is already configured in slides.md from Phase 1.

---

## Manual-Only Verifications

| Behavior | Requirement | Why Manual | Test Instructions |
|----------|-------------|------------|-------------------|
| ASCII art spectrum readable on projector | SLIDE-03 | Visual rendering quality | Render slides.html, check code block readability at <75 char width |
| Terminal examples feel authentic | SLIDE-04 | Subjective quality | Review each code block for realistic command/output pairs |
| Graduated complexity narrative flows | PRAC-03 | Narrative coherence | Read slides in sequence, verify escalation logic is convincing |

---

## Validation Sign-Off

- [ ] All tasks have automated verify or Wave 0 dependencies
- [ ] Sampling continuity: no 3 consecutive tasks without automated verify
- [ ] Wave 0 covers all MISSING references
- [ ] No watch-mode flags
- [ ] Feedback latency < 5s
- [ ] `nyquist_compliant: true` set in frontmatter

**Approval:** pending
