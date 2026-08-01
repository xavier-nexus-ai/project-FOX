# Checklist: Plan Gate

**Purpose:** Validate that a project plan meets Njin PM Framework standards before sprint execution begins.

**Run by:** Orchestrator (via compliance-check skill), PM (final review), Product Owner (story validation)

**Gate:** `plan_ready` in `cos.yaml`

---

## Section 1: Scope Alignment

- [ ] Plan references the approved scope document
- [ ] Every scope deliverable is covered by at least one epic
- [ ] No deliverable is missed
- [ ] No "scope creep" added (new items not in the approved scope)

**Rule:** If the plan has more than the scope, that's scope creep. Flag and escalate before approving.

---

## Section 2: Epic Structure

- [ ] 3-8 epics total (not 1 mega-epic, not 20 tiny epics)
- [ ] Each epic has a clear name and description
- [ ] Each epic is tied to a framework phase
- [ ] Each epic has success criteria
- [ ] Epics are sequenced in a logical delivery order

---

## Section 3: Story Quality

For every story in the plan:

- [ ] Written in format: "As a [role], I want [action], so that [outcome]"
- [ ] Has a concise, actionable title
- [ ] Has 2-4 acceptance criteria (specific and testable)
- [ ] Has an effort estimate (hours or points)
- [ ] Has dependencies identified
- [ ] Has an epic link
- [ ] Has sprint assignment
- [ ] Meets the 2h+ threshold (anything smaller is a checklist item in a parent)
- [ ] Project prefix applied if multi-project client (e.g., `[LBT] Story Name`)

---

## Section 4: Estimation Discipline

- [ ] PM was asked the estimation question (AI self-estimate vs dev team hours)
- [ ] PM response is documented
- [ ] If AI self-estimate: assumptions are documented for every story
- [ ] If dev estimate: hours came from the assigned developer
- [ ] Variance between AI and dev estimates (if both exist) is noted if >30%
- [ ] Complexity multipliers applied where appropriate
- [ ] Risk buffers applied for unknowns (new integration, first time, etc.)

---

## Section 5: Capacity Reality Check

- [ ] Starting assumption was 100% capacity (per rule)
- [ ] Real availability applied (leave, public holidays, other commitments)
- [ ] 25% buffer applied for unknowns
- [ ] Final capacity is realistic, not aspirational
- [ ] Capacity accounts for meeting load in each sprint
- [ ] James's time budget respected (4h/day max, 20h/week)
- [ ] If plan exceeds available capacity, scope is cut or timeline extended (not silently overcommitted)

---

## Section 6: Sprint 1 Ready

- [ ] Sprint 1 plan exists
- [ ] Sprint 1 contains the Earliest Possible Win
- [ ] Sprint 1 is ready to start (no unresolved dependencies)
- [ ] Dependencies within Sprint 1 are sequenced
- [ ] Sprint 1 capacity is confirmed with team
- [ ] Kickoff call is scheduled (1 week after activation call)

**Critical rule:** If the Earliest Possible Win isn't in Sprint 1, the kickoff has nothing to demo. Restructure.

---

## Section 7: njin-vibe Sync Readiness

- [ ] Every story has a Project Dashboard link (critical — breaks tracking otherwise)
- [ ] Required fields populated: Title, Status, Priority, Assigned, Due Date, Est Effort, Category, Type
- [ ] Max 2-3 Critical/High per client
- [ ] Task titles don't contain client names (linked via Project Dashboard relation)
- [ ] Project prefix applied where needed
- [ ] Ready to push via vibe-sync skill

---

## Section 8: Dependencies and Risks

- [ ] Third-party dependencies identified
- [ ] Client-side dependencies identified (access, approvals, inputs)
- [ ] Risk register updated with new risks from planning
- [ ] Mitigation or contingency noted for high-likelihood/high-impact risks
- [ ] Blockers from discovery that are still open are tracked forward

---

## Section 9: Framework Alignment

- [ ] Phases in the plan match the framework's phases
- [ ] Blocking gates for this engagement are mapped
- [ ] Framework-specific deliverables are not missed (e.g., Tone of Voice gate for Njin Method)
- [ ] Compliance check run by Orchestrator before this gate

---

## Section 10: Writing Standards

- [ ] Australian English
- [ ] No em dashes
- [ ] No corporate jargon
- [ ] Plan is scannable (tables, bullet points, headings)
- [ ] Client-facing sections are at third-grade reading level

---

## Verdict

- **Pass** — All sections checked, plan is ready for sprint execution
- **Pass with concerns** — Minor issues noted but not blocking
- **Fail** — Critical issues; route back to Coordinator

### Common Fail Reasons

| Fail Reason | Fix |
|-------------|-----|
| EPW not in Sprint 1 | Restructure sprint priority |
| Stories missing acceptance criteria | Coordinator or PO adds them |
| Capacity assumed at 100% | Apply real availability and buffer |
| Project Dashboard link missing | Add before sync |
| >30% variance between AI and dev estimates, unresolved | Discuss with PM before locking |
| Plan exceeds capacity silently | Re-scope or re-negotiate timeline |

---

## Post-Gate Actions (If Pass)

1. Orchestrator updates `cos.yaml`:
   - `gates.plan_ready.passed`: true
   - `gates.plan_ready.checked`: <timestamp>
   - `phase.planning.status`: complete
2. vibe-sync skill pushes plan to njin-vibe
3. Change log entry
4. Workflow transitions to sprint-workflow.md

---

*Reference: `methodology/frameworks/sprint-management.md`, `methodology/planning/estimation-guide.md`, `methodology/ways-of-working/notion-task-guidelines.md`.*
