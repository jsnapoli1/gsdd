---
name: gsdd-writing-plans
description: Use when there is an approved GSDD spec and you need a codebase-aware implementation plan before touching production code.
---

# GSDD Writing Plans

Announce at start:
"I'm using the GSDD writing-plans skill to create the implementation plan."

Core rule:
Do not write production code yet.

Read `references/test-matrix.md` before finalizing the plan.

## Process

1. Read the approved spec.
2. Explore the codebase for reusable UI, domain models, endpoints, jobs, permissions, notifications, file handling, revision logic, and tests.
3. Prefer extending existing capabilities over adding one-off screens or endpoints.
4. Write the implementation plan to `docs/claude-plans/YYYY-MM-DD-{feature}.md`.
5. If the harness exposes Codex commands, invoke `/codex:adversarial-review` for adversarial review of the spec and plan before presenting the final plan to the human partner.
6. Record the Codex review outcome in the plan or handoff, including what Codex reviewed, the key findings, and what changed because of that review.
7. If Codex review is unavailable, perform an internal adversarial review and explicitly say that a fallback was used because Codex commands were unavailable in this harness.
8. Unless `--skip-review` is present, ask the human partner to approve the written plan before execution.

## Plan Requirements

Every plan must include:
- goal
- architecture summary
- reuse decisions
- files likely to change
- test matrix
- rollout and rollback notes
- observability notes
- bite-sized implementation slices
- definition of done for each slice

## Reuse Review

For each major part of the feature, inspect whether there is already:
- a suitable screen or route
- a similar API or server action
- an existing domain object or state machine
- an existing permission policy
- a queue or job that should be reused
- notification infrastructure
- file or revision handling utilities
- existing tests that should be extended

Document what you found and why you are reusing or not reusing it.

## Plan Quality Bar

- Break work into small slices that can be implemented and verified quickly.
- Every slice must have owned files or components.
- Every slice must state how it will be tested.
- Call out blockers and unresolved questions instead of guessing.
- Keep the plan specific enough that a bounded implementation agent can execute it without inventing behavior.

## Codex Review Gate

- Do not merely say that Codex should be used. If Codex commands are available, actually invoke `/codex:adversarial-review`.
- Do not present the plan as adversarially reviewed until the Codex review has happened.
- Do not hide a skipped Codex step behind generic wording like "reviewed" or "validated."
- If Codex cannot be invoked, say that explicitly and name the fallback as an internal adversarial review.

## Stop Conditions

Pause and ask for clarification if ambiguity affects:
- money
- permissions
- destructive actions
- external integrations
- state transitions
- audit or compliance requirements
