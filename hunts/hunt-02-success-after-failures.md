
---

## `hunts/hunt-02-success-after-failures.md`

```md
# Hunt 02 — Successful Logon After Multiple Failures

## Objective

Determine whether a successful logon occurred shortly after repeated failed attempts.

---

## Why It Matters

This pattern can suggest account compromise, successful guessing, or eventual correct use of credentials after multiple failures.

---

## Data Source

- `SecurityEvent`

---

## KQL

```kql
let Failed =
    SecurityEvent
    | where TimeGenerated >= ago(24h)
    | where EventID == 4625
    | summarize FailedCount = count(), LastFailed = max(TimeGenerated) by TargetUserName, IpAddress, Computer;
let Success =
    SecurityEvent
    | where TimeGenerated >= ago(24h)
    | where EventID == 4624
    | project SuccessTime = TimeGenerated, TargetUserName, IpAddress, Computer, LogonType;
Failed
| join kind=inner Success on TargetUserName, IpAddress, Computer
| where SuccessTime > LastFailed
| project TargetUserName, IpAddress, Computer, FailedCount, LastFailed, SuccessTime, LogonType
| sort by SuccessTime desc
