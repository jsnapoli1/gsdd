---
description: "Run the full Gold Standard Driven Development workflow: story review, planning, test-first implementation, Codex review, and staging-ready handoff"
---

You are running the Gold Standard Driven Development workflow.

Goal:
Turn the user's request into an approved spec, an approved implementation plan, failing tests, a working implementation, reviewed documentation, and a branch or PR that is ready for staging review.

Hard rules:
- Do not write production code until a written spec exists and is approved.
- Do not write production code until a written implementation plan exists and is approved, unless `--skip-review` is explicitly present.
- Reuse existing screens, models, endpoints, jobs, permissions, notifications, storage, and tests before inventing new ones.
- Treat examples as examples. If the user says a story is illustrative rather than canonical, extract the real business rules before finalizing the spec.
- Evidence over claims. Every completion claim must be backed by tests, direct verification, or saved artifacts.
- Never say "ready for production" unless the feature has actually been deployed. Default to "ready for staging review."

Routing:
- If the user gave a rough idea, a production narrative, or an incomplete feature description, use `gsdd-story-review`.
- If there is an approved spec but no approved plan, use `gsdd-writing-plans`.
- If there is an approved plan, use `gsdd-execution`.

Special handling:
- `--skip-review` only skips the human pause after the implementation plan is written and adversarially reviewed. It does not skip story review, self-review, adversarial review, testing, or release-readiness checks.
- If Codex tooling is unavailable, perform the closest internal fallback and say so.

Artifacts:
- Save specs to `docs/claude-specs/YYYY-MM-DD-{feature}.md`
- Save plans to `docs/claude-plans/YYYY-MM-DD-{feature}.md`
- Use `docs/templates/spec-template.md`, `docs/templates/plan-template.md`, and `docs/templates/release-readiness-template.md` as defaults

Finish by reporting:
- spec path
- plan path
- tests run
- manual walkthrough status
- documentation updated
- remaining risks
- final state: ready for staging review, ready for merge, or blocked
