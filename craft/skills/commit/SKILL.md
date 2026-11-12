---
name: commit
description: Commit all uncommitted changes with atomic, semantically grouped commits.
---

1. Review the status and diffs below
2. For untracked files (`??`), read them to understand what they contain
3. Group changes into atomic, semantic commits (don't lump unrelated changes)
4. For each group, stage the relevant files and commit

## Status
!`git status --short`

## Changes
!`git diff HEAD`

## Commit message format

Subject: under 50 chars, no trailing period. No code identifiers or paths. The verb should classify the change — e.g. Add (new), Fix (broken), Remove (gone), Refactor (restructure), Improve (enhance).

Body: omit when the subject and code say it all. Bullet list for multiple concerns, plain sentence for one. Explain *why*, not *how*. Include concrete details (versions, thresholds) when they matter.

Footer (optional): `Closes: #123`, `Fixes: #456`.

Examples:
```
Add sign up feature

- Allow account creation via email or OAuth
- Send welcome email on first login

Closes: #123
```

```
Improve bounds validation and conversions

Reject infinity so the type enforces its name
```

```
Fix typo in error message
```
