
---

## `hunts/hunt-01-failed-logons.md`

```md
# Hunt 01 — Failed Windows Logons

## Objective

Identify repeated failed Windows logon attempts that may indicate brute force, password spraying, or repeated authentication errors.

---

## Why It Matters

Repeated failed logons may indicate an attacker attempting to gain access, or a misconfigured system repeatedly trying bad credentials.

---

## Data Source

- `SecurityEvent`

---

## KQL

```kql
SecurityEvent
| where TimeGenerated >= ago(24h)
| where EventID == 4625
| summarize FailedLogons = count() by Account = TargetUserName, Computer, IpAddress
| sort by FailedLogons desc
