---
name: local-commit
description: >-
  Stage and commit with clear messages following project conventions. Use when
  the user wants commits without remote operations.
---

# Local commit workflow

## Scope

- Allowed: `git add`, `git commit`, `git status`, `git diff`.
- Avoid unless asked: `git push`, `git pull`, force-push, branch deletion.

## Instructions

1. Run `git status` and summarize staged vs unstaged changes.
2. Propose a commit message (conventional commits if the repo uses them: `feat:`, `fix:`, `chore:`).
3. Stage only files that belong to the logical change; avoid unrelated edits.
4. Commit with the agreed message.
5. Confirm with `git log -1 --oneline`.
