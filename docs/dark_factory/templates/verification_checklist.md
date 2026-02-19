# Verification — <Feature Name>
**Feature slug:** <feature_slug>

## Automated checks
- [ ] `bundle exec rspec`
- [ ] `bundle exec rubocop`
- [ ] `bundle exec brakeman`
- [ ] `yarn build:css` (if UI touched)

## Manual user flows
### Flow A —
- [ ] Step 1:
- [ ] Step 2:
- [ ] Expected result:

### Flow B —
- [ ] ...

## Security / privacy sanity
- [ ] Authorization enforced (Pundit) at controller boundaries
- [ ] No sensitive fields exposed in views/JSON
- [ ] No secrets logged

## Performance sanity (if relevant)
- [ ] Page loads < target
- [ ] No obvious N+1 (Bullet checks in dev)
