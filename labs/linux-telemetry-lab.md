
---

## `labs/linux-telemetry-lab.md`

```md
# Linux Telemetry Lab

## Objective

Validate that Linux telemetry is flowing into the logging platform and that I can use it to investigate authentication and administrative activity.

---

## Lab Setup

- **Host:** `UBUNTU-LAB`
- **OS:** Ubuntu / other Linux distribution
- **Role:** Test Linux endpoint
- **Telemetry goal:** SSH activity, auth logs, sudo usage, service activity

---

## Data Sources Used

Examples of useful Linux data sources:

- `Syslog`
- auth logs
- endpoint or agent tables available in the lab

---

## Test Activity Performed

To validate telemetry, I generated known Linux activity:

- failed SSH login
- successful SSH login
- `sudo` command
- service restart
- optional user or admin activity

---

## Validation Questions

I want to be able to answer:

- Who attempted to log in?
- Which source IP was involved?
- When did the login happen?
- Which host was targeted?
- Who used sudo?
- Were services restarted?

---

## Example Validation Queries

### SSH failures
```kql
Syslog
| where TimeGenerated >= ago(24h)
| where ProcessName =~ "sshd"
| where SyslogMessage has "Failed password"
| project TimeGenerated, Computer, SyslogMessage
| sort by TimeGenerated desc
