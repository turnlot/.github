# Contributing to Turnlot

This document outlines the development workflow and contribution guidelines for Turnlot repositories.

## Development Workflow

1. Create a new branch from the latest `main`.
2. Implement your changes locally.
3. Add or update tests where appropriate.
4. Push your branch and open a pull request.
5. Address review feedback and ensure all automated checks pass.
6. Merge the pull request into `main` once approved.

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

Write concise, descriptive commit messages using the imperative mood.

Examples:
- `Add PostgreSQL connection`
- `Fix duplicate lead notifications`
- `Refactor inventory matching logic`

## Pull Requests

All changes to `main` should be submitted through a pull request.

Pull requests should:

- Focus on a single feature, fix, or related set of changes.
- Clearly describe what changed and why.
- Include relevant tests or validation steps.
- Pass automated checks before merging.
- Receive review approval when another developer is available.

## Security

- Never commit credentials, API keys, tokens, or environment files.
- Use environment variables or an approved secrets manager for sensitive configuration.
- Do not include customer data in commits, tests, or pull requests.
- Report security concerns privately rather than through public issues.
