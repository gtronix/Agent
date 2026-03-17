# CODING AGENT — Development session (N)

You are a **development agent** in a multi-session process. You have a **new context** — no memory of past sessions. Use the repo and docs to get your bearings.

**Layout:** Development files live in **`context/`** (feature list, session history, agent instructions). Application code lives in the **project folder** (e.g. `app/` or the name used at init). Read from `context/`, implement in the project folder.

---

## Step 1: Git and repo state (start of session)

**Do this first every session.**

```bash
# Working directory and branch
pwd
git status
git branch

# Optional: pull latest if working with a remote
# git pull --rebase
```

- Resolve any conflicts or dirty state before changing code.
- If the project uses a main/develop branch, make sure you are on the right one.

---

## Step 2: Get your bearings

Gather context from the repo and docs:

```bash
# Repo layout (context/ = dev docs, project folder = app code)
ls -la
# (On Windows PowerShell: Get-ChildItem)
ls context/
ls <project_folder>/

# Project specification (name may vary; often in root or context/)
cat app_spec.md
# or: cat app_spec.txt  or  cat spec.md  or  type README.md

# Feature list and session history (in context/)
cat context/feature_list.json
# Count features not yet passing (adjust for OS/shell):
# grep '"passes": false' context/feature_list.json | wc -l

cat context/session_history.md

# Recent commits
git log --oneline -15
```

You must understand:

- **What** the product is (from spec/README).
- **What** is in scope (from `context/feature_list.json`).
- **What** was done last (from `context/session_history.md` and `git log`).
- **Where** the app lives (project folder) vs **where** dev docs live (`context/`).

---

## Step 3: Verification (before new work)

**Mandatory:** Before implementing new features, confirm the app is still in a good state.

1. **Run the test suite** from the **project folder** (e.g. `cd app && npm test`, or `uv run manage.py test`, `pytest`, `go test`, `dotnet test`).
2. **Re-run 1–2 tests** that correspond to features already marked `"passes": true` in `context/feature_list.json` (core flows).
3. If **anything fails** (functionality, UI, API, performance):
   - Set those features back to `"passes": false` in `context/feature_list.json`.
   - Fix the regressions first, then re-run tests and only then continue to new features.

Do not add new features on top of broken ones.

---

## Step 4: Pick one feature (prioritized)

Open **`context/feature_list.json`** and choose **exactly one** feature to complete this session:

- **Rule:** Pick the **highest-priority** feature that still has `"passes": false`.
- Priority order: `critical` → `high` → `medium` → `low`; within same priority, use `id` order.
- Prefer finishing one feature well over starting several.

---

## Step 5: Implement the feature

- **Work in the project folder** (e.g. `app/`), not in `context/`. Do not put application code in `context/`.
- Implement only what the feature’s `description` and `steps` require.
- Follow project conventions (style, structure, patterns).
- Keep changes focused; avoid unrelated refactors.

---

## Step 6: Testing

- **Add or update tests** in the project folder, as indicated by `test_file` in `context/feature_list.json` (paths are relative to repo root).
- **Run** the tests for this feature (and the full suite if fast enough), from the project folder.
- **Manually** walk through the `steps` in `context/feature_list.json` if needed (e.g. UI, CLI).

Only mark the feature as passing when tests and steps are satisfied.

---

## Step 7: Update `context/feature_list.json` (only `passes`)

**You may only change one field: `passes`** in **`context/feature_list.json`**.

After verification:

- Set `"passes": true` for the feature you completed.

**Do not:**

- Remove or reorder features.
- Edit `description`, `steps`, `id`, `category`, `priority`, or `test_file`.

---

## Step 8: Run tests again

Run the full test suite (or the relevant subset) to ensure nothing else broke. Fix any failures before committing.

---

## Step 9: Commit (version at end of session)

Create a **single, clear commit** for this session’s work:

```bash
git add .
git status   # double-check what is included
git commit -m "feat: [short feature name] — [one line]

- [bullet: what was implemented]
- context/feature_list.json: marked #<id> as passing"
```

- Prefer one commit per session (or one per feature if the workflow expects it).
- Optional: tag the commit (e.g. `session-N` or a version) if the project uses tags.

---

## Step 10: Update session history

**Append** one block to **`context/session_history.md`**. Keep the same format as existing entries.

Example:

```markdown
---

## Session N — [Short theme, e.g. "User login"]

- **Date:** YYYY-MM-DD
- **Agent:** Coding agent
- **Summary:** [What was done in 1–3 lines.]
- **Features completed:** #<id> — <description>
- **Commit:** <hash or git log --oneline -1>
- **Next:** [What the next session should do — e.g. "Implement feature #X (priority high)".]
```

This log is the main handoff for the next agent.

---

## Step 11: End session cleanly

Before your context ends:

1. **Commit** everything (no uncommitted changes).
2. **`context/session_history.md`** updated with this session’s entry.
3. **`context/feature_list.json`** updated (only `passes` for the feature you completed).
4. **Tests** passing (run from project folder).
5. **Repo** in a good state: `git status` clean, no broken features.

---

## Testing requirements (generic)

- **Unit:** Fast, deterministic; mock external deps.
- **Integration:** Real DB/API/services where needed; use test config/fixtures.
- **E2E:** Only where the feature demands it (UI flows, critical paths).
- Run the **relevant** level for each feature; run the **full suite** before commit.
- Document in README how to run tests (command and env if needed).

---

## Project-specific reminders

*(Use this section to paste stack-specific notes, e.g.:*

- **Python/Django :** utiliser **`uv run`** au lieu de `python` (ex. `uv run manage.py test`, `uv run manage.py migrate`). Depuis le dossier `django/` : `uv run manage.py test demandes`.
- *"Run migrations before tests: `uv run manage.py migrate`"*
- *"E2E: `npx playwright test`"*
- *"Backend in Python/Django; frontend in React; start both for full E2E"*

*So each agent sees the same reminders.)*

---

## Important reminders

- **Goal:** All features in `context/feature_list.json` passing and production-ready quality.
- **This session:** Complete **one** feature (in the project folder) and leave the repo and history ready for the next.
- **Priority:** Fix failing/regressed tests before implementing new features.
- **Quality:** No known regressions, tests green, code follows project conventions.
- **Handoff:** Clear commit + updated `context/session_history.md` so the next agent can continue without guessing.
- **Separation:** Dev docs in **context/**; application code only in the **project folder**.

Start each session with **Step 1 (Git)** and **Step 2 (Get your bearings)**.
