# Contributing to Turnlot

This document outlines the development workflow and contribution guidelines for Turnlot repositories. Coding, tooling, and versioning standards are in the [Engineering Standards](https://github.com/turnlot/engineering/blob/main/engineering-standards.md) (organization members only).

## Development Workflow

All changes are developed on a dedicated branch and merged into `main` through a pull request. `main` is protected and does not accept direct pushes.

1. Create a new branch from the latest `main`.
2. Implement your changes locally.
3. Add or update tests where appropriate.
4. Run the repository's checks.
5. Push your branch and open a pull request targeting `main`.
6. Ensure all checks pass, and address review feedback if the pull request is reviewed.
7. Merge once the pull request meets the [review policy](#review-policy).

Create a branch:

```bash
git checkout main
git pull origin main
git checkout -b feat/short-description
```

Before opening a pull request, run the repository's checks. For Python repositories:

```bash
make check    # lint, format, types, and tests, as CI runs them
```

Stage changes deliberately, then commit and push:

```bash
git add -p            # or add specific files by name
git commit -m "feat: describe change"
git push -u origin feat/short-description
```

Avoid `git add .`, which can pick up environment files and local data. Every repository's `.gitignore` must exclude `.env` files.

GitHub Actions runs each repository's required checks on pull requests.

## Branch Naming

A branch is named for its commit type, then a short description: `type/short-description`. The types are the ones commits use, below.

Examples:
- `feat/production-environment`
- `fix/inventory-sync`
- `docs/review-policy`

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
- Describe what changed and why, what was checked, and what has to happen after merging.
- Say so if the change breaks an interface, includes a database migration, or changes a recorded decision.
- Pass every check before merging.

### Issues

Before opening a pull request, check whether it resolves an open issue, in this repository or another.

- If it resolves one fully, write `Closes #N` in the description, so merging closes it.
- If it resolves part of one, write `Part of #N` and say what is left.

### Review Policy

- A pull request is merged once its checks pass.
- When another developer is available to review, it needs their approval first, unless it contains only `docs` or `chore` changes.

The policy in force is recorded in the engineering standards (organization members only).

## Security

- Never commit credentials, API keys, tokens, or environment files.
- Use environment variables or an approved secrets manager for sensitive configuration.
- Do not include customer data in commits, tests, or pull requests.
- Report security concerns privately as described in the [Security Policy](SECURITY.md), never through public issues.
