# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

GitHub special profile repository for user `ShousenZHANG` (rendered at https://github.com/ShousenZHANG). Repo name must match the username for GitHub to display `README.md` on the profile page. There is no application code, build system, package manager, or test suite. This repo is content plus one scheduled SVG generation workflow.

## Layout

- `README.md` - the profile page itself. Markdown rendered by GitHub. Uses a pure Markdown/HTML hero, selected work, and a workflow-generated 3D activity skyline.
- `.github/workflows/activity.yml` - scheduled job that regenerates the 3D contribution skyline.

The README intentionally does not include a stack table, engineering-notes list, badge wall, stats cards, typing banner, capsule banner, or snake animation. Keep it sparse and high-signal.

## Workflows and Their Side Effects

All workflows write back to the repo on `workflow_dispatch`, schedule, or a profile README/workflow push. Understand the destination before editing.

| Workflow | File | Schedule (UTC) | Action | Output destination |
|---|---|---|---|---|
| Activity skyline | `.github/workflows/activity.yml` | `0 0 * * *` | `yoshi389111/github-profile-3d-contrib@v0.9.2` -> `crazy-max/ghaction-github-pages@v4` | Generates `profile-night-rainbow.svg`, copies it to `dist/github-activity-3d.svg`, and publishes that file to the **`output`** branch. |

The `output` branch is workflow-managed. Do not hand-edit it. Generated activity assets do not exist on `main`.

## README Asset Wiring

README image `src` URLs hard-code the GitHub username and the source branch/path. When changing assets, update both ends:

- **Activity skyline** references `https://raw.githubusercontent.com/ShousenZHANG/ShousenZHANG/output/github-activity-3d.svg`.
- The source asset comes from `github-profile-3d-contrib` output `profile-3d-contrib/profile-night-rainbow.svg`.
- The workflow copies only the selected SVG into `dist/` before publishing to `output`, which prevents generated SVG churn on `main`.

## Visual Direction

Editorial profile page with one high-impact visual.

| Surface | Direction |
|---|---|
| Hero | Pure Markdown, centered, no remote banner image. |
| Project section | Two selected work cards with concrete engineering proof. |
| Activity section | Single 3D neon/cyberpunk skyline. This is the one visual exception to the otherwise quiet page. |

Avoid reintroducing generic GitHub profile clutter: profile-view counters, trophy widgets, large badge walls, dense stats cards, activity graphs, or multiple competing animations.

## Manual Regeneration

Trigger the activity workflow on demand from the Actions tab via "Run workflow" (`workflow_dispatch` is enabled). The workflow also runs when README or the workflow file changes on `main`, so pushing a profile redesign should refresh `output/github-activity-3d.svg`.

## Editing Conventions

- README edits: keep GitHub-compatible Markdown and inline HTML only (`<div align="center">`, `<table>`, `<p align="center">`, `<img>`). GitHub-flavored Markdown does not support custom CSS.
- Section headers are plain `## <Name>` with no ornament glyphs.
- Hero is pure Markdown (`# Eddy Zhang` plus a `<sub>` positioning line and `<sup>` link row). Do not reintroduce capsule-render, typing-SVG banners, or large remote hero images.
- Keep project evidence before the activity visual. The profile should read as senior engineering signal first and visual flourish second.
- Commit message style for human commits: `<type>: <description>` (Conventional Commits). Bot commits use fixed messages.
- Username `ShousenZHANG` appears in README image URLs and `activity.yml` `USERNAME` env. Renaming the GitHub account requires updating those references plus the repo name itself.
