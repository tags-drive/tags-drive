# Contributing

This file contains common rules for **Tags Drive** repositories.

##

- [GitHub Flow](#github-flow)
  - [Commit prefixes](#commit-prefixes)
  - [Atomicity](#atomicity)
- [Release formatting](#release-formatting)

## GitHub Flow

**Tags Drive** uses [GitHub flow](https://help.github.com/articles/github-flow/)

### Commit prefix

Every commit must have at least one of the next prefixes

- `[FEAT]` - New feature
- `[UPD]` - Update of existing functionality
- `[FIX]` - Bug fixe
- `[REF]` - Code refactoring
- `[DOC]` - Updates to documentation
- `[WIP]` - Work in progress.

**Examples:**

- There's an issue **#15** - "Update API". Branch `update-api` can contain following commits:

  - `[WIP] update GET /api/test`
  - `[WIP] update GET /api/test/file`
  - `[WIP] [DOC] update README.md`

  Merge commit must have message `[UPD] resolve #15 (Update API)`

- There's an issue **#16** - "Fix sort order". It can be resolved in a single commit. The commit message must be `[FIX] fix #16 (Fix sort order)`

### Atomicity

Every change must be atomic. If it can be done with a single commit, a commit message must have prefixes `[UPD]`, `[FIX]`, `[FEAT]` and etc.

If there are a lot of work and a special branch is needed, every commit message must have prefix `[WIP]`. Merge commit message can use prefixes `[UPD]`, `[FIX]`, `[FEAT]` and etc.

## Release formatting

Release notes should contain these Emoji for better readability

| Emoji         | Code            | Definition      |
| ------------- | --------------- | --------------- |
| :sparkles:    | `:sparkles:`    | major feature   |
| :hammer:      | `:hammer:`      | refactoring     |
| :bug:         | `:bug:`         | fix bug         |
| :exclamation: | `:exclamation:` | need attention  |
| :boom:        | `:boom:`        | breaking change |

**Release example:**

> **Features**
>
> - :sparkles: major feature – issue #99999
> - minor feature – PR #99998
>
> **Updates**
>
> - :hammer: refactor `foo` function – issue #99997
> - update function comments – commit `1a8d66e`
>
> **Fixes**
>
> - :bug: fix some small bug – issue #99996
> - :exclamation: fix security bug – PR #99995
