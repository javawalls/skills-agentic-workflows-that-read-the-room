---
name: update-github-info
description: Refresh Mona's GitHub Info page with practical, source-backed updates.
intent: Keep Mona's GitHub Info page current with concise, useful guidance backed by official GitHub sources.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
strict: true
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
tools:
  bash: [cat]
  edit: true
  web-fetch: {}
safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
    base-branch: main
    draft: false
---

# Update GitHub Info

Read `notes/mona-notes.md` and `site/content/github-info.md`. Fetch both
https://github.blog/latest/ and https://github.blog/changelog/ with the web-fetch
tool. Also web fetch https://awesome-copilot.github.com/workflows/. Follow links
on those official sites when needed to verify details.

Select up to three recent, genuinely useful updates that help developers learn
GitHub faster or fit the page's existing themes. Keep the summaries short and
practical, preserve the editorial angle, and link each update to its official
source. Do not copy article text or add unsupported claims. Refresh a concise
recent-updates section in `site/content/github-info.md`, replacing stale entries
as needed; do not change any other file.

If either required source cannot be fetched, the evidence is insufficient, or
there is no meaningful change to make, call `noop` with a brief reason. Otherwise,
use the configured `create-pull-request` safe output to open one non-draft PR
against `main` for Mona to review. Summarize the changes and include the source
links in the PR description. Never write directly to `main` or use another
GitHub write mechanism.

Open a pull request for Mona to review.
