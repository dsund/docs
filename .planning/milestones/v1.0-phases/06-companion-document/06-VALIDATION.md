---
phase: 6
slug: companion-document
status: draft
nyquist_compliant: false
wave_0_complete: false
created: 2026-04-16
---

# Phase 6 — Validation Strategy

> Per-phase validation contract for feedback sampling during execution.

---

## Test Infrastructure

| Property | Value |
|----------|-------|
| **Framework** | Manual markdown review + grep verification |
| **Config file** | none — content authoring phase |
| **Quick run command** | `grep -c "##" companion.md` |
| **Full suite command** | `node -e "const fs=require('fs'); const c=fs.readFileSync('companion.md','utf8'); const sections=['Introduktion','GSD i korthet','Kom igång','Full Workflow','Scenarion','Best Practices','Referens']; const missing=sections.filter(s=>!c.includes(s)); if(missing.length){console.error('Missing:',missing);process.exit(1)}else{console.log('All sections present')}"` |
| **Estimated runtime** | ~1 second |

---

## Sampling Rate

- **After every task commit:** Run `grep -c "##" companion.md`
- **After every plan wave:** Run full suite command
- **Before `/gsd-verify-work`:** Full suite must be green
- **Max feedback latency:** 1 second

---

## Per-Task Verification Map

| Task ID | Plan | Wave | Requirement | Test Type | Automated Command | File Exists | Status |
|---------|------|------|-------------|-----------|-------------------|-------------|--------|
| 06-01-01 | 01 | 1 | COMP-01 | grep | `grep -c "##" companion.md` | ✅ | ⬜ pending |
| 06-01-02 | 01 | 1 | COMP-02 | grep | `grep -l "gsd-insert-phase\|gsd-review\|gsd-autonomous" companion.md` | ✅ | ⬜ pending |
| 06-01-03 | 01 | 1 | COMP-03 | manual | Manual review — standalone readability | ✅ | ⬜ pending |
| 06-01-04 | 01 | 1 | PRAC-05 | grep | `grep "gsd-insert-phase" companion.md` | ✅ | ⬜ pending |
| 06-01-05 | 01 | 1 | PRAC-06 | grep | `grep "gsd-review" companion.md` | ✅ | ⬜ pending |
| 06-01-06 | 01 | 1 | PRAC-07 | grep | `grep "gsd-autonomous" companion.md` | ✅ | ⬜ pending |

*Status: ⬜ pending · ✅ green · ❌ red · ⚠️ flaky*

---

## Wave 0 Requirements

*Existing infrastructure covers all phase requirements.*

---

## Manual-Only Verifications

| Behavior | Requirement | Why Manual | Test Instructions |
|----------|-------------|------------|-------------------|
| Standalone readability | COMP-03 | Comprehension requires human judgment | Read companion.md without slides context; verify GSD concepts are self-explanatory |
| Wiki-friendly markdown | COMP-03 | Rendering requires visual check | Open companion.md in GitHub preview; verify no broken formatting |
| Swedish/English term consistency | COMP-01 | Language nuance requires human review | Spot-check terms against TERMINOLOGY.md |

---

## Validation Sign-Off

- [ ] All tasks have `<automated>` verify or Wave 0 dependencies
- [ ] Sampling continuity: no 3 consecutive tasks without automated verify
- [ ] Wave 0 covers all MISSING references
- [ ] No watch-mode flags
- [ ] Feedback latency < 1s
- [ ] `nyquist_compliant: true` set in frontmatter

**Approval:** pending
