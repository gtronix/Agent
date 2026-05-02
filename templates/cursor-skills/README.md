# Optional Cursor Agent Skills (templates)

These folders are **templates** for [Cursor Agent Skills](https://cursor.com/docs): copy a folder into `~/.cursor/skills/<name>/` or `.cursor/skills/<name>/` in a project, then refine `SKILL.md`.

They are **not** required for the multi-session workflow in `context/init.md` and `context/agent.md`.

| Folder | Intent |
|--------|--------|
| `log/` | Structured progress logging (complements `context/session_history.md` if you want a separate log file). |
| `commit/` | Conventions for staging and committing (restrict push/pull if you automate locally). |
| `self-optimization/` | Post-run review: improve instructions, context, or skills from what went wrong or slow. |

Official skill layout uses `SKILL.md` with YAML frontmatter (`name`, `description`). Adjust bodies to match your team.
