
---

## `hunts/hunt-04-suspicious-powershell.md`

```md
# Hunt 04 — Suspicious PowerShell Command Lines

## Objective

Look for PowerShell commands with suspicious arguments such as encoded commands, hidden windows, or execution bypass.

---

## Why It Matters

Attackers often use suspicious PowerShell flags to avoid detection or to run payloads more easily.

---

## Data Source

- `DeviceProcessEvents`
- or `SecurityEvent`

---

## KQL

```kql
DeviceProcessEvents
| where TimeGenerated >= ago(7d)
| where FileName =~ "powershell.exe" or FileName =~ "pwsh.exe"
| where ProcessCommandLine has_any ("-enc", "-encodedcommand", "bypass", "downloadstring", "iex", "invoke-expression", "hidden")
| project TimeGenerated, DeviceName, AccountName, ProcessCommandLine, InitiatingProcessFileName
| sort by TimeGenerated desc
