---
name: gsdd-execution-internal
description: Internal execution workflow used by the gsdd-execute command for test-first implementation, verification, documentation, and review.
---

# GSDD Execution Internal

This skill is internal. Humans should invoke `gsdd-execute`, not `gsdd-execution-internal`.

Announce at start:
"I'm using the GSDD execution skill to implement this approved plan."

Read `references/definition-of-done.md` before marking work complete.

This skill is the source of truth for execution behavior. Keep command files thin and put workflow requirements here.

## Preconditions

Do not start production edits unless:
- an approved spec exists
- an approved plan exists, or the user explicitly used `--skip-review`

If this skill is reached from `/gsdd:gsdd` or `/gsdd:gsdd-execute` and either prerequisite is missing, go back and complete story review and planning first, then resume execution automatically.

## Process

1. Create an isolated branch or worktree when the repo supports it.
2. Verify the baseline with relevant existing tests, lint, and typecheck before editing.
3. Break the approved plan into bounded implementation slices with a clear definition of done per slice.
4. Send each implementation slice to `/codex:rescue`. Claude should not write the slice itself unless the user explicitly asks Claude to do the coding instead of Codex.
5. Use `/codex:rescue` for the failing tests first and then for the minimal implementation needed for that same slice.
6. Wait for `/codex:rescue` to finish before continuing. Do not ask to run Codex in the background and do not continue while the rescue task is still running.
7. Record the Codex implementation handoff in the working notes or handoff, including the owned scope, proposed tests, code changes, and what was adopted or changed.
8. After each Codex-delivered slice, run targeted verification before moving on.
9. After feature completion, run the feature test suite and then the full regression suite.
10. Perform a manual walkthrough of the original user story when a UI or workflow is involved.
11. Update repository documentation concisely.
12. Prepare the release-readiness claim with concrete evidence: tests run, manual walkthrough status, docs updated, and remaining risks.
13. Before Claude says the work is finished, invoke `/codex:adversarial-review` on the implementation, documentation, and release-readiness claim.
14. Wait for `/codex:adversarial-review` to finish before continuing. Do not ask to run Codex in the background and do not continue while the review is still running.
15. Treat this final `/codex:adversarial-review` as a hard gate. Claude must not confirm completion until Codex has had a chance to pick apart the work and the resulting findings are resolved.
16. If Codex finds an implementation gap, send the next bounded fix slice back through `/codex:rescue`, then rerun the required verification before requesting a fresh `/codex:adversarial-review`.
17. If Codex finds a documentation or release-readiness gap, update the documentation or evidence, then request a fresh `/codex:adversarial-review`.
18. If Codex finds a plan gap, return to the planning phase, update the approved plan, and only then resume execution before requesting a fresh `/codex:adversarial-review`.
19. If Codex finds a spec gap or missing product rule, return to story review and spec approval, then re-plan as needed before resuming execution and requesting a fresh `/codex:adversarial-review`.
20. Repeat this loop until `/codex:adversarial-review` reports no blocking gaps.
21. Record the final adversarial review outcome in the handoff, including findings, resolutions, and any accepted residual risk.
22. Create logical commits or a PR according to repo convention.

## Hard Rules

- No production code without failing tests first.
- Do not let Claude absorb bounded implementation work that should be sent to `/codex:rescue`.
- Do not rely on UI tests alone. Cover business rules and side effects directly.
- Do not hand a subagent vague work. Every subtask must have owned scope, expected verification, and a definition of done.
- Do not claim success based on code inspection alone.
- Do not say "production-ready" unless deployment has happened.
- Do not claim that Codex reviewed the work unless `/codex:adversarial-review` or `/codex:rescue` was actually invoked.
- Do not silently skip a required Codex step.
- Do not continue execution while a `/codex:rescue` task is still running.
- Do not continue execution while an adversarial review is still running.
- Do not ask whether Codex rescue should run in the background. Wait for the rescue result.
- Do not ask whether Codex should run in the background. Wait for the review result.
- Do not let Claude declare "finished", "done", "ready for staging review", or "ready for merge" until the final adversarial review step has completed.

## Required Verification

- targeted tests for each implementation slice
- feature-specific suite
- full app suite
- manual click-through when the feature affects user workflows
- adversarial review findings resolved and the review rerun until no blocking gaps remain

## Implementation Delegation

Claude is the workflow controller. Codex is the bounded implementer.

- Claude should scope the slice, send it to `/codex:rescue`, wait for the result, then verify it.
- Codex should write the failing tests and the bounded implementation for that slice.
- Claude should only write code directly when the user explicitly asks Claude not to offload that slice to Codex.
- If a slice is too large or vague for `/codex:rescue`, Claude should split it into smaller slices and resend them. Claude should not use that vagueness as a reason to just implement the whole thing itself.

## Adversarial Review Loop

When `/codex:adversarial-review` returns findings, route them to the right stage instead of hand-waving them away:

- implementation defect or missing test coverage: send the bounded fix slice to `/codex:rescue`, then rerun targeted verification
- documentation or release-readiness defect: update docs or evidence, then rerun review
- plan defect: return to planning, update the approved plan, then resume execution
- spec defect or missing product rule: return to story review/spec approval, then re-plan and resume execution

After each fix, rerun the verification required by that stage and then invoke a fresh `/codex:adversarial-review` again.
Do not treat the previous review result as still valid after making changes.
The purpose of the fresh review is to confirm the fix worked and that nothing newly introduced was identified.
The loop ends only when the most recent `/codex:adversarial-review` reports no blocking gaps.

Use Codex for:
- `/codex:adversarial-review` for adversarial plan review
- `/codex:rescue` for test-first implementation of each bounded slice
- `/codex:adversarial-review` for the final adversarial review of implementation, documentation, and release-readiness claims immediately before handoff

If Codex disagrees with Claude, resolve the disagreement in favor of evidence from tests, codebase patterns, and the approved spec.

## Codex Handoff Contract

- Treat Codex use as a concrete workflow step, not a suggestion.
- Invoke `/codex:adversarial-review` before claiming the plan, implementation, or documentation received adversarial review.
- Send bounded implementation slices to `/codex:rescue` rather than writing them directly in Claude.
- Wait for `/codex:rescue` to complete before continuing. Do not send it to the background.
- If `/codex:rescue` cannot cleanly own a slice, split the slice smaller and resend it.
- The final completion gate must explicitly mention `/codex:adversarial-review` and happen before Claude confirms the work is finished.
- Wait for `/codex:adversarial-review` to complete before continuing. Do not send it to the background.
- If `/codex:adversarial-review` finds gaps, continue the workflow loop automatically until the gaps are resolved and Codex has re-reviewed the result.
- After implementing anything found in adversarial review, trigger a new `/codex:adversarial-review` to confirm no new issues were introduced.
- Include a short Codex review record in the final handoff:
  - scope sent to Codex
  - key findings or recommendations
  - changes made in response
  - unresolved disagreements, if any

## One-Shot Completion

When this skill is reached from `/gsdd:gsdd` or `/gsdd:gsdd-execute`, treat the entire workflow as one continuous run.

- Do not stop after an intermediate milestone while there is still implementation, verification, documentation, or adversarial-review work remaining.
- If a missing prerequisite or a Codex finding forces a return to story review or planning, do that work and then resume execution automatically.
- The one-shot run ends only when the implementation is complete, verification has passed, `/codex:adversarial-review` reports no blocking gaps, documentation is updated, and the handoff is ready for staging review or ready for merge.
