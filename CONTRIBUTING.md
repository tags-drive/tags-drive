# Contributing

This file contains common rules for Tags-Drive repositories.

## GitHub Flow

Tags-Drive uses [GitHub flow](https://help.github.com/articles/github-flow/)

## Commit prefixes

- `[WIP]` - Work in progress.
- `[FIX]` - Bug fixes
- `[FEAT]` - New feature
- `[REF]` - Code refactoring
- `[DOC]` - Updates to documentation

**Examples:**

- There's an issue #15 - "Update API". Branch `api-updating` should contain following commits:

  - `[WIP] update GET /api/test`
  - `[WIP] update GET /api/test/file`
  - `[DOC] update README.md`

  Merge commit should have message `[FEAT] Resolve #15 (Update API)`

- There's an issue #16 - "Fix sort order". It can be resolved in one commit. Then commit message must be `[FIX] fix #16 (Fix sort order)`
