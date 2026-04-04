# GSDD Test Matrix

Every serious feature does not need every test type, but the plan must actively consider each category and explain the chosen coverage.

## Functional Coverage

- Unit tests for core business rules
- Integration tests for boundaries between components
- API or contract tests for server behavior
- UI interaction tests for the main user journey

## Risk Coverage

- Permission and role tests
- Validation and failure-path tests
- Empty-state and no-match tests
- Status transition tests
- Notification tests
- Async job or queue tests
- File, attachment, and revision tests

## Confidence Coverage

- A user can click through the implemented flow
- The server persists the expected data
- Side effects happen exactly once when they should
- Failure messaging is actionable
- Regressions in adjacent flows are unlikely
