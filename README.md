# LaLaPad Gen2 Experimental Build Log

This repository is a public snapshot of my current LaLaPad Gen2 ZMK firmware work.

It is intentionally published as an experimental build log and customization repo, not as an official manual or official support channel.

Use it at your own risk. Hardware wiring, force thresholds, haptic tuning, and split behavior here are tailored to one ongoing experiment and may not be correct for another build.

## 日本語補足

このリポジトリは、LaLaPad Gen2 向けの個人的な ZMK カスタム実験の最新版スナップショットです。

- 公式の手順書ではありません
- 実験ログ / build log として公開しています
- 再現や流用は自己責任でお願いします
- 元プロジェクトの公式見解やサポート窓口ではありません

元の LaLaPad Gen2 プロジェクトおよびそのベースとなる構成・発想に対して、敬意とクレジットを明記したうえで公開しています。

## Status

- Experimental build log
- Latest known working snapshot only
- Not an official LaLaPad Gen2 repository
- Not affiliated with the original project maintainer beyond using their public work as the base

## Credits

LaLaPad Gen2 itself, the original project structure, and the upstream firmware base are credited to the original creator and maintainer:

- ShiniNet / LaLaPad Gen2
- Upstream repository references are preserved in `config/west.yml` and the project history/docs where relevant

This public snapshot is a downstream personal customization layer on top of that base.

## License

This snapshot keeps the repository `LICENSE` file as-is and does not try to override the upstream license terms.

If you publish derivatives, keep the license notice intact and also verify the licenses of any upstream dependencies fetched through `west`.

## What Is Included

- Current shield/config files for `lalapadgen2`
- Current custom drivers, behaviors, and input processors
- Experimental documentation under `docs/experiments/interaction-feedback/`
- Optional local diagnostic tools under `tools/`
- GitHub Actions build workflow

## What Is Intentionally Not Included

- Old private workspace/editor metadata
- Local dependency checkouts under `deps/`
- Internal agent instruction files
- Private development history cleanup or rewritten git history

## Build Notes

This repo expects the usual ZMK user-config style workflow.

Typical structure:

1. Initialize/update dependencies with `west` using `config/west.yml`
2. Build with the included `build.yaml`
3. Flash the generated artifacts to the appropriate half

The exact hardware assumptions and wiring notes are documented in:

- `docs/experiments/interaction-feedback/PROJECT_CONTEXT.md`
- `docs/experiments/interaction-feedback/HARDWARE_AND_PIN_PLAN.md`
- `docs/experiments/interaction-feedback/CURRENT_FORCE_BEHAVIOR_SPEC.md`
- `docs/experiments/interaction-feedback/EXPERIMENTAL_BOM.md`

## Warning

This is not a canonical source of truth for LaLaPad Gen2 assembly or support.

If you are looking for the original project, the safest interpretation is:

- upstream project for the base hardware and official guidance
- this repo for one experimental downstream firmware state
