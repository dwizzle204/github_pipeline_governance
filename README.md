# GitHub Pipeline Governance

## Educational Use Only
This repository is intended for education and learning sessions.
Workflows here are examples for teaching governance patterns and should not be treated as production-ready controls without additional hardening and review.

Template version: `0.1.1` (see `VERSION` and `CHANGELOG.md`).

Central source of truth for reusable GitHub Actions workflows used by Azure Function learning/template repositories.

## Purpose
This repository exists to separate pipeline logic from application repositories.

Application repos keep small wrapper workflows for local trigger behavior.
This governance repo owns shared pipeline implementation, security posture, and versioned upgrades.

## What is in this repository
- Reusable workflows in `.github/workflows/*.yml` using `on: workflow_call`
  - `app-ci.yml`
  - `app-release.yml`
  - `app-deploy-dev.yml`
  - `app-deploy-stage.yml`
  - `app-swap-slots.yml`
  - `infra-validate.yml`
  - `infra-terratest.yml`
  - `infra-plan.yml`
  - `infra-apply.yml`
  - `version-bump-check.yml`
- Consumer guidance in `docs/CONSUMING.md`
- Baseline history snapshot in `.github/workflows/reusable/` (imported originals)

## What is not in this repository
- No application code
- No Terraform modules for app infrastructure
- No repo-specific trigger rules for each consumer

## Versioning model
- Release immutable tags: `v1.0.0`, `v1.0.1`, ...
- Optionally maintain a moving major tag: `v1`
- Consumers should pin to immutable tags (or commit SHA for stricter pinning)

## Consumer pattern
A consumer repository keeps wrapper workflows under its own `.github/workflows/`:

```yaml
jobs:
  validate:
    uses: your-org/github_pipeline_governance/.github/workflows/app-ci.yml@v1.0.0
    with:
      app_dir: src/function_app
      tests_dir: tests
      function_name: HttpExample
```

## Learning-template note
This repo intentionally allows placeholders in examples (for example `your-org`) so learners can replace values in exercises.

## Validation
This repository includes a lint workflow to validate YAML syntax and enforce reusable-workflow conventions on pull requests.
