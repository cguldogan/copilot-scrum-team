---
name: release-notes
description: Generate release notes and a deployment checklist from completed work (PRs/commits/issues) in a Scrum sprint or release.
argument-hint: Provide completed stories/tasks/PR links and target version/date. I will produce release notes + checklist.
agent: scrum-master-agent
#tools: ['agent']
---
Generate release notes suitable for sharing with stakeholders.

Produce:
1) **Release Summary**
- Version / release name
- Date: ${input:date:YYYY-MM-DD}
- Sprint/release goal
2) **What’s New**
Bulleted list grouped by theme (UX, API, Performance, Security, etc.)
3) **Fixes**
Bulleted list
4) **Known Issues / Limitations**
Bulleted list
5) **Upgrade / Migration Notes**
DB migrations, config changes, feature flags
6) **Deployment Checklist**
- Pre-deploy
- Deploy
- Post-deploy verification
7) **Rollback Plan (high level)**

Rules:
- Be clear, non-technical where possible, but include technical notes when needed for operators.
