## Summary
Clearly describe what this PR does and why. Provide context for reviewers.

## Related Issues
Link the issue this PR closes:
- Fixes #<issue-number>
- Part of #<epic-or-feature-number>

(Required: Every PR must reference a User Story or Bug.)

## Changes Included
- Brief list of major changes
- Mention files, modules, or packages significantly impacted
- Note breaking changes (if any)

## Technical Notes
Add details that help reviewers:
- Algorithms, model logic, or architectural decisions
- API contract updates (request/response schemas)
- Configuration or environment variable changes
- External integrations (LLM providers, APIs, services)
- Performance, latency, or cost considerations

## Screenshots / Evidence (if applicable)
For UI or visual changes:
- Before / After screenshots
- Screen recordings

For backend / APIs:
- Sample request/response payloads
- Logs showing successful behavior
- Benchmark or load-test results (if performance-related)
- Model inference examples (if applicable)

## Testing
Describe testing performed:
- Unit tests added/updated (pytest)
- Integration / API tests added/updated
- Manual verification steps
- Relevant test data or fixtures used

## Deployment / Rollback Notes
(Required if PR affects production behavior)
- Deployment steps or configuration changes
- Rollback plan
- Feature flags or toggles used
- Model rollout or versioning considerations (if applicable)

## Checklist
### Functional
- [ ] Acceptance criteria fully met
- [ ] User Story or Bug linked (Fixes #ID)
- [ ] No breaking changes OR breaking changes documented

### Code Quality
- [ ] Code follows project conventions (PEP8 / project standards)
- [ ] Type hints and schemas updated where applicable
- [ ] No unreachable, dead, or temporary code
- [ ] Logging added where needed; no sensitive data logged

### Tests
- [ ] Unit tests added/updated and passing
- [ ] Integration / API tests added/updated and passing
- [ ] Test coverage meets team standards

### Documentation
- [ ] API documentation updated (Swagger / OpenAPI auto-docs)
- [ ] README / developer docs updated
- [ ] Configuration changes documented

### Security
- [ ] Inputs validated / sanitized
- [ ] Access control verified
- [ ] No secrets or credentials committed
- [ ] External API / model usage reviewed for security concerns

### Review Readiness
- [ ] PR assigned to reviewer(s)
- [ ] PR title follows naming convention
- [ ] PR is small and focused (recommended <300 lines)
