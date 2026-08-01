# Workflow: Scoping a Project

**Purpose:** Take client discovery output and produce a framework-aligned scope document. Enforces the rule that plans must align to framework delivery procedures, not just proposals.

**Duration:** Typically 1 day (can extend if gaps need client follow-up).

**Owner:** PM (driving), Orchestrator (coordinating), Business Analyst (executing)

---

## Prerequisites

- [ ] Discovery phase complete
- [ ] Discovery Report produced and PM-reviewed
- [ ] `discovery_complete` gate passed in `cos.yaml`
- [ ] Any critical gaps resolved or formally noted as caveats
- [ ] Engagement type confirmed

---

## Workflow Steps

### Step 1: Orchestrator Creates Scoping Handoff

Orchestrator:
1. Reads `cos.yaml` to confirm discovery is complete
2. Reads the Discovery Report
3. Consults framework-router skill to confirm which delivery framework applies
4. Creates handoff document for Business Analyst with:
   - Context: client name, engagement type, discovery findings
   - Task: run scoping skill, produce framework-aligned scope document
   - Inputs: Discovery Report, handover bundle, framework reference
   - Expected output: scope document with deliverables as outcomes
   - Constraints: must consult framework reference, must include Earliest Possible Win
5. Saves handoff to `docs/handoffs/scoping-handoff.md`

---

### Step 2: PM Reviews Handoff

PM reads the handoff document. Verifies:
- [ ] Context is accurate
- [ ] Framework reference is correct
- [ ] Inputs are complete
- [ ] Expected output is clear
- [ ] No missing information that would lead to a bad scope

If any issue, PM amends the handoff. If good, PM proceeds to Step 3.

---

### Step 3: Business Analyst Runs Scoping Skill

PM opens new chat:

```
@.claude/agents/business-analyst.md
```

BA:
1. Reads handoff document
2. Runs `scoping` skill
3. Consults `methodology/frameworks/<engagement_type>.md` for framework reference
4. Consults `methodology/sops/` if applicable (e.g., playbook-creation-sop.md)
5. Maps every deliverable in the scope to a framework phase
6. Identifies gaps between proposal and framework procedure
7. Frames deliverables as outcomes, not features
8. Includes Earliest Possible Win prominently
9. Produces scope document (text output, not file write)

**Critical rule:** If the proposal and the framework procedure conflict, the framework wins. Flag the conflict to the PM.

---

### Step 4: Orchestrator Extracts and Writes Scope

Orchestrator:
1. Reviews BA's text output
2. Extracts scope document content
3. Writes to `docs/scoping/scope-document.md`
4. Updates `cos.yaml`:
   - `deliverables.scope_document`: path
   - `phase.scoping.deliverables.scope_document`: true
5. Adds change log entry

---

### Step 5: Orchestrator Runs Compliance Check

Orchestrator invokes `compliance-check` skill on the scope document:

**Checks run:**
- [ ] Phases match the framework delivery procedure
- [ ] All phases have defined deliverables
- [ ] Blocking gates are identified
- [ ] Earliest Possible Win is present
- [ ] Deliverables framed as outcomes, not features
- [ ] No corporate jargon (leverage, synergy, holistic, etc.)
- [ ] Estimates are reasonable (if included)
- [ ] Australian English, no em dashes

**Verdict:** Pass / Pass with concerns / Fail

If **Fail**: route back to BA with specific issues. Do not proceed.
If **Pass with concerns**: present to PM with concerns noted.
If **Pass**: proceed to Step 6.

---

### Step 6: PM Reviews Scope

PM reads the scope document. Verifies:
- [ ] Scope accurately reflects what was agreed
- [ ] Framework-aligned (phases match framework)
- [ ] Earliest Possible Win is specific and achievable
- [ ] Deliverables are outcome-framed
- [ ] Any gaps are flagged with specific client asks
- [ ] Assumptions and risks are documented

If issues, PM amends or routes back to BA. If good, PM approves.

---

### Step 7: Update COS

Orchestrator updates `cos.yaml`:
- `phase.scoping.deliverables.scope_document`: true
- `phase.scoping.deliverables.scope_pm_approved`: true
- `phase.scoping.status`: complete
- `gates.scope_approved.passed`: true
- `gates.scope_approved.checked`: <timestamp>
- Change log entry

---

### Step 8: Client Review (Optional)

Depending on engagement type, scope may need client sign-off before planning begins.

**For Njin Method (playbook engagements):** Client review typically happens at end of Immersion phase.

**For AI Orchestration:** Scope is reviewed with client during Mapping phase.

**For Vibe/Web/Product:** Client review is usually required before sprint planning.

If client review is needed:
1. Communication Agent drafts client-facing scope summary
2. PM sends to client
3. Wait for response (3-5 business days)
4. Incorporate feedback
5. Re-run compliance check if material changes

---

### Step 9: Handoff to Planning

Orchestrator creates handoff for Coordinator:
- Approved scope document
- Framework reference
- Client capacity/deadline constraints
- Task: create project plan with epics, stories, sprint plan

Workflow transitions to `plan-workflow.md`.

---

## Deliverables

| Deliverable | Path |
|-------------|------|
| Scope document | `docs/scoping/scope-document.md` |
| Compliance report (if any issues) | `docs/scoping/compliance-report.md` |
| Handoff to Coordinator | `docs/handoffs/planning-handoff.md` |

---

## Failure Modes

| Failure | Recovery |
|---------|----------|
| BA cannot find framework reference | Orchestrator points to `methodology/frameworks/` — do not proceed without reference |
| Compliance check fails | Route back to BA with specific issues — do not proceed |
| Scope doesn't match proposal | Flag the conflict. Framework wins. Escalate to James if client pushback expected |
| Earliest Possible Win missing | Cannot pass scope gate — BA must add it |
| Client rejects scope | Incorporate feedback, re-run BA scoping, re-run compliance |

---

## Anti-Patterns

- **Scope built from proposal alone** — this is the Avanti anti-pattern. Never do this.
- **Running scoping before discovery is complete** — these are sequential, not parallel.
- **Generic deliverables** — "setup CRM" is not a deliverable. "Eliminate 10 hours of manual data entry per week" is.
- **Skipping compliance check** — always run it before presenting to PM.
- **Client review before PM approval** — PM reviews first, always.

---

*Reference: `methodology/sops/sop-003-discovery-procedure.md`, `methodology/frameworks/` for framework references.*
