# AGENT.md — Rails Tabler Starter (Hotwire) Agent Contract

This repository is a Rails application template optimized for:
- Rails + Hotwire (Turbo + Stimulus)
- Tabler (Bootstrap 5) UI
- Fast solo-dev iteration with strong verification gates

## Baseline Stack (do not change without updating docs)
- Rails: ~> 8.1.x
- Hotwire: turbo-rails, stimulus-rails
- AuthN: Devise (+ devise_invitable)
- AuthZ: Pundit
- Admin: rails_admin
- Jobs/cache/cable: solid_queue, solid_cache, solid_cable
- DB: sqlite3 (prod-optimized)
- CSS: cssbundling-rails with sass + postcss
- Tests: RSpec + Capybara system tests

## Primary Commands
### Setup & Run
- `bin/setup`
- `bin/dev` (runs web + css watch)

### Tests
- `bundle exec rspec`
- `bundle exec rspec spec/system` (system tests)

### Lint & Security
- `bundle exec rubocop`
- `bundle exec brakeman`

### CSS
- `yarn build:css` (one-shot)
- `yarn watch:css` (watch)

## Rules for Agents / Contributors
- Prefer standard Rails patterns over clever abstractions.
- Hotwire-first UI: Turbo Frames/Streams + Stimulus controllers for interactivity.
- Keep authorization explicit via Pundit policies (no implicit “admin checks” in controllers).
- All new features must include:
  - acceptance criteria (Given/When/Then) in a spec doc
  - request/system specs for the critical flows
- Do not introduce new infra dependencies (Redis, Kafka, etc.) without a written decision record.

## Where to put things
- Specs: `docs/specs/`
- Decision records: `docs/decisions/`
- Release notes / rollouts: `docs/releases/`
- Temporary scratch: `docs/scratch/` (not long-lived)

## Definition of Done (hard gate)
A feature is “done” only when:
- `bundle exec rspec` passes
- `bundle exec rubocop` passes (or waivers documented)
- `bundle exec brakeman` passes (or waivers documented)
- Acceptance criteria can be verified from the spec doc