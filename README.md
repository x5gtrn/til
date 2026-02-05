# TIL (Today I Learned)

This repository is my **public** collection of small, reusable learnings.

- One note = one idea
- Keep it short, practical, and searchable
- Avoid private context (clients, money, health, exact locations, etc.)

This TIL repo is designed to work nicely with my **LIFE** repository (private “Life OS”):

- LIFE imports this repo daily via **git subtree**
- LIFE automatically generates:
  - a TIL index
  - a daily digest (“what changed today”)
  - an ISO-week digest (“what changed this week”)

---

## Why TIL?

TIL helps you:

- build a daily output habit with low friction
- improve recall by writing tiny summaries
- create a personal knowledge base you can search later
- share useful insights with others (and future you)

---

## How to write a good TIL

### Recommended structure (template)

```md
# <Title>

## What
## Why it matters
## How
## Example
## References
```

### Recommended structure ([Front Matter](https://jekyllrb.com/docs/front-matter/))

```yaml
---
title: "How can I adopt the TIL and LIFE repositories into my life?"
layout: post
date: 2026-02-05T12:13
category: github
tags:
    - lerning
    - self-managenent
    - github
---
```

### Rules of thumb

- **Prefer one file per topic**, rather than a giant single file
- Use **descriptive filenames**:
  - `s3-presigned-url-expiration.md`
  - `spring-graphql-multipart-upload.md`
- Add links to official docs / sources when helpful
- Keep it **generalized** (no confidential details)

---

## Repository structure (suggested)

Start small; expand only when needed.

```text
til/
  README.md
  aws/
  graphql/
  java/
  linux/
  devops/
  ruby/
  music-production/
  dj/
```

---

## Public-safe content policy (important)

Do NOT include:

- client/company names or internal project names
- exact money amounts, invoices, contracts
- health / medical details
- precise locations or personal schedules
- private messages or identifying information

If you’re not sure, write it first in your private LIFE repo, then rewrite as a generalized learning here.

---

## Workflow with LIFE (optional)

If you use [the LIFE template repo](https://github.com/x5gtrn/LIFE-Template):

1. Create this TIL repo (public) and push commits normally
2. In your LIFE repo, set:
   - `TIL_REMOTE_URL="https://github.com/YOUR_GITHUB_NAME/til.git"`
3. LIFE will sync daily via GitHub Actions and generate digests automatically

---

## Commit frequency & message conventions

This repo is optimized for **consistency** and **searchability**, not complex release management.

### How often should I commit?

Recommended patterns:

- **Ideal:** 1 commit per day (≈ 1 TIL)
- **Practical:** 3–5 commits per week is still great
- **Busy days:** batching is allowed (write multiple small notes and commit once)

Small and frequent beats perfect and rare.

> If you use the LIFE template repo, it syncs this TIL repo daily (04:00 JST) and will reflect changes automatically in digests.

### Should I push directly to `main`?

For a personal TIL repository: **Yes, pushing directly to `main` is recommended.**

Why:

- TIL changes are usually tiny
- “Write → commit → push” keeps the habit frictionless
- The LIFE repo sync workflow typically tracks `main`

When to consider PRs/branches:

- team/shared TIL repo
- you want review before publishing
- large refactors (mass rename, moving many files)

In those cases, use a short-lived branch like:

- `chore/restructure-til` → PR → merge to `main`

### Commit message style (choose one and stay consistent)

#### Option A (minimal)

```
til: <topic>
```

Examples:

- `til: s3 presigned url expiration`
- `til: spring graphql multipart upload`

#### Option B (recommended: include area)

```
til(<area>): <topic>
```

Examples:

- `til(aws): iam policy for s3 access`
- `til(graphql): file upload patterns`
- `til(linux): ripgrep search tips`

#### Option C (multiple files / broader edits)

```
til: update <area> notes
```

Examples:

- `til: update aws notes`
- `til: update linux tips`

**Recommendation:** Use **Option B** (`til(<area>): ...`) for the best long-term readability.

### What should be in one commit?

- Prefer **one note = one commit** when possible
- It’s OK to include multiple changes if they are tightly related (same topic/area)

### Quick sustainability rules

- If writing feels hard, allow “tiny commits”:
  - add a reference link and fill details later
  - append 1–3 lines to an existing note
- If you’re unsure whether something is public-safe, write it in LIFE (private) first and rewrite a generalized version here.

---

## License

Choose any license you like (MIT/CC0 are common for personal notes), or keep it without a license if you prefer.

