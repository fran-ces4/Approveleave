# Workday Manager: View Inbox Tasks

## Overview

This topic lets a manager view all actionable tasks in their Workday inbox. Tasks include absence requests, benefits changes, organization assignments, Workday account edits, and any other business processes awaiting the manager's action.

## Trigger phrases

- "Show me my inbox tasks"
- "What tasks are waiting for me?"
- "Show my pending tasks"
- "Any items in my Workday inbox?"
- "What needs my attention?"
- "Show tasks for John"

## Files

| File | Description |
|------|-------------|
| `topic.yaml` | Copilot Studio topic definition with conversation flow |
| `msdyn_HRWorkdayWorkflowManagerGetInboxTasks.xml` | Workday API template for fetching all inbox tasks |

## Workday APIs used

| API | Service | Purpose |
|-----|---------|---------|
| `Get_Inbox_Tasks` | Workflow | Retrieves all actionable inbox tasks for the manager |

## Task types returned

Based on the Workday inbox, this topic will display tasks such as:
- **Absence requests** — time-off requests from direct reports
- **Change benefits** — benefits enrollment or personal info changes
- **Edit Workday account** — account modification requests
- **Change organization assignments** — org structure changes

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
│         Fetch all inbox tasks from Workday                   │
└──────────────────────────┬──────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────┐
│     Parse and merge response into display table              │
└──────────────────────────┬──────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────┐
│    Filter by subject name (if provided)                      │
└──────────────────────────┬──────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────┐
│    AI formats table as markdown for the user                 │
└─────────────────────────────────────────────────────────────┘
```

## Dependencies

- **msdyn_HRWorkdayWorkflowManagerGetInboxTasks** template config must be saved in Copilot Studio
- **WorkdayManagerCheck** system topic must be installed
- **WorkdaySystemGetCommonExecution** system topic must be installed
- Manager's employee ID must be available via `Global.ESS_UserContext_Employee_Id`

## ⚠️ Admin verification required

The `Get_Inbox_Tasks` API and its response XPaths may vary by Workday tenant. Your Workday admin should verify:
1. The Workflow service is enabled
2. The ISU has "View Inbox" permissions for the relevant business processes
3. The response XPaths in the XML template match your tenant's actual response structure
