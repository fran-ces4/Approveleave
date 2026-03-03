# Workday Manager: Act on Inbox Task

## Overview

This topic lets a manager approve, deny, or send back any inbox task from their Workday inbox. It fetches all pending tasks (absence requests, benefits changes, org assignments, etc.), presents an Adaptive Card form for the manager to choose an action, and submits the result back to Workday.

## Trigger phrases

- "Approve the task for John"
- "Deny the benefits change"
- "Send back the absence request"
- "I want to approve a task from my inbox"
- "Approve the pending request"

## Files

| File | Description |
|------|-------------|
| `topic.yaml` | Copilot Studio topic definition with conversation flow |
| `msdyn_HRWorkdayBusinessProcessManagerActOnTask.xml` | Workday API template for acting on any business process |
| `cards/step1-approval-form.json` | Standalone Adaptive Card for the action form |
| `cards/step2-confirmation.json` | Standalone Adaptive Card for the confirmation screen |

## Workday APIs used

| API | Purpose |
|-----|---------|
| `Get_Inbox_Tasks` (Workflow service) | Retrieves all inbox tasks so the manager can select one |
| `Approve_Or_Deny_Business_Process` (Staffing service) | Submits the approve, deny, or send back action |

## Flow

```
┌─────────────────────────────────────────────────────────────┐
│                    User triggers topic                       │
└──────────────────────────┬──────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────┐
│              Verify user is a manager                        │
└──────────────────────────┬──────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────┐
│         Fetch inbox tasks from Workday                       │
└──────────────────────────┬──────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────┐
│   Show Adaptive Card form (select task + action)             │
└──────────────────────────┬──────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────┐
│      Submit approve / deny / send back to Workday            │
└──────────────────────────┬──────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────┐
│        Show confirmation card with result                    │
└─────────────────────────────────────────────────────────────┘
```

## Dependencies

- **msdyn_HRWorkdayWorkflowManagerGetInboxTasks** template config must be saved (shared with the View Inbox Tasks topic)
- **msdyn_HRWorkdayBusinessProcessManagerActOnTask** template config must be saved
- **WorkdayManagerCheck** system topic must be installed
- **WorkdaySystemGetCommonExecution** system topic must be installed
- Manager's employee ID must be available via `Global.ESS_UserContext_Employee_Id`
