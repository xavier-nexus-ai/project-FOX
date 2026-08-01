# Checklist: Sprint Gate (Sprint Readiness)

**Purpose:** Validate that a sprint is ready to start before locking it. Prevents half-baked sprints that waste team time.

**Run by:** Coordinator (initial check), Orchestrator (compliance check), PM (final approval)

**Gate:** `kickoff_ready` (for sprint 1) or sprint-level gate for subsequent sprints

---

## Section 1: Sprint Definition

- [ ] Sprint number is assigned
- [ ] Sprint start and end dates set (fortnightly cadence)
- [ ] Sprint goal is defined in one sentence
- [ ] Sprint plan exists and is written down

---

## Section 2: Stories in the Sprint

For every story committed to the sprint:

- [ ] Acceptance criteria are specific and testable (2-4 per story)
- [ ] Effort estimate exists
- [ ] Owner is assigned (never "TBD")
- [ ] Dependencies are identified
- [ ] Dependencies within this sprint are sequenced (not running in parallel if they shouldn't)
- [ ] Dependencies outside this sprint are already done or in progress
- [ ] Story meets 2h+ threshold

---

## Section 3: Capacity Validation

- [ ] Sprint was planned starting at 100% capacity
- [ ] Actual availability applied (leave, holidays, other projects, meetings)
- [ ] 25% buffer applied for unknowns
- [ ] Total planned effort fits within adjusted capacity
- [ ] No individual team member is overcommitted
- [ ] James's 4h/day budget respected

**Rule:** If capacity doesn't fit the scope, cut the scope — don't promise what can't be delivered.

---

## Section 4: Dependencies Ready

- [ ] All external dependencies (client access, approvals, third-party) are in place or have confirmed delivery dates
- [ ] Any blocker from last sprint that affects this sprint is resolved
- [ ] Required inputs from the client have been received
- [ ] Tools and access needed by the team are ready

---

## Section 5: Sprint 1 Specific Checks (skip for Sprint 2+)

- [ ] Earliest Possible Win is in this sprint
- [ ] Kickoff call is scheduled (1 week after activation call)
- [ ] Quick win deliverable is ready to demo at kickoff
- [ ] Client has been briefed on what's coming
- [ ] Dashboard access is active for the client

---

## Section 6: Sprint 2+ Specific Checks (skip for Sprint 1)

- [ ] Previous sprint retrospective is complete
- [ ] Previous sprint's ONE recommendation has been applied
- [ ] Carry-forward items from last sprint are re-estimated at full effort
- [ ] Velocity trend is noted (improving / stable / declining)
- [ ] Next sprint plan does not exceed 90% of last sprint's velocity

---

## Section 7: njin-vibe Sync

- [ ] Sprint exists in njin-vibe
- [ ] All stories in the sprint are linked to Project Dashboard
- [ ] Sprint calendar entries are created (recurring fortnightly events)
- [ ] Dashboard sections for the sprint are ready

---

## Section 8: Communication Ready

- [ ] Client knows the sprint is starting
- [ ] Sprint review date is scheduled
- [ ] Any client inputs needed during the sprint are requested
- [ ] Communication channel is active (WhatsApp, Slack, email)

---

## Section 9: Risk Check

- [ ] New risks from planning are in the risk register
- [ ] Active blockers from prior sprints are still tracked
- [ ] Mitigation plans for high-impact risks exist

---

## Section 10: Writing Standards (for client-facing sprint comms)

- [ ] Australian English
- [ ] No em dashes
- [ ] No corporate jargon
- [ ] Sprint goals framed as outcomes, not activities
- [ ] Success criteria are measurable

---

## Verdict

- **Pass** — Sprint is ready to start
- **Pass with concerns** — Minor issues, proceed with documented caveats
- **Fail** — Critical issues; do not start the sprint

### Common Fail Reasons

| Fail Reason | Fix |
|-------------|-----|
| Story has no acceptance criteria | Product Owner adds them, or Coordinator writes them |
| Client access not in place | Chase client, delay sprint start if critical |
| Capacity overcommitted | Cut scope to fit |
| Quick win not ready for Sprint 1 kickoff | Halt until resolved |
| Project Dashboard link missing | Add before sync |
| Prior sprint retrospective not done | Run it before starting next sprint |

---

## Post-Gate Actions (If Pass)

1. Orchestrator updates `cos.yaml`:
   - `sprints.current`: N
   - `phase.sprint_execution.status`: in_progress
   - Change log entry
2. vibe-sync skill pushes sprint data
3. Coordinator announces sprint start internally
4. Communication Agent sends sprint start notification to client (if applicable)

---

## Mid-Sprint Re-Check

This checklist is also run mid-sprint if re-planning is triggered. Key questions at mid-sprint:
- Is velocity tracking on plan?
- Are there new blockers?
- Is scope still realistic?
- Do we need to defer or cut any stories?

If mid-sprint re-plan is needed, run the relevant sections again and update COS.

---

*Reference: `methodology/frameworks/sprint-management.md`, `methodology/sops/sop-004-sprint-review.md`, `methodology/planning/sprint-planning-guide.md`.*
