# HANDOFF: FFG Pre-Sales Playbook Fixes

## Context
The FFG pre-sales developer guide and handbook have been reviewed by a Fulfilment Specialist and scored 5.9/10. The strategic foundation is solid but there are structural gaps that need fixing before client review.

## Files to Modify
- `playbooks/master-playbook/ffg/07c-pre-sales-developer-guide.md`
- `playbooks/master-playbook/ffg/08c-pre-sales-handbook.md`

## Files to Read First
- `cos.yaml` — Full file
- `playbooks/master-playbook/tone-of-voice.md` — All content must match
- `docs/updated-docs/extracted-content.md` — FFG sales scripts (Docs 1-9, 11, 13)
- `playbooks/master-playbook/fhl/07c-pre-sales-developer-guide.md` — Reference for how FHL did it right (Interacting/FUP staging, emoji legend, lost reasons)
- `.claude/agents/pre-sales-specialist.md` — Agent definition with T-System rules
- `.njin-method/skills/playbook-structure-expert/skill.md` — Template compliance requirements

## Priority 1: Must Fix (Blocking)

### 1. Restructure Pipeline — Interacting and FUP Must Be First Two Stages
The current FFG pipeline does NOT start with Interacting and FUP. This is a core T-System requirement. Look at how the FHL playbook does it correctly and mirror that structure.

- Stage 1: Interacting (new lead arrives, auto-reply fires, SDR reviews)
- Stage 2: FUP (first human follow-up — if lead responded call in 5 mins, if not move to T1)
- Then T1 onwards for the outbound sequence

Renumber all subsequent stages accordingly.

### 2. Add Red Dot Protocol
No stale lead thresholds exist in either document. Add a Red Dot SLA table to the developer guide and reference it in the handbook at each manual stage.

Suggested starting thresholds (need client validation):

| Stage | SLA | Escalation |
|-------|-----|-----------|
| Interacting | 1 hour (business hours) | Alert SDR at 1hr, Sam Drew at 2hrs |
| FUP | 5 mins (if responded), 24hrs (if not) | Alert SDR, Sam Drew at 48hrs |
| T1 | 2 hours after entering stage | Alert SDR |
| T3 | 4 hours after T2 completes | Alert SDR |
| T5 | 4 hours after T4 completes | Alert SDR |
| T7 | 4 hours after T6 completes | Alert SDR |
| Not Responding | 24 hours to decide Lost/Nurture | Alert Sam Drew |
| Qualified | 4 hours to complete handoff | Alert SDR, Sam Drew at 8hrs |

Escalation chain: SDR → Sam Drew (Head of Asset & SME) → Rowdy → Nathan

### 3. Add Lost Reasons List to the Developer Guide
Currently missing. Add:

| Reason | When to Use |
|--------|------------|
| Ghosting / Unreachable | Full sequence completed, no engagement |
| Wrong Number | Phone invalid or belongs to someone else |
| Spam | Bot or fake submission |
| Not Qualified (Income) | Doesn't meet minimum criteria |
| Not Qualified (Product) | Needs a product FFG doesn't offer |
| Went Elsewhere | Chose another broker/lender |
| Wrong Entity | Should be FHL or UMI, not FFG |
| Duplicate | Already exists in system |
| Do Not Contact | Requested removal |
| Nurture Exhausted | Completed nurture with no re-engagement |

### 4. Add Emoji Legend to the Developer Guide
Match FHL's format:

| Emoji | Meaning |
|-------|---------|
| 🔴 | Manual stage — SDR action required |
| 🟡 | Manual stage — SDR call required |
| ⚡ | Automated stage — system handles this |
| 🟢 | Qualification complete |
| 🔵 | Broker-owned stage |
| ✅ | Converted — exits pipeline |

### 5. Add Business Hours & SLA to Both Documents

| Setting | Value |
|---------|-------|
| Business hours | Mon-Fri, 8:30am - 5:30pm AEST |
| Speed-to-contact SLA | 5 minutes (if lead responded or inbound call) |
| First outbound attempt | Within 24 hours of lead entry |
| Automation send window | 8:30am - 7:00pm AEST (no sends outside hours) |
| Weekend handling | Leads captured, auto-reply sent, SDR follow-up Monday AM |

## Priority 2: Important Fixes

### 6. Create Script-to-Stage Map Table
One table mapping each T-number to the applicable FFG sales script from extracted-content.md:

| T-Number | Stage | Applicable Script | Doc Reference |
|----------|-------|------------------|---------------|
| T1 | Intro Call | Cold Call Script + Warm Lead Script | Doc 1, Doc 2 |
| T3 | Second Call | Follow-Up Call Script | Doc 4 |
| Settlement | Post-Settlement | Settlement Calls | Doc 6 (EMPTY — PENDING CLIENT) |
| Qualification | Lender Options | Lender Options Call Process | Doc 5 |
| Approval | Approval Call | Approval Call Process | Doc 3 |
| etc. | | | |

Map ALL 9 available scripts to their place in the pipeline.

### 7. Deepen ICA Messaging Differentiation
At T1 (first outreach) and the qualification touchpoint, the messaging for each ICA should feel genuinely different, not just a word swap:

- **Young Practical Motor:** "We make it simple. Let's work out what you can afford and find the right car loan."
- **Established Personal Finance:** "We've helped thousands of people in your situation. Let's look at what works best."
- **Prime Convenience Repeat:** "Welcome back. Let's get this sorted quickly for you."
- **Business Asset:** "Let's look at how we can structure this to work for your business and your tax position."
- **Prime Vehicle:** "We'll make this smooth and efficient. Let's find you the best deal."

### 8. Add Day-in-the-Life Schedule to the Handbook
For a broker handling ~12 new leads/day (375/month / ~20 working days):

| Time | Activity |
|------|----------|
| 8:30 | Check FUP stage — any responses overnight? Call first. |
| 9:00 | Check Interacting — review new leads, move to FUP |
| 9:30-11:00 | Work T1/T3/T5/T7 call stages |
| 11:00 | Check automations running (T2/T4/T6 not stuck) |
| 1:00-3:00 | Continue call stages + callbacks |
| 3:00 | Review Qualified — complete any pending handoffs |
| 4:30 | Review Not Responding — Lost/Nurture decisions |
| 5:00 | Pipeline health check — nothing stuck |

### 9. Add Quick Reference Card to the Handbook
One-page cheat sheet. Mirror the format from the FHL handbook's Quick Reference Card.

### 10. Add Metric Expectations
Even if approximate:

| Metric | Target |
|--------|--------|
| Calls per day | TBC (set with Sam Drew) |
| Speed-to-contact (responded leads) | < 5 minutes |
| Contact rate | 75% (current target) |
| Qualification rate | TBC |
| Tagging completeness | 100% of Qualified leads fully tagged |

### 11. Add Escalation Protocol to the Handbook
When does a broker escalate?
- Complex commercial deal → Sam Drew
- Client complaint → Rowdy
- Compliance concern → Nathan
- Technical issue (POLR) → CTO/Matty

### 12. Flag Settlement Call Script Gap
Doc 6 (Settlement Calls) was EMPTY. Add explicit note: "PENDING CLIENT INPUT — Settlement call script content needed from Rowdy/team."

## Priority 3: Polish

### 13. Merge Consecutive Same-Type Touchpoints
Review the full sequence. If any consecutive stages are the same channel (e.g., two SMSs in a row with no other channel between), merge them into one stage.

### 14. Add Common Mistakes to the Handbook
- Calling outside business hours (QLD = no daylight saving)
- Not checking Ambition before calling (lead already in process elsewhere)
- Not updating stage after a call
- Skipping voicemail on no-answer
- Sending generic SMS instead of ICA-matched
- Leaving a lead in Not Responding without making a Lost/Nurture decision

### 15. Consolidate the Developer Guide into Single Master Pipeline Table
If there are multiple overlapping tables, merge into one: Stage Name, T-Number, Type (Manual/Auto), Automation Trigger, Description, Exit Criteria, Red Dot SLA.

## Constraints
- Australian English, no em dashes, third-grade reading level for the handbook
- Compliance: never use "advice", "guarantee", "financial hardship"
- Validate against playbooks/master-playbook/tone-of-voice.md (minimum 24/30)
- FHL pre-sales documents are a good reference for structure — mirror their patterns
- Do NOT redesign the pipeline strategy. Fix the structural gaps within the existing approach.
