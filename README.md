# SWN-Contact-Data-Authority

Software developed to maintain data as a single source of truth for SWN

# SWN Contact Data Authority

This repository contains the **authoritative engineering artifacts** for the SWN Contact Data Authority system.

Non-code documentation (requirements, runbooks, training, security policy) lives in **SharePoint**.  
See **Governance – Authoritative Sources of Truth** for details.

---

## Repository Structure

/
├── src/
│ ├── function-app/
│ │ ├── Handlers/
│ │ ├── Soap/
│ │ ├── Models/
│ │ ├── Services/
│ │ └── Program.cs
│ │
│ ├── dataverse/
│ │ ├── solution/
│ │ └── schema-notes.md
│ │
│ └── flows/
│ ├── exports/
│ └── design-notes.md
│
├── docs/
│ ├── architecture/
│ │ ├── overview.md
│ │ ├── system-context.md
│ │ └── integration-flow.md
│ │
│ ├── adr/
│ │ ├── ADR-0001-function-hosting.md
│ │ ├── ADR-0002-keyvault-secrets.md
│ │ └── ADR-0003-soap-gateway.md
│ │
│ ├── api/
│ │ ├── contracts/
│ │ │ ├── upsert-contact.request.json
│ │ │ ├── upsert-contact.response.json
│ │ │ └── README.md
│ │ ├── error-model.md
│ │ └── versioning.md
│ │
│ ├── security/
│ │ ├── identity-model.md
│ │ ├── keyvault-usage.md
│ │ └── environment-boundaries.md
│ │
│ ├── operations/
│ │ ├── logging-and-telemetry.md
│ │ └── failure-modes.md
│ │
│ └── standards/
│ └── naming-conventions.md
│
├── .github/
│ └── workflows/
│ └── ci.yml
│
└── README.md

---

## Authoritative Sources

| Domain                  | Authoritative Location                             |
|-------------------------|----------------------------------------------------|
| Source code             | GitHub                                             |
| API contracts           | GitHub (`/docs/api/contracts`)                     |
| Architecture decisions  | GitHub (ADRs)                                      |
| Naming conventions      | GitHub (`/docs/standards`)                         |
| Product requirements    | SharePoint                                         |
| Operations & runbooks   | SharePoint                                         |
| Security policies       | SharePoint                                         |
| Training & onboarding   | SharePoint                                         |
| Secrets & credentials   | Azure Key Vault                                    |

---

## Environments

This project uses dedicated Dataverse environments for development, testing, staging, and production. Record of environment IDs and solution name:

- Dev Environment ID: `5e9ceb44-8a98-e9b0-a720-864bb9aebf16`
- Test Environment ID: `ff35fa38-1852-e6b9-b0ea-44ebe974a712`
- Staging Environment ID: `6e4c75cc-561f-e6cd-a6fc-29f3dffc480a`
- Prod Environment ID: `d4070d43-11ab-e567-b2fa-e2bc1cedd009`
- Solution Name: `RFRSWNCDA`

Notes:
- Staging is a dedicated pre-production environment used for final verification, UAT, and smoke tests. CI/CD will deploy release candidates to Staging for validation prior to promoting the same build to Production.
- Use the Power Platform CLI or the Power Platform Admin Center to import and publish the `RFRSWNCDA` solution into each environment.
- Secrets and environment-specific configuration (including SWN credentials) must be stored in Azure Key Vault per the repository security policy.

---

## Governance Notes

- GitHub artifacts require pull requests.
- SharePoint artifacts are authoritative for non-code domains.
- Conflicts are resolved using the Authoritative Sources matrix.

---

## Formatting & Linting

This repository follows a small set of Markdown formatting conventions to remain compliant with common markdown linters (for example, `markdownlint`):

- Headings: Use ATX-style headings (`#`, `##`, etc.). Ensure a single blank line after each heading.
- Code and directory listings: Use fenced code blocks with a language hint (`text` for trees).
- Paragraphs: Separate paragraphs with a single blank line.
- Lists: Use `-` for unordered lists. Indent subitems by two spaces.
- Tables: Use pipe-delimited tables with a header separator line. Visually align columns using spaces so vertical separators line up; left-align content unless numeric.
- Files: Keep README sections concise. If additional guidelines are required, add them to `CONTRIBUTING.md`.

Example table style is used above in the Authoritative Sources section.
