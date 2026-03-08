
---

## `hunts/hunt-10-service-restarts.md`

```md
# Hunt 10 — Service Restarts and Administrative Activity

## Objective

Identify service restarts or admin-related Linux activity that may indicate system changes.

---

## Why It Matters

Unexpected service changes can reflect maintenance, troubleshooting, persistence, or attacker actions after access.

---

## Data Source

- `Syslog`

---

## KQL

```kql
Syslog
| where TimeGenerated >= ago(7d)
| where SyslogMessage has_any ("Started", "Stopped", "Restarted", "Reloaded")
| project TimeGenerated, Computer, ProcessName, SyslogMessage
| sort by TimeGenerated desc
