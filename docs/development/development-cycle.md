# Development Cycle and Copilot Usage Standards

## Authority

- The development lifecycle described here is derived from the authoritative SharePoint governance document.
- This repository is authoritative for:
  - Engineering practices
  - Copilot usage standards
  - Implementation details
- In case of conflict:
  - SharePoint governs process and policy
  - GitHub governs engineering execution

## Development Cycle for SWN Contact Data Authority

### 1. Plan
- Define minimum viable scope (MVP).
- Identify required SWN operations.
- Establish Dev, Test, and Prod environments.

### 2. Design
- Design Dataverse schema and relationships.
- Define security roles and access boundaries.
- Specify JSON to SOAP contracts.

### 3. Build
- Implement functionality in small vertical slices.
- Keep SOAP translation isolated in Azure Functions.
- Version all contracts and decisions.

### 4. Test
- Unit test transformation logic.
- Perform integration testing across environments.

### 5. Release
- Use pull requests and reviews.
- Promote changes from Dev to Test to Prod.

### 6. Operate
- Monitor logs and failures.
- Maintain runbooks and operational documentation.

---

## 10 Best Practices for Coding with Copilot

1. Define one clear objective per session.
2. Provide explicit context and constraints.
3. Use structured prompts and outputs.
4. Externalize decisions into documents.
5. Version contracts and schemas.
6. Close each session with a summary.
7. Avoid long, unstructured conversations.
8. Store authoritative artifacts outside the chat.
9. Reuse prompt templates consistently.
10. Treat ChatGPT as a collaborator, not as memory.
