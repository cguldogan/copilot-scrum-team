---
name: daily-scrum
description: Run a Daily Scrum and produce meeting notes plus an updated progress snapshot for the sprint.
argument-hint: Provide what changed since last update, PRs/commits, and any blockers.
agent: scrum-master-agent
#tools: ['agent']
---
You are running a Daily Scrum.

Use the input (and any referenced files) to produce:
1) **Daily Scrum Notes**
- Date: ${input:date:YYYY-MM-DD}
- Attendees: ${input:attendees:comma-separated names/agents}
- Sprint Goal: (pull from context if available)
- Yesterday (Done)
- Today (Todo)
- Blockers
- Risks / Dependencies
2) **Updated Sprint Backlog Table**
Columns: Item | Owner | Status (Done/In Progress/Blocked/Left) | Notes/Next step
3) **Action Items**
Each: Owner | Action | Due (if known)

Rules:
- Don’t ask the user to plan; infer and proceed.
- If something is blocked, state exactly what is needed to unblock and who owns it.
