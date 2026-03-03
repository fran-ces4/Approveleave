# Workday Manager: Approve or Deny Time Off Request

## Overview

This topic lets a manager approve or deny a pending time-off request from one of their direct reports. It fetches pending requests from Workday, presents an Adaptive Card form for the manager to make a decision, and submits the result back to Workday.

## Trigger phrases

- "Approve time off for John"
- "Deny Sarah's leave request"
- "Approve the pending PTO request"
- "I want to approve a leave request from my team"

## Files

| File | Description |
|------|-------------|
| `topic.yaml` | Copilot Studio topic definition with conversation flow |
| `msdyn_HRWorkdayAbsenceManagerApproveTimeOff.xml` | Workday API template for approving/denying requests |
| `cards/step1-approval-form.json` | Standalone Adaptive Card for the approval form |
| `cards/step2-confirmation.json` | Standalone Adaptive Card for the confirmation screen |

## Workday APIs used

| API | Purpose |
|-----|---------|
| `Get_Time_Off_Requests` | Retrieves pending requests so the manager can select one |
| `Approve_Or_Deny_Business_Process` | Submits the approval or denial decision |

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
│     Show Adaptive Card form (select request + decision)      │
└──────────────────────────┬──────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────┐
│        Submit approval/denial to Workday                     │
└──────────────────────────┬──────────────────────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────┐
│        Show confirmation card with result                    │
└─────────────────────────────────────────────────────────────┘
```

## Dependencies

- **msdyn_HRWorkdayAbsenceManagerGetTimeOffRequests** template config must be saved (shared with the View topic)
- **msdyn_HRWorkdayAbsenceManagerApproveTimeOff** template config must be saved
- **WorkdayManagerCheck** system topic must be installed
- **WorkdaySystemGetCommonExecution** system topic must be installed
- Manager's org ID must be available via `Global.ESS_UserContext_ManagerOrganizationId`
