---
phase: 1
slug: foundation-setup
status: draft
nyquist_compliant: false
wave_0_complete: false
created: 2026-04-15
---
# Phase 1 — Validation Strategy

> Per-phase validation contract for feedback sampling during execution.

---

## Test Infrastructure

| Property | Value |
|----------|-------|
| **Framework** | File existence checks + Marp CLI build |
| **Config file** | none — Wave 0 installs Marp CLI |
| **Quick run command** | `npx @marp-team/marp-cli --stdin < slides.md > /dev/null 2>&1 && echo PASS` |
| **Full suite command** | `npx @marp-team/marp-cli slides.md -o /dev/null --allow-local-files && echo PASS` |
| **Estimated runtime** | ~5 seconds |

---

## Sampling Rate

- **After every task commit:** Run quick run command
- **After every plan wave:** Run full suite command
- **Before `/gsd-verify-work`:** Full suite must be green
- **Max feedback latency:** 10 seconds

---

## Per-Task Verification Map

| Task ID | Plan | Wave | Requirement | Test Type | Automated Command | File Exists | Status |
|---------|------|------|-------------|-----------|-------------------|-------------|--------|
| 01-01-01 | 01 | 1 | SLIDE-01 | build | `npx @marp-team/marp-cli slides.md --stdin < /dev/null` | ❌ W0 | ⬜ pending |
| 01-01-02 | 01 | 1 | SLIDE-05 | content | `grep -c "English.*Swedish\|term.*English" terminology.md` | ❌ W0 | ⬜ pending |

*Status: ⬜ pending · ✅ green · ❌ red · ⚠️ flaky*

---

## Wave 0 Requirements

- [ ] `npm install --save-dev @marp-team/marp-cli` — Marp CLI for build validation
- [ ] `package.json` — Node project init if not present

*Marp CLI is required for automated validation of slide deck syntax and rendering.*

---

## Manual-Only Verifications

| Behavior | Requirement | Why Manual | Test Instructions |
|----------|-------------|------------|-------------------|
| Section divider visual appearance | SLIDE-01 | CSS styling renders visually | Open rendered HTML, verify bold centered title with separator line |
| Terminology consistency | SLIDE-05 | Requires reading Swedish text for term usage | Scan slide content for any non-English GSD terms |

---

## Validation Sign-Off

- [ ] All tasks have `<automated>` verify or Wave 0 dependencies
- [ ] Sampling continuity: no 3 consecutive tasks without automated verify
- [ ] Wave 0 covers all MISSING references
- [ ] No watch-mode flags
- [ ] Feedback latency < 10s
- [ ] `nyquist_compliant: true` set in frontmatter

**Approval:** pending
