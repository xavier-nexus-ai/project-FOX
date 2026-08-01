# FHL Current-State Process Map
# T-System Pipeline Architecture

> **Purpose:** Map every existing FHL manual touchpoint chronologically with T-numbers, identify gaps, and design the automation layer that fills them. FHL pre-sales is the on-ramp to an 18-month post-settlement lifecycle. Tags captured here power everything downstream.
> **Source Data:** Activation Meeting Transcript, COS.yaml (fhl_customer_lifecycle, fhl_writing_guidance, sendgrid_automations.fhl), Extracted Docs (Doc 10: 18-Month Lifecycle Playbook), ICA Matrix + Definitions
> **Last Updated:** 2026-03-23

---

## How to Read This Document

- **T prefix** = Direct touchpoints (calls, SMS, emails to the lead)
- **N prefix** = Nurture sequence (automated, after manual exhaustion)
- **Q prefix** = Qualification stage (journey classification + tag capture)
- **PA prefix** = Pre-Appointment sequence
- **TD prefix** = Document collection path
- **LC prefix** = Lifecycle touchpoints (post-settlement, 18 months)
- **RC prefix** = Reactivation / Customer Care sequence
- Manual touchpoints marked with **[BROKER]**
- Automated touchpoints marked with **[SYSTEM]**
- Semi-automated (template exists, manually triggered) marked with **[TEMPLATE]**

---

## Key Differences from FFG

| Factor | FFG | FHL |
|--------|-----|-----|
| Volume | 375 leads/month | 55 leads/month |
| Cadence length | 4 days (Days 1-4) | Extended (evidence: SendGrid emails at Days 2, 5, 9, 16) |
| Consideration cycle | Days to weeks | Weeks to months (mortgage decision) |
| Journey classification | Not required (all asset finance) | Required (FHB/New Purchase/Refinance/Investor/Commercial) |
| Post-settlement lifecycle | Basic nurture | 18-month structured plan (7 touchpoints) |
| Revenue type | One-time commission ($2,300 avg) | Commission + trail (0.65% of NAF ongoing) |
| LMS | Ambition (has API) | Infynity (NO API - CSV/PDF only) |
| Team | ~10 brokers + SDR | Bill Robb (Head), Paige Beveridge, Angel |
| Declined path | 90-Day Plan (20% convert) | Not documented (opportunity) |
| Online form completion | 80%+ complete online | Unknown (likely lower - mortgage apps more complex) |

---

## Pipeline Entry Points

FHL receives approximately 55 leads/month:
- Most come through Fox Finance Group website (home loans component on more mature site)
- Some through foxhomeloans.com.au directly
- Referral hopper: ~250 businesses (real estate agents, conveyancers)
- Phone inquiries (hottest leads, same as FFG pattern)

**[ASSUMPTION]** FHL lead source breakdown not explicitly provided. FFG pattern is 67% organic website, 26% phone, 7% other. FHL likely similar but with higher referral percentage given real estate/conveyancer partnerships.

**Journey Detection at Intake:**
Capture these tags on every new FHL contact:
- Purchase Type: First Home Buyer / New Purchase / Refinance / Investor / Commercial
- Source: Organic / Referral (which partner) / Phone / Cross-sell from FFG
- Urgency indicators: Pre-approval needed? Under contract? Fixed rate expiring?

**Purchase Type Routing:**
- **Commercial** >> Bill Robb (Head of Home Loans / Partnerships)
- **Investor** >> Bill Robb
- **Refinance** >> Paige Beveridge
- **First Home Buyer** >> Paige Beveridge or Angel
- **New Purchase** >> Any available broker

**[NEEDS VALIDATION]** Broker routing by Purchase Type is inferred from team roles. Client validation required.

---

## Primary Pipeline: Inbound Lead to Appointment

### STAGE: Interacting (24hr RED dot)

**Purpose:** Lead has replied to any touchpoint. Broker must pick up within 24 hours.
**Entry:** Lead replies to SMS, email, voicemail, or calls in.
**Exit:** Broker makes contact and moves to Qualification.
**Red Dot:** 24-hour escalation if no broker action.

---

### STAGE: FUP - Follow Up (24hr task)

**Purpose:** Broker has had an interaction that needs follow-up within 24 hours.
**Entry:** Broker logs an interaction that requires a callback or follow-up action.
**Exit:** Follow-up completed, lead moves to appropriate next stage.

---

### Pre-Contact Auto-Response

| T# | Day | Channel | Type | Action | Current State |
|----|-----|---------|------|--------|---------------|
| T1 | 0 | SMS | [TEMPLATE] | "Inquiry received, home lending specialist will be in touch" | Exists - manually triggered (same pattern as FFG) |
| T2 | 0 | Email | [TEMPLATE] | "Inquiry received, here's next steps" | Exists - matches FHL SendGrid "No Customer Contact" Instant email |

**Gap identified:** T1 and T2 are template-triggered, not automated. Should fire within 60 seconds of inquiry.

**Proposed change:** Automate T1 + T2 via N8N webhook. Fire instantly, 24/7. Include Purchase Type-relevant content in email (if TypeForm captures enough to classify at this stage).

---

### Day 1 - First Contact Push

| T# | Day | Time | Channel | Type | Action | Current State |
|----|-----|------|---------|------|--------|---------------|
| T3 | 1 | Morning (within 5 min) | Phone | [BROKER] | Call Attempt 1. Priority call. Do not delay. No voicemail on first attempt. | Exists - manual |
| T4 | 1 | Afternoon | Phone | [BROKER] | Call Attempt 2. If no answer, leave voicemail. Send SMS + email with callback options. | Exists - manual. SMS/email template-triggered. |

**After T4 (if no contact):** Lead has received 2 call attempts, 1 voicemail, 1 SMS, 1 email, plus auto-response SMS/email. Options given: call back, tell us a time, book online.

**[EVIDENCE NOTE]** FFG does 3 attempts on Day 1. FHL likely does 2 (lower volume, more complex leads, need prep time between calls). FHL SendGrid "No Customer Contact" has its next email on Day 2, suggesting a tighter call window on Day 1.

---

### Day 2 - Follow-Up

| T# | Day | Time | Channel | Type | Action | Current State |
|----|-----|------|---------|------|--------|---------------|
| T5 | 2 | Morning | Phone | [BROKER] | Call Attempt 3. If no answer, leave voicemail. | Exists - manual |
| T6 | 2 | Afternoon | Email | [TEMPLATE] | Follow-up email with value content. | Matches FHL SendGrid "No Customer Contact" Day 2 email |

---

### Day 5 - Mid-Week Check

| T# | Day | Time | Channel | Type | Action | Current State |
|----|-----|------|---------|------|--------|---------------|
| T7 | 5 | Morning | Phone | [BROKER] | Call Attempt 4. If no answer, leave voicemail. "Breakup" tone - we're here when you're ready. | Exists - manual |
| T8 | 5 | Same day | Email | [TEMPLATE] | Breakup email with online booking link + value content. | Matches FHL SendGrid "No Customer Contact" Day 5 email |

---

### Day 9 - Final Manual Push

| T# | Day | Time | Channel | Type | Action | Current State |
|----|-----|------|---------|------|--------|---------------|
| T9 | 9 | Any | Phone | [BROKER] | Final call attempt. Last voicemail. "Your file stays open." | Exists - manual |
| T10 | 9 | Same day | Email | [TEMPLATE] | Final manual email. Purchase Type content if known. | Matches FHL SendGrid "No Customer Contact" Day 9 email |
| T11 | 9 | Same day | SMS | [TEMPLATE] | "We tried to reach you. Your file is open whenever you're ready. [BOOKING LINK]" | Likely exists - template |

---

### Day 16 - Last Automated Email

| T# | Day | Channel | Type | Action | Current State |
|----|-----|---------|------|--------|---------------|
| T12 | 16 | Email | [SYSTEM] | Final "No Customer Contact" automation email. | Matches FHL SendGrid "No Customer Contact" Day 16 email |

---

### MANUAL PROCESS ENDS AT T11 (Day 9)

**Current state after T12:** Lead enters basic nurture. FHL has two existing nurture automations:
1. "Nurture Up to 3 Months" (7 emails: Day 14, 30, 45, 75, 90, 91, 120) - 61.6% open rate
2. "Nurture Up to 6 Months" (7 emails: Day 30, 60, 90, 120, 150, 180, 210) - 67.4% open rate (best FHL performer)

**[ASSUMPTION]** It's unclear which nurture sequence a lead enters, or if they overlap. Likely "Up to 3 Months" fires first, then "Up to 6 Months" continues. The content of these emails is not documented.

**Critical gap:** Unlike FFG (where 80%+ complete forms online), FHL mortgage applications are more complex. Online self-completion rate is likely lower. This makes the nurture sequence MORE important for FHL than FFG.

---

## "Not Responding Yet" - Designed Nurture (NEW)

These touchpoints replace the current generic nurture automations with Purchase Type-targeted content. Mortgage leads have a 3-6 month consideration cycle. This sequence must keep Fox front-of-mind without being pushy.

**Routing logic:** If Purchase Type was captured during T3-T11 interactions (even partial), use it. If unknown, default to "New Purchase" content (broadest appeal).

### Short-Term Nurture (Weeks 2-4)

| N# | Day | Channel | Type | Content Theme | Purchase Type Personalisation |
|----|-----|---------|------|---------------|-------------------------------|
| N13 | 14 | Email | [SYSTEM] | Educational value content | FHB: "Deposit basics explained" / New Purchase: "Borrowing power snapshot" / Refinance: "Rate health check guide" / Investor: "Portfolio strategy check" / Commercial: "What lenders look for" |
| N14 | 21 | SMS | [SYSTEM] | Social proof | All: "Another QLD family just settled with us. See their story: [LINK]" |
| N15 | 30 | Email | [SYSTEM] | Value-add offer | All: "Free borrowing power check - no credit impact, no commitment. Reply YES." |

### Medium-Term Nurture (Months 2-3)

| N# | Day | Channel | Type | Content Theme | Purchase Type Personalisation |
|----|-----|---------|------|---------------|-------------------------------|
| N16 | 45 | Email | [SYSTEM] | Market update | FHB: "First home buyer grants and changes" / New Purchase: "What's happening in your local market" / Refinance: "Rate movements this quarter" / Investor: "Rental yield trends" / Commercial: "Commercial lending update" |
| N17 | 60 | SMS | [SYSTEM] | Soft check-in | All: "Still thinking about your home loan? No rush. We're here when you're ready. - [Broker Name], Fox Home Loans" |
| N18 | 75 | Email | [SYSTEM] | Case study / testimonial | FHB: first-timer success story / Investor: portfolio growth story / Refinance: savings story |
| N19 | 90 | Email | [SYSTEM] | Repricing or rate update | FHB: "How much deposit do you really need?" / Refinance: "Quarterly rate check - here's what moved" / Investor: "Interest-only vs principal-and-interest: which is right now?" |

### Long-Term Nurture (Months 4-6)

| N# | Day | Channel | Type | Content Theme | Purchase Type Personalisation |
|----|-----|---------|------|---------------|-------------------------------|
| N20 | 120 | Email | [SYSTEM] | Seasonal/timely content | All: property market seasonal trends, tax time tips, government scheme updates |
| N21 | 150 | SMS | [SYSTEM] | Re-engagement | All: "Checking in. If your plans have changed, that's okay. If not, we'd love to help. Reply CALL and we'll reach out." |
| N22 | 180 | Email | [SYSTEM] | Final nurture / reactivation | All: "Your file is still open. One click to restart: [BOOKING LINK]. If things have changed, reply REMOVE and we'll update your preferences." |

**After N22 (Day 180):** If no response, move to "Nurture Cold Lead" (existing FHL automation: 7 emails over 2 years at Day 30, 90, 180, 270, 365, 540, 730). 55.7% open rate, 1.73% unsub - highest unsub rate, so don't over-contact.

**If reply received at ANY N-number:** Route to Interacting stage. Broker picks up within 24 hours. Treat as warm lead.

---

## Qualification Stage (When Contact Is Made)

When a broker makes live contact at any T-number (T3-T11), the Qualification stage begins. This is the CRITICAL data capture moment. Tags set here power the entire 18-month lifecycle.

### Q1: Journey Classification Decision Tree

```
START: "What brings you to Fox Home Loans?"

├── Buying first home >> FIRST HOME BUYER
│   Confirm: Never owned property, using FHB grants/schemes
│
├── Buying a home (already own/have owned) >> NEW PURCHASE
│   Confirm: Upgrading, downsizing, or relocating
│
├── Looking at rates / checking options >> REFINANCE
│   Confirm: Has existing mortgage, exploring better deal
│
├── Investment property >> INVESTOR
│   Confirm: Already owns home (or not), buying for investment
│   Note: FHB buying first as investment = classify as INVESTOR
│
├── Commercial property >> COMMERCIAL
│   Confirm: Business purpose, not residential
│
└── Not sure / exploring >> NEW PURCHASE (default)
    Qualify further during appointment
```

### Q2: Segmentation Tag Capture Checklist

These tags MUST be captured during the qualification call or appointment. Without them, the 18-month lifecycle automation cannot personalise.

| Tag Category | What to Capture | How to Ask | Where It's Used |
|-------------|----------------|------------|-----------------|
| **Purchase Type** | FHB / New Purchase / Refinance / Investor / Commercial | "What brings you to Fox Home Loans today?" | Every lifecycle touchpoint |
| **Employment** | PAYG / Self-employed | "Are you employed full-time, or do you run your own business?" | Month 6: Repricing approach varies |
| **Household** | Single / Couple / Dependants | "Will this be in your name only, or with a partner?" + "Any dependants?" | Month 9: ICA-targeted cross-sell content |
| **Likely next needs** | Vehicle / Travel / Wedding / Reno-Solar / Debt consolidation / Business finance | "Any big purchases or plans coming up in the next 12 months?" | Month 9: FFG Momentum Pack targeting |
| **Product preference** | Fixed / Variable / Split / Offset / IO / OO + key dates | Captured during application, not qualification call | Month 18: Action Window triggers (fixed expiry) |
| **Urgency** | Pre-approval needed / Under contract / Fixed expiring / Just exploring | "Where are you in the process? Just exploring, or do you have a timeline?" | Prioritisation and nurture intensity |
| **Source** | Organic / Referral (partner name) / Phone / FFG cross-sell | System-captured at intake | Attribution and referral partner tracking |

### Q3: Purchase Type-Specific Qualification (Talk Tracks)

**First Home Buyer** (Writing guidance: explain fundamentals, deposit/LVR basics, up-front costs, pre-approval flow, confidence-building)
- "Have you spoken to a broker before, or is this your first time?"
- "Do you have a deposit saved, or are you still working toward that?"
- "Have you looked into first home buyer grants or stamp duty concessions?"
- "Would it help to start with a pre-approval so you know exactly what you can afford?"

**New Purchase** (Writing guidance: readiness, borrowing power, offer/contract timing, pre-approval, reducing friction)
- "Have you sold your current property, or is this a second purchase?"
- "Do you have a property in mind, or are you still looking?"
- "Would a pre-approval help you move quickly when you find the right place?"
- "Is there a timeline you're working to?"

**Refinance** (Writing guidance: triggers, what to compare, equity/LVR, 'health check' decision path)
- "What prompted you to look at refinancing? Rate, features, or something else?"
- "How long have you been with your current lender?"
- "Do you know roughly what your property is worth today?"
- "Would you like us to do a quick health check on your current loan - no commitment, just to see where you stand?"

**Investor** (Writing guidance: cash flow language, long-term strategy, structure/features, risk management WITHOUT giving advice)
- "Is this your first investment property, or do you have others?"
- "What's your main goal - cash flow, capital growth, or both?"
- "Are you looking at residential or commercial?"
- "How is your current lending structured? We can look at how this fits into your broader strategy."

**Commercial** (Writing guidance: documentation, timelines, deal structure variables, 'what to prepare' checklists)
- "What type of commercial property are you looking at?"
- "Is this owner-occupied or investment?"
- "Do you have your financials ready, or would it help to know what's needed?"
- "What's the timeline? Are you in negotiation or still exploring?"

### Q4: Broker Routing

| Purchase Type | Primary Broker | Backup |
|---------------|---------------|--------|
| First Home Buyer | Paige Beveridge | Angel |
| New Purchase | Any available | Bill Robb |
| Refinance | Paige Beveridge | Angel |
| Investor | Bill Robb | Paige Beveridge |
| Commercial | Bill Robb | -- |

**[NEEDS VALIDATION]** Broker routing inferred from team roles. Client validation required.

### Q5: Docs Checklist Trigger (Purchase Type-Specific)

After qualification, trigger the correct docs checklist in POLR:

**All Purchase Types:**
- Photo ID (driver's licence or passport)
- 2 most recent payslips (PAYG) OR 2 years tax returns + financials (self-employed)
- 3 months bank statements (all accounts)
- Existing loan statements (if applicable)

**First Home Buyer - Additional:**
- Savings evidence (3-6 months)
- FHB grant application (if eligible)
- Proof of genuine savings vs gift/inheritance

**Refinance - Additional:**
- Current loan statement showing balance, rate, features
- Current property valuation (we can provide via Cotality)
- Any fixed rate expiry dates

**Investor - Additional:**
- Rental income evidence (lease agreement, bank deposits)
- Portfolio summary (other properties, LVRs)
- Tax depreciation schedule (if available)

**Commercial - Additional:**
- Business financials (2 years P&L, balance sheet)
- ATO portal / tax returns
- Lease agreements (if investment)
- Business plan (if applicable)

---

## Pre-Appointment Sequence

**Trigger:** Appointment booked with FHL broker (at any point during T3-T11 or from nurture re-engagement).

| PA# | Timing | Channel | Type | Action | Purchase Type Personalisation |
|-----|--------|---------|------|--------|-------------------------------|
| PA1 | Instant | Email + SMS | [SYSTEM] | Confirmation: "Your appointment is booked with [Broker Name] on [Date/Time]. Here's what to bring." | Include Purchase Type-specific docs checklist |
| PA2 | 24hr before | SMS | [SYSTEM] | Reminder: "Just a reminder about your appointment tomorrow at [Time] with [Broker Name]." | None needed |
| PA3 | 2hr before | SMS | [SYSTEM] | Final reminder: "Looking forward to chatting in 2 hours. Call [Broker Direct] if anything changes." | None needed |

**[OPTIONAL ENHANCEMENT]** Identity-framed pre-call content (invoke identity-framing skill). Send Purchase Type-specific content between PA1 and PA2:
- FHB: "What first home buyers wish they knew before their broker meeting"
- Refinance: "3 questions to ask your broker about refinancing"
- Investor: "How smart investors structure their lending"

---

## Branching Paths

### Post-Contact Application Pipeline

Once a broker makes live contact and takes an application, the lead moves through FHL's deal pipeline. Unlike FFG, FHL does NOT have documented stage-by-stage scripts. The process is:

| Stage | Action | Owner | Script Reference | Notes |
|-------|--------|-------|-----------------|-------|
| Application Taken | Full fact-find during appointment | Broker | No documented script | Q2 tags captured here if not already |
| Assessment | Broker assesses application against lender panel | Broker | -- | Multiple lender comparison |
| Pre-Approval | Submit to chosen lender(s) | Broker | -- | May submit to 2-3 lenders |
| Approval / Conditional Approval | Notify customer of approval + conditions | Broker | No documented script (adapt FFG Doc 3?) | |
| Docs Collection | Customer provides remaining documents | Broker + [SYSTEM] | See TD sequence below | |
| Unconditional Approval | All conditions met | Broker | -- | |
| Settlement | Loan settles | Broker | -- | Triggers Month 1 lifecycle |

**Gap identified:** FHL has NO documented call scripts for the application pipeline stages. FFG has 8 scripts (Docs 1-9). FHL needs at minimum:
- Application/Fact-Find guide (Purchase Type-specific)
- Approval notification script
- Settlement congratulations script (triggers lifecycle entry)

---

### Post-Application: Document Collection

**Trigger:** Application taken but documents still outstanding.
**Current state:** FHL "No Docs Returned" SendGrid automation exists (4 emails: Instant, Day 1, 3, 3). 58.8% open rate, 3.4% click rate.

| TD# | Timing | Channel | Type | Action | Current State |
|-----|--------|---------|------|--------|---------------|
| TD1 | Instant | Email | [SYSTEM] | Docs reminder: what's needed (Purchase Type-specific checklist) | Existing SendGrid automation |
| TD2 | Day 1 | Phone | [BROKER] | Call to check on docs, offer help | Manual |
| TD3 | Day 1 | Email | [SYSTEM] | Second reminder | Existing SendGrid automation |
| TD4 | Day 3 | Email | [SYSTEM] | Third reminder | Existing SendGrid automation |
| TD5 | Day 3 | SMS | [SYSTEM] | "Quick reminder about your docs. Need help? Call [Broker Direct]." | Existing SendGrid automation |
| TD6 | Day 5 | Phone | [BROKER] | Final call if docs still outstanding | Manual |

**Current performance:** Unknown return rate (FFG is 80%+). Mortgage docs are more complex (tax returns, property valuations, etc.), so return rate likely lower.

---

### Infynity Data Import (NO API)

**The Problem:** FHL uses Infynity as their LMS. It has NO API. Data must be exported as CSV or PDF.

**Impact on Pipeline:**
- Settlement data cannot auto-trigger Month 1 lifecycle
- Application data cannot auto-populate POLR
- Loan product details (fixed/variable, rate, term) must be manually entered

**Proposed Workflow:**
1. **Weekly CSV export** from Infynity (broker or admin task)
2. **N8N import workflow** parses CSV, matches to POLR contact records
3. **Settlement detection** triggers Month 1 lifecycle sequence
4. **Product data** (fixed/variable, rate, term, expiry) populated into POLR for lifecycle triggers

**Minimum data needed from CSV:**
- Customer name + contact details (matching key)
- Settlement date
- Loan amount, rate, product type (fixed/variable), term
- Lender name
- Property address
- Fixed rate expiry date (if applicable)

**[ESCALATE TO DEVELOPER]** Infynity CSV format needs investigation. What fields are available? What's the export process? Can it be scheduled or is it manual only?

---

## Post-Settlement: 18-Month Customer Lifecycle (LC Sequence)

**Source:** Rowdy's 18-Month Customer Lifecycle Playbook (Doc 10). This is the destination. Pre-sales is the on-ramp.

**Trigger:** Settlement confirmed (from Infynity CSV import or manual entry in POLR).

**Critical dependency:** Segmentation tags from Q2 must be present in POLR. Without them, lifecycle touchpoints cannot personalise.

### Tag-to-Touchpoint Dependency Map

| Tag Set at Qualification (Q2) | Used at Lifecycle Touchpoint |
|-------------------------------|------------------------------|
| Purchase Type (FHB/Investor/Refinancer/New Purchase) | LC2 (Month 3): Segmented 90-Day Confidence Pack modules |
| Employment (PAYG/Self-employed) | LC3 (Month 6): Repricing approach varies by employment complexity |
| Likely next needs | LC4 (Month 9): FFG Momentum Pack targeting (which pack to send) |
| Product (Fixed/Variable/IO) | LC7 (Month 18): Action Window triggers (fixed expiry date) |
| Household (Single/Couple/Dependants) | LC4 (Month 9): ICA-targeted cross-sell content |

**If tags are missing:** Broker must capture during Month 1 Welcome call (LC1). Flag in POLR as "tags incomplete" with RED dot.

### Lifecycle Touchpoints

| LC# | Month | Name | Channel | Type | Deliverable | CRM Action |
|-----|-------|------|---------|------|-------------|------------|
| LC1 | 1 | Welcome + Setup Verified | Phone + Email/SMS | [BROKER] | Phone call. If no contact: "Your Loan Setup Snapshot" one-pager | Confirm setup, introduce FFG + refer-a-friend, set expectations, log outcomes |
| LC2 | 3 | 90-Day Confidence Pack | Email + Phone follow-up | [BROKER] + [SYSTEM] | 1-page PDF: "Your Property Position and Loan Health" with Cotality valuation | Segmented module: FHB gets "First-Year Homeowner Plan" / Investor gets "90-Day File Check" / Refinancer gets "Savings Proof + Equity Baseline" |
| LC3 | 6 | Proactive Pricing Review | Phone + Email | [BROKER] | Repricing review. If improved: communicate savings. If no change: explain why + next steps. One-pager if no contact. | Log pricing request submitted/approved/declined, rate notes, next eligibility date |
| LC4 | 9 | FFG Momentum + Opportunity Pack | Email (completed content) | [SYSTEM] + [BROKER] follow-up | Purchase Type-specific pack (see FFG Momentum Pack below). Equity Release pack if applicable. | Log pack type, CTA response, opportunity type if yes. Internal referral to FFG if applicable. |
| LC5 | 12 | Annual Property + Loan Strategy Review | Phone + Email | [BROKER] | 2-page "Annual Property and Loan Strategy Review": updated valuation, repricing check, equity built, next 12-month strategy | Log recommended pathway, next key trigger |
| LC6 | 15 | Refinance Pathway | Email + Phone follow-up | [BROKER] + [SYSTEM] | 1-page "Your Options Map": 3 paths (pay down faster / invest-upgrade / refinance) with pros-cons and recommendation | Log option map delivered, chosen direction, trigger for action window |
| LC7 | 18 | Action Window | Phone + Email | [BROKER] | "Action Window Plan": recommended action, timeline, checklist. Only activate if trigger present. | Log action taken, outcome |

### LC4: FFG Momentum Packs (Month 9 Cross-Sell)

**Golden rule from Rowdy:** "Must NOT feel like lead generation. Must feel like: We prepared options based on what customers like you typically need next."

| Purchase Type | Pack Name | Content Focus | Cross-Sell to FFG |
|---------------|-----------|---------------|-------------------|
| New Purchase | New Home Momentum Pack | Car upgrade, furniture, solar, small renos, debt consolidation | Yes - all scenarios |
| FHB | First Home Momentum Pack | Car upgrade, furniture, solar, travel/wedding, debt consolidation | Yes - all scenarios |
| Investor | Investor Leverage Pack | Vehicle finance, equipment finance, business finance, consolidation, reno funds | Yes - all scenarios |
| Refinancer | Refi Savings Accelerator Pack | Consolidate expensive debts, refinance car/personal loans, fund planned purchases | Yes - all scenarios |
| All (if applicable) | Equity Release/Top-Up Pack | Home upgrades, small renos, debt consolidation via equity release | FHL retains (equity release is FHL product) |

**Cross-sell handover:** If customer responds to FFG Momentum Pack, route to FFG team. Use ICA-to-FHL Purchase Type mapping in reverse:
- FHB customer >> Young Practical Motor Borrower (FFG ICA)
- New Purchase customer >> Established Personal Finance or Prime Vehicle (FFG ICA)
- Investor customer >> Prime Convenience Repeat or Business Asset (FFG ICA)
- Refinancer customer >> Established Personal Finance (FFG ICA)

### LC2: Cotality Integration (Month 3 and Month 12)

**Purpose:** Provide free property valuation as a trust-building value-add.
**Tool:** Cotality subscription (already paid for). Can generate report within 1 minute.
**Integration:** Cotality API into POLR (details pending).

**Month 3 use:** Benchmark valuation. "This is your starting line, not a refinance trigger."
**Month 12 use:** Updated valuation showing equity growth since Month 3. Supports refinance pathway discussion.

**[OPEN]** Cotality API integration details pending. Manual process (broker generates report, attaches to email) works as interim.

### Repricing Workflow (Quarterly)

**Trigger:** Every 3 months, check if repricing is available with current lender.
**Process:**
1. Log into lender system
2. Submit repricing request with rationale (e.g., LVR improvement)
3. Get answer same day (usually)
4. If approved: communicate savings to customer
5. If declined: document why, set next eligibility date

**Commission:** None. Builds massive trust and protects trail commission.

**Automation opportunity:** Quarterly trigger in POLR flags all customers due for repricing check. Broker gets task list. Currently ad-hoc.

**[ENHANCEMENT]** Offshore resource ($2,500/month) could do repricing research and hand opportunities to brokers (discussed in activation meeting).

---

## Customer Care Reactivation (Existing FHL Clients)

**Trigger:** Post-lifecycle customer (18+ months) or customer who fell out of lifecycle sequence.
**Current state:** No documented FHL customer care reactivation process. FFG has Consumer Customer Care Script (Doc 2/13) generating 41 new inquiries/month from outbound calls alone.

| RC# | Channel | Type | Action |
|-----|---------|------|--------|
| RC1 | Phone | [BROKER] | Outbound customer care call. Adapted from FFG Consumer Customer Care Script. Focus on: rate check, property valuation update, refinance opportunity, life changes. |
| RC2 | Email | [SYSTEM] | If no answer: automated email with same messaging. |
| RC3 | SMS | [SYSTEM] | If no answer after email: SMS with callback option. |

**Purchase Type personalisation for RC1:**
- FHB (now homeowner): "How's the house? We'd love to do a quick rate check and see how your equity has grown."
- Investor: "Checking in on your investment portfolio. Any plans for the next property? We can run the numbers."
- Refinancer: "It's been a while since your refinance. Worth checking if there's a better deal available now."
- New Purchase: "How's the new place? We like to check in and make sure you're still on the best rate."
- Commercial: "Any commercial property plans for the business this year?"

**FFG cross-sell flag:** During RC1, if customer mentions car, personal loan, equipment, consolidation, route to FFG.

---

## Existing SendGrid Automations (Reference)

These automations already exist. The T-System and lifecycle wraps around them, not replaces them.

| Automation | Emails | Schedule | Open Rate | Click Rate | Unsub Rate | T-System Mapping |
|-----------|--------|----------|-----------|------------|------------|-----------------|
| FHL New Customer Database Entry | 8 | Day 5, 90, 182, 350, 455, 547, 637, 727 | 62.4% | 5.2% | 1.31% | Overlaps with LC1-LC7 lifecycle (REPLACE with new lifecycle) |
| FHL No Customer Contact | 5 | Instant, Day 2, 5, 9, 16 | 52.0% | 2.5% | 0.26% | Maps to T2, T6, T8, T10, T12 (REPLACE with T-System) |
| FHL No Docs Returned | 4 | Instant, Day 1, 3, 3 | 58.8% | 3.4% | 0.85% | Maps to TD1-TD5 doc collection path (KEEP + enhance) |
| FHL Nurture Up to 3 Months | 7 | Day 14, 30, 45, 75, 90, 91, 120 | 61.6% | 2.3% | 0.63% | Maps to N13-N19 short/medium nurture (REPLACE with Purchase Type-targeted) |
| FHL Nurture Up to 6 Months | 7 | Day 30, 60, 90, 120, 150, 180, 210 | 67.4% | 3.7% | 0.82% | Maps to N16-N22 medium/long nurture (REPLACE with Purchase Type-targeted) |
| FHL Nurture Cold Lead | 7 | Day 30, 90, 180, 270, 365, 540, 730 | 55.7% | 2.4% | 1.73% | KEEP as cold nurture catch-all after N22 |

**Key insight:** FHL "No Customer Contact" has the LOWEST open rate (52%) of all automations. The current generic content isn't working. Purchase Type-targeted content should improve this significantly.

---

## Gap Analysis Summary

| Gap | Current State | Proposed Solution | Priority |
|-----|--------------|-------------------|----------|
| T1/T2 not automated | Template-triggered manually | Automate via N8N webhook, fire within 60 seconds | High |
| No Purchase Type classification at intake | Generic treatment for all leads | Journey classification decision tree (Q1) at first contact | High |
| No segmentation tag capture | Tags not systematically collected | Q2 checklist built into qualification call + POLR fields | High |
| Generic nurture after manual exhaustion | 52% open rate (lowest automation) | Purchase Type-targeted N13-N22 nurture (3-6 month consideration cycle) | High |
| No pre-appointment sequence | No confirmation, no reminders | PA1-PA3 automated sequence with Purchase Type-specific docs checklist | High |
| Infynity has no API | Manual/CSV data entry for settlement | Weekly CSV import workflow via N8N | High |
| No FHL-specific call scripts | No documented scripts for any stage | Create application, approval, settlement scripts (adapt FFG where possible) | Medium |
| Existing SendGrid lifecycle overlaps with new plan | 8-email "New Customer Database Entry" at Day 5-727 | Replace with Rowdy's 18-month lifecycle (LC1-LC7) | Medium |
| No customer care reactivation for FHL | FFG has process (41 inquiries/month), FHL has none | RC1-RC3 adapted from FFG Consumer Customer Care Script | Medium |
| Repricing not systematised | Ad-hoc, not on quarterly schedule | Quarterly trigger in POLR, task list for brokers | Medium |
| Cotality integration pending | Manual property valuations | API integration for Month 3 and Month 12 automated reports | Medium |
| No cross-sell trigger at Month 9 | No FFG Momentum Pack process | LC4 with Purchase Type-specific packs and FFG handover | Medium |
| Broker routing not documented | Informal/assumed | Documented routing table with Purchase Type mapping | Low |

---

## Cross-Sell Integration Points

The unified value journey has cross-sell triggers embedded at these touchpoints:

| Touchpoint | Trigger | Action |
|-----------|---------|--------|
| Q2 (Qualification) | Broker captures "likely next needs" tag | If vehicle/equipment/business finance: flag for FFG |
| LC1 (Month 1 Welcome) | Broker introduces FFG team | Plant seed for future asset finance needs |
| LC4 (Month 9 FFG Momentum) | Purchase Type-targeted pack sent | If customer responds: route to FFG team |
| LC5 (Month 12 Annual Review) | Review reveals non-mortgage needs | If applicable: warm introduction to FFG |
| RC1 (Reactivation) | Customer mentions non-mortgage needs | Route to FFG |

**Note:** Cross-sell is a trigger point within the unified value journey, not a separate pipeline.

---

## Key Metrics to Track

| Metric | Current | Target | Source |
|--------|---------|--------|--------|
| Speed to first call | Unknown | Under 5 minutes during business hours | POLR task creation timestamp |
| Contact rate (T3-T11) | Unknown (FFG is 65%) | 70% | POLR |
| Qualification completion (tags captured) | 0% (tags not tracked) | 90%+ | POLR |
| Purchase Type classification rate | 0% | 95%+ of contacted leads | POLR |
| Appointment booking rate | Unknown | 40%+ of contacted leads | POLR |
| Docs return rate | Unknown (FFG is 80%+) | 75%+ | POLR |
| Nurture re-engagement rate | Unknown | 10%+ of N13-N22 sequence | POLR |
| Pre-appointment show rate | Unknown | 85%+ | POLR |
| FHL No Customer Contact open rate | 52% (lowest) | 65%+ (with Purchase Type targeting) | SendGrid / POLR |
| Lifecycle touchpoint completion | 0% (no structured lifecycle) | 80%+ of LC1-LC7 executed on time | POLR |
| Month 9 FFG cross-sell conversion | 0% (no process) | 15%+ respond to Momentum Pack | POLR |
| Customer Care reactivation rate | 0% (no FHL process) | Match FFG (41+ inquiries/month scaled to FHL volume) | POLR |
| Repricing check completion | Ad-hoc | 100% quarterly for all active clients | POLR |
| Trail commission retention | Unknown (1-2 clawbacks/month) | Under 1 clawback/month | Infynity |

---

## Assumptions Register

These items are inferred from available data but need client validation:

| # | Assumption | Evidence | Validation Needed |
|---|-----------|----------|-------------------|
| 1 | FHL outbound cadence runs Days 1-9 (not Days 1-4 like FFG) | FHL SendGrid "No Customer Contact" schedule: Instant, Day 2, 5, 9, 16 | Confirm how many days brokers chase FHL leads |
| 2 | FHL brokers make ~4 call attempts (not 8 like FFG) | Lower volume (55 vs 375 leads), more complex leads, smaller team (3 vs 10+) | Confirm actual call attempt count |
| 3 | Broker routing by Purchase Type as documented | Inferred from team roles (Bill = commercial/investor, Paige = refinance/FHB) | Confirm with client |
| 4 | FHL online form completion rate is lower than FFG's 80% | Mortgage applications are more complex than car loan applications | Get actual data from Infynity |
| 5 | FHL does not have a 90-Day Declined Plan like FFG | No FHL declined automation in SendGrid inventory | Confirm: what happens to declined FHL applications? |
| 6 | Tags are not currently captured systematically | No evidence of tag fields in any system | Confirm with CTO/Matty |

---

*This process map is the foundation for the developer guide, SDR/broker handbook, call scripts, and customer lifecycle. Every T-number, N-number, Q-number, and LC-number referenced in those documents traces back to this document.*
