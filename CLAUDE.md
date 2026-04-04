# Gold Standard Driven Development Maintainer Notes

## Commands Stay Thin

Keep command files small. Commands should route into skills, not duplicate skill logic.

## Skills Are Behavior Code

Treat skill text as executable behavior. Small wording changes can change agent outcomes. Make deliberate edits and keep hard gates explicit.

## Workflow Order

Do not weaken this order:

1. Story review
2. Approved spec
3. Approved plan
4. Failing tests
5. Minimal implementation
6. Targeted verification
7. Full regression
8. Adversarial review
9. Documentation update
10. Staging-ready handoff

## Codex Expectations

When the harness supports Codex commands, use them for adversarial review and bounded implementation support.

When Codex commands are unavailable:
- say so explicitly
- perform the closest internal fallback
- do not claim that Codex reviewed the work

## Done Means Staging-Ready

Do not tell the human partner that work is "ready for production" unless deployment has already happened. The default completion state for this plugin is "ready for staging review" or "ready for merge."
