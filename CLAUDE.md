# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

GitHub special profile repository for user `ShousenZHANG` (rendered at https://github.com/ShousenZHANG). Repo name must match the username for GitHub to display `README.md` on the profile page. There is no application code, build system, package manager, or test suite. This repo is content plus one scheduled SVG generation workflow.

## Layout

- `README.md` - the profile page itself. Markdown rendered by GitHub. Uses a pure Markdown/HTML hero, selected work, stack matrix, engineering notes, and workflow-generated snake animation.
- `.github/workflows/snake.yml` - scheduled job that regenerates the contribution snake SVGs.

The old `profile-3d-contrib/` generated assets and `.github/workflows/3d-contrib.yml` workflow were removed because README does not reference them and the workflow caused daily commit churn on `main`.

## Workflows and Their Side Effects

All workflows write back to the repo on `workflow_dispatch` or schedule. Understand the destination before editing.

| Workflow | File | Schedule (UTC) | Action | Output destination |
|---|---|---|---|---|
| Snake animation | `.github/workflows/snake.yml` | `0 0 * * *` | `Platane/snk/svg-only@v3` -> `crazy-max/ghaction-github-pages@v4` | Publishes `github-snake.svg` and `github-snake-dark.svg` to the **`output`** branch, not `main`. README references these via raw.githubusercontent.com on the `output` branch. |

The `output` branch is workflow-managed. Do not hand-edit it. Snake assets do not exist on `main`.

## README Asset Wiring

README image `src` URLs hard-code the GitHub username and the source branch/path. When changing assets, update both ends:

- **Snake `<picture>`** references `output` branch paths `github-snake.svg` (light) and `github-snake-dark.svg` (dark). Snake palette and dot colors are configured inside `snake.yml` through the `outputs:` query string. Change colors there, not in README. Dot colors are achromatic GitHub greys, not the green contribution palette: light `#ebedf0,#d0d7de,#8c959f,#57606a,#24292f`; dark `#0d1117,#21262d,#30363d,#7d8590,#e6edf3`. Snake body is solid `#24292f` in light mode and `#ffffff` in dark mode.
There are intentionally no third-party stats cards in README. The previous `streak-stats.demolab.com` card was removed because the public service can timeout or return 503 under load.

## Brand Palette

Editorial monochrome palette. Keep the profile quiet, high-signal, and native to GitHub's own visual environment.

| Token | Hex | Usage |
|---|---|---|
| `text-fg` | `#e6edf3` dark / `#24292f` light | Primary widget foreground, streak stroke/ring/fire, snake body. |
| `text-muted` | `#7d8590` | Secondary labels and dates. |
| `bg` | `#0d1117` | Streak canvas and dark widget backgrounds. |
| `surface` | `#161b22` | Reserved for future badges or subtle generated surfaces. |
| `border` | `#30363d` | Reserved for future dividers. |

Avoid chromatic accent colors in widgets. The current README intentionally does not use capsule-render, typing SVG, profile-view counters, trophy widgets, badge walls, third-party stats cards, or activity graphs.

## Manual Regeneration

Trigger the snake workflow on demand from the Actions tab via "Run workflow" (`workflow_dispatch` is enabled). No local build is possible because the action requires `GITHUB_TOKEN` and runs on Actions runners.

## Editing Conventions

- README edits: keep GitHub-compatible Markdown and inline HTML only (`<div align="center">`, `<table>`, `<p align="center">`, `<picture>`). GitHub-flavored Markdown does not support custom CSS.
- Section headers are plain `## <Name>` with no ornament glyphs.
- Hero is pure Markdown (`# Eddy Zhang` plus a `<sub>` positioning line and `<sup>` link row). Do not reintroduce capsule-render, typing-SVG banners, or large remote hero images.
- Keep project evidence before the stack section. The profile should read as senior engineering signal first and tool inventory second.
- Commit message style for human commits: `<type>: <description>` (Conventional Commits). Bot commits use fixed messages.
- Username `ShousenZHANG` appears in README image URLs and `snake.yml` `github_user_name` input. Renaming the GitHub account requires updating those references plus the repo name itself.
