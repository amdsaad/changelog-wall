# 0001: Static Nuxt 4 site from reviewed files in git

- Status: accepted
- Date: 2026-11-27

## Context

The wall is a public, read-only page of what the owner shipped each week. Two rules shape the stack:

- Nothing reaches the public page without the owner's review, so every entry needs a draft state and an explicit publish step.
- Only repos the owner opts in may appear (an allowlist), because some repos are private.

The choice was a static site built from data files versus a Nuxt 4 + Supabase app with draft/published rows and an admin page. The repo already held a bare Nuxt 4 scaffold with no Supabase, and `nuxt generate` builds a fully static site, so the real choice was where entries and their review state live: git or a database.

## Decision

- **Review gate is git.** Entries are files under `content/`. An entry with `status: draft` is a draft. The owner reviews entries as a PR diff, and merging publishes them. The production build leaves drafts out.
- **The allowlist is `repos.yml` in this repo.** It denies by default: an unlisted repo never appears. It changes only through a reviewed PR, like entries do.
- **The framework is Nuxt 4, prerendered** with `nuxt generate`. There is no server runtime and no Supabase.
- **Entries are read with `@nuxt/content` v3.** A collection schema makes the build fail on a project that isn't in `repos.yml`, a missing `status`, or a missing `week`.
- **Nothing runs at request time.** No comments, reactions, signups or counters. The RSS/Atom feed and the filter by project are both built at generate time.
- **Hosting is Cloudflare Workers static assets,** the same pattern as markly/landing.

## Consequences

- There is no auth, admin UI or row-level security to build or secure. The leak surface is the PR diff, and the owner already reviews there.
- Every published line has git history, and taking one down is a revert plus a redeploy.
- The VPS isn't involved. Its pipeline (`deploy-nuxt.yml`) ships a Nitro server, which this site doesn't have.
- A schema mistake fails the build instead of going live.
- Request-time features (comments, live search, analytics beyond Cloudflare's own) would need a new ADR.

## Left open

- Entry source (git history, merged PRs, hand-written notes, or a generated draft) and so whether drafts may sit on `main` with `status: draft` or only on branches.
- What counts as shipped.
- How much detail private repos show.
- The domain: a subdomain, or a path behind amdsaad.com.
