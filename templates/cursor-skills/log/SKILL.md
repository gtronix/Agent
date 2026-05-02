---
name: session-log
description: >-
  Append structured progress notes to logs.md (or a path the user specifies)
  during long agent runs. Use when the user wants an audit trail separate from
  git commits or context/session_history.md.
---

# Session log

## When to use

- Long sessions where incremental visibility helps.
- User explicitly asks to log progress to a file.

## Instructions

1. Confirm log path (default: `logs.md` at repo root unless the user names another file).
2. Append a short timestamped entry: date/time, action taken, files touched, blockers.
3. Do not replace or wipe existing log content; append only.
4. Keep entries concise (bullet list is fine).

## Output format (example)

```markdown
## YYYY-MM-DD HH:MM

- Done: …
- Next: …
```
