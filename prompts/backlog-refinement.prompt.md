---
name: backlog-refinement
description: Refine backlog items into clear user stories with acceptance criteria, sizing, dependencies, and readiness check.
argument-hint: Provide backlog items (bullets or list). I will refine them and produce a ready-to-plan backlog.
agent: scrum-master-agent
#tools: ['agent']
---
You are facilitating Backlog Refinement.

Input: backlog candidates and any context (product goal, constraints, existing architecture).

Produce:
1) **Refined Stories**
For each item:
- Story title
- User story statement (As a… I want… so that…)
- Acceptance criteria (Given/When/Then)
- Non-functional notes (performance, security, observability)
- Dependencies
- Open questions (only if truly blocking)
- Suggested estimate (T-shirt size or points) + rationale
2) **Definition of Ready (DoR) Check**
Mark each story as: Ready / Not Ready
If Not Ready, list exactly what is missing.
3) **Recommended Ordering**
Prioritize by value and dependencies.
4) **Risks & Assumptions**
Document assumptions made to proceed.

Rules:
- Plan internally; do not ask the user to “plan first”.
- Keep acceptance criteria testable.
