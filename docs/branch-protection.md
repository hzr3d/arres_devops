# Branch protection / rulesets (tutorial)

You cannot enforce GitHub branch protection from a workflow file alone; it must be configured in GitHub settings.
This project is designed so that branch protection can require the **policy workflow** status checks.

## Recommended settings (per repo)
In **Settings → Branches** (or **Settings → Rules → Rulesets**):
- Protect `main`
- Require a pull request before merging
- Require approvals: **1**
- Require status checks to pass before merging:
  - `policy-ci / lint`
  - `policy-ci / unit-tests`
  - `policy-ci / integration-tests` (optional)
  - `policy-ci / build-artifacts`
- Require conversation resolution (optional)
- Require signed commits (optional)

## Notes
- If integration tests are not present in a repo, the workflow step will be skipped and will not block merges.
- Pin `arres_devops` usage to a tag/SHA to prevent breaking changes.
