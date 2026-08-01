# Workflow: Sprint Execution Cycle

**Purpose:** The fortnightly sprint cycle — planning, execution, review, retrospective, re-planning. Repeats every 2 weeks throughout engagement delivery.

**Duration:** 2 weeks per sprint (Njin fortnightly cadence).

**Owner:** PM (driving), Coordinator (sprint operations), Customer Success (client reviews)

---

## Prerequisites

- [ ] `plan_ready` gate passed
- [ ] Sprint 1 plan exists (or prior sprint retrospective complete)
- [ ] njin-vibe synced with current sprint data
- [ ] Team capacity confirmed
- [ ] Kickoff call completed (for sprint 1)

---

## Sprint Lifecycle (Repeats Every 2 Weeks)

```
    SPRINT START
       |
       v
[1. Sprint Planning] (if re-planning) 
       |
       v
[2. Sprint Execution] (10 days)
       |
       v
[3. Sprint Review] (client-facing, "Results & ROI Session")
       |
       v
[4. Sprint Retrospective] (internal)
       |
       v
[5. Next Sprint Planning]
       |
       v
    SPRINT END / NEXT SPRINT START
```

---

## Stage 1: Sprint Planning

### Step 1.1: Pull Backlog

Orchestrator gathers:
- Carry-forward items from previous sprint
- New client requests since last sprint
- Blockers that have been resolved
- Remaining scope backlog

### Step 1.2: Coordinator Runs Sprint Planning

PM calls Coordinator. Coordinator:
1. Runs `sprint-planning` skill
2. Starts at 100% capacity
3. Adjusts with real availability (PM provides)
4. Applies 25% buffer
5. Sequences by dependencies
6. Prioritises revenue-first
7. Locks sprint scope

### Step 1.3: Estimation Decision

Coordinator asks PM the estimation question if stories are new or significantly changed. For carry-forward items, re-estimate at the start of the new sprint (don't reduce for partial progress).

### Step 1.4: PM Approves and Syncs

PM approves sprint plan. Orchestrator invokes `vibe-sync` skill to push to njin-vibe.

**Gate check — Sprint Ready:**
- [ ] Sprint scope locked
- [ ] Capacity applied
- [ ] All stories have acceptance criteria
- [ ] Dependencies sequenced
- [ ] njin-vibe synced

---

## Stage 2: Sprint Execution (10 working days)

### Step 2.1: Team Executes Stories

- Devs work through stories per sprint plan
- PM monitors progress via njin-vibe dashboard
- Blockers logged immediately in COS and flagged to PM
- No silent scope changes — everything goes through PM approval

### Step 2.2: Mid-Sprint Check (Day 5)

Orchestrator prompts PM for mid-sprint health check:
- Velocity tracking (are we on pace?)
- Blocker status
- Any scope change requests
- Need to re-plan?

If velocity tracking 25%+ below plan at midpoint, trigger re-plan.

### Step 2.3: Continuous COS Updates

Throughout sprint, Orchestrator logs:
- Story completions
- Blockers raised and resolved
- Scope changes (if any)
- Daily progress if PM requests

---

## Stage 3: Sprint Review (Client-Facing)

### Step 3.1: Prepare Sprint Review

Coordinator + Communication Agent prepare sprint report:
1. Pull completion data from COS and njin-vibe
2. Calculate metrics (planned vs actual, completion rate, velocity)
3. Frame results as outcomes (hours saved, ROI delivered, not just "stories completed")
4. Communication Agent drafts client-facing version

**PM reviews sprint report before client sees it.**

### Step 3.2: Run "Results and ROI Session"

Not a status update. A Results and ROI Session.

**Structure:**
1. **Re-sell the decision** — remind client why they engaged Njin
2. **Results delivered** — what's done, in outcome language
3. **ROI to date** — cumulative value against the original promise
4. **Next sprint preview** — what's coming, inputs needed
5. **Seed next-stage upsell** — plant the idea (don't hard-pitch)

### Step 3.3: Capture Client Feedback

Communication Agent logs client feedback. Orchestrator updates COS with:
- Client sentiment
- New requests
- Any scope changes requested

---

## Stage 4: Sprint Retrospective (Internal)

### Step 4.1: Orchestrator Runs Retrospective Skill

Orchestrator invokes `retrospective` skill following SOP-004. 9 steps:

1. Pull completion data
2. Compare planned vs actual
3. Identify slipped items with reasons
4. Identify active blockers
5. Calculate velocity
6. Document wins (3 max), concerns (3 max), patterns
7. Produce ONE actionable recommendation
8. Update COS
9. Commit to GitHub, distribute internally

### Step 4.2: Review Findings with PM

PM reads retrospective output:
- Are the patterns accurate?
- Is the recommendation actionable?
- Any disagreements with the data?

### Step 4.3: Update COS

Orchestrator writes sprint results to `cos.yaml.sprints.history`:
- Number
- Planned / actual hours
- Velocity
- Carry-forward items
- Blockers
- Recommendation

---

## Stage 5: Next Sprint Planning

### Step 5.1: Apply Retrospective Insights

The retrospective's recommendation feeds into the next sprint plan:
- If velocity is declining, reduce planned scope
- If the same blocker keeps appearing, address it before starting new work
- If a story was underestimated, carry it forward at full effort (don't reduce)

### Step 5.2: Return to Stage 1

Next sprint planning begins. Cycle repeats.

---

## Re-Planning Triggers (Mid-Sprint)

| Trigger | Response |
|---------|----------|
| Blocker unresolved 24+ hours | PM assesses impact, may defer story |
| Scope change approved by PM | Coordinator updates plan, re-syncs njin-vibe |
| Team member unexpectedly unavailable | Recalculate capacity, adjust scope |
| Story significantly underestimated (>30% over) | Flag to PM, decide extend or defer |
| Velocity 25%+ below plan at midpoint | PM-triggered re-plan of remaining sprint |

---

## Cross-Sprint Tracking

Orchestrator maintains in `cos.yaml.sprints`:
```yaml
sprints:
  current: 3
  total_planned: 6
  history:
    - number: 1
      velocity: 28
      completion_rate: 92
    - number: 2
      velocity: 24
      completion_rate: 85
```

Flags to watch:
- **Velocity trend:** improving / stable / declining
- **Carry-forward accumulation:** stories repeatedly carried forward signal a real problem
- **Blocker recurrence:** same blocker twice = yellow flag, three times = red flag

---

## Anti-Patterns

- **Sprint review as status update** — always use Results & ROI Session structure
- **Planning >90% of last sprint's velocity** — build buffer for unknowns
- **Silently deferring stories** — every carry-forward is logged and PM-approved
- **Skipping retrospective** — the patterns only show over multiple sprints
- **Estimating carry-forwards at reduced effort** — always re-estimate at full effort
- **Not running mid-sprint check** — blockers caught late cost more than blockers caught early

---

## Deliverables Per Sprint

| Deliverable | Path |
|-------------|------|
| Sprint plan | `docs/planning/sprint-N-plan.md` |
| Sprint review (client-facing) | `docs/sprints/sprint-N-review.md` |
| Sprint retrospective (internal) | `docs/sprints/sprint-N-retrospective.md` |
| Updated COS | `cos.yaml` |
| njin-vibe sync | logged in COS |

---

*Reference: `methodology/frameworks/sprint-management.md`, `methodology/sops/sop-004-sprint-review.md`, `methodology/planning/sprint-planning-guide.md`.*
