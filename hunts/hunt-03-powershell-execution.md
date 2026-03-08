
---

## `hunts/hunt-03-powershell-execution.md`

```md
# Hunt 03 — PowerShell Execution Activity

## Objective

Identify PowerShell execution and determine who launched it, when, and on which system.

---

## Why It Matters

PowerShell is widely used for administration, but it is also commonly abused by attackers for execution, discovery, and download activity.

---

## Data Source

- `DeviceProcessEvents`
- or `SecurityEvent` with process creation logs

---

## KQL

```kql
DeviceProcessEvents
| where TimeGenerated >= ago(24h)
| where FileName =~ "powershell.exe" or FileName =~ "pwsh.exe"
| project TimeGenerated, DeviceName, AccountName, FileName, ProcessCommandLine, InitiatingProcessFileName
| sort by TimeGenerated desc
