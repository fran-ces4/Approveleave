# Topic Buddy – Manager Scenarios

Copilot Studio topic definitions and Adaptive Card samples for Workday Manager Self-Service scenarios.

## Getting started

1. Install the recommended VS Code extensions (see below)
2. Clone this repo
3. Open in VS Code — Copilot will automatically pick up conventions from `.github/copilot-instructions.md`
4. Create a branch for your scenario: `git checkout -b scenario/<your-scenario-name>`
5. Add your scenario folder under `ManagerScenarios/`
6. Open a PR when ready for review

## Recommended VS Code extensions

| Extension | Purpose |
|---|---|
| [Adaptive Card Previewer](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vscode-adaptive-cards) | Preview card JSON files directly in VS Code |
| [YAML](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml) | Syntax highlighting and validation for `topic.yaml` files |

## Folder structure

```
ManagerScenarios/
├── WorkdayManagerViewInboxTasks/
│   ├── topic.yaml
│   ├── msdyn_HRWorkdayWorkflowManagerGetInboxTasks.xml
│   └── README.md
└── WorkdayManagerApproveTimeOff/
    ├── topic.yaml
    ├── msdyn_HRWorkdayAbsenceManagerApproveTimeOff.xml
    ├── cards/
    │   ├── step1-approval-form.json
    │   └── step2-confirmation.json
    └── README.md
```

## Testing cards

Paste any file from a scenario's `cards/` folder into the [Adaptive Card Designer](https://adaptivecards.io/designer/) to preview it. Card files use static sample data in place of Power Fx expressions.

## Deploying a topic to Copilot Studio

### 1. Upload XML templates

For each XML file in the scenario folder:
1. Open the Employee Self-Service agent in Copilot Studio
2. Go to **Solutions → Default → New → More → Other → Employee Self-Service Template Configuration**
3. Fill in the form:
   - **Name**: a human-readable label
   - **Unique name**: must match the `<request>` value in the XML (e.g., `msdyn_HRWorkdayAbsenceManagerApproveTimeOff`)
   - **Value**: paste the entire XML file contents
4. Select **Save and close** — repeat for each XML file

### 2. Import the topic

1. In Copilot Studio, go to the **Topics** tab
2. Select **+ Add a topic → From blank**
3. Select **More → Open code editor** (top-right)
4. Paste the full contents of `topic.yaml` and save

### 3. Configure Workday permissions

Work with your Workday admin to grant the required security domain permissions. Consult the [Workday extensibility article](https://learn.microsoft.com/en-us/copilot/microsoft-365/employee-self-service/workday-extensibility) for guidance.

### 4. Test in Copilot Studio

Use the built-in **Test** panel with trigger phrases from the scenario's `README.md`.

## Conventions

See [`.github/copilot-instructions.md`](.github/copilot-instructions.md) for the full set of authoring conventions. Key points:

- Scenario folders: `WorkdayManager<ScenarioName>`
- `scenarioName` values: `msdyn_HRWorkday<Domain><Action>`
- All card text in **sentence case**
- Prefer `FactSet` over `Table` for key-value summaries
- Always handle API errors with `AnswerQuestionWithAI` + retry loop
- Always initialize variables with `SetVariable` before using them in conditions
