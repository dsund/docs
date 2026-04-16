---
phase: 5
slug: framing-intro-landscape
status: draft
nyquist_compliant: false
wave_0_complete: false
created: 2026-04-16
---

# Phase 5 — Validation Strategy

> Per-phase validation contract for feedback sampling during execution.

---

## Test Infrastructure

| Property | Value |
|----------|-------|
| **Framework** | Manual review (presentation slides) |
| **Config file** | slides.md |
| **Quick run command** | `grep -c '^---' slides.md` |
| **Full suite command** | `grep -c '^---' slides.md && grep -c '## ' slides.md` |
| **Estimated runtime** | ~1 second |

---

## Sampling Rate

- **After every task commit:** Run `grep -c '^---' slides.md` (verify slide count)
- **After every plan wave:** Verify section structure and content completeness
- **Before `/gsd-verify-work`:** Full content review against success criteria
- **Max feedback latency:** 2 seconds

---

## Per-Task Verification Map

| Task ID | Plan | Wave | Requirement | Test Type | Automated Command | File Exists | Status |
|---------|------|------|-------------|-----------|-------------------|-------------|--------|
| 05-01-01 | 01 | 1 | SLIDE-02 | content | `grep 'section' slides.md` | ✅ | ⬜ pending |
| 05-01-02 | 01 | 1 | CTXT-01 | content | `grep -i 'problem\|pain' slides.md` | ✅ | ⬜ pending |
| 05-01-03 | 01 | 1 | CTXT-02 | content | `grep -i 'agent.*framework\|LLM.*tools' slides.md` | ✅ | ⬜ pending |
| 05-01-04 | 01 | 1 | CTXT-03 | content | `grep -i 'BMAD\|comparison' slides.md` | ✅ | ⬜ pending |
| 05-01-05 | 01 | 1 | CTXT-04 | content | `grep -i 'collaborat\|replac' slides.md` | ✅ | ⬜ pending |

*Status: ⬜ pending · ✅ green · ❌ red · ⚠️ flaky*

---

## Wave 0 Requirements

Existing infrastructure covers all phase requirements — slides.md already exists with established patterns from Phases 1–4.

---

## Manual-Only Verifications

| Behavior | Requirement | Why Manual | Test Instructions |
|----------|-------------|------------|-------------------|
| Narrative flow | CTXT-04 | Subjective narrative quality | Read slides 1–10 aloud; skeptic→practitioner arc should feel natural |
| BMAD comparison fairness | CTXT-03 | Balanced tone assessment | Review comparison slides for neutral, non-dismissive language |
| Pacing appropriateness | SLIDE-02 | Timing judgment | Estimate ~1 min/slide for content slides; total should fit ~60 min |

---

## Validation Sign-Off

- [ ] All tasks have automated verify or Wave 0 dependencies
- [ ] Sampling continuity: no 3 consecutive tasks without automated verify
- [ ] Wave 0 covers all MISSING references
- [ ] No watch-mode flags
- [ ] Feedback latency < 2s
- [ ] `nyquist_compliant: true` set in frontmatter

**Approval:** pending
