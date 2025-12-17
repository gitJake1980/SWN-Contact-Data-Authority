# Contributing to SWN-Contact-Data-Authority

Thank you for contributing. This repository follows strict project and coding standards to ensure the codebase is consistent, reviewable, and deployable. This CONTRIBUTING.md documents required workflows, branch protection rules, coding style expectations, and operational practices required for the project.

## Table of contents

- Purpose
- Getting started
- Branching and pull request process
- Commit message convention
- Code style and formatting
- EditorConfig and tooling
- Testing and quality gates
- Secrets and configuration
- Dataverse and schema guidelines
- Azure and deployment
- Documentation
- Reviews and approvals
- Contact

## Purpose

This repository implements a Dataverse-backed source of truth and an Azure Function SOAP gateway for SendWordNow (SWN). Contributions must adhere to the rules below. All code and documentation must be written and reviewed under these standards.

## Getting started

- Use Visual Studio 2026 for development on both office and home machines.
- Open the solution from the repository root in Visual Studio.
- Use the following Visual Studio settings (where applicable):
  - __Tools > Options > Text Editor > C# > Formatting__ - follow the repository .editorconfig rules.
  - __Tools > Options > Source Control__ - ensure Git integration is enabled.

Refer to `docs/standards/naming-conventions.md` and `docs/development/development-cycle.md` for additional project-specific guidance.

## Branching and pull request process

- The `main` branch is protected. Direct pushes to `main` are prohibited.
- Use feature branches named as `feature/<short-description>`, bugfix branches `bugfix/<short-description>`, and hotfix branches `hotfix/<short-description>`.
- Open a pull request (PR) from your branch to `main` when ready. PR must target `main` and include:
  - A clear description of the change.
  - Reference to any related issue number.
  - Testing notes and how to validate the change.
- PR reviews:
  - Require at least one approving review from a reviewer other than the author.
  - All status checks must pass before merging (build, unit tests, static analysis).
- Use squash merges for PRs to keep history linear unless otherwise approved.

## Commit message convention

- Use Conventional Commits style. Examples:
  - `feat(dataverse): add contact entity mapping`
  - `fix(function): correct SOAP envelope encoding`
  - `chore(ci): update GitHub Actions matrix`
- The commit subject line should be 50 characters or less; the body (if present) should explain why the change was made.

## Code style and formatting

- Code must adhere to the repository .editorconfig. The .editorconfig will be provided in the repo root and is authoritative for formatting rules (indentation, naming, etc.).
- Preferred language: C# for Azure Functions and related libraries.
- Follow these rules unless the .editorconfig specifies otherwise:
  - Use 4-space indentation for C#.
  - Use PascalCase for public types and methods.
  - Use camelCase for private fields and parameters. Prefix private readonly fields with `_` is allowed if .editorconfig specifies.
  - Avoid region directives unless justified.
  - Keep methods concise; break out helper methods where it improves readability and testability.

Refer to `docs/standards/naming-conventions.md` for exact naming rules.

## EditorConfig and tooling

- An `.editorconfig` file will be present at the repository root. It is mandatory: all contributors must ensure their IDE/editor honors it.
- If using Visual Studio, ensure __Tools > Options > Text Editor > General__ has "Detect when file is changed outside the environment" enabled and that EditorConfig support is active.
- Configure pre-commit or IDE formatting so code is formatted per .editorconfig before committing.

## Testing and quality gates

- Unit tests are required for all non-trivial logic. Place tests in a `tests` folder following established project structure.
- GitHub Actions CI pipeline must run on PRs and main. The pipeline must include:
  - Build step (dotnet build or equivalent)
  - Unit test step (dotnet test)
  - Static analysis step (e.g., dotnet format or Roslyn analyzers)
  - Security/secret scanning where applicable
- Tests must pass before merging. Aim for high unit test coverage for business logic (MVP: critical paths covered).

## Secrets and configuration

- All credentials and secrets (including SWN credentials and endpoints) must be stored in Azure Key Vault.
- Use Managed Identity to allow the application (Azure Function) to access Key Vault. Never store secrets in source code or repository configuration files.
- Document required Key Vault secret names in `docs/development/development-cycle.md` and/or in the Azure deployment scripts.

## Dataverse and schema guidelines

- Dataverse entities must map to the SWN contracts and XSDs in `schemas/swn` to minimize transformation friction.
- For MVP implement entities: `Contact`, `Group`, `SWNSyncLog`.
- Design entity attributes to reflect the XSD types and required fields. Keep naming consistent with `docs/standards/naming-conventions.md`.
- Flows should be triggered on create/update events in Dataverse and must call the Azure Function endpoint.

## Azure and deployment

- Azure Function must be HTTP-triggered and implement a SOAP gateway that accepts Dataverse-power-platform-friendly JSON and returns JSON.
- Function must retrieve SWN credentials from Key Vault using a Managed Identity.
- Deployments are gated by branch protections and CI. Use GitHub Actions to build and deploy to staging and production slots.
- Document any required Azure resources and RBAC roles in `docs/development/development-cycle.md`.

## Documentation

- Keep `README.md` up to date with setup and deployment instructions.
- Project documentation should live under `docs/` with clear folders: `docs/standards/`, `docs/development/`, `docs/schemas/`, `docs/copilot/`.
- The `schemas/swn` directory contains WSDL/XSDs and is the source for Dataverse mapping decisions.

## Reviews and approvals

- Security-sensitive changes (secrets, authentication, or public exposure) require an additional security review.
- Significant design changes should be discussed via an issue before implementation.

## Contact

- For questions about repository standards or the CI pipeline, open an issue or contact the repository owner.

---

By contributing you agree to follow these rules. Failure to comply may result in changes being requested or contributions being rejected.