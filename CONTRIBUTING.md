# Contributing to TurnLot

This document outlines the development workflow and contribution guidelines for TurnLot repositories. Coding, tooling, and versioning standards are in the [Engineering Standards](https://github.com/turnlot/engineering/blob/main/engineering-standards.md) (organization members only).

## Development Workflow

All changes are developed on a dedicated branch and merged into `main` through a pull request. `main` is protected and does not accept direct pushes.

1. Create a new branch from the latest `main`.
2. Implement your changes locally.
3. Add or update tests where appropriate.
4. Run the repository's checks.
5. Push your branch and open a pull request targeting `main`.
6. Address review feedback and ensure all required checks pass.
7. Merge once the pull request meets the [review policy](#review-policy).

Create a branch:

```bash
git checkout main
git pull origin main
git checkout -b feature/feature-name
```

Before opening a pull request, run the repository's checks. For Python repositories:

```bash
ruff check .
ruff format --check .
mypy
pytest -v
```

Stage changes deliberately, then commit and push:

```bash
git add -p            # or add specific files by name
git commit -m "feat: describe change"
git push -u origin feature/feature-name
```

Avoid `git add .`, which can pick up environment files and local data. Every repository's `.gitignore` must exclude `.env` files.

GitHub Actions runs each repository's required checks on pull requests.

## Branch Naming

Use descriptive branch names with the following prefixes:

| Prefix | Purpose |
|---|---|
| `feature/` | New functionality |
| `fix/` | Bug fixes |
| `refactor/` | Code improvements without changing functionality |
| `docs/` | Documentation updates |
| `chore/` | Maintenance and configuration |

Examples:
- `feature/database`
- `fix/inventory-sync`
- `refactor/lead-matching`

## Commits

Commit messages follow [Conventional Commits](https://www.conventionalcommits.org/): `type(optional scope): description`, written in the imperative mood.

| Type | Use for |
|---|---|
| `feat` | New functionality |
| `fix` | Bug fixes |
| `refactor` | Code changes that don't change behavior |
| `docs` | Documentation only |
| `chore` | Maintenance and configuration |
| `test` | Adding or changing tests |
| `ci` | CI workflow changes |
| `perf` | Performance improvements |

Mark breaking changes with `!` after the type (`feat!: ...`) or a `BREAKING CHANGE:` footer.

Examples:
- `feat: add PostgreSQL connection`
- `fix(ingestion): prevent duplicate lead imports`
- `refactor(matching): simplify inventory matching logic`

## Pull Requests

All changes to `main` are submitted through a pull request.

Pull requests should:

- Focus on a single feature, fix, or related set of changes.
- Clearly describe what changed, why, and its potential impact.
- Include relevant tests or validation steps.
- Pass required checks before merging.

### Review Policy

- Pull requests need one approval from another developer before merging.
- Pull requests containing only `docs` or `chore` changes may be merged by their author once checks pass.

## Security

- Never commit credentials, API keys, tokens, or environment files.
- Use environment variables or an approved secrets manager for sensitive configuration.
- Do not include customer data in commits, tests, or pull requests.
- Report security concerns privately as described in the [Security Policy](SECURITY.md), never through public issues.
