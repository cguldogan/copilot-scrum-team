---
name: qa-report-backend
description: Backend QA report format with defects (repro steps) and Passed/Failed/Blocked summary.
argument-hint: Provide scope, build/version, endpoints tested, and notes.
agent: qa-agent
#tools: ['agent']
---
Create a backend QA report in this exact format:

### QA Notes
- Scope (stories/endpoints/ACs):
- Environment/assumptions:
- Results:
  - Passed:
  - Failed:
  - Blocked:

### Defects
For each defect:
- Title:
- Steps to reproduce:
- Expected vs Actual:
- Severity (Blocker/Critical/Major/Minor):
- Notes:

### Progress Snapshot
- Done:
- Next / Todo:
- Left:
- Blockers:
