# INITIALIZER AGENT — Session 1

You are the **first agent** in a multi-session development process. Your job is to set up the foundation for all future coding agents, regardless of project type (web app, API, CLI, mobile, etc.).

**Layout:** Development files (feature list, session history, agent instructions) live in **`context/`**. The actual application code lives in a **project folder** (e.g. `app/` or the project name). Keep them separate.

---

## 1. Check for `app_spec.md` — create and request update if missing

- **Check** for a project specification file named **`app_spec.md`** in the workspace (repository root or inside `context/` if it already exists).
- **If `app_spec.md` is not found:**
  1. Ensure **`context/`** exists (create it if needed: `mkdir context` or `New-Item -ItemType Directory -Path context` on PowerShell).
  2. Create **`context/app_spec.md`** (or `app_spec.md` at repo root) with the template below.
  3. **Tell the user:** the file was created and must be updated with project details (goals, scope, tech stack, main features, constraints). Do **not** proceed with building the feature list or project scaffold until the spec has been filled in.
  4. **Stop** the initialization here; a later session (or the user) will complete `app_spec.md` and then the Initializer can continue from step 2.

**Template for a new `app_spec.md`:**

```markdown
# Project specification

<!-- Update this file with project details before continuing initialization. -->

## Overview
- **Project name:**
- **Purpose / goal:**
- **Target users or context:**

## Scope
- Main features or capabilities:
- Out-of-scope (optional):

## Technical context
- Stack / language / framework (if known):
- Constraints or requirements (e.g. deployment, compliance):

## Notes
- Any other details that will guide the feature list and implementation.
```

- **If `app_spec.md` exists:** Continue to step 2.

---

## 2. Ensure `context/` exists and holds development files

- **Check** if a `context` folder exists at the repository root.
- **If it does not exist,** create it: `mkdir context` (or `New-Item -ItemType Directory -Path context` on PowerShell).
- All development-related files live under **`context/`**, separate from the application code:
  - **`context/app_spec.md`** — project specification (step 1)
  - **`context/feature_list.json`** — created in step 4
  - **`context/session_history.md`** — created in step 5
  - **`context/init.md`** and **`context/agent.md`** — agent instructions (if they exist at repo root, move them into `context/` so everything stays in one place).

---

## 3. Read the project specification

Read **`app_spec.md`** fully (from repo root or `context/`). It defines what needs to be built. Do not continue until it contains real project details (not just the template placeholders).

---

## 4. Create `context/feature_list.json` (single source of truth)

From the spec, create **`context/feature_list.json`**. This file is the **single source of truth** for development and must not be edited (except the `passes` field) in later sessions.

### Schema (generic)

```json
[
  {
    "id": 1,
    "category": "functional",
    "priority": "critical",
    "description": "Short, testable description of the feature",
    "steps": [
      "Step 1 to verify the feature",
      "Step 2 to verify the feature"
    ],
    "passes": false,
    "test_file": "path/to/test_file.ext"
  }
]
```

### Fields

| Field         | Purpose |
|--------------|---------|
| `id`         | Unique integer, stable across sessions |
| `category`   | e.g. `functional`, `style`, `security`, `performance`, `api`, `data`, `config` — adapt to project |
| `priority`   | `critical` \| `high` \| `medium` \| `low` — **used to order work** |
| `description`| One clear, testable sentence |
| `steps`      | List of verification steps (2–15 steps; mix short and long) |
| `passes`     | Always `false` at creation; only this field may be changed later |
| `test_file`  | Path to test file **relative to repo root** (e.g. `app/tests/unit/foo.test.js`) — tests live in the project folder |

### Rules for `feature_list.json`

- **Cover the spec:** Every requirement becomes at least one feature. Prefer more, smaller features over fewer, vague ones.
- **Prioritize:** Order by `priority` (critical → high → medium → low). Put foundational features first (auth, core models, config, etc.).
- **Categories:** Use categories that match the project (e.g. add `api`, `ui`, `cli` if relevant).
- **Mix step counts:** Some features with 2–5 steps, some with 10+.
- **All start as failing:** Every feature has `"passes": false` initially.
- **Never remove or edit (except `passes`):** In future sessions, only `passes` may be set to `true`. Do not remove features, change descriptions, or modify steps.

---

## 5. Create session history in `context/`

Create **`context/session_history.md`** to log each development session. Keep it in `context/` with the other development files.

### Initial content

```markdown
# Session history

Each session appends a new entry. Used by later agents to understand what was done and what to do next.

---

## Session 0 — Project init

- **Date:** [today]
- **Agent:** Initializer
- **Summary:** Created feature_list.json, session_history.md, project scaffold, initialized git.
- **Commit:** (will be filled after first commit)
- **Next:** Session 1 agent continues from feature list and this log.
```

Later agents will **append** one block per session (see `context/agent.md`).

---

## 6. Project folder (application code, separate from context)

Create a **dedicated project folder** for the application. Name it from the spec (e.g. `app`, `api`, or the product name). All application code, tests, and project-specific config live here — **not** in the repo root and **not** in `context/`.

**Target layout:**

```
<repo_root>/
├── context/                    # Development only (do not put app code here)
│   ├── init.md                 # This file
│   ├── agent.md                # Coding agent instructions
│   ├── feature_list.json
│   └── session_history.md
├── <project_folder>/           # e.g. app/ or my-app/
│   ├── README.md               # How to run and test this project
│   ├── .env.example            # (optional)
│   ├── <source>/                # e.g. src/, lib/
│   └── <tests>/                 # e.g. tests/, spec/, __tests__/
├── .gitignore                  # Repo-wide
└── README.md                   # Repo overview + pointer to project folder
```

### Minimum in project folder

- **README.md** — project name, how to run, how to test, link to spec
- Source and test directories (or single entry point) as required by the stack

### Optional (depending on spec)

- Config files (e.g. `package.json`, `pyproject.toml`, `go.mod`) inside the project folder
- Environment example (e.g. `.env.example`) in the project folder

Do **not** invent a full framework layout; only add what the spec implies or what is needed to run and test. Keep **context/** for development docs and lists only.

---

## 7. Initialize Git and first version

1. **Initialize repository** (if not already):
   ```bash
   git init
   ```

2. **First commit** with everything created so far:
   - `context/` (app_spec.md, feature_list.json, session_history.md, init.md, agent.md)
   - Project folder and its contents
   - Root `.gitignore` and `README.md`

3. **Commit message** (adapt to what you actually created):
   ```text
   chore: initial setup — context/, project folder, feature list, session history

   - context/ with app_spec.md, feature_list.json, session_history.md, agent docs
   - project folder scaffold
   - README and .gitignore
   ```

4. **Optional:** Create a tag for this state, e.g. `v0.1.0-init` or `session-0`.

---

## 8. Testing strategy (generic)

- **Unit tests:** Fast, isolated; path pattern like `tests/unit/` or `**/*.test.*`.
- **Integration tests:** Services/DB/API; path like `tests/integration/`.
- **E2E tests:** Full flows; path like `tests/e2e/` (or stack equivalent).

In `context/feature_list.json`, set `test_file` to the path **relative to repo root** (e.g. `app/tests/unit/foo.test.js`). Document in the **project folder’s README** how to run tests (e.g. `npm test`, `pytest`, `go test`).

---

## 9. Prioritizing features

- **critical:** Must work for the product to be usable (e.g. core auth, core data flow).
- **high:** Important for MVP or main use cases.
- **medium:** Important but not blocking.
- **low:** Nice-to-have or polish.

Initializer must order `context/feature_list.json` so that critical and high features are clearly at the top. Later agents will pick the **highest-priority feature with `passes: false`** first.

---

## 10. End of Session 1

Before finishing:

1. **Commit** any remaining changes (no uncommitted work).
2. **Update `context/session_history.md`** with the real commit hash and date.
3. **Verify** the repo is clean: `git status`, all files committed.
4. Leave **clear “next steps”** in the last line of `context/session_history.md` for the next agent.

The next agent will start with a fresh context and use **`context/feature_list.json`** + **`context/session_history.md`** + git history to continue. They will implement features in the **project folder**, not in `context/`.

---

## 11. Optional: start first feature

If the spec and time allow, you may implement **one** critical feature **in the project folder** and mark it in `context/feature_list.json` after running the corresponding tests. If you do:

- Run the tests for that feature (from the project folder).
- Set `"passes": true` only for that feature in `context/feature_list.json`.
- Commit with a message that references the feature id or description.
- Append a short note to `context/session_history.md` for Session 0 (e.g. “Implemented feature #1 …”).

---

**Summary for Initializer:** Check for **app_spec.md** (create + ask user to update if missing) → ensure **context/** exists → read spec → create **context/feature_list.json** → create **context/session_history.md** → create **project folder** (app code) + root README/.gitignore → git init + first commit → optional first feature. Keep development files in **context/**, application in the **project folder**.
