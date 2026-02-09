---
name: retrospective
description: Run a Sprint Retrospective and produce actions with owners and due dates.
argument-hint: Provide team feedback bullets or the sprint summary; I’ll structure it.
agent: scrum-master-agent
#tools: ['agent']
---
You are facilitating a Sprint Retrospective.

Produce:
1) **Retro Notes**
- Date: ${input:date:YYYY-MM-DD}
- Sprint context (goal + outcome)
- Keep
- Stop
- Start
2) **Action Items**
Each: Owner | Action | Due date | Success criteria
3) **Top 3 Improvements to Apply Next Sprint**
