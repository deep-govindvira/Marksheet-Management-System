## Summary
Clearly describe what this PR does and why. Provide context for reviewers.

## Related Issues
Link the issue this PR closes:
- Fixes #<issue-number>
- Part of #<epic-or-feature-number>

(Required: Every PR must reference a User Story or Bug.)

## Changes Included
- Brief list of major changes
- Mention files or modules significantly impacted
- Note breaking changes (if any)

## Technical Notes
Add details that help reviewers:
- Algorithms / architectural decisions
- API contract updates
- Database schema or migration changes (Flyway/Liquibase)
- Feature flags added/updated
- Performance considerations

## Screenshots / Evidence (if applicable)
For UI or visual changes:
- Before / After screenshots
- Screen recordings

For backend:
- Sample request/response payloads
- Logs showing successful behavior
- Benchmark results (if performance-related)

## Testing
Describe testing performed:
- Unit tests added/updated
- Integration tests added/updated
- Manual verification steps
- Relevant test data

## Deployment / Rollback Notes
(Required if PR affects production behavior)
- Migration steps
- Rollback plan
- Feature flag strategy

## Checklist
### Functional
- [ ] Acceptance criteria fully met
- [ ] User Story or Bug linked (Fixes #ID)
- [ ] No breaking changes OR breaking changes documented

### Code Quality
- [ ] Code follows project conventions
- [ ] Types, interfaces, DTOs updated
- [ ] No unreachable, dead, or temporary code
- [ ] Logging added where needed; no sensitive logs

### Tests
- [ ] Unit tests added/updated, all passing
- [ ] Integration tests added/updated, all passing
- [ ] Test coverage meets team standards

### Documentation
- [ ] API documentation updated
- [ ] README / developer docs updated
- [ ] Migration instructions included (if any)

### Security
- [ ] Inputs validated / sanitized
- [ ] Access control verified
- [ ] No secrets committed

### Review Readiness
- [ ] PR assigned to reviewer
- [ ] PR title follows naming convention
- [ ] PR is small and focused (recommended <300 lines)
