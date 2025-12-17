# Naming Conventions

Applies to both SharePoint and GitHub; this is foundational for long-term clarity.

## General rules (everywhere)

- Use Title Case for human-facing documents and pages.
- Use kebab-case (lowercase-with-hyphens) for folders and files in GitHub (for example: `system-context.md`).
- Avoid dates in filenames unless the document is explicitly time-bound.
- Avoid version numbers in filenames unless superseded versions must coexist.
- Prefer stable names and document history instead of renaming.

## SharePoint naming conventions

### Documents

- Format: `<Category> – <Topic> – <Qualifier>.docx`  
  - `Category` is mandatory.  
  - `Qualifier` is optional.
- Examples:
  - `Product – Functional Requirements.docx`
  - `Operations – Deployment Runbook.docx`
  - `Security – Key Vault Access Policy.docx`
  - `Training – Admin User Guide.docx`
- Rules:
  - One document = one responsibility.

### Pages

- Format: Plain-English Title (Title Case).
- Examples:
  - `Start Here`
  - `System Overview`
  - `Architecture Summary`
  - `Operational Status & Health`
- Rules:
  - Pages are for navigation and narrative.
  - Pages should link to documents, not duplicate them.

### Document libraries

- Keep a flat structure; no nested folders deeper than one level unless unavoidable.
- Suggested libraries:
  - `Product & Requirements`
  - `Operations & Runbooks`
  - `Security & Governance`
  - `Training & Onboarding`

## GitHub naming conventions

### Folders

- Use lowercase and kebab-case.
- Be descriptive, not clever.
- Examples:
  - `docs/architecture`
  - `docs/adr`
  - `docs/api/contracts`

### Markdown files

- Format: `<topic>.md` (kebab-case).
- Examples:
  - `system-context.md`
  - `integration-flow.md`
  - `error-model.md`

### ADRs

- Format: `ADR-####-short-title.md`
- Examples:
  - `ADR-0001-function-hosting.md`
  - `ADR-0002-keyvault-secrets.md`
- Rules:
  - Numbers are never reused or renumbered.

## Markdown linter & formatting rules

These rules are intended to be enforced by markdownlint, Vale, or a comparable tool.

- Use ATX-style headings (`#`, `##`, `###`). Do not mix Setext-style headings.
- Heading levels should increase by one level at a time.
- Use a single blank line between a heading and the following paragraph.
- Use hyphens (`-`) for unordered lists.
- Leave a blank line before lists and fenced code blocks.
- Use fenced code blocks with the language specified (for example: ```csharp).
- Soft-wrap lines at ~80 characters for readability.
- Files must end with a single newline and contain no trailing whitespace.
- Use spaces only (no hard tabs).
- Use inline code (backticks) for filenames, paths, class names, and commands.
- Filenames and folder paths must be all-lowercase with hyphens; file extensions must be lowercase (`.md`, `.docx`).

## Pull request and commit guidance

- Fix linter errors before merging; CI will fail on naming or Markdown rule violations.
- When changing naming rules or structure, link the PR to the relevant ADR or add rationale.
- Use clear commit messages that reference changed doc paths.

## Exceptions

- If a legacy filename cannot change, document the reason in the PR description and link to an ADR if applicable.

