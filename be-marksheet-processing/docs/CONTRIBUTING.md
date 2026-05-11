# Contributing Guidelines — Backend (Spring Boot)

These guidelines define how backend work must be planned, implemented, reviewed, and merged.  
All contributors must follow these rules to ensure reliability, traceability, and high engineering quality.

---

# 1. Workflow

## 1.1 Work must begin with a tracked issue
All backend work must be linked to one of:
- User Story (`user-story`)
- Bug (`bug`)
- Spike (`spike`)
- Technical Debt (`tech-debt`)

Use the appropriate GitHub Issue Template.

## 1.2 Branching
Create a branch using this pattern:
- `feature/<issue-number>-short-summary`
- `bugfix/<issue-number>-short-description`
- `spike/<issue-number>`
- `techdebt/<issue-number>`

Examples:
- `feature/123-user-update-endpoint`
- `bugfix/88-login-null-pointer`

## 1.3 Commit Message Standards
Use conventional commits:
- `feat: add order creation API`
- `fix: resolve NPE when saving user`
- `docs: update API documentation`
- `test: add integration tests for user API`
- `chore: upgrade Spring Boot version`

## 1.4 Pull Requests
- Use the backend PR template.
- PRs must be small and single-purpose.
- Every PR must reference an issue (`Fixes #123`).
- At least 1 reviewer required.
- PR must pass CI before merging.

---

# 2. Engineering Requirements

## 2.1 API Contract Requirements
When adding or modifying an endpoint:
- Update OpenAPI/Swagger contract.
- Document request/response schema.
- Include success + error examples.
- Maintain backward compatibility unless agreed otherwise.
- Validate inputs using DTO validation annotations.

## 2.2 Database Migration Rules
- All schema changes must use Flyway/Liquibase.
- No manual DB edits.
- Migration file naming must follow:
`V<timestamp>__short_description.sql`

- Changes must be idempotent and reversible.

## 2.3 Logging Standards
- Use structured logging.
- Never log passwords, tokens, keys, or sensitive PII.
- Include correlation ID in logs.
- Errors must include sufficient context for debugging.

## 2.4 Error Handling Standards
- All errors must produce unified JSON error format.
- Use custom exceptions + `@ControllerAdvice`.
- Validation errors must return structured error messages.

## 2.5 Security Practices
- All inputs must be validated.
- Authorization must be checked on every endpoint.
- Secrets must not be committed (use environment variables or Vault).
- Follow OWASP recommendations.

---

# 3. Testing Requirements

## 3.1 Mandatory Tests
Every feature must include:
- Unit tests (JUnit, Mockito)
- Integration tests (`@SpringBootTest`)
- API contract validation where applicable

## 3.2 Coverage Requirements
Minimum coverage:
- **70% line coverage**
- **80% for service layer**

## 3.3 Test Data
- Use Testcontainers when DB interaction exists.
- Avoid hardcoded local DB assumptions.
- Use meaningful, realistic test data.

---

# 4. Code Quality Standards

## 4.1 Architecture
- Use layered architecture (Controller → Service → Repository).
- Keep business logic in Service layer.
- DTOs must be separate from entities.
- Do not expose entities in API responses.

## 4.2 Style & Clean Code
- Follow Java 17+ conventions.
- Write self-explanatory code.
- No unused code, commented-out blocks, or dead branches.
- Dependency injection via constructor injection only.

## 4.3 Performance
- Avoid unnecessary DB calls.
- Use pagination for large result sets.
- Index database columns when needed.
- Cache where appropriate (Spring Cache).

---

# 5. CI/CD Requirements
A PR will not be merged unless:
- All unit and integration tests pass.
- The project builds successfully.
- Linting, formatting, and static analysis pass.
- No new critical Sonar issues introduced.

---

# 6. After Merge
- Update the User Story to **Done**.
- Close the associated issue(s).
- Tag the commit if part of a release.

---

These rules ensure consistency, maintainability, and engineering quality across the backend codebase.


  
