---
description: "Execute an approved GSDD plan with TDD, bounded slices, Codex review, and release-readiness checks"
---

Run execution in one-shot mode.

If an approved spec or approved implementation plan is missing, create them first by using `gsdd-story-review` and `gsdd-writing-plans` in one-shot mode, then continue automatically into `gsdd-execution-internal`.

Do not stop after spec review or plan review just to ask whether Claude should continue. For this command, approval to continue is implicit in the command invocation unless the user explicitly asks to pause.

When the spec and plan are ready, use the `gsdd-execution-internal` skill and continue through implementation, verification, repeated `/codex:adversarial-review`, and staging-ready handoff without stopping early.
