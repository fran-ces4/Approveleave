# Copilot instructions for Workday Copilot Studio scenarios

This repo contains Copilot Studio topic definitions and Adaptive Card samples for Workday Manager Self-Service scenarios.

## Topic YAML conventions

- Each scenario lives in its own folder under `ManagerScenarios/`, e.g. `WorkdayManagerApproveTimeOff/`.
- The main file is always `topic.yaml` using `kind: AdaptiveDialog`.
- `inputs` block comes before `modelDescription`.
- Use `intent: {}` (empty object), not `triggerQueries`.
- Use `CancelAllDialogs` instead of `EndDialog`.
- Use snake_case for node IDs (e.g., `check_manager_status`).
- Reuse the shared execution wrapper for all Workday API calls:
  ```yaml
  dialog: msdyn_copilotforemployeeselfservice.topic.WorkdaySystemGetCommonExecution
  ```
  The correct solution prefix is `msdyn_copilotforemployeeselfservice` (no `hr` suffix). Using `msdyn_copilotforemployeeselfservicehr` will cause "Selected topic is no longer available" errors.
- The `WorkdaySystemGetCommonExecution` dialog accepts two inputs (`parameters`: String, `scenarioName`: String) and returns three outputs (`errorResponse`: String, `isSuccess`: Boolean, `workdayResponse`: String).
- Follow the scenario naming pattern for `scenarioName` values:
  `msdyn_HRWorkday<Domain><Action>` — e.g. `msdyn_HRWorkdayAbsenceManagerApproveTimeOff`.
- Always identify the manager via `Global.ESS_UserContext_ManagerOrganizationId`.
- **Always initialize variables with `SetVariable` before using them in conditions**, even if the value will be overwritten by a `BeginDialog` output binding. Initialize booleans to `=false` and strings to `=""`.
- Reference `BeginDialog` output variables only inside the `ConditionGroup` branch that checks them — not before the condition.
- Use `AnswerQuestionWithAI` to humanize Workday error messages before showing them to the user.
- On API failure, always offer a retry using `Question` with `BooleanPrebuiltEntity` + `GotoAction`.

## Adaptive Card conventions

- All card text (headings, labels, button titles) must use **sentence case**.
- Text size conventions:
  - **Headings**: `"size": "Medium"` with `"weight": "Bolder"`
  - **Body text**: default size (omit the `size` property)
  - **Secondary text** (hints, captions): `"size": "Small"`
- Use `FactSet` for key-value data summaries. Only use `Table` when `FactSet` cannot provide the needed layout.
- **Input cards** use `AdaptiveCardPrompt` with `output`/`outputType` bindings and `actions: []` at top level (buttons inside `ActionSet` in the body).
- **Display-only cards** use `SendActivity` with `attachments` > `AdaptiveCardTemplate`.
- Include `'$schema': "http://adaptivecards.io/schemas/adaptive-card.json"` in all cards.
- Use `label` property on inputs instead of separate `TextBlock` headers.
- Cards extracted as standalone test files go in a `cards/` subfolder, prefixed with their step number: `step1-`, `step2-`, etc.
- Standalone card files use static sample data in place of Power Fx expressions.

## Trigger phrases

Write trigger phrases in plain, natural manager language (e.g. "Approve time off for John", "Show me my team's pending requests").
