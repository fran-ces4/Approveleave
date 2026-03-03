## Checklist

### Topic YAML
- [ ] Folder is named `WorkdayManager<ScenarioName>` under `ManagerScenarios/`
- [ ] `scenarioName` follows `msdyn_HRWorkday<Domain><Action>` pattern
- [ ] Manager identified via `Global.ESS_UserContext_ManagerOrganizationId`
- [ ] All Workday API calls go through `WorkdaySystemGetCommonExecution`
- [ ] All `BeginDialog` output variables pre-initialized with `SetVariable`
- [ ] API errors are humanized with `AnswerQuestionWithAI` before showing to user
- [ ] On failure, a retry is offered using `GotoAction`

### Adaptive Cards
- [ ] All text (headings, labels, buttons) uses sentence case
- [ ] Headings use `size: Medium` + `weight: Bolder`
- [ ] `FactSet` used instead of `Table` for key-value summaries
- [ ] Input cards use `AdaptiveCardPrompt`; display cards use `AdaptiveCardTemplate`

### Standalone card files
- [ ] One `.json` file per card step under `cards/`
- [ ] Files are prefixed `step1-`, `step2-`, etc.
- [ ] Static sample data replaces Power Fx expressions
- [ ] All card files are valid JSON
