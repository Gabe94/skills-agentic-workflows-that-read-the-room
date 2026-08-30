---
name: update-github-info
description: Refresh Mona's GitHub Info content from official GitHub updates.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
strict: true
network:
  allowed:
    - github.blog
    - github.com
tools:
  github:
    mode: gh-proxy
    toolsets: [repos]
  edit: true
safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Read `notes/mona-notes.md` and the current `site/content/github-info.md` with GitHub repository API tools. Do not use terminal, CLI, or sandboxed commands to read repository guidance or reference files.

Use `web-fetch` to read these official public sources:

- https://github.blog/latest/
- https://github.blog/changelog/

Select recent, developer-relevant updates that fit Mona's editorial guidance. Update `site/content/github-info.md` with concise, practical summaries and an explicit source for each GitHub Blog or Changelog item.

Use the configured `create-pull-request` safe output to open a pull request titled for Mona's review. Do not write directly to `main`. If the sources contain no worthwhile changes or the content is already current, call `noop` with a short reason instead.