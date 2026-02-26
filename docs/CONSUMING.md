# Consuming Governance Workflows

Use thin wrapper workflows in each application repository that call this repository's reusable workflows.

## Pinning Policy
- Recommended: pin to immutable release tag (`v1.0.0`) or commit SHA.
- Optional convenience: maintain moving major tag (`v1`) in addition to immutable tags.

## Reusable Workflows
- `.github/workflows/app-ci.yml`
- `.github/workflows/app-release.yml`
- `.github/workflows/app-deploy-dev.yml`
- `.github/workflows/app-deploy-stage.yml`
- `.github/workflows/app-swap-slots.yml`
- `.github/workflows/infra-validate.yml`
- `.github/workflows/infra-plan.yml`
- `.github/workflows/infra-apply.yml`
- `.github/workflows/version-bump-check.yml`

## Behavior Notes
- Terraform reusable workflows honor caller-provided `config_directory` for scanning and tfvars staging.
- `app-deploy-stage.yml` validates artifact provenance by checking the release workflow name, source branch, event type, and successful run conclusion.
- Caller wrappers can override provenance expectations through:
  - `expected_release_workflow_name`
  - `expected_release_branch`

## Adoption Pattern
In a consumer repository workflow:

```yaml
jobs:
  validate:
    uses: your-org/github_pipeline_governance/.github/workflows/app-ci.yml@v1.0.0
    with:
      app_dir: src/function_app
      tests_dir: tests
      function_name: HttpExample
```

## Release Process
1. Change workflow logic in this governance repo.
2. Validate YAML and run pilot consumers.
3. Create immutable tag (for example `v1.0.1`).
4. Open consumer PRs updating `@v1.0.0` to `@v1.0.1`.
5. Promote broadly after pilot repos pass.
