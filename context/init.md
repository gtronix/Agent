# INITIALIZER AGENT — Session 1

You are the **first agent** in a multi-session development process. Your job is to set up the foundation for all future coding agents, regardless of project type (web app, API, CLI, mobile, etc.).

**Layout:** Development files (feature list, session history, agent instructions) live in **`context/`**. The actual application code lives in a **project folder** (e.g. `app/` or the project name). Keep them separate.

## Document map

| File | Role |
|------|------|
| `app_spec.md` (root or `context/`) | Product scope — must be filled before deriving features |
| `context/feature_list.json` | Created in step 4 — single source of truth for work items |
| `context/session_history.md` | Created in step 5 — append-only session log |
| This file | Initializer workflow |
| `context/agent.md` | Coding agent workflow for sessions after init |

---

## 1. Check for `app_spec.md` — create and request update if missing

- **Check** for **`app_spec.md`** at the repository root **or** `context/app_spec.md`.
- **If neither exists:**
  1. Ensure **`context/`** exists (`mkdir context` or PowerShell equivalent).
  2. Create **`context/app_spec.md`** or **`app_spec.md`** at repo root using the template below (root is easier for contributors to spot).
  3. **Tell the user** the file must be filled with project details before continuing. Do **not** build the feature list or scaffold until the spec is real.
  4. **Stop** here until `app_spec.md` is completed.

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

- **If a spec exists:** Continue to step 2.

---

## 2. Ensure `context/` exists and holds development files

- **Create** `context/` at the repo root if missing.
- Development artifacts belong under **`context/`**:
  - **`context/app_spec.md`** — optional copy or sole location if you do not use root `app_spec.md`
  - **`context/feature_list.json`** — step 4
  - **`context/session_history.md`** — step 5
  - **`context/init.md`** and **`context/agent.md`** — this template ships them here; if legacy copies exist **only** at repo root, remove duplicates after confirming content matches.

---

## 3. Read the project specification

Read the spec from **`app_spec.md`** or **`context/app_spec.md`** (whichever exists). Do not continue until it contains real project details, not placeholder bullets alone.

---

## 4. Create `context/feature_list.json` (single source of truth)

From the spec, create **`context/feature_list.json`**. Later sessions may only change **`passes`**.

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
| `category`   | e.g. `functional`, `style`, `security`, `performance`, `api`, `data`, `config` |
| `priority`   | `critical` \| `high` \| `medium` \| `low` — **orders work** |
| `description`| One clear, testable sentence |
| `steps`      | Verification steps (2–15; mix short and long) |
| `passes`     | `false` at creation; **only this field** may change later |
| `test_file`  | Path relative to repo root (e.g. `app/tests/unit/foo.test.js`) |

### Rules for `feature_list.json`

- **Cover the spec:** Every requirement maps to at least one feature; prefer small, testable features.
- **Prioritize:** Foundational work first (auth, core models, config).
- **Categories:** Match the project (`api`, `ui`, `cli`, etc.).
- **Mix step counts:** Some 2–5 steps, some longer.
- **All start failing:** `"passes": false` until implemented.
- **Immutability (except `passes`):** Do not delete features or rewrite descriptions/steps in later sessions.

---

## 5. Create session history in `context/`

Create **`context/session_history.md`**.

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
- **Next:** Coding agent continues from feature list and this log (see `context/agent.md`).
```

Later agents append one block per session (see **`context/agent.md`**).

---

## 6. Project folder (application code, separate from context)

Create a **dedicated project folder** named from the spec (e.g. `app`, `api`). Application code, tests, and project config live here — **not** in `context/`.

**Target layout:**

```
<repo_root>/
├── context/
│   ├── init.md
│   ├── agent.md
│   ├── feature_list.json
│   └── session_history.md
├── <project_folder>/
│   ├── README.md
│   ├── .env.example            # optional
│   ├── <source>/
│   └── <tests>/
├── .gitignore
├── README.md
└── app_spec.md                 # optional if not only under context/
```

### Minimum in project folder

- **README.md** — how to run and test; link to spec
- Source and tests as required by the stack

Do **not** invent a full framework; add only what the spec implies or what is needed to run and test.

---

## 7. Initialize Git and first version

1. `git init` if needed.
2. First commit should include `context/`, project folder, root `README.md` and `.gitignore`, and `app_spec.md` if at root.
3. Example message:

   ```text
   chore: initial setup — context/, project folder, feature list, session history

   - context/ with app_spec (if present), feature_list.json, session_history.md, agent docs
   - project folder scaffold
   - README and .gitignore
   ```

4. Optional tag: `v0.1.0-init` or `session-0`.

---

## 8. Testing strategy (generic)

- **Unit:** Fast, isolated.
- **Integration:** Services / DB / API.
- **E2E:** Full flows when needed.

Set `test_file` in `context/feature_list.json` relative to repo root. Document test commands in the **project folder README**.

---

## 9. Prioritizing features

- **critical:** Product unusable without it.
- **high:** MVP / main journeys.
- **medium:** Important, not blocking.
- **low:** Polish / nice-to-have.

Order **`feature_list.json`** so critical and high items come first by priority and `id` as needed.

---

## 10. End of Session 1

1. Commit all changes.
2. Update **`context/session_history.md`** with real date and commit hash.
3. `git status` clean.
4. Clear **Next** line for the following agent.

---

## 11. Optional: start first feature

If time allows, implement **one** critical feature in the project folder, set **`passes`: true** only for that row after tests pass, commit, and note it in **`session_history.md`**.

---

**Summary:** Spec present and real → **`context/`** + **`context/feature_list.json`** + **`context/session_history.md`** → **project folder** + root README / `.gitignore` → git commit → optional first feature. Dev files stay in **`context/`**; code stays in the **project folder**.
