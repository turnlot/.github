# TurnLot GitHub Configuration

Organization-wide GitHub configuration and community files for TurnLot. Files here apply to every TurnLot repository that doesn't define its own.

| Path | Purpose |
|---|---|
| [`profile/README.md`](profile/README.md) | Public organization profile |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Development workflow, commits, and review policy |
| [`SECURITY.md`](SECURITY.md) | Vulnerability reporting and security practices |
| [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE/) | Default issue forms |
| [`.github/PULL_REQUEST_TEMPLATE.md`](.github/PULL_REQUEST_TEMPLATE.md) | Default pull request template |
| [`.github/workflows/python-ci.yml`](.github/workflows/python-ci.yml) | Shared CI workflow for Python repositories |
| [`.github/workflows/python-image.yml`](.github/workflows/python-image.yml) | Shared image build and ECR publish for Python repositories that run as jobs |

Repositories call the shared workflows at a major tag, such as `@v1`. Backward-compatible changes move the tag; breaking changes get a new major tag.

This repository is public. Internal engineering documentation (architecture, domain model, data flow, engineering standards, and decision records) lives in the private [`turnlot/engineering`](https://github.com/turnlot/engineering) repository.
