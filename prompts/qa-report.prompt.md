---
name: qa-report
description: Standard QA report format with defects (repro steps) and Passed/Failed/Blocked summary.
argument-hint: Provide scope, build/version, and test notes.
agent: scrum-master-agent
---
Create a QA report in this exact format:

### QA Notes
- Scope:
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
- Severity (Blocker/Major/Minor):
- Notes:

### Progress Snapshot
- Done:
- Next / Todo:
- Left:
- Blockers:
