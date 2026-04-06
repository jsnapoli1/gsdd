---
description: "Run the full Gold Standard Driven Development workflow: story review, planning, test-first implementation, Codex review, and staging-ready handoff"
---

Run GSDD in one-shot mode.

Treat `/gsdd:gsdd` as a full end-to-end orchestrator:
- if the request is still a rough story, produce the spec
- if a plan is missing, write the plan
- if code has not been implemented, execute the plan
- continue looping until the work reaches staging-ready handoff

Do not stop after spec review or plan review just to ask whether Claude should continue. For this command, approval to continue is implicit in the command invocation unless the user explicitly asks to pause.

When code-writing is required, continue from story review to planning to `gsdd-execute` automatically.

Hard gates:
- Do not write production code before an approved spec exists.
- Do not write production code before an approved implementation plan exists unless `--skip-review` is explicitly present.
- Do not claim adversarial review happened unless `/codex:adversarial-review` was actually invoked.
- Do not let Claude declare the work finished until the final adversarial review step has happened on the implementation, documentation, and release-readiness claim.
- Do not stop the one-shot workflow while there is remaining code-writing, verification, or adversarial-review work to do.

Artifacts default to:
- `docs/claude-specs/YYYY-MM-DD-{feature}.md`
- `docs/claude-plans/YYYY-MM-DD-{feature}.md`
- `docs/templates/spec-template.md`
- `docs/templates/plan-template.md`
- `docs/templates/release-readiness-template.md`
