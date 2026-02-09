---
name: definition-of-ready
description: Evaluate whether stories are ready for sprint planning using a Definition of Ready checklist; output gaps and actions.
argument-hint: Provide stories (titles + brief). I will run a DoR check and produce gaps/actions.
agent: scrum-master-agent
#tools: ['agent']
---
Run a Definition of Ready (DoR) check.

For each story, output:
- Ready? (Yes/No)
- Missing info (if any)
- Actions to make it ready (owner suggestions: PO/Dev/QA)
- Risks if pulled into sprint as-is

Use this DoR checklist (unless overridden):
- Clear user value
- Testable acceptance criteria
- Dependencies identified
- UX notes/screens if applicable
- API contract expectations if applicable
- Data/model impacts identified
- Non-functional requirements noted (security/perf/observability)
- Sizing is feasible within sprint capacity
- QA approach identified

Also output:
- **Top blockers across stories**
- **Recommended next refinement actions**
