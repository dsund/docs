---
phase: 3
slug: core-payload-full-workflow
status: draft
nyquist_compliant: false
wave_0_complete: false
created: 2026-04-15
---

# Phase 3 — Validation Strategy

> Per-phase validation contract for feedback sampling during execution.

---

## Test Infrastructure

| Property | Value |
|----------|-------|
| **Framework** | PowerShell string matching (same as Phase 2) |
| **Config file** | None — inline verification commands |
| **Quick run command** | `powershell -Command "$c = Get-Content slides.md -Raw; ..."` |
| **Full suite command** | Same as quick run — all checks in one pass |
| **Estimated runtime** | ~2 seconds |

---

## Sampling Rate

- **After every task commit:** Run relevant PowerShell content checks
- **After every plan wave:** Full suite — all requirement checks in one pass
- **Before `/gsd-verify-work`:** Full suite must be green + human Marp preview
- **Max feedback latency:** 5 seconds

---

## Per-Task Verification Map

| Task ID | Plan | Wave | Requirement | Test Type | Automated Command | File Exists | Status |
|---------|------|------|-------------|-----------|-------------------|-------------|--------|
| 03-01-01 | 01 | 1 | DEEP-01 | automated | `$c -match 'new-project.*discuss.*plan.*execute.*verify' -or ($c -match 'livscykeln' -and $c -match 'discuss' -and $c -match 'verify')` | ❌ W0 | ⬜ pending |
| 03-01-02 | 01 | 1 | DEEP-02 | automated | `$c -match 'orchestrator' -and $c -match 'agents'` | ❌ W0 | ⬜ pending |
| 03-01-03 | 01 | 1 | DEEP-03 | automated | `$c -match '\.planning/' -and $c -match 'ROADMAP' -and $c -match 'STATE'` | ❌ W0 | ⬜ pending |
| 03-01-04 | 01 | 1 | DEEP-04 | automated | `$c -match 'resume-work' -or $c -match 'projektminne' -or $c -match 'session'` | ❌ W0 | ⬜ pending |
| 03-01-05 | 01 | 1 | DEEP-05 | automated | `$c -match 'task completion.*goal' -or ($c -match 'Task.*klara' -and $c -match 'mål.*uppnått')` | ❌ W0 | ⬜ pending |
| 03-01-06 | 01 | 1 | DEEP-06 | automated | `$c -match '--discuss' -and $c -match '--research' -and $c -match '--full'` | ✅ Partial | ⬜ pending |
| 03-01-07 | 01 | 1 | PRAC-08 | automated | `$c -match 'new-project' -and ($c -match 'cleanup' -or $c -match 'livscykel' -or $c -match 'workspace')` | ❌ W0 | ⬜ pending |

*Status: ⬜ pending · ✅ green · ❌ red · ⚠️ flaky*

---

## Wave 0 Requirements

- [ ] No existing test infrastructure for Phase 3 checks — all verification commands are inline PowerShell
- [ ] Human visual verification (Marp preview) is required as final gate — cannot be fully automated

*Matches Phase 2's validation approach — inline PowerShell checks + human Marp preview*

---

## Manual-Only Verifications

| Behavior | Requirement | Why Manual | Test Instructions |
|----------|-------------|------------|-------------------|
| Marp visual rendering | ALL | Marp rendering fidelity cannot be verified by string matching | Open slides.md in Marp preview, verify Section 3 and Section 5 render correctly |
| Slide readability | ALL | Back-of-room readability is subjective | Verify font sizes, spacing, one-idea-per-slide in Marp preview |

---

## Validation Sign-Off

- [ ] All tasks have `<automated>` verify or Wave 0 dependencies
- [ ] Sampling continuity: no 3 consecutive tasks without automated verify
- [ ] Wave 0 covers all MISSING references
- [ ] No watch-mode flags
- [ ] Feedback latency < 5s
- [ ] `nyquist_compliant: true` set in frontmatter

**Approval:** pending
