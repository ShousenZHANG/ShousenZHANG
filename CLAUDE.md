# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

GitHub special profile repository for user `ShousenZHANG` (rendered at https://github.com/ShousenZHANG). Repo name must match the username for GitHub to display `README.md` on the profile page. There is no application code, build system, package manager, test suite, or workflow. This repo is a single hand-edited `README.md`.

## Layout

- `README.md` - the profile page itself, rendered by GitHub. Pure Markdown/HTML: a centered hero, a one-line intro, a three-column focus table, a two-card "Selected Work" section, and a closing GitHub `> [!NOTE]` call-to-action. No generated assets.

The README intentionally omits a stack table, engineering-notes list, badge wall, stats cards, contribution snake, 3D skyline, typing banner, and capsule banner. Keep it sparse, high-signal, and within roughly one screen.

## Visual Direction

Editorial profile page, restraint over decoration — matching the prevailing top-tier convention, where respected senior/staff engineers use zero generated widgets and let concrete proof carry the page.

| Surface | Direction |
|---|---|
| Hero | Pure Markdown, centered. Role + domain in bold, a `<sub>` tech line, and a `<sup>` link row. No remote banner image. |
| Intro | One concrete sentence about what is shipped, not adjectives. |
| Focus table | Three columns: current focus, engineering base, operating style. |
| Selected Work | Two cards with concrete, verifiable engineering proof (real metrics, awards). |
| Closing | A single `> [!NOTE]` availability call-to-action. |

Avoid reintroducing generic profile clutter: profile-view counters, trophy widgets, large badge walls, dense stats cards, activity graphs, a contribution snake, or a 3D skyline. At senior level these read as dated template signals.

## Editing Conventions

- README edits: keep GitHub-compatible Markdown and inline HTML only (`<div align="center">`, `<table>`, `<sub>`, `<sup>`). GitHub-flavored Markdown does not support custom CSS.
- Section headers are plain `## <Name>` with no ornament glyphs.
- Project proof must stay honest and verifiable — cite real facts (e.g. Joblit "JD → PDF under 5 seconds", "Runner-up, Coding Fest 2025"); never invent numbers.
- Keep the page to roughly one screen and lead with engineering signal.
- Commit message style: `<type>: <description>` (Conventional Commits).
- Username `ShousenZHANG` appears in README links; renaming the GitHub account requires updating those references plus the repo name itself.

## History

A scheduled workflow (`.github/workflows/activity.yml`) previously generated a 3D contribution skyline and a contribution-snake asset, published to an `output` branch. Both were removed in favor of a zero-generated-visual, top-tier layout. The `output` branch may still exist as an orphan; it is unused and safe to delete.
