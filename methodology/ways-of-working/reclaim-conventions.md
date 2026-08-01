# Reclaim Conventions

How tasks get named and tracked in Reclaim — the time-based task management system that auto-schedules work into James's calendar.

---

## What Reclaim Is

Reclaim is where James's individual tasks live. It books time in his calendar automatically based on priority and estimated effort. Unlike Notion (project-level) or njin-vibe (team-level), Reclaim is personal and calendar-integrated.

---

## Task Naming Convention

**Format:** `Task Name | Brand < > Client`

### Examples:
- `POLR V1 Prototype | Njin < > Fox`
- `GHL Comparison Demo | Njin < > Fox`
- `Playbook Finalised | Njin < > Dexion`
- `V2 Architecture Decisions | AIpreneurs`
- `Auto Top-Up Review with Jose | AIpreneurs < > James Killick Co`

### Rules:
- **Brand first, client second** — brand is what James is doing, client is who it's for
- **Use pipe `|` as separator**
- **Use `< >` to link brand and client**
- **For internal projects (no client):** just use the brand — `Phase 34 Vector DB | OpenClaw`, `Team Adoption Sprint | Njin PM Tool`

---

## Task Metadata

Every Reclaim task should have:

| Field | What to set |
|-------|------------|
| **Priority** | P1 / P2 / P3 / P4 |
| **Estimated duration** | In 15-minute chunks (hours × 4 = chunks) |
| **Category** | WORK (for task work), HABIT (for recurring habits) |
| **Due date** | Realistic target |
| **Notes** | Brief context — link to related docs, what the task is about |

---

## Priority Levels

| Priority | Use for |
|----------|---------|
| **P1** | Critical, client-facing, time-sensitive, overdue |
| **P2** | Important, due this week, key deliverables |
| **P3** | Active work, not urgent, can flex |
| **P4** | Backlog, parking, not yet committed |

---

## Time Chunks

Reclaim works in 15-minute increments:

- 15 min = 1 chunk
- 30 min = 2 chunks
- 1 hour = 4 chunks
- 2 hours = 8 chunks
- 4 hours = 16 chunks

**Rule:** Estimate in chunks, not in vague hours. Specific beats aspirational.

---

## Budget Constraints

James has a **maximum of 4 hours per day** for Reclaim tasks, ~20 hours per week. This is based on calendar analysis:
- Habits consume ~4.5h/day
- Real meetings ~3.3h/day
- Buffers ~2h/day
- In an 11-hour working day (7am-6pm AEST)

**What this means for Reclaim:**
- Don't schedule more than 20 hours of task work per week
- Best days (light Mondays/Fridays) can stretch to 4h+
- Heavy meeting days (Wednesdays) can be near zero
- If the maths doesn't add up, flag it — don't silently overcommit

---

## AIpreneurs Rule

**AIpreneurs tasks go in Reclaim and COS, NOT Notion.** This is a critical rule — do not create Notion tasks for AIpreneurs projects. Reclaim handles them exclusively.

---

## What Goes in Reclaim vs Elsewhere

| System | What goes there |
|--------|-----------------|
| **Reclaim** | James's personal tasks, scheduled in calendar time blocks |
| **Notion** | Njin Method team tasks (not James's personal work) |
| **njin-vibe** | Sprint plans, epics, user stories for active engagements |
| **COS** | Project state, phases, milestones (NOT day-to-day tasks) |

---

## Reclaim Task Lifecycle

1. **Create** — Task created with title, priority, estimate, notes
2. **Schedule** — Reclaim auto-schedules into James's calendar based on priority and estimated duration
3. **Work** — James works the task in the scheduled time block
4. **Complete** — Mark as complete in Reclaim — closes the calendar block
5. **Review** — Weekly retrospective looks at completed vs slipped tasks

---

## Common Patterns

### Client task (Njin Method)
```
Title: Playbook Section 9 Draft | Njin < > Fox
Priority: P1
Duration: 8 chunks (2 hours)
Notes: FHL playbook, draft of Funnels section. Reference: [Google Doc link]
```

### Internal project task
```
Title: Framework Deploy Script | Njin PM Tool
Priority: P2
Duration: 12 chunks (3 hours)
Notes: Build deploy.sh for PM framework. Reference: cos.yaml in orchestration project.
```

### AIpreneurs task (no client - internal product)
```
Title: V2 Auth Domain Decision | AIpreneurs
Priority: P2
Duration: 4 chunks (1 hour)
Notes: Decide auth.aipreneurs.com vs app.aipreneurs.com/auth. Reference: architecture doc.
```

### Dual brand (service delivered internally)
```
Title: Monthly Financial Review | AIpreneurs < > James Killick Co
Priority: P3
Duration: 4 chunks (1 hour)
Notes: JKC delivers the review to AIpreneurs as a service.
```

---

## Critical Rules

1. **Always use the naming format** — `Task Name | Brand < > Client`
2. **Never exceed 20 hours/week of work task time** — flag if commitments exceed
3. **Priority discipline** — don't flag everything as P1 or the priority system is meaningless
4. **AIpreneurs = Reclaim only, never Notion**
5. **Include context in notes** — future you needs to know what the task is about

---

**Source:** Global `CLAUDE.md` (Reclaim naming conventions), master project `CLAUDE.md` (time budget rules).
