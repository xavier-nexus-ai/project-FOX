# Notion Task Guidelines

How tasks get created, tracked, and managed in Notion. **Notion is for Njin Method tasks ONLY.** AIpreneurs and internal framework tasks live in Reclaim and COS, not Notion.

---

## What Qualifies as a Task

A task is a meaningful deliverable with:
- **Estimated effort:** 2+ hours (anything shorter is a checklist item, not a task)
- **A clear "done" state:** you can definitively say it's finished
- **A specific owner:** one person is accountable

**NOT a task:**
- Anything under 30 minutes (add to a parent task's checklist instead)
- Setup steps (included in the parent task's scope)
- Recurring admin (use a running "Open Items" checklist in the project page)

---

## Required Fields

Every Notion task must have:

| Field | Required? | Notes |
|-------|-----------|-------|
| **Title** | Yes | Clear, specific task name. Include project prefix for multi-project clients (e.g., `[LBT] AI SDR Setup`) |
| **Status** | Yes | Backlog / Current Sprint / In Progress / For Internal Review / Completed |
| **Priority** | Yes | Critical / High / Medium / Low |
| **Assigned** | Yes | Single owner — never leave blank |
| **Due Date** | Yes | Realistic target, not aspirational |
| **Est Effort (Hours)** | Yes | Actual estimate, not placeholder |
| **Category** | Yes | Custom / AI Portal / AI Agent / AI Automation / Automation / Voice / Chatbots / CRM / Training |
| **Type** | Yes | Client or Internal |
| **Technologies** | Where relevant | Claude Code, GHL, etc. |
| **Project Dashboard** | **CRITICAL** | Link via relation field — never leave blank for client tasks |
| **Body** | Yes | Overview, scope, dependencies, context, acceptance criteria |

---

## Project Dashboard Linking — CRITICAL RULE

**Every client task MUST link to its Project Dashboard page.**

1. **When creating tasks for ANY client:** ALWAYS search the Project Dashboard data source first to find the client's dashboard page. Then set the `Project Dashboard` relation field using the page URL format: `https://www.notion.so/<uuid-without-dashes>`.
2. **When finding tasks for a client:** Filter the Tasks DB by the `Project Dashboard` relation to get only that client's tasks. Do NOT rely on text matching in titles.

**Why this matters:** Without the Project Dashboard link, tasks become orphaned. The client's dashboard won't show them. Reports won't roll them up. It breaks project tracking.

**Never create a client task without this link.**

---

## Title Conventions

- **Don't include the client name in the title.** The Project Dashboard relation handles that.
- **Use project prefixes for multi-project clients:** `[LBT] AI SDR Setup`, `[BAP] Pipeline Config`
- **Be specific and actionable:** "POLR V1 Prototype — FHL 18-Month Nurture Sequence" not "Nurture work"
- **No internal jargon clients won't understand** (these titles are visible to clients in the dashboard)

---

## Priority Scale

| Priority | Definition | Max per client |
|----------|------------|----------------|
| **Critical** | Blocks revenue, escalation from James/George, time-sensitive client-facing deadline | 1-2 |
| **High** | Due this sprint, client expectation, required for phase completion | 1-2 |
| **Medium** | Next sprint, not time-critical | No limit |
| **Low** | Backlog, nice-to-have, not essential to current deliverables | No limit |

**Rule:** Maximum 2-3 Critical/High per client at any time. If more are flagged as Critical, they're not actually critical — force a triage conversation.

---

## Status Values

| Status | Meaning |
|--------|---------|
| **Backlog** | Identified but not yet scheduled |
| **Current Sprint** | Committed to this sprint, not yet started |
| **In Progress** | Actively being worked on |
| **For Internal Review** | Work complete, awaiting internal review |
| **Completed** | Done, reviewed, delivered |

---

## Task Body Structure

Every task body should contain:

```markdown
## Overview
[1-2 sentence summary of what this task accomplishes and why]

## Scope
[Bullet points of specific deliverables within this task]

## Dependencies
[What must be in place or done first]

## Context
[Background the assignee needs — decisions made, client preferences, constraints]

## Acceptance Criteria
- [ ] [Specific, testable criteria for "done"]
- [ ] [Another criterion]

## Checklist (for sub-tasks under 30 min)
- [ ] [Small step]
- [ ] [Small step]
```

---

## Grouping Rules

**Do:** Create one parent task with a checklist of related small items.

**Don't:** Create 5 separate cards for 5 related items. That's noise.

**Example:**
- ❌ Bad: 5 tasks — "Create folder structure", "Add brand guide", "Add current scripts", "Add case studies", "Send to client"
- ✅ Good: 1 task — "Set up [Client] <> Njin shared folder" with a checklist of all 5 items

---

## The "Open Items" Pattern

For ongoing small items that don't deserve full tasks, use a running **Open Items** checklist in the project page. Not recurring tasks. Update the checklist as items come and go.

This prevents the Tasks DB from filling with noise.

---

## Notion vs Other Systems — What Lives Where

| System | What goes there |
|--------|-----------------|
| **Notion Tasks DB** | Njin Method client tasks ONLY, linked to Project Dashboard |
| **Reclaim** | James's personal task queue (also AIpreneurs tasks) |
| **njin-vibe** | Sprint plans, epics, user stories for active engagements |
| **COS** | Project state, phase tracking, milestones — NOT day-to-day tasks |

---

## Critical Rules (Do Not Break)

1. **Notion is for Njin Method tasks ONLY.** AIpreneurs, internal framework, and dev tasks go elsewhere.
2. **Every client task must have a Project Dashboard relation link.** No exceptions.
3. **Max 2-3 Critical/High per client.** More means you're lying about priority.
4. **Tasks are 2+ hours.** Shorter items are checklist items in a parent task.
5. **No em dashes in task titles or bodies.** Ever.

---

**Source:** Global `CLAUDE.md` (Notion task rules), `docs/background/templates/notion-task-guidelines.md`.
