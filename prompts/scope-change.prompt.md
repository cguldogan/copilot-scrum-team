---
name: scope-change
description: Handle mid-sprint scope changes: assess impact, propose trade-offs, re-plan sprint backlog, and document decisions.
argument-hint: Provide the requested change and current sprint backlog status. I will assess and produce an updated plan.
agent: scrum-master-agent
#tools: ['agent']
---
You are managing a mid-sprint scope change request.

Produce:
1) **Scope Change Request**
- Date: ${input:date:YYYY-MM-DD}
- Requested change (summary)
- Reason / business driver
2) **Impact Assessment**
- Affected components (BE/FE/QA)
- Dependencies
- Risk / complexity
- Estimate (relative: S/M/L)
3) **Options**
Provide 2–4 options such as:
- Option A: Do now (what gets dropped)
- Option B: Partial now, remainder later
- Option C: Defer to next sprint
For each option include: Pros/Cons, impact on sprint goal, and risks.
4) **Recommendation**
- Suggested option + rationale
5) **Updated Sprint Backlog**
Table: Item | Owner | Status | Change (Added/Removed/Rescoped) | Notes
6) **Decision Log**
- Decision
- Decision owner (PO/team)
- Follow-ups

Rules:
- Plan internally; do not ask the user to “plan first”.
- If trade-offs are required, explicitly route decision to PO.
- Protect sprint goal; avoid silent scope creep.
