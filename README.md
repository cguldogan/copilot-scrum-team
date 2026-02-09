# Copilot Scrum Team

A complete **Scrum team powered by GitHub Copilot custom agents and reusable prompts**. This project provides a set of specialized AI agents that mirror real Scrum roles — Scrum Master, Product Owner, Backend Developer, Frontend Developer, and QA — along with prompt templates for every major Scrum ceremony and workflow.

Drop these files into any repository and get a fully coordinated AI Scrum team inside VS Code.

## Overview

```
┌─────────────────────────────────────────────────────────┐
│                   Scrum Master Agent                    │
│            (coordination + sprint artifacts)            │
├──────────┬──────────┬──────────┬──────────┬─────────────┤
│ Product  │ Backend  │ Frontend │ Backend  │  Frontend   │
│  Owner   │   Dev    │   Dev    │   QA     │    QA       │
│  Agent   │  Agent   │  Agent   │  Agent   │   Agent     │
└──────────┴──────────┴──────────┴──────────┴─────────────┘
```

Agents hand off work to each other automatically — the Scrum Master coordinates, Dev agents implement, QA agents validate, and the Product Owner accepts or rejects increments.

## Repository Structure

```
├── copilot-instructions.md          # Global working agreement for all agents
├── agents/
│   ├── scrum-master-agent.agent.md  # Scrum Master & Delivery Coordinator
│   ├── product-owner-agent.agent.md # Product Owner (priorities + acceptance)
│   ├── development-agent-backend.agent.md   # Backend Developer
│   ├── development-agent-frontend.agent.md  # Frontend Developer
│   ├── qa-agent.agent.md            # Backend QA
│   └── qa-agent-fe.agent.md         # Frontend QA
├── prompts/
│   ├── sprint-planning.prompt.md    # Sprint Planning ceremony
│   ├── daily-scrum.prompt.md        # Daily Scrum / standup
│   ├── sprint-review.prompt.md      # Sprint Review ceremony
│   ├── retrospective.prompt.md      # Sprint Retrospective
│   ├── backlog-refinement.prompt.md # Backlog Refinement session
│   ├── definition-of-ready.prompt.md# Definition of Ready check
│   ├── triage.prompt.md             # Bug / Incident Triage
│   ├── scope-change.prompt.md       # Mid-sprint Scope Change handling
│   ├── release-notes.prompt.md      # Release Notes + Deployment Checklist
│   ├── dev-status-update.prompt.md  # Generic dev status update
│   ├── dev-status-update-backend.prompt.md  # Backend dev status update
│   ├── dev-status-update-frontend.prompt.md # Frontend dev status update
│   ├── qa-report.prompt.md          # Generic QA report
│   ├── qa-report-backend.prompt.md  # Backend QA report
│   └── qa-report-frontend.prompt.md # Frontend QA report
└── README.md
```

## Agents

### Scrum Master Agent

The central coordinator. Facilitates all Scrum ceremonies, maintains sprint artifacts (goal, backlog, progress snapshots, blockers), and orchestrates handoffs between Dev, QA, and PO agents.

**Handoffs to:** Backend Dev, Frontend Dev, Backend QA, Frontend QA, Product Owner

### Product Owner Agent

Clarifies requirements, prioritizes the backlog, writes acceptance criteria, and accepts or rejects sprint increments. Routes decisions back to the Scrum Master for coordination.

**Handoffs to:** Scrum Master

### Backend Development Agent

Implements backend features — APIs, services, data layers, and integrations. Focuses on correctness, security, scalability, and maintainability. Reports dev notes with testing instructions for QA.

**Model:** Claude Sonnet 4.5 | **Handoffs to:** Backend QA, Scrum Master

### Frontend Development Agent

Implements frontend features — React/UI flows with attention to usability, accessibility, responsiveness, and performance. Always implements loading, error, and empty states.

**Model:** Claude Sonnet 4.5 | **Handoffs to:** Frontend QA, Scrum Master

### Backend QA Agent

Validates backend increments: API correctness, auth/authz, validation, error handling, and regression. Reports defects with repro steps and severity classification.

**Model:** Claude Sonnet 4.5 | **Handoffs to:** Scrum Master, Backend Dev (escalation)

### Frontend QA Agent

Validates frontend increments: user flows, accessibility, responsiveness, and error/loading states. Includes A11y and responsive quick-pass checks in every report.

**Model:** Claude Sonnet 4.5 | **Handoffs to:** Scrum Master, Frontend Dev (escalation)

## Prompt Templates

Reusable prompt files for common Scrum ceremonies and workflows. Each prompt is pre-wired to the appropriate agent.

| Prompt | Description | Agent |
|--------|-------------|-------|
| **Sprint Planning** | Goal, scope, stories/tasks, dependencies, handoffs | Scrum Master |
| **Daily Scrum** | Standup notes + updated sprint backlog table | Scrum Master |
| **Sprint Review** | Delivered vs deferred, acceptance summary, follow-ups | Scrum Master |
| **Retrospective** | Keep/Stop/Start + action items with owners | Scrum Master |
| **Backlog Refinement** | Refine items into stories with ACs, sizing, DoR check | Scrum Master |
| **Definition of Ready** | DoR checklist evaluation with gaps and actions | Scrum Master |
| **Triage** | Bug/incident classification, severity, owners, sprint impact | Scrum Master |
| **Scope Change** | Impact assessment, trade-off options, updated backlog | Scrum Master |
| **Release Notes** | What's new, fixes, known issues, deployment checklist | Scrum Master |
| **Dev Status Update** | Done/Next/Left/Blockers + testing notes | Scrum Master |
| **Dev Status (Backend)** | Backend-specific status with curl/test examples | Backend Dev |
| **Dev Status (Frontend)** | Frontend-specific status with a11y/responsive notes | Frontend Dev |
| **QA Report** | Passed/Failed/Blocked + defect list | Scrum Master |
| **QA Report (Backend)** | Backend QA with endpoint-level results | Backend QA |
| **QA Report (Frontend)** | Frontend QA with a11y & responsive quick pass | Frontend QA |

## Workflows — How to Run Scrum with These Prompts

Below are step-by-step workflows for the most common scenarios. Each step references a prompt you can run directly in Copilot Chat.

---

### 1. Starting a New Project

When you're kicking off a brand-new project and want to go from idea to first sprint:

| Step | Prompt to Use | What You Provide | What You Get |
|------|--------------|-------------------|--------------|
| **1** | **Backlog Refinement** | Raw feature ideas, product goals, constraints | Refined user stories with acceptance criteria, sizing, and DoR check |
| **2** | **Definition of Ready** | The refined stories from step 1 | Readiness checklist — which stories are sprint-ready and what's missing |
| **3** | **Sprint Planning** | Sprint goal, ready stories, team capacity | Sprint backlog with tasks, dependencies, sequencing, and handoff briefs for Dev/QA/PO |
| **4** | Start building | Mention `@development-agent-backend` or `@development-agent-frontend` with a task | Code implementation with dev notes and testing instructions |

> **Tip:** You don't need all your ideas perfectly formed. Paste rough bullets into Backlog Refinement and the agent will structure everything for you.

---

### 2. Running a Sprint (Day-to-Day)

Once a sprint is underway, use this daily loop:

| Step | Prompt to Use | When | What You Provide |
|------|--------------|------|-------------------|
| **1** | **Daily Scrum** | Every day / session start | What changed since last update, PRs/commits, blockers |
| **2** | **Dev Status Update** (or Backend/Frontend variant) | After completing work | What you worked on, what's next, blockers |
| **3** | **QA Report** (or Backend/Frontend variant) | After testing | Scope, build/version, test results |
| **4** | **Triage** | When bugs surface | Bug reports, logs, repro steps |
| **5** | **Scope Change** | When priorities shift mid-sprint | The requested change + current sprint status |

**Example flow for a typical day:**
1. Run **Daily Scrum** to get an updated sprint backlog and surface blockers.
2. Ask `@development-agent-backend` to implement the next task — it will produce code + dev notes.
3. Run **QA Report (Backend)** to validate the increment — the QA agent runs tests and reports defects.
4. If a bug is found, run **Triage** to classify severity and decide on immediate action.
5. Run **Dev Status Update** to record progress before ending the session.

---

### 3. Handling Bugs and Incidents

When something breaks or a defect is reported:

| Step | Prompt to Use | What Happens |
|------|--------------|--------------|
| **1** | **Triage** | Classify severity & priority, identify owners, propose root cause hypotheses and mitigations |
| **2** | **Scope Change** *(if needed)* | Assess sprint impact, propose trade-offs (what gets dropped to fix the bug), get PO decision |
| **3** | **Dev Status Update** | Track fix progress with testing instructions for QA |
| **4** | **QA Report** | Verify the fix, confirm regression coverage |

---

### 4. Closing a Sprint

At the end of a sprint, run these ceremonies in order:

| Step | Prompt to Use | What You Provide | What You Get |
|------|--------------|-------------------|--------------|
| **1** | **Sprint Review** | Completed work, PRs, demos, unfinished items | Delivered vs deferred summary, PO acceptance decisions, follow-up stories |
| **2** | **Retrospective** | Team feedback, what went well/poorly | Keep/Stop/Start analysis, action items with owners and due dates |
| **3** | **Release Notes** *(if releasing)* | Completed stories, PRs, target version | Stakeholder-ready release notes + deployment checklist + rollback plan |

---

### 5. Backlog Refinement Session

Run this anytime you need to prepare stories for an upcoming sprint:

1. **Backlog Refinement** — Paste raw ideas, feature requests, or tech debt items. The agent produces structured stories with acceptance criteria, sizing, and dependencies.
2. **Definition of Ready** — Run the DoR check on the refined stories to confirm they're sprint-ready. The agent flags gaps and suggests actions to close them.

> **Tip:** Run refinement regularly (not just before planning) to keep a healthy backlog of ready stories.

---

### 6. Mid-Sprint Scope Change

When a stakeholder requests a change or new urgent work appears:

1. **Scope Change** — Provide the requested change and current sprint status. The agent assesses impact, proposes 2–4 options with trade-offs, and recommends one.
2. **Daily Scrum** — After the decision, run a standup to update the sprint backlog and communicate changes.

---

### 7. Preparing a Release

When you're ready to ship:

1. **QA Report** — Final validation pass across backend and frontend.
2. **Sprint Review** — Get PO sign-off on delivered increments.
3. **Release Notes** — Generate stakeholder-facing notes, deployment checklist, and rollback plan.

---

### Quick Reference: Which Prompt for What?

| I want to… | Use this prompt |
|-------------|----------------|
| Turn raw ideas into user stories | **Backlog Refinement** |
| Check if stories are ready for a sprint | **Definition of Ready** |
| Plan a sprint | **Sprint Planning** |
| Run a daily standup | **Daily Scrum** |
| Report dev progress | **Dev Status Update** |
| Report QA results | **QA Report** |
| Triage a bug or incident | **Triage** |
| Handle a mid-sprint priority change | **Scope Change** |
| Close out a sprint | **Sprint Review** |
| Reflect and improve | **Retrospective** |
| Prepare release documentation | **Release Notes** |

---

## Getting Started

### Prerequisites

- [VS Code](https://code.visualstudio.com/) with [GitHub Copilot](https://github.com/features/copilot) enabled
- Copilot Chat with agent mode support

### Installation

1. **Clone this repo** (or copy the files into your project):
   ```bash
   git clone https://github.com/cguldogan/copilot-scrum-team.git
   ```

2. **Copy into your project** (optional — if you want to add it to an existing repo):
   ```bash
   cp -r copilot-scrum-team/agents/ your-project/.github/agents/
   cp -r copilot-scrum-team/prompts/ your-project/.github/prompts/
   cp copilot-scrum-team/copilot-instructions.md your-project/.github/copilot-instructions.md
   ```

3. **Open VS Code** and start using agents in Copilot Chat.

### Usage Examples

**Run Sprint Planning:**
Open Copilot Chat and use the Sprint Planning prompt, providing your sprint goal and backlog candidates.

**Daily Standup:**
Use the Daily Scrum prompt with yesterday's progress and any blockers.

**Delegate to an agent directly:**
Mention an agent (e.g., `@scrum-master-agent`) and describe the task. The agent will coordinate with others via handoffs.

**Triage a bug:**
Use the Triage prompt with bug reports, logs, or incident summaries. The agent will classify severity, assign owners, and propose fixes.

## Design Principles

- **Minimize user involvement** — agents coordinate with each other via handoffs; the user acts as sponsor, not coordinator.
- **Plan internally** — no agent asks the user to "plan first"; they infer and proceed.
- **Concrete outputs over discussion** — every response includes structured artifacts (tables, checklists, snapshots).
- **Consistent reporting** — all agents follow the same Meeting Notes + Progress Snapshot format defined in the global instructions.
- **Clarifications policy** — agents first try to infer from repo context; if still unclear, they route questions through the Scrum Master rather than asking the user directly.

## Customization

- **Edit `copilot-instructions.md`** to change the global working agreement, Definition of Done, or reporting format.
- **Edit agent files** in `agents/` to adjust individual agent behavior, models, or handoff targets.
- **Edit or add prompt files** in `prompts/` to create new ceremony templates or adjust existing ones.
- **Change models** — each agent specifies its model in the YAML frontmatter. Adjust to your preference.

## License

MIT
