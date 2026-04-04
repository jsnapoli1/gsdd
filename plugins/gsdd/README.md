# GSDD Plugin

This is the installable Claude Code plugin for Gold Standard Driven Development.

## Included Commands

- `gsdd`
- `gsdd-story-review`
- `gsdd-plan`
- `gsdd-execute`

## Included Skills

- `gsdd-story-review`
- `gsdd-writing-plans`
- `gsdd-execution`

## Expected Outputs In A User Project

- `docs/claude-specs/YYYY-MM-DD-{feature}.md`
- `docs/claude-plans/YYYY-MM-DD-{feature}.md`

## Local Testing

From the marketplace repo root:

```bash
claude --plugin-dir ./plugins/gsdd
```
