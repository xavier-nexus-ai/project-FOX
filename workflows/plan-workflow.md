# Workflow: Project Planning (Scope > Epics > Stories > Sprint)

**Purpose:** Take an approved scope and produce a complete project plan with epics, user stories, estimates, and a sprint schedule.

**Duration:** 1-2 days.

**Owner:** PM (driving), Orchestrator (coordinating), Coordinator (executing), Product Owner (validating)

---

## Prerequisites

- [ ] Scope document exists and is PM-approved
- [ ] `scope_approved` gate passed
- [ ] Engagement type confirmed
- [ ] Client capacity and deadlines known

---

## Workflow Steps

### Step 1: Orchestrator Creates Planning Handoff

Orchestrator:
1. Reads approved scope document
2. Reads `methodology/planning/estimation-guide.md` for baseline durations
3. Reads `methodology/planning/sprint-planning-guide.md` for sprint rules
4. Creates handoff for Coordinator with:
   - Scope document content
   - Framework reference
   - Known client constraints (deadlines, capacity)
   - Task: break scope into epics, stories, estimates, sprint plan

Saves to `docs/handoffs/planning-handoff.md`. PM reviews.

---

### Step 2: Coordinator Breaks Scope into Epics

PM opens new chat:

```
@.claude/agents/coordinator.md
```

Coordinator:
1. Reads handoff
2. Identifies major deliverables in scope
3. Groups into epics (each epic = one major deliverable or outcome)
4. Each epic gets: name, description, success criteria, framework phase it belongs to
5. Outputs epic list as text

**Typical epic count:** 3-8 epics per engagement.

---

### Step 3: Coordinator Breaks Epics into Stories

For each epic, Coordinator:
1. Runs `story-writer` skill
2. Decomposes epic into user stories in format: "As a [role], I want [action], so that [outcome]"
3. Each story gets: title, role, acceptance criteria (2-4), dependencies, epic link
4. Enforces 2h+ rule — anything smaller becomes a checklist item in a parent story
5. Applies project prefix for multi-project clients: `[LBT] Story Name`

---

### Step 4: Coordinator Asks Estimation Question

**Critical checkpoint.** Coordinator asks PM:

> "Should I estimate hours for these stories myself, or do you want to pull hours from the dev team?"

PM decides based on:
- **AI self-estimate** if: early planning, well-defined work, similar to prior, speed matters
- **Dev team estimate** if: sprint commitment, technical uncertainty, custom build, specific dev assigned

If PM doesn't respond, default to AI self-estimate with a flag for later validation.

---

### Step 5: Coordinator Estimates (or Waits for Dev Estimates)

**If AI self-estimate:**
- Coordinator runs `estimation` skill
- Applies heuristics from `methodology/planning/estimation-guide.md`
- Documents assumptions for each estimate
- Applies complexity multipliers and risk buffers
- Outputs estimates with confidence levels

**If dev team estimate:**
- Coordinator pauses
- PM collects hours from dev team
- PM provides estimates to Coordinator
- Coordinator incorporates without overriding

---

### Step 6: Coordinator Plans Sprint 1

Coordinator runs `sprint-planning` skill:
1. Starts with 100% capacity assumption
2. PM provides real availability (leave, meetings, other commitments)
3. Applies 25% buffer for unknowns
4. Sequences stories by dependencies
5. Applies revenue-first prioritisation
6. Fills sprint to capacity
7. Identifies carry-over if over capacity

Output: Sprint 1 plan with stories, estimates, dependencies, blockers.

---

### Step 7: Coordinator Plans Full Engagement Roadmap

For multi-sprint engagements, Coordinator lays out:
- Sprint 2, 3, 4... through engagement end
- Deliverables per sprint
- Milestones aligned to framework phases
- Client-facing checkpoints (demos, reviews, sign-offs)

---

### Step 8: Orchestrator Extracts Plan and Writes Files

Orchestrator:
1. Reviews Coordinator's text output
2. Writes:
   - `docs/planning/project-plan.md` — full engagement plan
   - `docs/planning/sprint-1-plan.md` — detailed sprint 1
   - `docs/planning/stories/` — individual story files (one per story)
3. Updates `cos.yaml`:
   - `phase.planning.deliverables.epics_created`: true
   - `phase.planning.deliverables.stories_created`: true
   - `phase.planning.deliverables.estimates_complete`: true
   - `phase.planning.deliverables.sprint_1_planned`: true
   - `sprints.total_planned`: N
4. Change log entry

---

### Step 9: Product Owner Reviews Stories (Optional but Recommended)

For large engagements or first-time project types, route to Product Owner for story validation:

```
@.claude/agents/product-owner.md
```

Product Owner:
1. Reviews each story for quality
2. Checks acceptance criteria are testable
3. Verifies 2h+ threshold
4. Checks grouping rules (one parent task with checklist, not 5 cards)
5. Validates Critical/High priority limits (max 2-3 per client)
6. Flags issues

Fix any issues before proceeding.

---

### Step 10: Orchestrator Runs Compliance Check

Orchestrator invokes `compliance-check` skill on the plan:

**Checks:**
- [ ] Plan aligns to scope
- [ ] Phases match framework
- [ ] Every story has acceptance criteria
- [ ] Estimates are reasonable
- [ ] Capacity is realistic (not 100% assumption left in place)
- [ ] Dependencies are sequenced
- [ ] Earliest Possible Win is in sprint 1

**If fail:** route back to Coordinator with specific issues.
**If pass:** proceed to Step 11.

---

### Step 11: PM Approves Plan

PM reads:
- Project plan
- Sprint 1 plan
- Sample stories

Verifies realistic, aligned, executable. Approves or requests amendments.

---

### Step 12: Sync to njin-vibe

Orchestrator invokes `vibe-sync` skill:
- Pushes epics, stories, sprint plan to njin-vibe
- Confirms Project Dashboard links are set on every task
- Logs sync completion in COS

---

### Step 13: Update COS and Gate

Orchestrator updates `cos.yaml`:
- `gates.plan_ready.passed`: true
- `gates.plan_ready.checked`: <timestamp>
- `phase.planning.status`: complete
- Change log entry

Workflow transitions to `sprint-workflow.md`.

---

## Deliverables

| Deliverable | Path |
|-------------|------|
| Project plan | `docs/planning/project-plan.md` |
| Sprint 1 plan | `docs/planning/sprint-1-plan.md` |
| Individual stories | `docs/planning/stories/` |
| njin-vibe sync confirmation | logged in COS |

---

## Failure Modes

| Failure | Recovery |
|---------|----------|
| Scope is too vague to plan | Route back to BA to clarify scope — do not force a plan on vague scope |
| Capacity doesn't fit scope | PM decides: reduce scope, extend timeline, or increase resources. Never silently over-commit. |
| Dev team estimates much higher than AI | Flag variance >30% to PM before locking sprint |
| Stories too large (>16h) | Break down further. No sprint gets stories larger than 16h un-broken. |
| Project Dashboard link missing in njin-vibe | Cannot sync — must fix before advancing |
| Earliest Possible Win not in sprint 1 | Restructure sprint — the EPW must be visible to client at kickoff |

---

## Anti-Patterns

- **Planning at 100% capacity** — always apply the 25% buffer and real availability
- **Vague acceptance criteria** — every story needs 2-4 specific, testable criteria
- **Skipping the estimation question** — Coordinator must ask PM; never default silently
- **Over-committing to look productive** — plan 90% of last sprint's velocity, not 110%
- **Creating tasks without Project Dashboard relation** — breaks njin-vibe tracking

---

*Reference: `methodology/planning/estimation-guide.md`, `methodology/planning/sprint-planning-guide.md`, `methodology/frameworks/sprint-management.md`.*
