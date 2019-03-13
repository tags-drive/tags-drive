# Contributing

This file contains common rules for Tags-Drive repositories.

## GitHub Flow

Tags-Drive uses [GitHub flow](https://help.github.com/articles/github-flow/)

## Commit prefixes

- `[WIP]` - Work in progress.
- `[UPD]` - Update of existing functionality
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

## Atomicity

Every change must be atomic. If it can be done with a single commit, a commit message must have prefixes `[UPD]`, `[FIX]`, `[FEAT]` and etc.

If there are a lot of work and a special branch is needed, every commit message must have prefix `[WIP]`. Merge commit message can use prefixes `[UPD]`, `[FIX]`, `[FEAT]` and etc.
