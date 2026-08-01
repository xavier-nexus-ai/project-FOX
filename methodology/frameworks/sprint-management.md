# Sprint Management Framework

**Name:** Njin Sprint Management Framework
**Version:** 1.0
**Purpose:** Defines how Njin project managers plan, run, review, and re-plan sprints. Covers estimation, capacity planning, story format, review cadence, and re-planning triggers. Designed for use with the njin-vibe PMO platform and the Claude Code PM framework.

---

## Overview

Njin runs fortnightly sprints. Sprints are planned by the Coordinator agent under PM oversight. Estimation starts at 100% capacity and is adjusted based on actual availability. The PM chooses the estimation approach: AI self-estimate or dev team input. Stories must be compatible with njin-vibe. Reviews are client-facing "Results and ROI Sessions" — not just status updates.

---

## Sprint Lifecycle

Each sprint moves through four stages:

1. **Sprint Planning** — scope confirmed, stories created, effort estimated
2. **Sprint Execution** — work delivered by the team
3. **Sprint Review** — results reviewed with client
4. **Sprint Retrospective and Re-planning** — internal review, next sprint planned

---

## Stage 1 — Sprint Planning

### Purpose
Define exactly what will be delivered in the sprint, assign effort estimates, confirm capacity, and set expectations with the PM and client.

### Inputs
- Approved scope of work
- Previous sprint review outcomes (if not the first sprint)
- Team availability
- njin-vibe sprint structure

### Process

**Step 1: Coordinator opens sprint plan**
The Coordinator agent begins with a 100% capacity assumption. This is a deliberate starting point — it ensures no scope is cut prematurely. Actual capacity is applied as an adjustment in Step 3.

**Step 2: Estimation approach — PM decision required**

The Coordinator asks the PM:

> "Should I estimate hours for this sprint myself, or do you want to pull hours from the dev team?"

| Approach | When to use | How it works |
|---|---|---|
| **AI self-estimate** | Early sprints, no dev input available, or tight timeline | Coordinator generates estimates using task type, complexity, and framework knowledge. Documents assumptions. |
| **Dev team hours** | When dev team has reviewed scope, or for complex technical work | PM collects hours from devs. Coordinator incorporates into plan without overriding. |

If the PM does not respond to the estimation question, the Coordinator defaults to AI self-estimate and flags this assumption in the plan for PM review.

**Step 3: Capacity adjustment**

After estimates are set at 100%, the PM provides actual availability:
- Leave, public holidays, other project commitments
- Known blockers or dependencies

Coordinator adjusts the sprint plan and flags if scope must be deferred.

**Step 4: Story creation**

Stories are created in the following format for njin-vibe compatibility:

```
As a [role], I want [action], so that [outcome].
```

Each story includes:
- **Title** — concise action description
- **Role** — who benefits (client persona or internal role)
- **Acceptance criteria** — what "done" looks like (2-4 criteria)
- **Effort estimate** — in hours or story points
- **Sprint assignment** — which sprint this belongs to
- **Dependencies** — what must be complete before this starts
- **Epic link** — which epic this story belongs to

Epics group related stories under a major deliverable. Each client engagement has 1-4 epics active at a time.

**Step 5: njin-vibe sync**

Once the sprint plan is approved by the PM, the njin-vibe Sync skill pushes all stories and sprint data to the njin-vibe platform. This is a skill, not a standalone agent — it runs as part of the Coordinator's toolkit.

### Outputs
- Sprint plan with stories, estimates, and capacity
- Epic assignments for all stories
- Sprint calendar entries in njin-vibe
- PM-approved sprint scope

### Gates — must be met before sprint begins
- [ ] Estimation approach confirmed by PM
- [ ] Capacity adjustment applied (not still at 100% assumption)
- [ ] All stories have acceptance criteria
- [ ] Sprint plan approved by PM
- [ ] njin-vibe synced

---

## Stage 2 — Sprint Execution

### Purpose
Deliver the committed sprint scope. Surface blockers early. Keep the client informed without burdening them with noise.

### Process
- Team executes stories per sprint plan
- PM monitors progress in njin-vibe dashboard
- Blockers logged immediately in COS and flagged to PM
- Changes to scope must go through a change request — not just happen silently
- PM updates roadmap if any deferral or re-ordering occurs

### Decision Points

| Trigger | Action |
|---|---|
| Blocker identified mid-sprint | Log in COS, assess impact, flag to PM. PM decides: resolve, defer, or descope. |
| Client requests scope change | Log change request, estimate effort, get PM approval before accepting |
| Team velocity below plan | Flag to PM, identify cause, adjust remaining sprint scope if needed |

---

## Stage 3 — Sprint Review

### Purpose
Demonstrate completed work to the client, show ROI to date, and build confidence in continued delivery. Every review is a "Results and ROI Session" — not a status update.

### Cadence
- Fortnightly, aligned to sprint end
- Held in the client's preferred channel (video call standard)

### Structure

| Segment | Description |
|---|---|
| **Re-sell the decision** | Briefly re-anchor why the client engaged Njin. Remind them of the problem and cost of inaction. |
| **Results delivered** | Walk through what was completed this sprint. Use outcome language: hours saved, errors reduced, revenue impacted. |
| **ROI to date** | Show cumulative value delivered against the original promise. |
| **Next sprint preview** | Preview what's coming next, set expectations, confirm any inputs needed from the client. |
| **Seed next-stage upsell** | If appropriate, mention what a next phase could unlock. Don't pitch hard — plant the idea. |

### Outputs
- Sprint report (AI-generated, PM-reviewed before sending)
- Updated roadmap
- Feedback summary
- KPI tracker update
- Meeting transcript indexed to vector database

### Human Checkpoint
PM must review the AI-generated sprint report before it is sent to or presented to the client.

---

## Stage 4 — Sprint Retrospective and Re-planning

### Purpose
Capture learnings from the sprint and plan the next one. Internal only — not client-facing.

### Process
1. PM reviews what was completed, deferred, or blocked
2. Root causes of any blockers or missed deliverables documented
3. Learnings noted in COS change log
4. Next sprint planning begins using Stage 1 process
5. Any scope adjustments from retrospective feed into next sprint plan before capacity planning

### Outputs
- Retrospective notes in COS
- Inputs for next sprint planning
- Updated scope if required

---

## Capacity Planning Rules

| Rule | Detail |
|---|---|
| **Start at 100%** | Always begin sprint planning assuming full availability. Never pre-cut scope based on assumed unavailability. |
| **Adjust with facts** | Apply actual availability when confirmed. Leave, holidays, and competing commitments reduce available hours. |
| **Document the adjustment** | Record what was cut or deferred and why. This becomes the input for next sprint planning. |
| **Never silently defer** | If a story moves out of a sprint, the PM must be informed and the change logged. |
| **Flag the gap** | If capacity drops below what the scope requires, flag it to the PM and client immediately — don't deliver a surprise at sprint review. |

---

## Estimation Guidelines

### AI Self-Estimate
Used when dev team input is not available or when a fast estimate is needed.

- Coordinator estimates based on: task type, estimated complexity, similar work in framework history
- Estimates are documented with assumptions listed
- PM must review and approve before the sprint is locked
- Estimates carry a +/-20% buffer by default; PM can override

### Dev Team Estimate
Used for complex technical work or when accuracy is critical.

- PM collects hours directly from dev team before sprint planning
- Coordinator incorporates dev hours without overriding them
- If dev estimate significantly differs from AI estimate, flag the variance to PM
- Variance of >30% triggers a discussion before sprint is locked

---

## Re-planning Triggers

| Trigger | Response |
|---|---|
| Blocker unresolved for 24+ hours | PM assesses impact; may defer story to next sprint |
| Scope change approved by PM | Coordinator updates sprint plan; njin-vibe synced |
| Team member unavailable unexpectedly | Capacity recalculated; scope adjusted accordingly |
| Client provides late inputs | Assess if it impacts sprint scope; may extend or defer affected stories |
| Story significantly underestimated | Flag to PM; decide whether to extend or defer |
| Sprint velocity tracking 25%+ below target at midpoint | PM-triggered review; re-plan remaining sprint scope |

---

## njin-vibe Integration

Sprints are the unit of work in njin-vibe. The framework interacts with the platform via the njin-vibe Sync skill.

| Action | When |
|---|---|
| Push sprint plan | After PM approves sprint plan (end of Stage 1) |
| Update task statuses | During sprint execution (ongoing) |
| Push sprint report | After PM reviews and approves (end of Stage 3) |
| Sync retrospective notes | After Stage 4 complete |

The njin-vibe Sync skill is part of the Coordinator agent's toolkit. It is not a standalone agent. It triggers at agreed checkpoints: on demand, at handoff points, or on PM instruction.

---

## Sprint Roles

| Role | Responsibility |
|---|---|
| **PM** | Approves sprint plan, reviews sprint report, makes re-planning decisions, confirms estimation approach |
| **Coordinator agent** | Generates sprint plan, estimates effort, manages capacity, syncs to njin-vibe |
| **Customer Success** | Runs sprint review with client, tracks KPIs, flags feedback |
| **PMO** | Calendar management, dashboard sections, blocker tracking |
| **Dev team** | Delivers stories, provides effort estimates when requested, flags blockers immediately |

---

## Common Failure Modes

| Failure | How to avoid it |
|---|---|
| Planning from the proposal alone | Always use the framework delivery procedure as the primary input, not just the proposal |
| Skipping capacity adjustment | Never leave the sprint plan at 100% assumption — always confirm with PM |
| Silently deferring stories | Every deferral must be logged and PM-approved |
| Sprint review as status update | Always use Results and ROI Session structure — re-sell, show value, seed next stage |
| Estimation without assumptions documented | Every AI self-estimate must include assumptions — PM cannot review what they can't see |
