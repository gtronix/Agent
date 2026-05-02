# CODING AGENT — Development session (N)

You are a **development agent** in a multi-session process. You have a **new context** — no memory of past sessions. Use the repo and docs to get your bearings.

**Layout:** Development files live in **`context/`** (feature list, session history, agent instructions). Application code lives in the **project folder** (e.g. `app/` or the name used at init). Read from `context/`, implement in the project folder.

## Document map

| File | Role |
|------|------|
| `context/feature_list.json` | Ordered backlog; only **`passes`** may change after creation |
| `context/session_history.md` | Append-only log for handoff between sessions |
| `app_spec.md` or `context/app_spec.md` | Product scope and technical context |
| `context/init.md` | Initializer workflow (session 1) |
| This file | Coding workflow (session 2+) |

Replace **(N)** in the title with the session number when pasting into a chat, or leave as a reminder that each run is stateless.

---

## Step 1: Git and repo state (start of session)

**Do this first every session.**

```bash
pwd
git status
git branch
# Optional: git pull --rebase
```

- Resolve conflicts or dirty state before changing code.
- Confirm you are on the intended branch (`main`, `develop`, etc.).

---

## Step 2: Get your bearings

```bash
ls -la
ls context/
ls <project_folder>/   # replace with your app folder name

# Spec (root or context — use whichever exists)
test -f app_spec.md && cat app_spec.md || cat context/app_spec.md

cat context/feature_list.json
# Optional: count remaining work — grep '"passes": false' context/feature_list.json | wc -l

cat context/session_history.md
git log --oneline -15
```

You must understand:

- **What** the product is (spec/README).
- **What** is in scope (`context/feature_list.json`).
- **What** was done last (`context/session_history.md`, `git log`).
- **Where** the app lives vs **`context/`**.

---

## Step 3: Verification (before new work)

**Mandatory:** Before implementing new features, confirm the app is still healthy.

1. Run the **test suite** from the **project folder** (e.g. `cd app && npm test`, `pytest`, `go test`).
2. Re-run **1–2 tests** tied to features already `"passes": true` (core flows).
3. If anything fails: set affected features to `"passes": false` in `context/feature_list.json`, fix regressions, re-run tests, then continue.

Do not stack new features on broken behavior.

---

## Step 4: Pick one feature (prioritized)

Open **`context/feature_list.json`** and choose **exactly one** feature for this session:

- **Highest-priority** feature with `"passes": false`.
- Order: `critical` → `high` → `medium` → `low`; within the same priority, prefer lower `id` unless the log says otherwise.
- Prefer finishing one feature well over starting several.

---

## Step 5: Implement the feature

- Work in the **project folder**, not in `context/`.
- Implement only what the feature’s `description` and `steps` require.
- Follow project conventions; keep changes focused.

---

## Step 6: Testing

- Add or update tests as indicated by `test_file` in `context/feature_list.json` (paths relative to repo root).
- Run tests for this feature and, when practical, the full suite.
- Manually verify `steps` when needed (UI, CLI).

Mark passing only when tests and steps pass.

---

## Step 7: Update `context/feature_list.json` (only `passes`)

**You may only change the `passes` field.**

After verification, set `"passes": true` for the completed feature.

**Do not** remove features, reorder, or edit `description`, `steps`, `id`, `category`, `priority`, or `test_file`.

---

## Step 8: Run tests again

Run the full suite (or the relevant subset). Fix failures before committing.

---

## Step 9: Commit (end of session)

```bash
git add .
git status
git commit -m "feat: [short feature name] — [one line]

- [what was implemented]
- context/feature_list.json: marked #<id> as passing"
```

Prefer one clear commit per session (or one per feature if your team prefers).

---

## Step 10: Update session history

**Append** one block to **`context/session_history.md`**, matching existing format:

```markdown
---

## Session N — [Short theme]

- **Date:** YYYY-MM-DD
- **Agent:** Coding agent
- **Summary:** [1–3 lines]
- **Features completed:** #<id> — <description>
- **Commit:** <hash or git log --oneline -1>
- **Next:** [What the next session should do]
```

---

## Step 11: End session cleanly

1. Everything **committed** (`git status` clean).
2. **`context/session_history.md`** updated.
3. **`context/feature_list.json`** — only `passes` updated for done work.
4. **Tests** green from the project folder.
5. No known broken features.

---

## Testing expectations (generic)

- **Unit:** Fast, deterministic; mock externals.
- **Integration:** Real DB/API/services with test config.
- **E2E:** When the feature requires full flows.

Document how to run tests in the **project folder README**.

---

## Project-specific reminders

*(Paste stack-specific commands here for every agent: package manager, migrate, E2E runner, env files.)*

---

## Important reminders

- **Goal:** All features in `context/feature_list.json` passing, production-quality.
- **This session:** Complete **one** feature; leave repo and history obvious for the next agent.
- **Priority:** Fix regressions before new features.
- **Handoff:** Commit + `context/session_history.md` so the next session needs no guesswork.
- **Separation:** Dev artifacts in **`context/`**; application code only in the **project folder**.

Start with **Step 1** and **Step 2**.
