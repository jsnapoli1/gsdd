# GSDD Definition Of Done

Work is not done until all applicable items below are true.

## Specification And Plan

- The implemented behavior matches the approved spec.
- The implementation stayed within the approved plan or the plan was updated intentionally.

## Testing

- New tests were written before production code.
- The new tests were observed failing for the expected reason.
- Targeted tests pass.
- Feature-level tests pass.
- Full-suite regression tests pass.

## Workflow Confidence

- A real user path can be clicked through if the feature is user-facing.
- Permissions behave correctly.
- Failure states are covered.
- Notifications, jobs, files, and revisions behave correctly when applicable.

## Review And Docs

- Adversarial review findings are resolved or consciously documented.
- High-level repository documentation is updated when behavior changed.
- Remaining risks are called out explicitly.

## Final Language

Use one of these completion states:
- ready for staging review
- ready for merge
- blocked

Do not use "ready for production" unless deployment has already happened.
