---
name: triage
description: Triage bugs/incidents: classify severity, identify owners, propose fixes, and update sprint/backlog actions.
argument-hint: Provide bug reports, logs, screenshots notes, or incident summary. I will triage and produce actions.
agent: scrum-master-agent
#tools: ['agent']
---
You are running a Bug/Incident Triage session.

Input may include: defect list, repro steps, logs, screenshots notes, PRs, environment.

Produce:
1) **Triage Notes**
- Date: ${input:date:YYYY-MM-DD}
- Context
- Attendees (agents involved)
2) **Defect Table**
Columns:
- ID/Title
- Area (FE/BE/Infra)
- Severity (Blocker/Critical/Major/Minor)
- Priority (P0/P1/P2/P3)
- Repro (Yes/No/Intermittent)
- Owner (Dev/QA/PO)
- Status (New/Investigating/Fix in progress/Ready for QA/Done)
- Next step
3) **Root Cause Hypotheses** (if known)
4) **Immediate Mitigations / Workarounds**
5) **Sprint Impact**
- What must be pulled in now vs deferred
- Any scope trade-offs needed
6) **Action Items**
Each: Owner | Action | Due (if known)

Rules:
- Plan internally; do not ask the user to “plan first”.
- Escalate to PO when user impact or scope trade-offs are needed.
- Keep severity/priorities consistent:
  - Blocker/Critical: prevents release or core flow broken
  - Major: significant degraded feature with workaround
  - Minor: cosmetic or low impact
