# SOC Analyst Portfolio — Foundations + Telemetry

This repository documents my first SOC analyst milestone: building a small lab with Windows and Linux telemetry, validating that logs are flowing, and using KQL to investigate activity.

The goal of this milestone is to answer the core SOC questions:

- **What happened?**
- **When did it happen?**
- **Who did it?**
- **Where did it happen?**

---

## Milestone Scope

**Milestone 1 — Foundations + Telemetry Online**  
**Deadline:** Fri, 20 Mar 2026

### Objectives
- Logs flowing from **Windows + Linux**
- Ability to answer: **what happened, when, who, where**
- **10 KQL mini-hunts**
- **KQL cheat sheet**
- **Portfolio structure live**

---

## Repository Structure

```text
soc-analyst-portfolio/
│
├── README.md
├── labs/
│   ├── windows-telemetry-lab.md
│   └── linux-telemetry-lab.md
├── hunts/
│   ├── hunt-01-failed-logons.md
│   ├── hunt-02-success-after-failures.md
│   ├── hunt-03-powershell-execution.md
│   ├── hunt-04-suspicious-powershell.md
│   ├── hunt-05-rare-processes.md
│   ├── hunt-06-account-and-group-changes.md
│   ├── hunt-07-ssh-failures.md
│   ├── hunt-08-ssh-success-after-failures.md
│   ├── hunt-09-sudo-usage.md
│   └── hunt-10-service-restarts.md
├── cheat-sheets/
│   └── kql-cheat-sheet.md
└── screenshots/
