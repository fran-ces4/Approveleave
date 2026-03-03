# Workday Manager: View Pending Time Off Requests

## Overview

This topic lets a manager view pending time-off requests from their direct reports. Data is fetched from Workday's Absence Management API and displayed as a markdown table by the AI.

## Trigger phrases

- "Show me pending time off requests from my team"
- "Who on my team has requested time off?"
- "Review leave requests from my direct reports"
- "Any pending PTO requests from my reports?"

## Files

| File | Description |
|------|-------------|
| `topic.yaml` | Copilot Studio topic definition with conversation flow |
| `msdyn_HRWorkdayAbsenceManagerGetTimeOffRequests.xml` | Workday API template for fetching time-off requests |

## Workday APIs used

| API | Purpose |
|-----|---------|
| `Get_Time_Off_Requests` | Retrieves pending time-off requests for the manager's direct reports |

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
│         Fetch pending requests from Workday                  │
└──────────────────────────┬──────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────┐
│     Parse and merge response into display table              │
└──────────────────────────┬──────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────┐
│    Filter by employee name (if provided)                     │
└──────────────────────────┬──────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────┐
│    AI formats table as markdown for the user                 │
└─────────────────────────────────────────────────────────────┘
```

## Dependencies

- **msdyn_HRWorkdayAbsenceManagerGetTimeOffRequests** template config must be saved in Copilot Studio
- **WorkdayManagerCheck** system topic must be installed
- **WorkdaySystemGetCommonExecution** system topic must be installed
- Manager's org ID must be available via `Global.ESS_UserContext_ManagerOrganizationId`
