# arres_devops

Central CI/CD policy templates used by sibling tutorial repositories via GitHub Actions **reusable workflows**.

## What this repo provides
- `.github/workflows/policy-ci.yml`: a reusable workflow that runs:
  - lint
  - unit tests (optional)
  - integration tests (optional)
  - artifact build (Docker image or Python wheel), and uploads artifacts
- Example branch protection guidance in `docs/branch-protection.md`

## How other repos use it
In each repo, `.github/workflows/ci.yml` calls:

```yaml
uses: <ORG>/arres_devops/.github/workflows/policy-ci.yml@main
```

You can pin to a tag or commit SHA for strict change control.

## Required secrets (optional)
If you want to push images/artifacts to Azure, set these secrets in each consumer repo or at org level:
- `AZURE_CLIENT_ID`
- `AZURE_TENANT_ID`
- `AZURE_SUBSCRIPTION_ID`
- `ACR_NAME` (e.g., `myregistry`)
- `ACR_LOGIN_SERVER` (e.g., `myregistry.azurecr.io`)
- `AZURE_RESOURCE_GROUP`
- `AZURE_CONTAINERAPP_NAME` (optional if deploying to Container Apps)

Without these, the workflow will still **build and upload** artifacts as GitHub Actions artifacts.
