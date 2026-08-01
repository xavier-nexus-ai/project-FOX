# Sprint Planning Guide

How to plan sprints at Njin — sizing, velocity, capacity allocation, dependency sequencing, and prioritisation.

---

## Sprint Basics

- **Cadence:** Fortnightly (every 2 weeks)
- **Format:** Epic > User Stories > Tasks
- **Planning mode:** Start at 100% capacity, adjust with facts
- **Review style:** Results & ROI Session (not status updates)
- **Tracking:** njin-vibe is source of truth for sprint state

---

## The 5-Step Planning Process

### Step 1: Pull the backlog

Start with what's in the client's scope document and any carry-forward items from the previous sprint. Sources:
- Scope document (from BA)
- Previous sprint review (carry-forward items)
- Client requests logged since last sprint
- Blockers resolved since last sprint

### Step 2: Start at 100% capacity

Coordinator assumes full availability. This is deliberate — it surfaces the full scope before cuts are made. Don't pre-cut based on assumed unavailability.

### Step 3: Apply real capacity

Get actual availability from the PM:
- Team member leave
- Public holidays
- Competing commitments
- Known meetings

Calculate: `nominal hours × availability factor × 0.75 buffer`

### Step 4: Prioritise and sequence

Apply the prioritisation framework (below) and sequence stories based on dependencies.

### Step 5: Lock and sync

PM approves. Coordinator syncs to njin-vibe via the vibe-sync skill.

---

## Prioritisation Framework

Sprint items are prioritised in this order:

### 1. Revenue-generating, client-facing work
Anything the client sees or that affects client revenue comes first. No exceptions.

### 2. Critical blockers
Work that, if not done, blocks other work or creates a domino effect.

### 3. Commitments with external deadlines
Anything tied to a client milestone, launch date, or third-party dependency.

### 4. Framework-required deliverables
Work that's part of the delivery procedure — gates, phase exit requirements.

### 5. Quality of life improvements
Refactoring, optimisation, internal tooling.

### 6. Nice-to-haves
Everything else.

**Rule:** Fill the sprint from top of list down, stop when capacity runs out. Don't cram nice-to-haves in if they push out critical work.

---

## Capacity Rules

### Rule 1: Start at 100%
Never pre-cut based on assumed unavailability. Put everything in first, then cut based on real capacity.

### Rule 2: Adjust with facts
Apply actual availability after the initial capacity assumption is set. Leave, holidays, competing commitments all reduce hours.

### Rule 3: Apply the 25% buffer
Real-world capacity is ~75% of nominal. Context switching, unplanned interruptions, meetings that run long — all eat hours. Build it in.

### Rule 4: Document the adjustment
Record what was cut or deferred and why. This becomes input for the next sprint plan.

### Rule 5: Never silently defer
If a story moves out of a sprint, the PM must be informed and the change logged. Hidden deferrals destroy trust.

### Rule 6: Flag the gap
If capacity drops below what the scope requires, flag it to the PM and client immediately. Don't deliver the surprise at sprint review.

---

## Story Structure for njin-vibe

```
As a [role], I want [action], so that [outcome].
```

Every story includes:
- **Title** — concise action description
- **Role** — who benefits
- **Acceptance criteria** — 2-4 criteria defining "done"
- **Effort estimate** — hours or story points
- **Sprint assignment** — which sprint
- **Dependencies** — what must be complete first
- **Epic link** — which epic this belongs to

---

## Dependency Sequencing

Order stories within a sprint based on dependencies:

| Dependency type | How to handle |
|-----------------|---------------|
| **Blocking dependency** (B needs A done) | A must be in the same sprint or earlier, scheduled before B |
| **Soft dependency** (B is easier after A) | Same sprint is fine, schedule A first if possible |
| **External dependency** (waiting on client/third party) | Schedule after the dependency is confirmed resolved; don't commit until then |
| **Parallel work** | Assign to different team members, no sequencing required |

**Rule:** If a story has a dependency that isn't in this sprint or already done, either pull the dependency in or defer the story.

---

## Sprint Sizing

A standard Njin sprint covers 2 weeks. For a single full-time contributor:

- Nominal hours: 60 (30h × 2 weeks)
- Available after buffer: 45 hours (60 × 0.75)
- Deliverable scope: 4-8 meaningful stories typically

For a team:
- Multiply by team members with % allocation
- Apply individual availability factors
- Do NOT assume 100% focus on any one project

---

## Velocity Tracking

After each sprint, record:
- **Planned hours**
- **Completed hours** (only fully complete stories count)
- **Velocity:** completed hours / planned hours × 100%

**Use velocity for next sprint planning:**
- Don't plan more than 90% of last sprint's velocity (buffer for unknowns)
- Watch the trend — improving, stable, or declining?
- 3 sprints of declining velocity = process change needed

---

## Re-planning Triggers

Mid-sprint re-plans happen when:

| Trigger | Response |
|---------|----------|
| Blocker unresolved for 24+ hours | PM assesses impact, may defer story |
| Scope change approved by PM | Coordinator updates plan, syncs to njin-vibe |
| Team member unavailable unexpectedly | Recalculate capacity, adjust scope |
| Client provides late inputs | Assess impact, may extend or defer affected stories |
| Story significantly underestimated (>30% over) | Flag to PM, decide extend or defer |
| Sprint velocity tracking 25%+ below plan at midpoint | PM-triggered review, re-plan remaining scope |

---

## Carry-Forward Rules

Items that don't complete in a sprint:

1. **Partial progress:** Log exact progress percentage, carry into next sprint at full estimated effort (don't reduce)
2. **Blocked items:** Move to "blocked" backlog, address the blocker before rescheduling
3. **Deprioritised items:** Return to backlog, re-prioritise in next planning session
4. **Abandoned items:** Log the decision and reason in the COS, remove from backlog

**Rule:** Nothing silently disappears between sprints. Every item has an explicit decision.

---

## Sprint Review Structure

Sprint reviews are Results & ROI Sessions, not status updates:

1. **Re-sell the decision** — remind why the client engaged Njin
2. **Results delivered** — what was completed, in outcome language
3. **ROI to date** — cumulative value against the original promise
4. **Next sprint preview** — what's coming, what inputs are needed
5. **Seed next-stage upsell** — plant the idea of what could come next

**Human checkpoint:** PM reviews the AI-generated sprint report before sending or presenting.

---

## Common Sprint Planning Mistakes

| Mistake | Fix |
|---------|-----|
| Planning at 100% availability | Apply the 25% buffer and actual availability factors |
| Not sequencing by dependencies | Map dependencies before committing stories |
| Over-committing to look productive | Plan 90% of last sprint's velocity, not 110% |
| Vague acceptance criteria | Write 2-4 specific, testable criteria per story |
| Carrying items forward without re-estimating | Re-estimate carryover at the start of the next sprint |
| Letting client scope change mid-sprint without approval | Require PM approval and re-plan before accepting changes |

---

**Source:** `docs/ip-vault/frameworks/sprint-management.md`, Apr 7 meeting transcript (sprint planning decisions), master project `CLAUDE.md`.
