
---

## `hunts/hunt-09-sudo-usage.md`

```md
# Hunt 09 — Sudo Usage

## Objective

Identify when elevated Linux privileges were used and by whom.

---

## Why It Matters

Privilege use is important during investigations because it may show administrative changes, escalation, or post-login activity.

---

## Data Source

- `Syslog`

---

## KQL

```kql
Syslog
| where TimeGenerated >= ago(7d)
| where ProcessName =~ "sudo"
| project TimeGenerated, Computer, SyslogMessage
| sort by TimeGenerated desc
