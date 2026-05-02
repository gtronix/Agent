# Project specification

<!-- Fill this before running the Initializer. Workflow: context/init.md → context/feature_list.json; then context/agent.md per session. App code lives outside context/ (see context/init.md). -->

## Overview

- **Project name:** e.g. *My App*, *api-gateway*, *cli-tool*
- **Purpose / goal:** e.g. *Internal dashboard to track X* ; *REST API for Y* ; *CLI to automate Z*
- **Target users or context:** e.g. *Internal teams* ; *Third-party developers* ; *CI/CD pipelines*

## Scope

- **Main features or capabilities:**
  - e.g. *User authentication (login / logout)*
  - e.g. *CRUD on core resource X*
  - e.g. *Export to CSV/PDF*
  - e.g. *Configurable settings per tenant*
- **Out-of-scope (optional):**
  - e.g. *Mobile app in v1* ; *External API integrations for MVP*

## Technical context

- **Stack / language / framework (if known):** e.g. *Python 3.x, FastAPI* ; *Node.js, Express* ; *Go, stdlib* ; *React + Django*
- **Constraints or requirements** (e.g. deployment, compliance, performance):
  - e.g. *Deploy on Docker / Kubernetes*
  - e.g. *SQLite dev, PostgreSQL prod*
  - e.g. *Sub-200ms p95 for read endpoints*

## Testing strategy

- **Unit tests:** e.g. `tests/unit/`, `npm test`, `pytest`, `go test ./...`
- **Integration / E2E (if applicable):** e.g. `tests/integration/`, `tests/e2e/`, `npx playwright test`

## Notes

- e.g. *Conventions: REST for API, JSON responses.*
- e.g. *Feature list will be derived from this spec; one feature = one testable requirement.*
