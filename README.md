# Agent

Multi-session, agent-driven development workflow. Development files live in **`context/`**; application code lives in a dedicated **project folder**.

## Layout

| Location | Purpose |
|----------|---------|
| **`context/`** | Dev docs: spec, feature list, session history, agent instructions |
| **`app_spec.md`** | Project specification (overview, scope, tech stack) |
| **`init.md`** | Initializer agent — Session 1 setup |
| **`agent.md`** | Coding agent — Session N feature implementation |
| **Project folder** | Application code, tests, project README (e.g. `app/`) |

## Workflow

1. **Session 1 (Initializer)** — Use **`init.md`**: ensure `app_spec.md` is filled, create `context/`, `context/feature_list.json`, `context/session_history.md`, project folder, root README, then git init and first commit.
2. **Session N (Coding)** — Use **`agent.md`**: read `context/feature_list.json` and `context/session_history.md`, pick the highest-priority feature with `passes: false`, implement it in the project folder, run tests, set `passes: true`, commit, and append to session history.

## Key files

- **`context/feature_list.json`** — Single source of truth for features (only `passes` is updated after creation).
- **`context/session_history.md`** — Log of each session for handoff between agents.
- **`app_spec.md`** — Update with real project details before running the Initializer.

## Getting started

1. Edit **`app_spec.md`** with your project name, purpose, scope, and technical context.
2. Run the **Initializer** (follow `init.md`) to create `context/` and the project scaffold.
3. Run **Coding** sessions (follow `agent.md`) to implement features from the feature list.
