# Public Release Audit

This note describes what was intentionally kept or excluded from `public-release/`.

## Included

- Firmware source and config needed to reproduce the current custom build
- Build metadata: `build.yaml`, `zephyr/module.yml`, `.github/workflows/build.yml`
- Documentation that explains the current hardware and behavior
- Optional diagnostic tools that are general enough to publish
- Repository `LICENSE`

## Excluded

- `deps/`
  - local dependency checkouts
  - nested `.git` directories
- `.obsidian/`
  - local editor/workspace metadata
- `AGENTS.md`
  - local coding-agent instruction file
- `docs/experiments/interaction-feedback/AGENTS.md`
  - internal task-routing helper
- `docs/experiments/interaction-feedback/REPO_BASELINE.md`
  - internal repo-orientation memo
- `docs/experiments/interaction-feedback/CODEX_TASK_BRIEF.md`
  - internal implementation brief
- `docs/experiments/interaction-feedback/TRACKPAD_STATE_EVENT_SPEC.md`
  - old planning notes including optional piezo context
- `docs/experiments/interaction-feedback/TRACKPAD_BEHAVIOR_SPEC.md`
  - old planning notes including optional piezo context
- `docs/experiments/interaction-feedback/CURRENT_TRACKPAD_BEHAVIOR_BASELINE.md`
  - historical baseline memo with optional piezo context
- `docs/experiments/interaction-feedback/FIRMWARE_MVP_SPEC.md`
  - historical MVP memo

## Sensitive String Scan Summary

A simple repo scan was run for:

- API keys
- secrets/tokens/passwords
- Wi-Fi terms
- local absolute paths
- personal handles/usernames

Findings addressed in the public snapshot:

- Removed internal-only docs that referenced local workflow/Codex context
- Removed a doc that referenced a personal GitHub fork URL
- Removed old docs that still carried historical optional piezo discussion

No obvious secrets, tokens, passwords, Wi-Fi credentials, or local absolute filesystem paths were found in `public-release/` after cleanup.

## Residual Risk

- This is a pattern-based scan, not a formal secret audit
- Hardware notes still reflect personal experimental tuning choices
- Documentation may still contain historical context that is useful but not polished as an official guide
