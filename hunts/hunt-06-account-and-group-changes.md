
---

## `hunts/hunt-06-account-and-group-changes.md`

```md
# Hunt 06 — Account and Group Changes

## Objective

Identify account creation, account changes, and group membership modifications.

---

## Why It Matters

Unexpected account or privilege changes may indicate persistence, privilege escalation, or unauthorized administration.

---

## Data Source

- `SecurityEvent`

---

## KQL

```kql
SecurityEvent
| where TimeGenerated >= ago(7d)
| where EventID in (4720, 4722, 4724, 4728, 4732, 4735)
| project TimeGenerated, Computer, EventID, SubjectUserName, TargetUserName, Activity
| sort by TimeGenerated desc
