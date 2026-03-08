
---

## `cheat-sheets/kql-cheat-sheet.md`

```md
# KQL Cheat Sheet — SOC Analyst Foundations

This cheat sheet contains practical KQL patterns I used during my first SOC analyst milestone.

---

## 1) Basic Structure

A typical KQL query looks like this:

```kql
TableName
| where TimeGenerated >= ago(24h)
| project TimeGenerated, Computer, AccountName
| sort by TimeGenerated desc
