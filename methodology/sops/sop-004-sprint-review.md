# SOP-004: Sprint Review and Retrospective

## Title and Purpose

**Title:** Sprint Review and Retrospective SOP
**Purpose:** Define a consistent, repeatable process for reviewing completed sprints. Produces a clear record of what was planned vs. delivered, identifies blockers and patterns, calculates velocity, and produces one actionable recommendation for the next sprint.

---

## Trigger

A sprint ends (fortnightly by default per the Njin delivery model). PM receives a notification from the sprint calendar, or the sprint end date arrives in `cos.yaml`.

---

## Prerequisites

- Sprint was formally planned — a sprint plan exists with a defined list of planned items and estimated hours
- At least one sprint has been completed (cannot run a review on Sprint 0 or a project with no tracked delivery)
- PM has access to the client project folder and `cos.yaml`
- Any njin-vibe data is up to date (PM has synced outstanding updates before running the review)

---

## Steps

### Step 1 — Pull Completion Data

**Who:** PM (via Coordinator agent or manually)
**What:**
1. Open `cos.yaml` — review the current sprint section
2. List every item that was in the sprint plan:
   - Item name
   - Planned hours
   - Actual hours (if tracked)
   - Status: Complete / Partial / Not Started / Blocked
3. Pull any supporting data from njin-vibe (task completion records, logged hours, status updates) using the njin-vibe sync skill if data is there
4. If hours were not tracked during the sprint, use the PM's best estimate and flag it as estimated (not measured)

**Output:** Raw completion data table. Saved as working notes in `sprints/sprint-[N]-review-data.md`.

---

### Step 2 — Compare Planned vs. Actual

**Who:** PM (via Coordinator agent)
**What:**
Produce a side-by-side comparison:

| Item | Planned Hours | Actual Hours | Status | Notes |
|---|---|---|---|---|
| [Item 1] | X | Y | Complete | — |
| [Item 2] | X | — | Blocked | Waiting on client access |
| [Item 3] | X | Y | Partial | 60% done, carries to next sprint |

Calculate:
- **Planned total hours**
- **Actual total hours delivered**
- **Completion rate:** (# items fully complete) / (# items planned) x 100
- **Hour variance:** actual vs. planned (positive = over-ran, negative = under-ran)

**Output:** Comparison table with calculated metrics.

---

### Step 3 — Identify Slipped Items

**Who:** PM
**What:**
For every item that is Partial or Not Started, record:
1. Item name
2. Reason it slipped (choose one primary reason):
   - Blocked by client (missing access, approvals, information)
   - Blocked by internal (dependency not ready, resource unavailable)
   - Scope grew during sprint
   - Estimation was off (underestimated complexity)
   - Deprioritised during sprint (something more urgent took over)
   - No reason recorded (flag this — it should not happen)
3. Whether it carries to the next sprint or is dropped/deferred

**Output:** Slipped items list with reasons. Carries-to-next list identified.

---

### Step 4 — Identify Blockers

**Who:** PM
**What:**
Separate from slipped items, identify any **active blockers** — issues that will affect the next sprint if not resolved now:

| Blocker | Type | Owner | Resolution Required By |
|---|---|---|---|
| Client hasn't provided CRM access | Client | PM to follow up | Before Sprint N+1 starts |
| Dev dependency not built | Internal | Xavier | Mid Sprint N+1 |

For each blocker, the PM must assign an owner and a resolution deadline before closing the review.

**Output:** Active blocker register. Each blocker has an owner and deadline.

---

### Step 5 — Calculate Velocity

**Who:** PM (via Coordinator agent)
**What:**
Velocity = the amount of work actually completed in the sprint, measured in story points or hours (whichever the project uses).

1. Sum total hours (or points) of fully completed items only — partial items do not count toward velocity
2. If this is Sprint 2 or later, compare to previous sprint(s):
   - Is velocity increasing, stable, or decreasing?
   - Note the trend
3. Use velocity to calibrate the next sprint plan — do not plan more than 90% of the last sprint's velocity (buffer for unknowns)

**Output:** Sprint velocity figure. Trend noted if Sprint 2+. Next sprint capacity estimate calculated.

---

### Step 6 — Document Wins, Concerns, and Patterns

**Who:** PM
**What:**

**Wins (what went well):**
- List 2-3 specific things that worked — delivered items, process improvements, client feedback received
- Be specific: "Delivered email automation on time and client confirmed it saved 3 hours/week" is a win. "Good sprint" is not.

**Concerns (what didn't go well):**
- List 2-3 specific problems — estimation errors, communication gaps, blockers that weren't caught early
- Be honest. Concerns that aren't documented repeat.

**Patterns (what's recurring):**
- Look across this sprint and any previous reviews in `cos.yaml`
- Are the same blockers appearing? The same items slipping? The same client not responding on access?
- A pattern appearing twice is a yellow flag. Three times is a red flag requiring a process change.

**Output:** Wins/concerns/patterns section in the sprint review document.

---

### Step 7 — Produce One Actionable Recommendation

**Who:** PM
**What:**
Based on everything above, produce exactly **one** recommendation for the next sprint. Not a list. One.

The recommendation must be:
- Specific (not "improve communication" — "schedule a mid-sprint check-in every Wednesday to catch blockers before they stall delivery")
- Actionable (someone can act on it immediately)
- Assigned (who is responsible for implementing it)

Write it as:
> **Recommendation:** [specific action] — owned by [person] — to be in place by [when].

**Output:** Single sprint recommendation, ready for PM to action.

---

### Step 8 — Update COS with Sprint Results

**Who:** PM
**What:**
Update `cos.yaml` with the following:

1. Mark sprint as complete — update the sprint status field
2. Record velocity for this sprint
3. Log slipped items with carry-forward status
4. Log active blockers with owners and deadlines
5. Add the sprint recommendation to the next sprint planning notes
6. Add a `change_log` entry summarising the sprint close

**Output:** `cos.yaml` updated. Sprint record is permanent and accessible in future sessions.

---

### Step 9 — Commit to GitHub and Distribute

**Who:** PM
**What:**
1. Commit the sprint review document and updated `cos.yaml` to GitHub
2. Distribute sprint summary to relevant stakeholders:
   - Internal: James and/or George (via group chat or email, depending on engagement)
   - Client-facing: If the client receives sprint reports, pass the summary to the Communication Agent to produce a client-facing version (strip internal notes, translate into outcomes language)
3. For retainer clients: the sprint report is a touchpoint — frame it as a "Results & ROI Session" update, re-sell why they bought, show ROI, seed next-stage upsell (per the Customer Success Management pattern in the onboarding flow)

**Output:** Sprint review document committed to GitHub. Summary distributed. Client-facing report (if applicable) queued for Communication Agent.

---

## Quality Check

Before closing the sprint review:

- [ ] Every planned item has a status (Complete / Partial / Not Started / Blocked) — none left blank
- [ ] Slipped items all have a documented reason (no unexplained slippage)
- [ ] All blockers have an owner and a resolution deadline
- [ ] Velocity calculated from completed items only (partials excluded)
- [ ] Wins, concerns, and patterns documented with specifics (no vague statements)
- [ ] Exactly one recommendation produced — not a list
- [ ] `cos.yaml` updated with sprint results and change log entry
- [ ] GitHub commit made
- [ ] Summary distributed to internal team
- [ ] Client-facing report queued if applicable

---

## Output

- `sprints/sprint-[N]-review.md` — full sprint review document
- `cos.yaml` updated — sprint closed, blockers logged, recommendation noted
- GitHub commit recorded
- Internal summary distributed
- Client-facing sprint report (if applicable) queued for Communication Agent
