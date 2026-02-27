## [0.1.1] - 2026-02-27

### Added
- Added centralized reusable Terraform Terratest workflow (`.github/workflows/infra-terratest.yml`) for consumer repositories to run repository-local Terraform tests via wrapper workflows.

### Changed
- Updated governance lint policy to include `infra-terratest.yml` in the reusable workflow contract checks.
- Updated governance documentation (`README.md`, `docs/CONSUMING.md`, `docs/ARCHITECTURE.md`) to include the new Terraform Terratest reusable workflow in the official catalog.

## [0.1.0] - 2026-02-26

### Added
- Initial public educational governance repository for centralized reusable GitHub Actions workflows.
- Reusable workflow catalog for app and Terraform lifecycle operations using `workflow_call`.
- Governance lint workflow (`lint-governance.yml`) with actionlint and policy checks.
- Consumer documentation for adoption, architecture, and wrapper patterns.

### Changed
- Clarified educational-use-only positioning and non-production intent in repository documentation.
