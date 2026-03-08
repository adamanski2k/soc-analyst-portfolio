
---

## `hunts/hunt-07-ssh-failures.md`

```md
# Hunt 07 — SSH Failures by Source IP

## Objective

Identify repeated failed SSH authentication attempts and group them by source IP.

---

## Why It Matters

Repeated SSH failures can indicate brute force attempts, password guessing, or poor credential hygiene.

---

## Data Source

- `Syslog`

---

## KQL

```kql
Syslog
| where TimeGenerated >= ago(24h)
| where ProcessName =~ "sshd"
| where SyslogMessage has "Failed password"
| extend SourceIP = extract(@"\b\d{1,3}(\.\d{1,3}){3}\b", 0, SyslogMessage)
| summarize Failures = count() by Computer, SourceIP
| sort by Failures desc
