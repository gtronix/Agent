# Agent workflow template

Multi-session, agent-driven development: **`context/`** holds planning and handoff; a dedicated **project folder** holds application code (created during init).

## Repository layout

```
Agent/
├── README.md                 # This file
├── app_spec.md               # Product spec — edit before running the Initializer (optional copy in context/)
├── context/
│   ├── init.md               # Initializer agent — session 1
│   ├── agent.md              # Coding agent — sessions 2+
│   ├── feature_list.example.json
│   └── session_history.example.md
└── templates/
    └── cursor-skills/        # Optional Cursor SKILL.md templates (see templates/cursor-skills/README.md)
```

After initialization you will also have:

- **`context/feature_list.json`** — backlog (only `passes` changes after creation)
- **`context/session_history.md`** — append-only session log
- **`<project_folder>/`** — e.g. `app/` with source and tests

## Quick start

1. Fill **`app_spec.md`** with real overview, scope, stack, and constraints.
2. Run an agent with **`context/init.md`** (Initializer): creates `feature_list.json`, `session_history.md`, project folder, git baseline.
3. Run agents with **`context/agent.md`** (Coding): one prioritized feature per session, tests green, update `passes` and session history.

## Where to look

| Need | File |
|------|------|
| First-time setup | `context/init.md` |
| Ongoing implementation | `context/agent.md` |
| Product definition | `app_spec.md` (or `context/app_spec.md`) |
| Backlog state | `context/feature_list.json` |
| What happened last session | `context/session_history.md` |
| Example JSON / history shape | `context/feature_list.example.json`, `context/session_history.example.md` |
| Optional Cursor skills | `templates/cursor-skills/` |

## Copying this template

Copy the repo (or these folders/files) into a new project, rename as needed, keep **`context/init.md`** and **`context/agent.md`** together with **`app_spec.md`**.
