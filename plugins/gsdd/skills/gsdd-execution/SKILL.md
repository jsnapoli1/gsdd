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
3. If the harness exposes Codex commands, invoke `/codex:rescue` to help produce the failing tests first with a bounded scope.
4. Record the Codex test-first handoff in the working notes or handoff, including the owned scope, proposed tests, and what was adopted or changed.
5. If Codex is unavailable, Claude must still write the tests first and explicitly note the fallback because Codex commands were unavailable in this harness.
6. Implement in small slices with a clear definition of done per slice.
7. After each slice, run targeted verification before moving on.
8. After feature completion, run the feature test suite and then the full regression suite.
9. Perform a manual walkthrough of the original user story when a UI or workflow is involved.
10. If the harness exposes Codex commands, invoke `/codex:adversarial-review` on the implementation and on the documentation before handoff.
11. Record the Codex review outcome in the handoff, including findings, resolutions, and any accepted residual risk.
12. Update repository documentation concisely.
13. Create logical commits or a PR according to repo convention.

## Hard Rules

- No production code without failing tests first.
- Do not rely on UI tests alone. Cover business rules and side effects directly.
- Do not hand a subagent vague work. Every subtask must have owned scope, expected verification, and a definition of done.
- Do not claim success based on code inspection alone.
- Do not say "production-ready" unless deployment has happened.
- Do not claim that Codex reviewed the work unless `/codex:adversarial-review` or `/codex:rescue` was actually invoked through an available command.
- Do not silently skip a required Codex step when the harness exposes Codex commands.

## Required Verification

- targeted tests for each implementation slice
- feature-specific suite
- full app suite
- manual click-through when the feature affects user workflows
- adversarial review findings resolved or explicitly documented

## If Codex Is Available

Use Codex for:
- `/codex:adversarial-review` for adversarial plan review
- `/codex:rescue` for test-first implementation help
- `/codex:adversarial-review` for adversarial implementation review
- `/codex:adversarial-review` for adversarial documentation review

If Codex disagrees with Claude, resolve the disagreement in favor of evidence from tests, codebase patterns, and the approved spec.

## Codex Handoff Contract

- Treat Codex use as a concrete workflow step, not a suggestion.
- When Codex is available, invoke `/codex:adversarial-review` before claiming the plan, implementation, or documentation received adversarial review.
- When bounded implementation help is needed, invoke `/codex:rescue` rather than describing a generic Codex handoff.
- Include a short Codex review record in the final handoff:
  - scope sent to Codex
  - key findings or recommendations
  - changes made in response
  - unresolved disagreements, if any
- If Codex is unavailable, say so explicitly and name the fallback review that was performed instead.
