---
name: commit
description: Commit all unstaged changes with atomic, semantically grouped commits.
disable-model-invocation: true
---

Commit all unstaged changes with atomic, semantically grouped commits.

Steps:
1. Review the status and diffs below
2. Group changes into atomic, semantic commits (don't lump unrelated changes)
3. For each group, stage the relevant files and commit

## Status
!`git status --short`

## Changes
!`git diff HEAD`

## Commit message format

Subject: under 50 chars, no trailing period. No code identifiers or paths. The verb should classify the change — e.g. Add (new), Fix (broken), Remove (gone), Refactor (restructure), Improve (enhance).

Body: prefer bullet lists over prose. One bullet per distinct concern. Explain *why*, not *how*. Include concrete details (versions, thresholds) when they matter. Omit body when the subject says it all.

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

- Reject infinity so the type enforces its name
- Add TryFrom<f64> convenience impl
```
