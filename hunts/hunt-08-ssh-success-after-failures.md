
---

## `hunts/hunt-08-ssh-success-after-failures.md`

```md
# Hunt 08 — SSH Success After Failures

## Objective

Determine whether a source IP that failed multiple SSH logins later succeeded.

---

## Why It Matters

This pattern may indicate successful guessing, correct credentials eventually being used, or follow-on access after repeated attempts.

---

## Data Source

- `Syslog`

---

## KQL

```kql
let SSHFails =
    Syslog
    | where TimeGenerated >= ago(24h)
    | where ProcessName =~ "sshd"
    | where SyslogMessage has "Failed password"
    | extend SourceIP = extract(@"\b\d{1,3}(\.\d{1,3}){3}\b", 0, SyslogMessage)
    | summarize FailedCount = count(), LastFailed = max(TimeGenerated) by Computer, SourceIP;
let SSHSuccess =
    Syslog
    | where TimeGenerated >= ago(24h)
    | where ProcessName =~ "sshd"
    | where SyslogMessage has_any ("Accepted password", "Accepted publickey")
    | extend SourceIP = extract(@"\b\d{1,3}(\.\d{1,3}){3}\b", 0, SyslogMessage)
    | project SuccessTime = TimeGenerated, Computer, SourceIP, SyslogMessage;
SSHFails
| join kind=inner SSHSuccess on Computer, SourceIP
| where SuccessTime > LastFailed
| project Computer, SourceIP, FailedCount, LastFailed, SuccessTime, SyslogMessage
| sort by SuccessTime desc
