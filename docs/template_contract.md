# Template Contract — rails-tabler-starter (Hotwire)

This document describes what is guaranteed to exist in apps generated from this template.

## Guaranteed stack
- Rails 8.1.x
- Turbo + Stimulus
- Devise (+ invite flow)
- Pundit authorization
- RailsAdmin installed
- Solid Queue/Cache/Cable
- SQLite by default
- RSpec + Capybara system tests
- CSS bundling with sass + postcss + Tabler/Bootstrap

## Conventions
- Hotwire-first UI. Prefer Turbo Frames/Streams over custom JS.
- Authorization: Pundit policies (explicit checks at controller actions).
- Testing: RSpec required for all non-trivial changes.

## Default quality gates
- `rspec` must pass
- `rubocop` must pass (or documented waiver)
- `brakeman` must pass (or documented waiver)

## When you may deviate
If you need a deviation (e.g., Postgres instead of SQLite, multi-tenancy off, different auth), write:
- a decision record in `docs/decisions/`
- update this contract if it becomes a new baseline
