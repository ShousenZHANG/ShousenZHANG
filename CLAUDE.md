# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

GitHub special profile repository for user `ShousenZHANG` (rendered at https://github.com/ShousenZHANG). Repo name must match the username for GitHub to display `README.md` on the profile page. There is no application code, build system, package manager, test suite, or workflow. This repo is a single hand-edited `README.md`.

## Layout

- `README.md` - the profile page itself, rendered by GitHub. Two centered lines only: bold positioning line, `<sub>` link row (Joblit · Portfolio · LinkedIn · Email). No name heading (sidebar already shows the name, and an `# h1` adds a border-bottom rule that bulks the card), no tables, no cards, no call-to-action, no "currently building" sentence (that fact lives in the joblit pinned-card description).

## Visual Direction

Follows the observed top-tier convention (Sindre Sorhus, Evan You, leerob): README is a few lines of assured positioning; **proof lives in pinned repositories and their descriptions**, not in README prose. The README must never restate what a pinned card already says.

The proof surface is the pinned set (managed in the GitHub UI, no public API): `joblit`, `PTE-Pilot`, `project-contest-platform`, `portfolio`. Repo descriptions carry the concrete facts (metrics, stack) and are edited via `gh repo edit --description`.

Deliberately hidden (do not reintroduce): résumé-style focus tables, per-project bullet lists, awards ("Runner-up, Coding Fest"), availability/job-seeking call-to-actions, and location text duplicated from the sidebar. Also avoid generic clutter: profile-view counters, trophy widgets, badge walls, stats cards, activity graphs, contribution snake, 3D skyline, typing banners.

## Editing Conventions

- README edits: keep GitHub-compatible Markdown and inline HTML only (`<div align="center">`, `<sub>`). GitHub-flavored Markdown does not support custom CSS.
- Any concrete claim must stay honest and verifiable (e.g. Joblit "JD → PDF under 5 seconds"); never invent numbers.
- Keep the README under ~10 rendered lines.
- Commit message style: `<type>: <description>` (Conventional Commits).
- Username `ShousenZHANG` appears in links; renaming the GitHub account requires updating those references plus the repo name itself.

## History

- 2026-07: page compressed from a card-based editorial layout (three-column focus table, two "Selected Work" cards, availability `> [!NOTE]` CTA) to the current ultra-minimal hero, after benchmarking top-tier profiles. Proof moved to pinned repos.
- Earlier: a scheduled workflow (`.github/workflows/activity.yml`) generated a 3D contribution skyline and contribution snake, published to an `output` branch. Removed. The `output` branch may still exist as an orphan; unused and safe to delete.
