# Commit Conventions

## Types

- `feat` — New feature or capability. Scopes: `api`, `chat`, `ui`
- `fix` — Bug fix. Scopes: `prompt`, `model`, `auth`
- `prompt` — Change in prompt engineering. Scopes: `system`, `few-shot`, `chain`
- `model` — Model configuration or version. Scopes: `claude`, `params`, `tokens`
- `refactor` — Refactoring without behavior change. Scopes: `pipeline`, `context`
- `docs` — Documentation only. Scopes: `readme`, `api`
- `test` — Add or correct tests. Scopes: `unit`, `eval`
- `chore` — Build, dependencies, tooling. Scopes: `deps`, `ci`
- `perf` — Performance improvement. Scopes: `cache`, `tokens`
- `ci` — Changes to the CI/CD pipeline. Scopes: `github`, `deploy`

## Format

```
<type>(<scope>): <subject>

[optional body]

[optional footer]
```

## Rules

1. Subject line maximum 72 characters
2. Use imperative mood: "add" not "adds"
3. No period at the end of the subject
4. Use "prompt:" for changes in prompts, few-shot, or templates
5. Use "model:" when switching Claude versions or parameters
6. Reference issues in the footer: Closes #42
7. Breaking changes: add BREAKING CHANGE to the footer
8. Do not add the "Co-Authored-By: Claude ..." trailer; remove it if a tool inserts it
9. Body bullets explain why, not what — the diff shows the what
10. Wrap the body at 72 columns

## Examples

- `feat(chat): add streaming response support`
- `prompt(system): improve instruction clarity for code generation`
- `model(claude): upgrade to claude-sonnet-4, adjust temperature to 0.3`
- `fix(prompt): correct escaping for user-injected content`
- `perf(tokens): reduce avg token usage by 18% with prompt compression`