# Changelog Wall

A public page listing what the owner shipped each week across their projects (the repos listed in `E:\home\CLAUDE.md`). One section per ISO week, newest first, grouped by project.

## Status

New repo, nothing built yet. Stack to be decided.

## Open questions (settle before building)

- **Source:** where entries come from: git history across the repos, merged PRs, hand-written notes, or a draft the owner edits before it goes live.
- **What counts as shipped:** merged to main, deployed, or released.
- **Private repos:** some repos are private (vps, learning, factory-lab, ...): which appear, and how much of their detail is shown.
- **Stack and hosting:** static site generated from data files vs. an app; where it's served (the VPS, Cloudflare, or a section of amdsaad.com).

## Rules

- Nothing reaches the public page without the owner reviewing it: no secrets, client names or private repo details.
- Save agreed designs and plans as Markdown in `docs/`.
- Commit on a feature branch; push, merge or deploy only with the owner's OK.
- Browser checks: serve over HTTP, screenshots under `.playwright-mcp/`.

## Agent skills

### Issue tracker

GitHub Issues on amdsaad/changelog-wall, via the gh CLI. See `docs/agents/issue-tracker.md`.

### Domain docs

Single-context: one `GLOSSARY.md` and `docs/adr/` at the repo root, created lazily. See `docs/agents/domain.md`.
