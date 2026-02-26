# Architecture

## Design goals
- Centralize workflow logic once.
- Keep consumer repositories simple.
- Roll out updates safely with version tags.

## Separation of concerns
- Governance repo responsibilities:
  - Reusable workflow implementation
  - Common action pinning and step hardening
  - Shared secret/input contracts
- Consumer repo responsibilities:
  - Triggers (`pull_request`, `push`, `workflow_dispatch`)
  - Environment assignment (`dev`, `production`)
  - Repository-specific variable and secret wiring

## Reusable workflow catalog
- `app-ci.yml`
- `app-release.yml`
- `app-deploy-dev.yml`
- `app-deploy-stage.yml`
- `app-swap-slots.yml`
- `infra-validate.yml`
- `infra-plan.yml`
- `infra-apply.yml`
- `version-bump-check.yml`

## Lint Policy
- `lint-governance.yml` enforces `workflow_call` on the reusable workflow catalog only.
- Additional non-reusable workflows are allowed when needed for repository operations.

## Upgrade flow
1. Update reusable workflows in this repo.
2. Validate with lint checks and pilot consumer repos.
3. Create a new immutable release tag.
4. Open consumer PRs to bump workflow references to the new tag.
