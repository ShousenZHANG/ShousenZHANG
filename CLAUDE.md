# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

GitHub special profile repository for user `ShousenZHANG` (rendered at https://github.com/ShousenZHANG). Repo name must match the username for GitHub to display `README.md` on the profile page. There is no application code, build system, package manager, or test suite — this repo is content + scheduled SVG generation.

## Layout

- `README.md` — the profile page itself. Markdown rendered by GitHub. Hosts a typing-SVG header, badges, project cards, and image tags pointing at remotely-hosted or workflow-generated assets.
- `.github/workflows/` — two scheduled jobs that regenerate visualizations daily.
- `profile-3d-contrib/` — committed output of the 3D contribution workflow. README references `profile-night-green.svg` from this directory via raw.githubusercontent.com.

## Workflows and Their Side Effects

Both workflows write back to the repo on `workflow_dispatch` or schedule. Understand the destination before editing.

| Workflow | File | Schedule (UTC) | Action | Output destination |
|---|---|---|---|---|
| 3D contribution calendar | `.github/workflows/3d-contrib.yml` | `0 1 * * *` | `yoshi389111/github-profile-3d-contrib@0.7.1` | Commits all `profile-*.svg` files into `profile-3d-contrib/` on `main` as `github-actions[bot]` with message `chore: update 3D contribution calendar`. This is the source of the recent commit churn visible in `git log`. |
| Snake animation | `.github/workflows/snake.yml` | `0 0 * * *` | `Platane/snk/svg-only@v3` → `crazy-max/ghaction-github-pages@v4` | Publishes `github-snake.svg` and `github-snake-dark.svg` to the **`output`** branch (not `main`). README references these via raw.githubusercontent.com on the `output` branch. |

The `output` branch is workflow-managed — do not hand-edit it. Snake assets do not exist on `main`.

## README Asset Wiring

README image `src` URLs hard-code the GitHub username and the source branch. When changing assets, update both ends:

- 3D calendar tag references `main` branch path `profile-3d-contrib/profile-night-green.svg`. Switching themes means picking a different file from the same directory (variants: `profile-green`, `profile-green-animate`, `profile-night-green`, `profile-night-rainbow`, `profile-night-view`, `profile-season`, `profile-season-animate`, `profile-south-season`, `profile-south-season-animate`, `profile-gitblock`).
- Snake `<picture>` tag references `output` branch paths `github-snake.svg` (light) and `github-snake-dark.svg` (dark). The dark variant's palette is configured inside `snake.yml` via the `outputs:` query string — change colors there, not in README.
- Streak stats and activity graph use third-party services (`streak-stats.demolab.com`, `github-readme-activity-graph.vercel.app`); accent color `00BFA6` is the brand color used across all assets.

## Manual Regeneration

Trigger either workflow on demand from the Actions tab via "Run workflow" (both have `workflow_dispatch` enabled). No local build is possible — the actions require `GITHUB_TOKEN` and run only on Actions runners.

## Editing Conventions

- README edits: keep the centered HTML structure (`<p align="center">`, `<table>`) — GitHub-flavored Markdown does not support CSS, so layout relies on inline HTML.
- Commit message style for human commits: `<type>: <description>` (Conventional Commits). Bot commits use the fixed message above; do not reformat them.
- Username `ShousenZHANG` appears in README image URLs, the 3D workflow `USERNAME` env, and the snake workflow `github_user_name` input. Renaming the GitHub account requires updating all three plus the repo name itself.
