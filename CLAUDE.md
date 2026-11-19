# Working in this repository

Organization-wide GitHub files for Turnlot: the public profile, the contributing guide, the security policy, issue and pull request templates, and the CI workflows every Python repository calls.

## This repository is public

Anyone can read every file, issue, pull request, and commit message here.

- No AWS account IDs, role ARNs, domains of internal systems, or names of people.
- Nothing about security gaps, open findings, audits, or reviews. Those belong in the private `turnlot/engineering` repository.
- Refer to internal documents by name ("the engineering standards"), noting they are for organization members. Do not quote them.
- A gap in something here is filed as an issue in a private repository, not in this one.

## The shared workflows reach every repository at once

`python-ci.yml` and `python-image.yml` are called at `@main` by `database`, `ingestion`, `matching`, and the `api`. A merged change takes effect in all of them immediately, and `python-image.yml` can publish container images.

- CI here (`lint.yml`) checks syntax and expressions only. It does not run the workflow.
- Before merging a change to a shared workflow, test it from a caller: open a pull request in one calling repository that points at the branch (`python-ci.yml@my-branch`), see it pass, and do not merge that pull request.
- Keep a change backward-compatible with every caller: a new input needs a default.
- Account IDs and role ARNs are inputs passed by the caller, never written here.
- Pin every action to a commit, with its version in a comment. Only actions on the organization's allow-list run; anything else is a downloaded file checked against a pinned checksum, as `lint.yml` does.
- Pass inputs to scripts through `env:`, not by writing `${{ ... }}` inside `run:`.
- Give every job a `timeout-minutes`.

## Before opening a pull request

- **Check whether the change resolves an open issue**, here or in the repositories it affects (`gh issue list -R turnlot/<repository>`).
- If it resolves one fully, write `Closes #N` in the description (`Closes turnlot/<repository>#N` for another repository), so merging closes it.
- If it resolves part of one, write `Part of #N`, and say in the description what is left.
- Never close an issue by hand without being asked.

## Style

- The company's name is written "Turnlot", not "TurnLot". Lowercase `turnlot` stays as it is in repository, package, and resource names.
- The contributing guide and templates describe what is actually done. If practice changes, change them in the same piece of work.
- Workflow files follow the comment separators used throughout: `# ===== / # ----- Section -----` for sections and `# --- Subsection ---` below them.
