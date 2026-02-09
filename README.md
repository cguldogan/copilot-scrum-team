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
