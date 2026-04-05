# Gold Standard Driven Development

Gold Standard Driven Development, or GSDD, is a Claude Code plugin and marketplace repo for turning rough feature requests into reviewed specs, reviewed plans, failing tests, working code, and staging-ready branches.

The workflow is intentionally opinionated:
- story first
- spec before code
- plan before implementation
- tests before production changes
- adversarial review before completion
- staging-ready before "done"

This project is heavily inspired by [obra/superpowers](https://github.com/obra/superpowers), especially its skill-first workflow, hard gates, and emphasis on evidence over claims.

## Repo Layout

- `.claude-plugin/marketplace.json`
  Marketplace manifest for Claude Code.
- `plugins/gsdd`
  The installable plugin.
- `plugins/gsdd/commands`
  Command entrypoints for the GSDD workflow.
- `plugins/gsdd/skills`
  Reusable behavior-shaping skills for story review, planning, and execution.

## What The Plugin Does

The `gsdd` plugin helps Claude:
- turn rough stories into approved specs
- explore the codebase before planning
- write implementation plans with explicit reuse decisions
- enforce test-first execution
- invoke `/codex:adversarial-review` for adversarial review
- invoke `/codex:rescue` for bounded implementation support
- explicitly record when Codex was used and when a fallback was required
- stop at "ready for staging review" unless deployment has happened

## Local Validation

Validate the marketplace:

```bash
claude plugin validate .
```

Validate the plugin itself:

```bash
claude plugin validate ./plugins/gsdd
```

Test the plugin without installing it:

```bash
claude --plugin-dir ./plugins/gsdd
```

## Marketplace Install

After pushing this repo to GitHub, add the marketplace:

```bash
claude plugin marketplace add YOUR_GITHUB_USERNAME/gold-standard-driven-development
```

Then install the plugin:

```bash
claude plugin install gsdd@gsdd-marketplace
```

Or from inside an interactive Claude Code session:

```text
/plugin marketplace add YOUR_GITHUB_USERNAME/gold-standard-driven-development
/plugin install gsdd@gsdd-marketplace
```
