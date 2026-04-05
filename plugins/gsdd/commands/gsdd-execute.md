---
description: "Execute an approved GSDD plan with TDD, bounded slices, Codex review, and release-readiness checks"
---

Use the `gsdd-execution` skill.

Assume there is already an approved spec and an approved implementation plan unless the user explicitly says otherwise.

If Codex commands are available in the harness, invoke `/codex:rescue` for test-first implementation support and `/codex:adversarial-review` for critique rather than only referencing Codex in the writeup.

Examples:
- "Send a task to codex to draft the failing tests for slice 1" means invoke `/codex:rescue`.
- "Have Codex Review this implementation before handoff" means invoke `/codex:adversarial-review`.
