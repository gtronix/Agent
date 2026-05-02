---
name: self-optimization
description: >-
  After an agent task, reflect on friction (missed instructions, wrong files,
  repeated errors) and suggest concrete improvements to repo docs, context/, or
  skills. Use when the user wants to tune the template or workflow.
---

# Self-optimization pass

## When to use

- End of a difficult session.
- User asks to improve agent instructions or project docs based on what happened.

## Instructions

1. List **what went wrong** or **what was ambiguous** (paths, missing commands, spec gaps).
2. Propose **specific edits**: which file (`context/agent.md`, `app_spec.md`, README, a Cursor skill), what to add or clarify.
3. Avoid vague advice; each suggestion should be a one-line actionable change.
4. Do not delete working instructions; **extend** or **narrow** them.
5. If the user approves, apply edits in small, reviewable chunks.

## Out of scope

- Changing application feature behavior unless the user asks for product work.
- Storing secrets or credentials in docs.
