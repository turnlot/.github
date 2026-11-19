# Turnlot GitHub Configuration

Organization-wide GitHub configuration and community files for Turnlot. Files here apply to every Turnlot repository that doesn't define its own.

| Path | Purpose |
|---|---|
| [`profile/README.md`](profile/README.md) | Public organization profile |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Development workflow, commits, and review policy |
| [`SECURITY.md`](SECURITY.md) | Vulnerability reporting and security practices |
| [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE/) | Default issue forms: a task and a bug report |
| [`.github/PULL_REQUEST_TEMPLATE.md`](.github/PULL_REQUEST_TEMPLATE.md) | Default pull request template |
| [`.github/workflows/python-ci.yml`](.github/workflows/python-ci.yml) | Shared CI workflow for Python repositories |
| [`.github/workflows/python-image.yml`](.github/workflows/python-image.yml) | Shared image build and ECR publish for Python repositories that run as jobs |
| [`.github/workflows/lint.yml`](.github/workflows/lint.yml) | Checks this repository's own workflows before a change to them is merged |

Repositories call the shared workflows at `@main`, so a merged change reaches every repository at once. A pull request here is checked for workflow syntax and expression errors. That does not run the workflow, so before merging a change to one, also test it by pointing one caller's pull request at your branch, such as `python-ci.yml@my-branch`.

This repository is public. Internal engineering documentation (architecture, domain model, data flow, engineering standards, and decision records) lives in the private [`turnlot/engineering`](https://github.com/turnlot/engineering) repository.
