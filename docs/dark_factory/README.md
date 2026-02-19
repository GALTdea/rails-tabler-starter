# Level 5 Dark Factory Flow (Hotwire Rails)

This template ships with a default development workflow:
**Spec → Plan → Implement → Verify → Ship**, with artifacts that keep you fast as a solo dev.

## Stages
### Stage 1 — High-Fidelity Specification (HFS)
Output: `docs/specs/<feature_slug>.md`
- Unambiguous behavior
- Domain invariants
- Edge cases
- Acceptance criteria (Given/When/Then)
- Test plan

### Stage 2 — Decomposition Plan (Phases + Commits)
Output: `docs/specs/<feature_slug>__plan.md`
- Phases (1–5)
- Each phase maps to commits
- Explicit “verify” step per phase

### Stage 3 — Implementation
Rules:
- Follow template conventions (Hotwire-first, Pundit policies, RSpec coverage)
- Keep changes small enough for clean review/rollback

### Stage 4 — Verification (Always Works™)
Output: `docs/specs/<feature_slug>__verification.md`
- Checklist of commands + user flows
- Performance expectations (if relevant)
- Security/privacy checks (if relevant)

### Stage 5 — Release / Rollout
Output: `docs/releases/<date>__<feature_slug>.md`
- Migration/backfill notes
- Feature flags
- Rollback plan
- Observability notes

## Templates
Use these:
- `docs/dark_factory/templates/high_fidelity_spec.md`
- `docs/dark_factory/templates/decomposition_plan.md`
- `docs/dark_factory/templates/verification_checklist.md`
- `docs/dark_factory/templates/release_runbook.md`
