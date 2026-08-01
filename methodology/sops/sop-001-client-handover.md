# SOP-001: Client Handover — Sales to PMO

## Title and Purpose

**Title:** Client Handover SOP — Sales to PMO
**Purpose:** Define the handover process after a client signs a contract, ensuring the PMO has everything it needs before discovery starts. Prevents the BA from beginning work with incomplete information.

---

## Trigger

Client signs contract and payment is confirmed (or first payment received for staged engagements). Sales marks the deal as won in GHL and moves the pipeline card to the PMO handover stage.

---

## Prerequisites

- Contract fully executed (e-signature complete)
- Payment confirmed or payment terms agreed
- Reverse brief approved by client prior to contract
- Scope of Work document exists (Google Doc)

---

## Steps

### Step 1 — Sales Packages the Handover Bundle

**Who:** Sales (James or George)
**What:**
Compile the following into a single handover folder (Google Drive or shared workspace):

| Item | Required? | Notes |
|---|---|---|
| Signed contract | Mandatory | PDF from e-signature platform |
| Scope of Work document | Mandatory | Defines deliverables, timeline, engagement type |
| Reverse brief (approved) | Mandatory | Confirms problem/cost framing |
| Proposal PDF | Mandatory | Includes deliverables translated into outcomes |
| Sales call transcripts | Mandatory | All recorded calls from prospecting through close |
| Reverse brief email thread | Mandatory | Client approval in writing |
| Client-provided documents | Where available | Any materials client shared during sales (e.g. brand guides, process docs, existing systems info) |
| GHL pipeline notes | Mandatory | Any notes logged in CRM during sales cycle |
| Engagement type | Mandatory | One of: Playbook, Retainer, Custom AI, Transformation |
| "Earliest Possible Win" | Mandatory | Defined during scoping — must be explicit |

**Output:** Handover bundle folder, link shared with PMO in group chat (WhatsApp or Slack).

---

### Step 2 — PMO Acknowledges Receipt

**Who:** PM (George or Michael)
**What:**
- Confirm receipt of handover bundle in group chat within 4 business hours
- Do a quick scan to verify all mandatory items are present (use the checklist in Step 5)
- If anything is missing, flag to Sales immediately — do not proceed until resolved

**Output:** Acknowledgement message in group chat. Any gaps flagged to Sales with specific items listed.

---

### Step 3 — PM Creates Client Project Folder

**Who:** PM
**What:**
1. Create a new folder under the appropriate workspace directory for the client
2. Copy all handover bundle files into the client folder
3. Clone or copy the Njin PM Framework template into the client project folder
4. Rename `CLAUDE.md` template with client-specific context (client name, engagement type, key outcomes)

**Output:** Client project folder with framework deployed and all source documents in place.

---

### Step 4 — PM Deploys the Framework

**Who:** PM
**What:**
1. Open Claude Code in the client project folder
2. Run the deploy script: `scripts/deploy.sh`
3. Verify `.claude/agents/` and `.claude/skills/` are present and populated
4. Confirm `cos.yaml` exists and is initialised (blank state, not yet populated)

**Output:** Framework deployed. Claude Code agents and skills available in client project.

---

### Step 5 — PM Runs Initialisation Agent

**Who:** PM (via Claude Code)
**What:**
1. Open Orchestrator: `@.claude/agents/orchestrator.md`
2. Instruct Orchestrator to start the Initialisation Agent: `@.claude/agents/initialization-agent.md`
3. Feed the Initialisation Agent the handover bundle (contract scope, transcripts, client docs)
4. Initialisation Agent ingests all materials and bootstraps the COS (`cos.yaml`) with:
   - Client name and engagement type
   - Key outcomes from contract/brief
   - Known deliverables
   - Phase set to: Pre-Discovery
5. PM reviews the populated `cos.yaml` before proceeding

**Output:** `cos.yaml` populated with initial client state. Project ready for discovery.

---

### Step 6 — PM Schedules Onboarding Activation Call

**Who:** PM (coordinated with Sales/Customer Success)
**What:**
- Schedule Onboarding Activation Call within 72 hours of payment confirmation (per onboarding flow)
- Add to client group chat (WhatsApp or Slack — confirm which applies for this client; corporate clients may need email/SMS)
- Send dashboard access credentials to client

**Output:** Activation call booked. Client notified. Dashboard access sent.

---

## Quality Check

Before marking the handover complete, the PM verifies:

- [ ] All mandatory handover bundle items are present
- [ ] Framework deployed — agents and skills confirmed present
- [ ] `cos.yaml` populated with client name, engagement type, outcomes, and deliverables
- [ ] Phase in `cos.yaml` set to Pre-Discovery (not left blank)
- [ ] Onboarding Activation Call scheduled within 72-hour window
- [ ] Client group chat (or email thread) created
- [ ] Dashboard account created and credentials sent to client
- [ ] No items flagged as missing by PM are still outstanding

If any box is unchecked, resolve before proceeding to discovery.

---

## Output

- Populated `cos.yaml` with initial client state
- Deployed PM Framework in client project folder
- Onboarding Activation Call on calendar
- Client dashboard access sent
- Handover bundle archived in client folder
