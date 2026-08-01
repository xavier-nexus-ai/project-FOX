# SOP-003: Discovery Procedure — Business Analyst Phase

## Title and Purpose

**Title:** Discovery Procedure SOP — BA Discovery Phase
**Purpose:** Define the step-by-step procedure for the Business Analyst's discovery phase. Ensures the BA follows the framework delivery procedure — not just the proposal — before any scoping or planning begins. Prevents the Avanti anti-pattern (plan created from proposal alone, without framework alignment).

---

## Trigger

`cos.yaml` phase is set to **Discovery** and the PM opens the Business Analyst agent.

---

## Prerequisites

- Initialisation Agent has been run — `cos.yaml` is populated with client name, engagement type, outcomes, and deliverables
- Handover bundle is in the client project folder (contract, SOW, transcripts, client docs)
- PM has reviewed and approved the Initialisation Agent's handover document before proceeding
- Engagement type is confirmed in `cos.yaml` (Playbook / Retainer / Custom AI / Transformation)

---

## Steps

### Step 1 — BA Reads All Background Documents

**Who:** Business Analyst agent (via PM session)
**What:**
1. BA reads every document in the client project folder:
   - Signed contract
   - Scope of Work
   - Reverse brief
   - Proposal
   - Sales call transcripts
   - Any client-provided materials (process docs, brand guides, existing systems info)
2. BA notes the engagement type from `cos.yaml` — this determines which framework reference applies in Step 2

**Output:** BA has full context on the client. No documents skipped.

---

### Step 2 — BA Consults the Correct Framework Reference

**Who:** Business Analyst agent
**What:**
The engagement type determines which framework delivery procedure the BA must follow. Consult the correct reference before producing any document plan.

| Engagement Type | Framework Reference |
|---|---|
| Retainer / Transformation | Map client journey first (reference: Emma/Legacy Thought Leaders workflow map pattern) |
| Playbook | Follow Njin Playbook delivery sequence — revenue pillar alignment required |
| Custom AI | Follow AI solution scoping procedure — technical requirements and integration mapping |
| Any type | Check `docs/ip-vault/` for extracted delivery sequences relevant to this engagement |

**Key rule:** Do not create a document plan based on the proposal alone. The framework delivery procedure defines what is required — the proposal defines what was sold. They must align, but the framework takes precedence on process.

**Output:** BA has identified the correct framework reference. Noted in working session.

---

### Step 3 — BA Creates the Requisite Document Plan

**Who:** Business Analyst agent
**What:**
Based on the engagement type and framework reference, the BA produces a **Requisite Document Plan** — a structured list of every document and artefact required to complete discovery and scoping correctly.

The plan includes:

| Column | Description |
|---|---|
| Document/Artefact | Name and description |
| Required For | Which phase or deliverable it supports |
| Status | Provided / Missing / Partial |
| Source | Who provides it (client, Sales, internal) |

At this stage, only mark items as "Provided" if the document is physically present in the client folder. Do not assume.

**Output:** Requisite Document Plan (draft). Saved as `discovery/requisite-document-plan.md` in client project folder.

---

### Step 4 — PM Reviews the Requisite Document Plan

**Who:** PM
**What:**
1. PM reads the Requisite Document Plan produced by the BA
2. PM checks: does the list reflect what the framework actually requires for this engagement type?
3. PM checks: are the "Provided" statuses accurate (documents physically present)?
4. PM either: approves the plan and instructs BA to proceed, OR requests amendments
5. Amendments are made and re-reviewed until PM approves

**This is a mandatory review gate — the BA does not proceed to Step 5 until the PM approves the document plan.**

**Output:** Requisite Document Plan approved by PM. Approval noted in handoff document.

---

### Step 5 — BA Analyses Provided Documents Against Requirements

**Who:** Business Analyst agent
**What:**
For each item marked "Provided" in the document plan, the BA:
1. Opens and reads the document in full
2. Assesses whether it satisfies the requirement it was provided for
3. Identifies any gaps within provided documents (e.g. transcript exists but doesn't cover required topics, SOW exists but missing pricing detail)
4. Notes partial items — a document that partially satisfies a requirement is not the same as a fully provided one

**Output:** Document analysis notes appended to the Requisite Document Plan. Each "Provided" item now has a quality assessment.

---

### Step 6 — BA Flags Missing Documents and Produces Gap Report

**Who:** Business Analyst agent
**What:**
1. BA compiles a **Discovery Gap Report** listing all items that are:
   - Entirely missing
   - Partially provided (and what's missing from them)
   - Present but insufficient quality for the requirement
2. For each gap, the BA produces a **specific client request** — not a generic "please provide more information" but a precise ask:

   Example:
   > "We need your current CRM workflow documented — specifically the steps from lead entry to first contact. A screen recording, written walkthrough, or existing SOP will all work."

3. Gap report is structured as a client-ready communication — the Communication Agent can convert it to a client-facing email or message if needed

**Workflow decision — missing documents:**
- If gaps are minor (1-2 items, non-blocking): proceed with caveats noted in `cos.yaml`, flag to PM
- If gaps are significant (blocking items missing): pause discovery, PM notifies client, workflow resumes when gaps are resolved

**Output:** Discovery Gap Report saved as `discovery/gap-report.md`. Specific client requests drafted and ready for Communication Agent.

---

### Step 7 — BA Produces Discovery Report

**Who:** Business Analyst agent
**What:**
After gap analysis is complete (or a "proceed with caveats" decision is made), the BA produces a **Discovery Report** covering:

1. **Client Context Summary** — who the client is, their business, the engagement goals
2. **Engagement Type and Framework Applied** — confirms which delivery procedure was followed
3. **Documents Reviewed** — full list with quality assessment
4. **Key Findings** — what was learned from the documents (goals, constraints, existing systems, pain points, quick wins)
5. **Gaps and Outstanding Requests** — summary of what's still needed and the specific requests sent/to be sent
6. **Readiness Assessment** — is discovery complete enough to proceed to scoping? Yes / No / Conditional
7. **Recommended Next Step** — what the PM should do next

**Output:** Discovery Report saved as `discovery/discovery-report.md`. `cos.yaml` updated with discovery findings and phase status.

---

### Step 8 — PM Reviews Discovery Report and Advances Phase

**Who:** PM
**What:**
1. PM reads the Discovery Report
2. If readiness is "Yes" or "Conditional" (and PM agrees): update `cos.yaml` phase to **Scoping**, approve the handoff document
3. If readiness is "No": PM coordinates with Sales/client to resolve gaps. Phase stays at Discovery.
4. PM commits changes to GitHub

**Output:** `cos.yaml` phase advanced to Scoping (or held at Discovery with gap resolution in progress). GitHub commit made.

---

## Quality Check

Before marking discovery complete:

- [ ] Engagement type confirmed in `cos.yaml`
- [ ] Correct framework reference consulted (not just the proposal)
- [ ] Requisite Document Plan approved by PM before analysis began
- [ ] Every "Provided" document has been read and assessed (not just listed)
- [ ] Gap Report produced with specific client requests (not generic asks)
- [ ] Discovery Report produced and reviewed by PM
- [ ] `cos.yaml` updated with discovery findings
- [ ] Any outstanding gaps either resolved or formally noted as "proceed with caveats"
- [ ] GitHub commit made

---

## Output

- `discovery/requisite-document-plan.md` — approved by PM
- `discovery/gap-report.md` — with specific client requests
- `discovery/discovery-report.md` — with readiness assessment
- `cos.yaml` updated — phase advanced or gap resolution tracked
- GitHub commit recorded
