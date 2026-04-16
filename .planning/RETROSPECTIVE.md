# Project Retrospective

*A living document updated after each milestone. Lessons feed forward into future planning.*

## Milestone: v1.0 — GSD-presentation

**Shipped:** 2026-04-16
**Phases:** 6 | **Plans:** 10

### What Was Built
- 755-line Marp slide deck with 8 sections (~35 content slides) for ~60 min presentation
- 821-line standalone companion document with 7 sections + appendix
- Swedish/English terminology reference (20 term mappings)
- Copilot integration guide (copilot-instructions.md)

### What Worked
- "Payload first, framing second" build order — writing core content before intro meant the hook was sharp and informed
- TERMINOLOGY.md as single source of truth for language policy — prevented drift across 6 phases
- ASCII art diagrams (agent architecture, workflow pipeline, decision tree) — effective visuals in pure markdown
- Phase 6 (companion) building on locked slide narrative — expansion was efficient because source content was stable

### What Was Inefficient
- Requirements traceability table in REQUIREMENTS.md fell behind — many requirements stayed "Pending" despite being complete in the phases
- PROJECT.md evolution was sporadic — Active requirements not moved to Validated after each phase transition

### Patterns Established
- Swedish prose with English technical terms works naturally for developer education material
- Scenario-driven pattern for advanced features (open with developer situation, not feature description)
- Goal-backward verification model (Exists → Substantive → Wired → Functional) as teaching tool
- Bash code blocks with `$` prompt and `✅` for success output — consistent terminal example style

### Key Lessons
1. Content documents benefit from sequential phase execution — each phase builds on the previous, and the narrative coherence shows
2. Advanced features (phase insertion, cross-AI review, autonomous mode) were correctly deferred to companion — they'd have cluttered the slides
3. The "balanced comparison" approach to GSD vs BMAD built credibility — honest assessment > sales pitch

### Cost Observations
- Sessions: ~5 sessions over 2 days
- Notable: Phase 6 (companion) was the largest phase (3 plans, 821 lines) but executed smoothly because all source content was locked

---

## Cross-Milestone Trends

### Process Evolution

| Milestone | Phases | Plans | Key Change |
|-----------|--------|-------|------------|
| v1.0 | 6 | 10 | Initial delivery — payload-first build order |

### Top Lessons (Verified Across Milestones)

1. (First milestone — lessons above will be validated in future milestones)
