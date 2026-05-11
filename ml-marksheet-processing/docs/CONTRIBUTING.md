# Contributing Guidelines — Backend (Python)

These guidelines define how backend work must be planned, implemented, reviewed, and merged  
for **Python-based backend services** (REST APIs, ML inference, LLM integrations).

All contributors must follow these rules to ensure reliability, traceability, and high engineering quality.

---

# 1. Workflow

## 1.1 Work must begin with a tracked issue
All backend work must be linked to one of:
- User Story
- Bug
- Spike
- Technical Debt

Use the appropriate GitHub Issue Template.

## 1.2 Branching
Create a branch using this pattern:
- `python/us-<issue-number>-short-summary`
- `python/bug-<issue-number>-short-description`
- `python/spike-<issue-number>`
- `python/tech-<issue-number>`

Examples:
- `python/us-123-add-inference-endpoint`
- `python/bug-88-fix-tokenization-error`

## 1.3 Commit Message Standards
Use conventional commits:
- `feat: add prediction endpoint`
- `fix: handle empty input payload`
- `docs: update API documentation`
- `test: add API integration tests`
- `chore: upgrade dependencies`

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
- OpenAPI / Swagger must be auto-generated.
- Request and response schemas must be defined (e.g., Pydantic models).
- Include success and error examples.
- Maintain backward compatibility unless agreed otherwise.
- Validate inputs using schema validation.

## 2.2 Data & Persistence Rules
- Avoid hardcoding storage assumptions.
- Use migrations if a database is involved.
- Data access must be abstracted behind a repository or service layer.
- Changes must be backward compatible where possible.

## 2.3 Logging Standards
- Use structured logging.
- Never log secrets, tokens, API keys, or sensitive PII.
- Include request or correlation IDs where applicable.
- Errors must include sufficient context for debugging.

## 2.4 Error Handling Standards
- All errors must return a consistent JSON error format.
- Use centralized exception handling (middleware or exception handlers).
- Validation errors must be explicit and user-friendly.

## 2.5 Security Practices
- All inputs must be validated.
- Authorization must be enforced on every protected endpoint.
- Secrets must not be committed (use environment variables or secret managers).
- Follow OWASP recommendations.
- External APIs, LLMs, or models must be used securely and responsibly.

---

# 3. Testing Requirements

## 3.1 Mandatory Tests
Every feature must include:
- Unit tests (pytest)
- Integration or API tests
- Model or inference validation tests (if applicable)

## 3.2 Coverage Requirements
Minimum coverage expectations:
- **70% overall**
- **Higher coverage for core business logic**

## 3.3 Test Data
- Use fixtures and mocks.
- Avoid reliance on local machine state.
- External services and LLMs must be mocked or stubbed in tests.
- Use realistic, meaningful test data.

---

# 4. Code Quality Standards

## 4.1 Architecture
- Separate concerns clearly (API → Service → Domain / Model).
- Keep business logic out of route handlers.
- Use schemas for input/output validation.
- Avoid tight coupling between API and model logic.

## 4.2 Style & Clean Code
- Follow PEP 8 and project-specific conventions.
- Use meaningful names and type hints where appropriate.
- No dead code, commented-out blocks, or unused dependencies.
- Prefer explicit over implicit behavior.

## 4.3 Performance
- Avoid unnecessary computations or repeated model loads.
- Be mindful of inference latency and cost.
- Cache results where appropriate.
- Use pagination or streaming for large responses.

---

# 5. CI/CD Requirements

A PR will not be merged unless:
- All unit and integration tests pass.
- Linting checks pass.
- CI pipeline completes successfully.
- No new critical issues are introduced.

---

# 6. After Merge
- Update the linked issue to **Done**.
- Close associated issues automatically (`Fixes #ID`).
- Tag or document changes if part of a release.
- Ensure deployed behavior matches expectations.

---

These rules ensure consistency, maintainability, and high engineering quality  
across all Python backend services.
