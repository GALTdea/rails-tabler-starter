# Decomposition Plan — <Feature Name>
**Feature slug:** <feature_slug>
**Baseline:** rails-tabler-starter @ <commit SHA>

## Phase 0 — Prep (optional)
- [ ] Create spec doc
- [ ] Identify impacted models/policies/views

## Phase 1 — Data layer
- [ ] Migrations/models/validations
- [ ] Policy scaffolding
- Verify:
  - [ ] rspec (model/policy)
  - [ ] rubocop

## Phase 2 — Backend behavior (controllers/services/jobs)
- [ ] Endpoints + responses
- [ ] Authorize via Pundit
- Verify:
  - [ ] rspec (request)

## Phase 3 — UI + Hotwire wiring
- [ ] Turbo Frames/Streams
- [ ] Stimulus controllers
- Verify:
  - [ ] system spec passes
  - [ ] manual flow checklist

## Phase 4 — Hardening
- [ ] Edge cases
- [ ] Brakeman + security review
- [ ] Rate limits / abuse checks (if applicable)

## Phase 5 — Release
- [ ] Migration/backfill plan done
- [ ] Release runbook created
- [ ] Rollback steps written

## Commit Map (recommended)
- Commit 1: Phase 1
- Commit 2: Phase 2
- Commit 3: Phase 3
- Commit 4: Phase 4
- Commit 5: Phase 5
