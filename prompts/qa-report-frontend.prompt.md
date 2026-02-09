---
name: qa-report-frontend
description: Frontend QA report format with defects (repro steps) and Passed/Failed/Blocked summary.
argument-hint: Provide scope, build/version, flows tested, and notes.
agent: qa-agent-fe
#tools: ['agent']
---
Create a frontend QA report in this exact format:

### QA Notes
- Scope (stories/flows/screens):
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

### A11y & Responsive Quick Pass
- Keyboard/focus:
- Semantics/ARIA:
- Mobile/tablet/desktop:

### Progress Snapshot
- Done:
- Next / Todo:
- Left:
- Blockers:
