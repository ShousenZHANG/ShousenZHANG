# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

GitHub special profile repository for user `ShousenZHANG` (rendered at https://github.com/ShousenZHANG). Repo name must match the username for GitHub to display `README.md` on the profile page. There is no application code, build system, package manager, or test suite — this repo is content + scheduled SVG generation.

## Layout

- `README.md` — the profile page itself. Markdown rendered by GitHub. Hosts a typing-SVG header, badges, project cards, and image tags pointing at remotely-hosted or workflow-generated assets.
- `.github/workflows/` — two scheduled jobs that regenerate visualizations daily.
- `profile-3d-contrib/` — committed output of the 3D contribution workflow. **Currently NOT referenced by README** — assets continue regenerating but are unused. Safe to delete the folder + workflow if you want to stop the daily commit churn.

## Workflows and Their Side Effects

All workflows write back to the repo on `workflow_dispatch` or schedule. Understand the destination before editing.

| Workflow | File | Schedule (UTC) | Action | Output destination |
|---|---|---|---|---|
| 3D contribution calendar | `.github/workflows/3d-contrib.yml` | `0 1 * * *` | `yoshi389111/github-profile-3d-contrib@0.7.1` | Commits all `profile-*.svg` files into `profile-3d-contrib/` on `main` as `github-actions[bot]` with message `chore: update 3D contribution calendar`. Source of recurring commit churn — README no longer embeds these. |
| Snake animation | `.github/workflows/snake.yml` | `0 0 * * *` | `Platane/snk/svg-only@v3` → `crazy-max/ghaction-github-pages@v4` | Publishes `github-snake.svg` and `github-snake-dark.svg` to the **`output`** branch (not `main`). README references these via raw.githubusercontent.com on the `output` branch. Palette uses brand rust `d97757`. |

The `output` branch is workflow-managed — do not hand-edit it. Snake assets do not exist on `main`.

## README Asset Wiring

README image `src` URLs hard-code the GitHub username and the source branch/path. When changing assets, update both ends:

- **Snake `<picture>`** references `output` branch paths `github-snake.svg` (light) and `github-snake-dark.svg` (dark). Snake palette + dot colors are configured inside `snake.yml` via the `outputs:` query string — change colors there, not in README.
- **Streak stats** and **activity graph** use third-party Vercel services (`streak-stats.demolab.com`, `github-readme-activity-graph.vercel.app`); brand accent color `d97757` (Anthropic rust) is the unified theme across all live widgets.
- **Capsule banner** (header/footer) uses `capsule-render.vercel.app` — gradient hex codes inline in the URL (`color=0:d97757,50:a64e30,100:0a0a0a`).
- **Typing SVG** uses `readme-typing-svg.demolab.com` — color param `color=D97757`.
- **Profile views** uses `komarev.com/ghpvc` — color `d97757`.

## Brand Palette (keep consistent across all widgets)

| Token | Hex | Usage |
|---|---|---|
| `accent` | `#d97757` | Primary brand accent (rust/Anthropic-warm). Stats titles, icons, streak ring, snake body, banner gradient peak. |
| `accent-dark` | `#a64e30` | Deeper rust for gradient mid-stops. |
| `bg` | `#0a0a0a` | Card backgrounds, label backgrounds, deep canvas. |
| `surface` | `#1a1a1a` | Tech-stack badge backgrounds. |
| `text` | `#e6edf3` / `#ffffff` | Primary text. |
| `muted` | `#8b949e` | Secondary labels, side text. |
| `cream` | `#f5e6d3` | Banner subtitle, light snake dot mid-tones. |

Brand-link badges (Portfolio = Vercel black, LinkedIn = `0A66C2`, Joblit) keep their natural brand colors and are intentional exceptions.

## Manual Regeneration

Trigger any workflow on demand from the Actions tab via "Run workflow" (all have `workflow_dispatch` enabled). No local build is possible — the actions require `GITHUB_TOKEN` and run only on Actions runners.

## Editing Conventions

- README edits: keep the centered HTML structure (`<p align="center">`, `<table>`) — GitHub-flavored Markdown does not support CSS, so layout relies on inline HTML.
- Section headers use `## ◆ <Name>` for visual rhythm — keep the diamond glyph for consistency.
- Commit message style for human commits: `<type>: <description>` (Conventional Commits). Bot commits use fixed messages — do not reformat them.
- Username `ShousenZHANG` appears in: README image URLs, `3d-contrib.yml` `USERNAME` env, `snake.yml` `github_user_name` input. Renaming the GitHub account requires updating all three plus the repo name itself.
