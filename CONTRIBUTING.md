# Contributing to blindbet

Thanks for taking the time to contribute. This guide describes the default contribution workflow for repositories in the `blindbet` organization. Individual repositories may add more specific instructions.

## Before You Start

- Check the repository README and open issues for project-specific context.
- For bugs, search existing issues before opening a new one.
- For larger changes, open an issue or discussion first so maintainers can help shape the approach.

## Workflow

1. Fork the repository.
2. Create a branch from the default branch.
3. Make a focused change.
4. Add or update tests when behavior changes.
5. Run the repository's documented checks locally.
6. Open a pull request with a clear description and linked issue when applicable.

## Branch Naming

Use short, descriptive branch names:

- `feature/add-payment-flow`
- `fix/login-error-state`
- `docs/update-api-examples`
- `chore/refresh-dependencies`

## Commit Style

Write commits in the imperative mood and keep the subject concise:

- `Add bug report issue form`
- `Fix account validation error`
- `Update contribution guidelines`

When a change needs more context, add a short commit body explaining why the change was made and any important tradeoffs.

## Pull Requests

Pull requests should be small enough to review comfortably and should include:

- A summary of what changed.
- The type of change.
- How the change was tested.
- Screenshots or recordings for user-facing UI changes.
- Any follow-up work or known limitations.

Maintainers may request changes before merging. Please keep the discussion focused, respectful, and grounded in the code and user impact.

## Coding Conventions

- Follow the style, architecture, and tooling already present in the repository.
- Prefer clear names and simple control flow.
- Keep unrelated refactors out of feature and bug-fix pull requests.
- Document behavior that is non-obvious or important for maintainers.
- Do not commit secrets, private keys, credentials, or generated local configuration.

## Reviews and Merging

Maintainers review pull requests for correctness, maintainability, security, test coverage, and fit with project direction. A pull request may be closed if it is inactive, out of scope, or superseded by another approach.

Thank you for helping improve `blindbet`.
