# GSDD Plugin

This is the installable Claude Code plugin for Gold Standard Driven Development.

Like `superpowers`, this plugin is skill-first:
- commands are thin entrypoints
- workflow behavior lives in `skills/*/SKILL.md`
- completion requires a final adversarial review before Claude confirms the work is finished

## Included Commands

- `gsdd`
- `gsdd-story-review`
- `gsdd-plan`
- `gsdd-execute`

## Included Skills

- `gsdd-story-review`
- `gsdd-writing-plans`
- internal execution skill used by `gsdd-execute`

## Workflow Order

1. Story review
2. Approved spec
3. Approved plan
4. Failing tests
5. Minimal implementation
6. Targeted verification
7. Full regression
8. Final `/codex:adversarial-review`
9. Documentation update
10. Staging-ready handoff

## Expected Outputs In A User Project

- `docs/claude-specs/YYYY-MM-DD-{feature}.md`
- `docs/claude-plans/YYYY-MM-DD-{feature}.md`

## Local Testing

From the marketplace repo root:

```bash
claude --plugin-dir ./plugins/gsdd
```
