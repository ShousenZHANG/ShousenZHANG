# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

GitHub special profile repository for user `ShousenZHANG` (rendered at https://github.com/ShousenZHANG). Repo name must match the username for GitHub to display `README.md` on the profile page. There is no application code, build system, package manager, or test suite. This repo is content plus one scheduled snake-GIF generation workflow.

## Layout

- `README.md` - the profile page itself. Markdown rendered by GitHub. Uses a pure Markdown/HTML hero, selected work, and a workflow-generated classic green contribution snake (GIF, dark/light).
- `.github/workflows/activity.yml` - scheduled job that regenerates the contribution snake GIFs.

The README intentionally does not include a stack table, engineering-notes list, badge wall, stats cards, typing banner, or capsule banner. Keep it sparse and high-signal.

## Workflows and Their Side Effects

All workflows write back to the repo on `workflow_dispatch`, schedule, or a profile README/workflow push. Understand the destination before editing.

| Workflow | File | Schedule (UTC) | Action | Output destination |
|---|---|---|---|---|
| Contribution snake | `.github/workflows/activity.yml` | `0 0 * * *` | `Platane/snk@v3` -> `crazy-max/ghaction-github-pages@v4` | Generates `github-snake.gif` and `github-snake-dark.gif`, then publishes them to the **`output`** branch. |

The `output` branch is workflow-managed. Do not hand-edit it. Generated activity assets do not exist on `main`.

## README Asset Wiring

README image `src` URLs hard-code the GitHub username and the source branch/path. When changing assets, update both ends:

- **Contribution snake** references `output` branch paths `github-snake.gif` for light mode and `github-snake-dark.gif` for dark mode, wired via `<picture>` + `prefers-color-scheme`.
- Snake color query values in `activity.yml` must URL-encode `#` as `%23`; otherwise `Platane/snk` may not apply the intended palette.
- GIF has no `prefers-color-scheme` support, so each theme gets its own file with an explicit `color_background` (`%23ffffff` light, `%230d1117` dark); the two GIFs are swapped by `<picture>`.
- The workflow publishes only the snake GIFs from `dist/` to `output`, which prevents generated asset churn on `main`.

## Visual Direction

Editorial profile page with one high-impact visual.

| Surface | Direction |
|---|---|
| Hero | Pure Markdown, centered, no remote banner image. |
| Project section | Two selected work cards with concrete engineering proof. |
| Activity section | A single classic green contribution snake (GIF). The one visual exception to the otherwise quiet page. |

Avoid reintroducing generic GitHub profile clutter: profile-view counters, trophy widgets, large badge walls, dense stats cards, or activity graphs.

## Manual Regeneration

Trigger the activity workflow on demand from the Actions tab via "Run workflow" (`workflow_dispatch` is enabled). The workflow also runs when README or the workflow file changes on `main`, so pushing a profile redesign should refresh the snake GIFs on `output`.

## Editing Conventions

- README edits: keep GitHub-compatible Markdown and inline HTML only (`<div align="center">`, `<table>`, `<p align="center">`, `<picture>`, `<img>`). GitHub-flavored Markdown does not support custom CSS.
- Section headers are plain `## <Name>` with no ornament glyphs.
- Hero is pure Markdown (`# Eddy Zhang` plus a `<sub>` positioning line and `<sup>` link row). Do not reintroduce capsule-render, typing-SVG banners, or large remote hero images.
- Keep project evidence before the activity visual. The profile should read as senior engineering signal first and visual flourish second.
- Commit message style for human commits: `<type>: <description>` (Conventional Commits). Bot commits use fixed messages.
- Username `ShousenZHANG` appears in README image URLs and `activity.yml` `USERNAME` env. Renaming the GitHub account requires updating those references plus the repo name itself.
