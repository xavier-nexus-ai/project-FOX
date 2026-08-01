# Weekly Plan Format

The standard structure for weekly priority plans at Njin. Used to plan James's work week and coordinate team capacity.

---

## Purpose

A weekly plan answers four questions:
1. What's the ONE bottleneck each day?
2. What can be done if time remains?
3. What's overdue and needs attention?
4. Is capacity aligned with commitments?

---

## File Naming Convention

`Project Management/Weekly Plans/priority-plan-YYYY-MM-DD.md`

Date is the Monday of the week being planned.

Example: `priority-plan-2026-04-07.md`

---

## Structure

### 1. Header
```markdown
# Weekly Priority Plan — [Week of Mon DD, YYYY]

**Budget:** 20 hours available (4h/day × 5 days)
**Total commitments:** XX hours
**Status:** On budget / Over budget / Under budget
```

### 2. Daily Bottleneck (ONE task per day)

Each day has ONE primary bottleneck. Not three, not a to-do list — ONE.

```markdown
## Monday
**Bottleneck:** [Specific task] | [Brand < > Client] | [Est. hours]
**Why this:** [1-2 sentences on why this matters most today]

## Tuesday
**Bottleneck:** [Specific task]
**Why this:** [...]

[continue for all 5 days]
```

### 3. Secondary Tasks (if time remains)

Tasks to work on after the bottleneck, if there's capacity left in the day.

```markdown
## Secondary Tasks
- [Task 1] | [Brand < > Client] | [Est. hours]
- [Task 2] | [Brand < > Client] | [Est. hours]
```

### 4. Quick Wins (<30 min)

Items that are fast to complete and clear mental load.

```markdown
## Quick Wins (<30 min each)
- [Item 1]
- [Item 2]
```

### 5. Overdue Items Table

Anything that has slipped past its deadline. This is the accountability section.

```markdown
## Overdue Items

| Task | Client | Due | Days Late | Repeat offender? |
|------|--------|-----|-----------|------------------|
| POLR V1 | Fox | 2026-04-01 | 6 | Yes — 3rd time |
| Playbook S9 | YCM | 2026-04-03 | 4 | No |
```

### 6. Capacity Summary

```markdown
## Capacity Summary

- Available this week: 20 hours
- Committed: 22 hours
- **Over budget by: 2 hours**

**What to cut:** [specific items to defer]
```

### 7. Revenue-First Ordering

When multiple clients compete, order them by revenue value and deadline urgency.

```markdown
## Revenue-First Ordering (External Paying Clients)

1. Fox — Playbook work — OVERDUE
2. YCM — Section 9 — Due Thursday
3. Dexion — CRM build — Due next week
4. Maritza & Alfredo — GHL access — Blocked on client
5. HBT — Nurture sequence — On track
```

### 8. Internal Projects (Separate)

```markdown
## Internal Projects (Time Permitting)

- AI Orchestrators — Client outreach
- Jimmy AI — Phase 34 Vector DB
- Njin PM Tool — Framework build
```

### 9. Next Week Lookahead

```markdown
## Next Week Lookahead

- [Client X] — [Upcoming work]
- [Deadline Y] — [What needs prep]
```

### 10. Recommendations

One section for each type of recommendation.

```markdown
## Recommendations

### Park / defer
- [Item] — [Why parking is the right call]

### Unblock
- [Item] — [What's needed to unblock]

### Revenue actions
- [Item] — [Why this moves revenue]
```

### 11. Stats

```markdown
## Stats

- P0 projects: X
- P1 projects: X
- P2 projects: X
- Overdue: X
- At risk: X
- Revenue at stake: $XX,XXX
```

---

## Planning Rules

### Rule 1: One bottleneck per day
Never more. One thing that, if completed, makes the day a win. Everything else is optional.

### Rule 2: Overdue first
Address overdue items before taking on new work. Overdue is a gravity well — it doesn't fix itself.

### Rule 3: Revenue first
External paying clients come before internal projects. Always. Internal work fills the gaps.

### Rule 4: Respect the budget
20 hours max for the week. If the plan is over budget, cut — don't pretend it'll fit.

### Rule 5: Meeting-aware
Subtract expected meeting hours from available capacity. Don't plan into meeting time.

### Rule 6: Fix before build
Never start a new engagement or new phase while a prior one has unresolved blockers.

### Rule 7: $500/hr test
Every task should pass the $500/hr test. If it's admin or busywork, delegate or automate — don't schedule it.

---

## The Weekly Planning Ritual

When to run it: End of Friday or start of Monday (before the week begins).

Process:
1. **Pull data sources** — Reclaim tasks, COS.yaml, calendar, Notion
2. **Identify overdue** — what has slipped past its deadline
3. **Identify bottlenecks** — what matters most this week
4. **Assign one bottleneck per day** — based on priority and dependencies
5. **Check capacity** — does it fit in 20 hours?
6. **Cut or defer** — if over budget, what comes off the plate?
7. **Save the plan** — `Project Management/Weekly Plans/priority-plan-YYYY-MM-DD.md`
8. **Commit to it** — tell the team what's happening

---

## Output Example (Abbreviated)

```markdown
# Weekly Priority Plan — Week of April 7, 2026

**Budget:** 20 hours available
**Total commitments:** 18 hours
**Status:** On budget

## Monday
**Bottleneck:** POLR V1 Prototype (FHL nurture) | Njin < > Fox | 4h
**Why this:** Overdue by 6 days. Client has signed and is waiting. Blocks downstream work.

## Tuesday
**Bottleneck:** Playbook Section 9 Draft | Njin < > YCM | 3h
**Why this:** Section needed for Thursday's client review. Tight timeline.

## Wednesday
**Bottleneck:** Weekly team training | Internal | 1h (5pm meeting)
**Why this:** Wednesday is heavy meeting day, limited task capacity.

[...]

## Overdue Items

| Task | Client | Due | Days Late | Repeat? |
|------|--------|-----|-----------|---------|
| POLR V1 | Fox | Apr 1 | 6 | Yes |
| GHL Demo | Fox | Apr 3 | 4 | No |

## Recommendations

### Park / defer
- Jimmy AI Phase 34 — Internal, can wait

### Unblock
- Dexion CRM build — needs James to confirm pricing with client

### Revenue actions
- Close Fox outstanding items this week — $X at stake
```

---

**Source:** Portfolio-level `game-plan` skill methodology, `docs/background/templates/weekly-plan-examples/`, master project `CLAUDE.md` (time budget rules).
