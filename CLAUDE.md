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

- **Snake `<picture>`** references `output` branch paths `github-snake.svg` (light) and `github-snake-dark.svg` (dark). Snake palette + dot colors are configured inside `snake.yml` via the `outputs:` query string — change colors there, not in README. Dot colors mirror GitHub's actual contribution graph palette (light: `#ebedf0,#9be9a8,#40c463,#30a14e,#216e39`; dark: `#0d1117,#0e4429,#006d32,#26a641,#39d353`).
- **Streak stats** and **activity graph** use third-party Vercel services (`streak-stats.demolab.com`, `github-readme-activity-graph.vercel.app`); brand accent color `#58a6ff` (GitHub link blue) is the unified widget theme.
- **Capsule banner** (header/footer) uses `capsule-render.vercel.app` — subtle blue glow gradient `color=0:0d1117,50:1f6feb,100:0d1117` for premium-minimal feel.
- **Typing SVG** uses `readme-typing-svg.demolab.com` — color param `color=58A6FF`.
- **Profile views** uses `komarev.com/ghpvc` — color `58a6ff`.

## Brand Palette (keep consistent across all widgets)

GitHub-native premium-minimalist palette. Mirrors GitHub's own dark-mode UI tokens for cohesion when the README renders inside github.com.

| Token | Hex | Usage |
|---|---|---|
| `accent` | `#58a6ff` | Primary widget accent (GitHub link blue). Streak ring, activity graph line, typing-SVG color, profile-views badge, focus badge, banner gradient peak. |
| `accent-emphasis` | `#1f6feb` | GitHub button blue. Used as gradient mid-stop in capsule banner. |
| `success` | `#3fb950` | GitHub success green. Used by `STATUS-OPEN TO WORK` badge. |
| `bg` | `#0d1117` | GitHub canvas dark. Card backgrounds, label backgrounds, banner edges, streak background. |
| `surface` | `#161b22` | GitHub subtle canvas. Tech-stack badge backgrounds, label backgrounds for CTA buttons. |
| `border` | `#30363d` | GitHub border. Reserved for any future divider. |
| `text` | `#e6edf3` / `#ffffff` | Primary text. |
| `muted` | `#7d8590` / `#c9d1d9` | Secondary labels, streak side labels, dates. |

Brand-link badges (Portfolio = Vercel black, LinkedIn `#0A66C2`, Gmail `#D14836`, Joblit `#00BFA6`, Claude `#D97757`) keep their natural brand colors and are intentional exceptions to the monochrome+blue palette.

## Manual Regeneration

Trigger any workflow on demand from the Actions tab via "Run workflow" (all have `workflow_dispatch` enabled). No local build is possible — the actions require `GITHUB_TOKEN` and run only on Actions runners.

## Editing Conventions

- README edits: keep the centered HTML structure (`<p align="center">`, `<table>`) — GitHub-flavored Markdown does not support CSS, so layout relies on inline HTML.
- Section headers use `## ◆ <Name>` for visual rhythm — keep the diamond glyph for consistency.
- Commit message style for human commits: `<type>: <description>` (Conventional Commits). Bot commits use fixed messages — do not reformat them.
- Username `ShousenZHANG` appears in: README image URLs, `3d-contrib.yml` `USERNAME` env, `snake.yml` `github_user_name` input. Renaming the GitHub account requires updating all three plus the repo name itself.
