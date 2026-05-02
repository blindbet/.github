# CLAUDE.md

> This file provides context and guidance for Claude working in this repository.
> Customize every section marked with `TODO` before committing.

---

## Project Overview

**Name:** <!-- TODO: Project / service name -->

**Purpose:** <!-- TODO: One or two sentences describing what this repo does and why it exists -->

**Owner / Team:** <!-- TODO: Team name or Slack channel -->

**Type:** <!-- TODO: e.g. REST API, React SPA, CLI tool, shared library, data pipeline… -->

---

## Tech Stack

<!-- TODO: Fill in the actual technologies used -->

| Layer | Technology |
|---|---|
| Language | <!-- e.g. TypeScript 5.x / Python 3.12 --> |
| Runtime / Framework | <!-- e.g. Node 20 / FastAPI / Next.js 14 --> |
| Database | <!-- e.g. PostgreSQL 15 / DynamoDB --> |
| Infrastructure | <!-- e.g. AWS ECS / Vercel / GCP Cloud Run --> |
| Package manager | <!-- e.g. pnpm / poetry / cargo --> |
| Test runner | <!-- e.g. Vitest / pytest / Jest --> |
| CI/CD | <!-- e.g. GitHub Actions / CircleCI --> |

---

## Repository Structure

```
.
├── src/                  # TODO: describe main source layout
│   ├── ...
├── tests/                # Unit & integration tests
├── docs/                 # Additional documentation
├── scripts/              # Dev / ops helper scripts
└── CLAUDE.md             # ← you are here
```

<!-- TODO: Expand or replace the tree above to match the actual layout. -->
<!-- Briefly note any non-obvious directories or naming conventions. -->

---

## Getting Started

### Prerequisites

```bash
# TODO: list required tools and versions
# e.g.
# node >= 20
# pnpm >= 9
# python >= 3.12
```

### Install dependencies

```bash
# TODO: replace with the actual install command
pnpm install
```

### Environment setup

```bash
# Copy the example env file and fill in secrets
cp .env.example .env
```

<!-- TODO: List any required environment variables that have no defaults -->

| Variable | Description | Required |
|---|---|---|
| `DATABASE_URL` | Connection string for the primary DB | ✅ |
| `API_KEY` | <!-- TODO --> | ✅ |

---

## Common Commands

<!-- TODO: keep this list current — it is the single source of truth for day-to-day dev tasks -->

```bash
# Development
pnpm dev          # Start local dev server
pnpm build        # Production build
pnpm start        # Run production build locally

# Testing
pnpm test         # Run all tests
pnpm test:unit    # Unit tests only
pnpm test:e2e     # End-to-end tests
pnpm test:watch   # Watch mode

# Code quality
pnpm lint         # Lint source files
pnpm lint:fix     # Auto-fix lint issues
pnpm format       # Run formatter (Prettier / Black / …)
pnpm typecheck    # Type-check without emitting

# Database (if applicable)
pnpm db:migrate   # Run pending migrations
pnpm db:seed      # Seed development data
pnpm db:reset     # Drop, recreate, migrate, seed
```

---

## Architecture

### High-level design

<!-- TODO: Describe the main components and how data flows through the system.
     A short paragraph or simple ASCII diagram is fine. -->

```
Client → API Gateway → [Service A] → Database
                     ↘ [Service B] → External API
```

### Key modules / packages

<!-- TODO: List the most important source modules and what each is responsible for -->

| Module | Responsibility |
|---|---|
| `src/api` | HTTP route handlers and request validation |
| `src/services` | Business logic, decoupled from transport layer |
| `src/db` | Database models and query helpers |
| `src/lib` | Shared utilities and cross-cutting concerns |

### External dependencies & integrations

<!-- TODO: List third-party services this repo calls -->

- **[Service name]** — purpose, auth method
- **[Service name]** — purpose, auth method

---

## Code Style & Conventions

### General

- **Language**: <!-- TODO: TypeScript strict mode / Python type hints required / … -->
- **Formatting**: <!-- TODO: Prettier (config in `.prettierrc`) / Black / gofmt / … -->
- **Linting**: <!-- TODO: ESLint (`eslint.config.ts`) / Ruff / Clippy / … -->
- **Max line length**: <!-- TODO: 100 chars / 120 chars / … -->

### Naming conventions

| Thing | Convention | Example |
|---|---|---|
| Files | <!-- kebab-case / snake_case --> | `user-service.ts` |
| Variables & functions | <!-- camelCase / snake_case --> | `getUserById` |
| Classes / types | PascalCase | `UserService` |
| Constants | UPPER_SNAKE_CASE | `MAX_RETRY_COUNT` |
| Database tables | <!-- snake_case plural --> | `user_accounts` |

### Patterns to follow

<!-- TODO: Add project-specific patterns Claude should know about -->

- **Error handling**: Always throw typed errors from `src/lib/errors.ts`; never swallow exceptions silently.
- **Validation**: Use [Zod / Pydantic / …] schemas at the boundary; never trust raw input deeper in the stack.
- **Logging**: Use the shared logger (`src/lib/logger.ts`) — never `console.log` in production code.
- **Async**: Prefer `async/await`; avoid callback-style unless interfacing with legacy code.

### Patterns to avoid

<!-- TODO: Add anti-patterns specific to this repo -->

- Do **not** import directly from `src/db` inside route handlers — go through the service layer.
- Do **not** commit secrets or hardcoded URLs; use environment variables.
- Do **not** use `any` types in TypeScript without a suppression comment explaining why.

---

## Testing

<!-- TODO: Describe the testing philosophy and structure -->

### Strategy

| Layer | Tool | Location | Notes |
|---|---|---|---|
| Unit | <!-- Vitest / pytest --> | `tests/unit/` | Pure logic, no I/O |
| Integration | <!-- Supertest / httpx --> | `tests/integration/` | Tests against real DB (test container) |
| E2E | <!-- Playwright / Cypress --> | `tests/e2e/` | Runs against staging URL |

### Writing tests

- Test files live next to source files **or** in `tests/` — <!-- TODO: pick one and delete the other -->
- Test file naming: `*.test.ts` / `*_test.py` <!-- TODO -->
- Aim for high coverage on `src/services/**`; lower tolerance is acceptable for thin route handlers.
- Use factories / fixtures from `tests/helpers/` rather than hand-rolling test data.

---

## Pull Request Guidelines

<!-- TODO: Adjust to match your team's actual process -->

1. Branch off `main` using the pattern `<type>/<short-description>` (e.g. `feat/add-oauth`, `fix/null-pointer`).
2. Keep PRs focused — one logical change per PR.
3. All CI checks must pass before merging.
4. Require at least **1** approving review (configured in branch protection).
5. Squash-merge into `main`; use [Conventional Commits](https://www.conventionalcommits.org/) for the merge commit message.

### Commit message format

```
<type>(<scope>): <short summary>

[optional body]

[optional footer: BREAKING CHANGE / closes #issue]
```

Types: `feat` | `fix` | `docs` | `refactor` | `test` | `chore` | `perf`

---

## Important Files & Docs

<!-- TODO: Add links to the most relevant docs Claude might need -->

| Resource | Link |
|---|---|
| API contract / OpenAPI spec | `docs/openapi.yaml` |
| ADRs (Architecture Decision Records) | `docs/adr/` |
| Runbook | <!-- TODO: link --> |
| Notion / Confluence | <!-- TODO: link --> |
| Jira / Linear board | <!-- TODO: link --> |

---

## Known Gotchas & Context

<!-- TODO: Add anything surprising, legacy, or non-obvious that would help Claude avoid mistakes -->

- <!-- e.g. "The `legacy/` directory is intentionally excluded from linting — do not add it to the ESLint config." -->
- <!-- e.g. "We use a custom fork of [library] pinned at commit abc123 because of [bug]. Do not upgrade." -->
- <!-- e.g. "The `USER_ID` in the DB is a UUID stored as a CHAR(36), not a native UUID column — mind implicit casts." -->

---

## Out of Scope

<!-- TODO: Explicitly list things Claude should NOT do in this repo -->

- Do not modify files under `generated/` — they are auto-generated by the build.
- Do not change `package.json` scripts without discussing with the team first.
- Do not alter database migration files that have already been applied to production.

---

*Last updated: May 2, 2026 by @lpiedade[https://github.com/lpiedade] *