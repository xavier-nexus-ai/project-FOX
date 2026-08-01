# Workflow: Discovery (BA Phase — Before Scoping)

**Purpose:** Run the Business Analyst's discovery phase to gather all required information before scoping can begin. Prevents the Avanti anti-pattern of planning from a proposal alone.

**Duration:** 1-3 days (depends on client responsiveness to gap requests).

**Owner:** PM (driving), Orchestrator (coordinating), Business Analyst (executing)

---

## Prerequisites

- [ ] Init phase complete
- [ ] `cos.yaml` and `CLAUDE.md` exist
- [ ] Handover bundle in `docs/background/`
- [ ] Engagement type confirmed in `cos.yaml`

---

## Workflow Steps

### Step 1: Orchestrator Creates Discovery Handoff

Orchestrator:
1. Reads `cos.yaml` to confirm we're in init-complete state
2. Reads engagement type to identify which framework reference to use
3. Creates handoff for Business Analyst with:
   - Context: client name, engagement type, what we know from handover
   - Task: run discovery skill, produce requisite document plan
   - Inputs: contents of `docs/background/`, framework reference path
   - Expected output: Requisite Document Plan, then (after PM review) Gap Report and Discovery Report
   - Constraint: consult framework reference, NOT just the proposal

Saves to `docs/handoffs/discovery-handoff.md`. PM reviews.

---

### Step 2: PM Reviews Handoff

PM reads the handoff. Key checks:
- Is the engagement type right?
- Is the framework reference correct for this type?
- Are all available background docs listed?

If issues, PM amends. If OK, PM proceeds.

---

### Step 3: Business Analyst Runs Discovery Skill (Part 1)

PM opens new chat:

```
@.claude/agents/business-analyst.md
```

BA (Part 1):
1. Reads handoff document
2. Reads all files in `docs/background/`
3. Consults `methodology/frameworks/<engagement_type>.md` for the delivery framework
4. Consults `methodology/scoping/<engagement_type>-scoping.md` for the intake checklist
5. Produces **Requisite Document Plan** as text output
6. Returns to PM for review

**Critical:** At this point, the BA has NOT yet analysed what's provided. It's only producing the list of what's NEEDED.

---

### Step 4: PM Reviews Requisite Document Plan (Mandatory Gate)

Orchestrator writes the plan to `docs/discovery/requisite-document-plan.md`.

**PM reads and checks:**
- [ ] Does the list match what the framework actually requires for this engagement type?
- [ ] Are the "Provided" statuses accurate (documents physically present in background)?
- [ ] Are any critical items missing from the required list that the BA should add?

**This is a mandatory review gate.** BA does not proceed until PM approves.

If PM requests changes:
- BA amends the plan
- PM re-reviews

If PM approves:
- Orchestrator updates `cos.yaml.phase.discovery.deliverables.requisite_document_plan`: true
- Orchestrator updates `cos.yaml.phase.discovery.deliverables.document_plan_pm_approved`: true

---

### Step 5: Business Analyst Runs Discovery Skill (Part 2)

PM (same chat or new chat) continues with BA:

BA (Part 2):
1. For each item marked "Provided" in the document plan:
   - Opens and reads the document in full
   - Assesses whether it satisfies the requirement
   - Identifies gaps within provided docs (e.g., transcript exists but doesn't cover required topics)
   - Notes partial items
2. Compiles a **Discovery Gap Report** listing:
   - Entirely missing items
   - Partially provided items
   - Present but insufficient quality
3. For each gap, produces a **specific client request** (not "please provide more information" but precise, actionable asks)

---

### Step 6: Orchestrator Extracts and Writes Gap Report

Orchestrator writes to `docs/discovery/gap-report.md`. Updates COS:
- `phase.discovery.deliverables.documents_analysed`: true
- `phase.discovery.deliverables.gap_report`: true

---

### Step 7: Decision Point — Gaps Handling

**If gaps are minor (1-2 items, non-blocking nice-to-haves):**
- Log as caveats in COS
- Flag to PM
- Proceed to Step 8 (Discovery Report)

**If gaps are significant (blocking items missing):**
- Orchestrator pauses discovery workflow
- Communication Agent drafts client-facing request based on gap report
- PM sends to client
- Update `cos.yaml.blockers` with client deadline
- Wait for client response (5 business days max before escalation)
- When received, return to Step 5 and re-analyse

---

### Step 8: Business Analyst Produces Discovery Report

BA produces the final Discovery Report covering:
1. **Client Context Summary** — who the client is, business, engagement goals
2. **Engagement Type and Framework Applied** — confirms delivery procedure followed
3. **Documents Reviewed** — full list with quality assessment
4. **Key Findings** — goals, constraints, existing systems, pain points, quick wins
5. **Gaps and Outstanding Requests** — summary of what's still needed
6. **Readiness Assessment** — Yes / No / Conditional for scoping
7. **Recommended Next Step** — what the PM should do next

---

### Step 9: Orchestrator Extracts and Writes Discovery Report

Orchestrator writes to `docs/discovery/discovery-report.md`. Updates COS:
- `phase.discovery.deliverables.discovery_report`: true
- `phase.discovery.deliverables.missing_items_requested`: true (if applicable)

---

### Step 10: PM Reviews Discovery Report

PM reads report. Decision:
- **Readiness Yes or Conditional:** approve, advance to scoping
- **Readiness No:** coordinate with Sales/client to resolve gaps, stay in discovery

---

### Step 11: Gate Check and Phase Advance

If PM approves and readiness is Yes/Conditional:

Orchestrator:
- `gates.discovery_complete.passed`: true
- `gates.discovery_complete.checked`: <timestamp>
- `phase.discovery.status`: complete
- `phase.scoping.status`: in_progress
- `cos.yaml.phase.current`: scoping
- Change log entry
- Commit to GitHub

Workflow transitions to `scope-workflow.md`.

---

## Deliverables

| Deliverable | Path |
|-------------|------|
| Requisite Document Plan | `docs/discovery/requisite-document-plan.md` |
| Gap Report | `docs/discovery/gap-report.md` |
| Discovery Report | `docs/discovery/discovery-report.md` |
| Handoff to Scoping | `docs/handoffs/scoping-handoff.md` |

---

## Anti-Patterns

- **Skipping the PM review gate on the Requisite Document Plan** — this is mandatory
- **Creating the document plan from the proposal alone** — always consult framework reference
- **Generic gap requests** — "please provide more info" is not a request; "we need your CRM admin credentials by Friday" is
- **Running discovery and scoping in parallel** — they are strictly sequential
- **Proceeding to scoping with hard blockers unresolved** — stops the workflow, always

---

*Reference: `methodology/sops/sop-003-discovery-procedure.md`, `methodology/frameworks/`, `methodology/scoping/`.*
