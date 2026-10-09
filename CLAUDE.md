# CLAUDE.md

> This file provides context and guidance for Claude working in any repository under the **blindbet** GitHub organization.
> Individual repositories may add their own `CLAUDE.md` to override or extend these defaults.

---

## Project Overview

**Name:** blindbet / `.github`

**Purpose:** Holds GitHub org-level defaults — community health files, issue/PR templates, and AI guidance — for the *blindbet* organization. Individual repos override by placing the same file at the same path inside their own repository.

**Owner / Team:** @lpiedade

**Type:** GitHub organization defaults repository (meta-repo, no deployable code)

---

## Tech Stack

This repository contains only Markdown and YAML — there is no runtime or build step. The table below reflects org-wide tooling used across service repositories.

| Layer | Technology |
|---|---|
| Docs format | Markdown (CommonMark), en-US |
| Package manager | pnpm (service repos) |
| CI/CD | GitHub Actions |
| IaC | Terraform / Docker / Kubernetes (`infra` repo) |

---

## Repository Structure

```
.github/
├── ISSUE_TEMPLATE/         # bug_report.yml, feature_request.yml, config.yml
├── profile/                # GitHub org profile README
├── CLAUDE.md               # ← you are here (org-level AI guidance)
├── CODE_OF_CONDUCT.md
├── COMMIT_CONVENTION.md    # Canonical commit type/scope reference
├── CONTRIBUTING.md
├── LICENSE
├── PULL_REQUEST_TEMPLATE.md
├── README.md
├── SECURITY.md
└── SUPPORT.md
```

---

## Getting Started

### Prerequisites

```bash
git  # that's all — no build or install step
```

### Validate issue templates (optional)

```bash
# Requires Node on PATH
npx js-yaml ISSUE_TEMPLATE/bug_report.yml
npx js-yaml ISSUE_TEMPLATE/feature_request.yml
```

---

## Code Style & Conventions

### General

- **Language**: All documentation must be written in **en-US**.
- **Formatting**: CommonMark Markdown; keep lines under 120 characters where practical.
- **YAML**: Issue templates must be valid GitHub issue form schema — validate before committing.

### Naming conventions

| Thing | Convention | Example |
|---|---|---|
| Markdown files | UPPER_SNAKE_CASE | `COMMIT_CONVENTION.md` |
| YAML issue templates | kebab-case | `bug_report.yml` |
| Branch names | `<type>/<short-description>` | `feat/add-oauth`, `fix/null-pointer` |

---

## Commit Conventions

The full reference is [`COMMIT_CONVENTION.md`](COMMIT_CONVENTION.md). A summary follows.

### Types and valid scopes

| Type | Purpose | Scopes |
|---|---|---|
| `feat` | New feature or capability | `api`, `chat`, `ui` |
| `fix` | Bug fix | `prompt`, `model`, `auth` |
| `prompt` | Change in prompt engineering | `system`, `few-shot`, `chain` |
| `model` | Model configuration or version | `claude`, `params`, `tokens` |
| `refactor` | Refactoring without behavior change | `pipeline`, `context` |
| `docs` | Documentation only | `readme`, `api` |
| `test` | Add or correct tests | `unit`, `eval` |
| `chore` | Build, dependencies, tooling | `deps`, `ci` |
| `perf` | Performance improvement | `cache`, `tokens` |
| `ci` | Changes to the CI/CD pipeline | `github`, `deploy` |

### Format

```
<type>(<scope>): <subject>

[optional body]

[optional footer]
```

### Rules

1. Subject line maximum **72 characters**.
2. Use imperative mood: "add" not "adds".
3. No period at the end of the subject.
4. Use `prompt:` for changes in prompts, few-shot examples, or templates.
5. Use `model:` when switching Claude versions or adjusting parameters.
6. Reference issues in the footer: `Closes #42`.
7. Breaking changes: add `BREAKING CHANGE` to the footer.

### Examples

```
feat(chat): add streaming response support
prompt(system): improve instruction clarity for code generation
model(claude): upgrade to claude-sonnet-4, adjust temperature to 0.3
fix(prompt): correct escaping for user-injected content
perf(tokens): reduce avg token usage by 18% with prompt compression
```

> Note: `prompt` and `model` are blindbet-specific types not part of the standard Conventional Commits spec. Linters may flag them as unknown — that is expected and intentional.

---

## Pull Request Guidelines

1. Branch off `main` using `<type>/<short-description>` (e.g. `feat/add-oauth`, `fix/null-pointer`).
2. Keep PRs focused — one logical change per PR.
3. All CI checks must pass before merging.
4. Require at least **1** approving review (configured in branch protection).
5. Squash-merge into `main`; the merge commit message must follow Conventional Commits.

---

## Issue tracker

**All issues for the blindbet platform live in [`blindbet/docs`](https://github.com/blindbet/docs/issues).**
No other repository in the org keeps its own issue backlog.

### Why one repo

blindbet is a multi-repo platform: many repositories, one system. A per-repo tracker splits the backlog
across one board per repository, so nobody can answer "what is open right now" without visiting all of
them, and work that spans services (most of it) has no natural home. Centralizing in `docs` buys a single
prioritizable queue, one place where specs and ADRs sit next to the issues that implement them, and
cross-service dependencies that GitHub can express natively instead of as prose.

`docs` is the right host because it already carries the specs (`spec/`), the decisions (`adr/`), and the
`ready-for-agent` triage flow the issues are graded against.

### Rules

1. **Create every issue in `docs`**, from any repo: `gh issue create --repo blindbet/docs ...`.
   `gh` infers the current clone when `--repo` is omitted, so pass it explicitly, always.
2. **Label the affected service** with `repo:<name>`. This is what keeps the central backlog filterable per
   service — it replaces the repo boundary you gave up. Cross-cutting work carries one label per touched
   service.
3. **Pull requests stay in their own repo.** Only issues are centralized; a PR belongs where the code is.
4. **Cross-reference with the full form** `blindbet/docs#42`. A bare `#42` in a commit or PR body resolves
   against the local repo and will silently point at the wrong thing.
5. **Never enable or reopen a per-repo backlog.** If you find issues in a service repo, migrate the open ones
   to `docs` and close the originals with a pointer comment.

### Known exception: CI failure issues

Service repos whose `.github/workflows/ci.yml` opens a `ci-failure` issue when `build & test` breaks on
`main` still file it in the service repo: the workflow authenticates with the built-in `GITHUB_TOKEN`,
which is scoped to its own repository and cannot create issues elsewhere.

Redirecting them to `docs` requires an org-scoped PAT stored as an org secret. Until that secret exists, leave
the workflows alone — pointing them at `docs` without it makes CI fail on the failure handler itself.

---

## Important Files & Docs

| Resource | Link |
|---|---|
| Issue backlog (all repos) | [`blindbet/docs` issues](https://github.com/blindbet/docs/issues) |
| Commit conventions (canonical) | [`COMMIT_CONVENTION.md`](COMMIT_CONVENTION.md) |
| Contribution guide | [`CONTRIBUTING.md`](CONTRIBUTING.md) |
| ADRs | `docs/adr/` |
| Org overview | [`README.md`](README.md) |
| Security reporting | [`SECURITY.md`](SECURITY.md) |

---

## Known Gotchas & Context

- This repo is the **fallback** for the entire org. Changes here affect every repository that has not overridden the file locally — review carefully before merging.
- YAML issue templates must conform to GitHub's issue form schema. Malformed templates silently break the issue creation UI without any visible error.
- The `prompt` and `model` commit types are blindbet-specific. Do not remove or rename them to align with upstream Conventional Commits tooling.
- `LICENSE` is a proprietary notice — do not alter it.

---

## Out of Scope

- Do **not** add service-specific instructions here — each repo should have its own `CLAUDE.md`.
- Do **not** modify `LICENSE`.
- Do **not** change GitHub Actions secrets, branch protection rules, or org-level settings from this file.
- Do **not** commit generated files or secrets.

---

*Last updated: May 2, 2026 by [@lpiedade](https://github.com/lpiedade)*
