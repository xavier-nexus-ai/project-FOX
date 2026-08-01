# HANDOFF: FHL Pre-Sales Playbook Fixes

## Context
The FHL pre-sales developer guide and handbook have been reviewed by a Fulfilment Specialist and rated as structurally strong. The T-System is correctly implemented, the manual/auto distinction is excellent, and Purchase Type messaging is well integrated. The fixes needed are operational, not structural.

## Files to Modify
- `playbooks/master-playbook/fhl/07c-pre-sales-developer-guide.md`
- `playbooks/master-playbook/fhl/08c-pre-sales-handbook.md`

## Files to Read First
- `cos.yaml` — Full file (especially `icas` data for 5-profile framework)
- `playbooks/master-playbook/tone-of-voice.md` — All content must match
- `docs/updated-docs/extracted-content.md` — Doc 10 (FHL lifecycle), Docs 16-17 (ICAs)
- `.njin-method/skills/playbook-structure-expert/skill.md` — Template compliance

## Priority 1: Must Fix

### 1. Complete Red Dot SLAs for All Manual Stages
Currently only FUP has a defined SLA. Add SLAs for every manual stage:

| Stage | SLA | Escalation |
|-------|-----|-----------|
| Interacting | 1 hour (business hours) | Alert SDR at 1hr, Bill Robb at 2hrs |
| FUP | 5 mins (if responded), 24hrs (if not) | Alert SDR, Bill Robb at 48hrs |
| T1 | 2 hours after entering stage | Alert SDR |
| T3 | 4 hours after T2 completes | Alert SDR |
| T5 | 4 hours after T4 completes | Alert SDR |
| T7 | 4 hours after T6 completes | Alert SDR |
| Not Responding | 24 hours to decide Lost/Nurture | Alert Bill Robb |
| Qualified | 4 hours to complete handoff data | Alert SDR, Bill Robb at 8hrs |
| Broker Assigned | 2 hours for SDR to complete warm handoff | Alert SDR, Bill Robb at 4hrs |

Escalation chain: SDR → Bill Robb (Head of Home Loans) → Rowdy → Nathan

Add this as a new subsection in the developer guide and reference it at each manual stage in the handbook.

### 2. Strip Embedded SMS/Email Templates from Developer Guide Stage Definitions
The developer guide is ~9 pages (exceeds 4-6 page limit). The SMS templates in Stage 4, email subjects in Stage 6, and breakup messages in Stage 8 should be referenced, not embedded.

Replace the full template text with a pointer to the relevant item in the FHL pre-sales scripts document.

Move all copy to `playbooks/master-playbook/fhl/10c-pre-sales-scripts.md`. For now, move to an appendix at the bottom of the developer guide if the script document is not ready.

### 3. Define `likely_next_needs` Auto-Calculation Logic
Currently referenced as "auto-calculated based on journey type" but no mapping exists. Add:

| Journey Type | Likely Next Needs |
|-------------|-------------------|
| First Home Buyer | Refinance (12-18mo), Investment property (24-36mo), Asset finance via FFG |
| New Purchase | Refinance (12-18mo), Asset finance via FFG |
| Refinance | Investment property (12-24mo), Asset finance via FFG |
| Investor | Portfolio expansion (6-12mo), Commercial finance, Asset finance via FFG |
| Commercial | Equipment finance via FFG, Additional commercial property |

This feeds directly into Month 9 FFG Momentum Pack in the lifecycle plan.

### 4. Add Doc Checklist Trigger Automation Spec
The developer guide lists the document checklists by journey type but doesn't specify implementation. Add automation spec:

| Field | Value |
|-------|-------|
| Trigger | `journey_type` field set at Qualified stage |
| Action | Display relevant checklist in lead card (conditional component) |
| Format | Checkbox list within lead record |
| Secondary action | Auto-send checklist email to lead with journey-specific doc requirements |
| Tool | N8N → POLR conditional display + SendGrid email |

## Priority 2: Should Fix

### 5. Add "What to Watch For" to Missing Stages in the Handbook
Currently missing from several stages. Add brief callouts:

- **T1 (Intro Call):** "Watch for: If they say they submitted a form by accident, mark as Lost (Not Qualified). Don't force the conversation."
- **T3 (Second Call):** "Watch for: If they answered but asked you to call back at a specific time, schedule the callback and keep them in T3. Don't move to T4."
- **T5 (Third Call):** "Watch for: Some leads open the email but don't respond. If POLR shows they clicked the email link, mention it on the call: 'I noticed you had a look at what I sent through.'"
- **Qualified:** "Watch for: Don't guess employment type or household type. Ask directly. Wrong tags will cause the wrong lifecycle content to fire for the next 18 months."

### 6. Add Architecture Rationale to Top of the Developer Guide
Add 1-2 sentences explaining why T-System for a small team:

> "T-System selected because the SDR role is new to FHL, the team includes a recent hire (Angel), cross-sell touchpoints require granular tracking for monetisation reporting, and the Purchase Type branching adds complexity that benefits from visible stage progression."

### 7. Acknowledge SDR Role Doesn't Exist Yet
Add a note to the handbook header:

> "Note: This handbook is written for the FHL SDR role. If this role is initially performed by a broker or shared resource, the same process applies. Discuss role assignment with Nathan/Bill Robb before rollout."

### 8. Add FHL Lead Volume Context to the Developer Guide
Add to the reporting area:

> "Expected volume: ~55 leads/month. At full T-System cadence (7 touchpoints per lead), this equates to approximately 385 touchpoint actions per month, manageable by one dedicated SDR or as a partial responsibility for a broker."

### 9. Resolve Calendar Integration TBC
Flag as blocking decision. Add note:

> "BLOCKING: Calendar integration (Calendly or native POLR) must be decided before Stage 14 automation can be built. This affects consultation booking, confirmation, and reminder workflows."

Add to COS open decisions if not already there.

### 10. Define Escalation Path
Currently just "alert to team lead + dashboard flag." Define properly:

| Tier | Who | When |
|------|-----|------|
| Tier 1 | SDR (self-alert) | SLA approaching |
| Tier 2 | Bill Robb | SLA breached by 1x |
| Tier 3 | Rowdy | SLA breached by 2x or pattern of breaches |
| Tier 4 | Nathan | Systemic issues only |

## Priority 3: Polish

### 11. Flag FHL ICA Dependency
Add note in both documents: "Note: FHL-specific ICAs (named personas like Taylor/Alex for FFG) are pending creation. Currently using journey types as proxy segmentation. When FHL ICAs are created, update messaging guidance throughout."

### 12. Migrate Voicemail Scripts to the Script Document
The handbook includes inline voicemail text at T1 and T3. Move full scripts to `playbooks/master-playbook/fhl/10c-pre-sales-scripts.md` with `script` code fences. Keep a brief pointer in the handbook.

## Constraints
- Australian English, no em dashes, third-grade reading level for the handbook
- Compliance: NEVER use "advice", "guarantee", "financial hardship" — critical for mortgage content
- Validate against playbooks/master-playbook/tone-of-voice.md (minimum 24/30)
- Do NOT redesign the pipeline. The structure is sound. Fix the operational gaps.
- The FHL playbook is the STRONGER of the two. These are refinements, not rewrites.
