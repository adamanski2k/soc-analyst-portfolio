
---

## `labs/windows-telemetry-lab.md`

```md
# Windows Telemetry Lab

## Objective

Validate that Windows telemetry is flowing into the logging platform and that I can use it to answer basic SOC investigation questions.

---

## Lab Setup

- **Host:** `WIN10-LAB`
- **OS:** Windows 10 / Windows 11
- **Role:** Test endpoint
- **Telemetry goal:** Authentication, process creation, PowerShell usage, account activity

---

## Data Sources Used

Examples of useful Windows data sources:

- `SecurityEvent`
- `DeviceProcessEvents`
- `DeviceLogonEvents`
- other Windows security or endpoint telemetry tables available in the lab

---

## Test Activity Performed

To validate telemetry, I generated known activity on the Windows host:

- successful logon
- failed logon
- PowerShell launch
- command execution
- optional local user / group change

---

## Validation Questions

I want to be able to answer:

- Who logged into the system?
- When did the login happen?
- Which host was involved?
- What process was launched?
- Did PowerShell execute?
- Was an account created or modified?

---

## Example Validation Queries

### Failed logons
```kql
SecurityEvent
| where TimeGenerated >= ago(24h)
| where EventID == 4625
| project TimeGenerated, Computer, TargetUserName, IpAddress, LogonType
| sort by TimeGenerated desc
