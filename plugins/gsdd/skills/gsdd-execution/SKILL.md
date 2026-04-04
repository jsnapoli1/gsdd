---
name: gsdd-execution
description: Use when there is an approved GSDD plan and the feature is ready for test-first implementation, verification, documentation, and review.
---

# GSDD Execution

Announce at start:
"I'm using the GSDD execution skill to implement this approved plan."

Read `references/definition-of-done.md` before marking work complete.

## Preconditions

Do not start production edits unless:
- an approved spec exists
- an approved plan exists, or the user explicitly used `--skip-review`

## Process

1. Create an isolated branch or worktree when the repo supports it.
2. Verify the baseline with relevant existing tests, lint, and typecheck before editing.
3. Use Codex to write the failing tests first when Codex is available.
4. If Codex is unavailable, Claude must still write the tests first and explicitly note the fallback.
5. Implement in small slices with a clear definition of done per slice.
6. After each slice, run targeted verification before moving on.
7. After feature completion, run the feature test suite and then the full regression suite.
8. Perform a manual walkthrough of the original user story when a UI or workflow is involved.
9. Use Codex adversarial review on the implementation and on the documentation.
10. Update repository documentation concisely.
11. Create logical commits or a PR according to repo convention.

## Hard Rules

- No production code without failing tests first.
- Do not rely on UI tests alone. Cover business rules and side effects directly.
- Do not hand a subagent vague work. Every subtask must have owned scope, expected verification, and a definition of done.
- Do not claim success based on code inspection alone.
- Do not say "production-ready" unless deployment has happened.

## Required Verification

- targeted tests for each implementation slice
- feature-specific suite
- full app suite
- manual click-through when the feature affects user workflows
- adversarial review findings resolved or explicitly documented

## If Codex Is Available

Use Codex for:
- adversarial plan review
- test-first implementation help
- adversarial implementation review
- adversarial documentation review

If Codex disagrees with Claude, resolve the disagreement in favor of evidence from tests, codebase patterns, and the approved spec.
