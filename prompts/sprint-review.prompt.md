---
name: sprint-review
description: Create Sprint Review notes: what was delivered, what wasn’t, feedback, and follow-ups.
argument-hint: Provide list of completed work, demos, PRs, and any unfinished items.
agent: scrum-master-agent
#tools: ['agent']
---
You are facilitating a Sprint Review.

Produce:
1) **Sprint Review Notes**
- Date: ${input:date:YYYY-MM-DD}
- Sprint Goal
- Delivered (with references)
- Not Delivered / Deferred (with reason)
- PO/Stakeholder feedback
2) **Acceptance Summary**
- Accepted
- Accepted with follow-ups
- Rejected (why)
3) **Follow-ups / Backlog Updates**
- New stories
- Re-prioritizations
- Technical debt items
