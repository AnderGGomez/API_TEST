# Copilot Instructions for BDD API Testing & Documentation Agent

## Project Context
This workspace is a specialized BDD (Behavior Driven Development) environment for API testing. It operates in two distinct modes based on the user's intent: **Execution** or **Documentation**.

- **Source of Truth**: API definitions are located in `resource/precreditCore.json`, `resource/precreditList.json`, `resource/precreditPreFlows.json`, `resource/precreditProduct.json` and `resource/precreditPayment.json`.
- **Behavior Definitions**: The agent's behavior is strictly governed by prompts in `.github/prompts/`.

## Operational Modes

### 1. Execution Mode (The "Engine")
**Trigger**: User asks to "run tests", "execute scenarios", or provides Gherkin syntax (Given/When/Then) for execution.
**Source**: Follow logic in `.github/prompts/api_test.prompt.md`.

*   **Goal**: Orchestrate technical execution of steps.
*   **Tools**:
    *   `rest-api/*`: For HTTP requests (When steps).
    *   `postgres/*`: For database validation (Given/Then steps).
    *   `edit/createFile`: **ONLY** for temporary dummy files required by upload tests.
*   **Critical Rules**:
    *   ❌ **NEVER** generate report files (.md, .json) in this mode.
    *   ✅ **ALWAYS** output execution logs directly in the chat (e.g., "🚀 Executing...", "✅ PASSED").
    *   ✅ **ALWAYS** validate data persistence using SQL queries when the scenario implies it.

### 2. Documentation Mode (The "Generator")
**Trigger**: User asks to "generate report", "create postman collection", or "document scenarios".
**Source**: Follow logic in `.github/prompts/report.prompt.md`.

*   **Goal**: Create static artifacts for delivery.
*   **Tools**: `edit/createFile` (Primary tool).
*   **Outputs**:
    *   `execution_report.md`: Detailed coverage report.
    *   `postman_collection.json`: Postman v2.1 collection with `pm.test()` scripts derived from Gherkin.
*   **Critical Rules**:
    *   ❌ **NEVER** execute live API calls in this mode.
    *   ✅ **ALWAYS** create physical files in the workspace root.
    *   ✅ **ALWAYS** map Gherkin "Then" steps to JavaScript assertions in Postman.

## Common Workflows

### Analysis Phase (Required for both modes)
Before acting, always:
<<<<<<< HEAD
1.  Read `resource/precreditCore.json`, `resource/precreditList.json`, `resource/precreditPreFlows.json`,`resource/precreditProduct.json` and `resource/precreditPayment.json`.
=======
1.  Read `resource/precreditCore.json`, `resource/precreditList.json`, `resource/precreditPreFlows.json` and `resource/precreditPayment.json`.
>>>>>>> 9bde5c4893bb29777c6711bb1e6e3be48eb1266f
2.  Map the user's Gherkin terms (e.g., "Service X") to the actual endpoints/methods in the JSON files.

### Database Interaction
- The project uses PostgreSQL.
- Use `dbhub-postgres-npx/execute_sql` to verify preconditions ("Given exists...") or postconditions ("Then record should exist...").

## File Structure
```
.github/prompts/
  ├── api_test.prompt.md    # Rules for Execution Mode
  └── report.prompt.md      # Rules for Documentation Mode
resource/
  ├── precreditCore.json    # API Definition 1
  └── precreditList.json    # API Definition 2
```
