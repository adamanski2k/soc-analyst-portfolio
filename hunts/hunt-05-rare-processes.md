
---

## `hunts/hunt-05-rare-processes.md`

```md
# Hunt 05 — Rare Processes

## Objective

Identify infrequently observed processes that may deserve review.

---

## Why It Matters

Rare processes can help surface unusual admin tools, attacker tooling, temporary payloads, or renamed binaries.

---

## Data Source

- `DeviceProcessEvents`

---

## KQL

```kql
DeviceProcessEvents
| where TimeGenerated >= ago(7d)
| summarize RunCount = count(), Devices = dcount(DeviceName) by FileName, ProcessCommandLine
| where RunCount <= 3
| sort by RunCount asc
