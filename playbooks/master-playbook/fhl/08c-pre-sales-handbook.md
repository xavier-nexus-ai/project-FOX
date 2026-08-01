# FHL Pre-Sales Handbook

**Brand:** Fox Home Loans (mortgages, refinance, investment property, commercial property)
**Playbook:** Pre-Sales SDR (suffix c)
**Version:** 1.1
**Created:** 2026-05-05
**Owner:** James
**Status:** Draft

---

## Purpose

Day-to-day manual for the FHL SDR working pre-sale leads. The pipeline automation does the heavy lifting. This handbook covers what you do as a human between the automated touches.

FHL pre-sale is different from FFG. The lead is researching a mortgage decision that may take months. Your job is not to push. Your job is to be the most useful, most trustworthy voice they hear during that research.

**Convention:** FHL shares the five FFG ICAs. They are defined once in Section 2 (`02-ideal-client-profiles-avatars.md`). Purchase Type is the FHL operating overlay. This playbook names them and points back. It never redefines them.

---

## Your Role

You handle pre-sale and qualification. Once the application is taken, the lead moves through the application pipeline (separate playbook). Your pre-sale ownership ends at Booked Out.

The FHL pipeline runs on T-System (touchpoint-per-stage). The developer guide has the full map.

- **Interacting** (➡️⚡️). Inbound replies land here. 24hr RED dot. Action and move to FUP, Engaged, or Qualified as appropriate.
- **FUP** (👤). Your manually parked follow-up with a scheduled task. 24hr RED dot from task fire time.
- **T-stages** (T1 to T12). Cadence runs Day 1 to Day 16. Auto stages (⚡️) fire automation. Manual stages (👤) create call tasks for you. Each call = one T = one log entry.
- **N-stages** (N13 to N22). Automated nurture from Day 21 to Day 270. You don't touch unless lead replies.
- **Engaged**. Re-entry from any T or N stage.
- **Qualified**. Purchase Type confirmed, segmentation tags captured.
- **Booked Out**. Appointment booked. Card exits to Closer Pipeline.

### Interacting vs FUP — know the difference

| Stage | Trigger | What you do |
|---|---|---|
| Interacting | They replied to us (inbound). | Action today. Live conversation window. |
| FUP | We agreed to come back to them at a set time. | Wait for the task to fire on the scheduled day, then call. |

### One call, one T, one log

Every call attempt is its own T stage. T3 is one call. T4 is one call. T5 is one call. Log each one in GHL with a disposition:

| Disposition | Card movement |
|---|---|
| `No Answer` or `Voicemail Left` | Card auto-advances to the next T stage. |
| `Connected` | Move card to Engaged or Qualified. |
| `Booked` | Move card to Booked Out. Complete handoff brief. |
| `Not Interested` | Mark Lost. |
| `Wrong Number` | Mark Lost (reason: bad data). Flag to Rowdie if it's a pattern. |

---

## Your Day

| Block | What you are doing |
|---|---|
| Hour 1 (start of shift) | Action Interacting (24hr RED) replies. Speed-to-contact tasks first. |
| Hours 2-3 | T-stage manual calls (T3 / T4 Day 1, T5 Day 2, T7 Day 5, T9 Day 9 final). |
| Hours 4-5 | Engaged stage replies from N-series leads. Cotality value-add reports for Refinance + Investor leads. |
| Hour 6 | Pre-appointment confirmations + same-day reminders. |
| End of shift | Update notes in GHL. Tag Purchase Type + segmentation fields. Move stages. |

GHL tells you what to do next. If the system is quiet, work the FHL Customer Care list (cos.yaml: FFG outbound calls produce 41 inquiries/month, FHL has no equivalent process yet, opportunity).

---

## Rules of the Road

### 1. Speed matters, but not at the cost of quality

A reply landing in Interacting is hot. SMS auto-fires within 5 minutes (T2). Your call goes out inside 30 minutes (T3). Mortgage leads expect a slightly more considered first call than a personal loan lead, they want context, not urgency.

### 2. We are the guide. They are the hero.

We don't sell mortgages. We help people sort the biggest financial decision of their life. The customer is the hero. We are the knowledgeable companion who walks beside them. StoryBrand framing in the tone-of-voice guide.

## Q1: Journey Classification (Decision Tree)

When you make live contact, the first job is classifying Purchase Type.

```
"What brings you to Fox Home Loans?"

├── Buying first home → FIRST HOME BUYER
│   Confirm: never owned property, using FHB grants/schemes
│
├── Buying a home (already own / have owned) → NEW PURCHASE
│   Confirm: upgrading, downsizing, relocating
│
├── Looking at rates / checking options → REFINANCE
│   Confirm: has existing mortgage, exploring better deal
│
├── Investment property → INVESTOR
│   Confirm: already owns home or not, buying for investment
│   Note: FHB buying first as investment = INVESTOR
│
├── Commercial property → COMMERCIAL
│   Confirm: business purpose, not residential
│
└── Not sure / exploring → NEW PURCHASE (default)
    Qualify further during appointment.
```

Tag GHL: `purchase_type`, `purchase_type_confidence:high` once confirmed.

---

## Q2: Segmentation Tag Capture (Mandatory)

These tags drive every downstream lifecycle touchpoint. **If you don't capture them at qualification, the lifecycle automation cannot personalise.**

| Tag | What to capture | How to ask |
|---|---|---|
| `purchase_type` | FHB / New Purchase / Refinance / Investor / Commercial | "What brings you to Fox today?" |
| `employment_band` | PAYG / Self-employed | "Are you employed full-time, or do you run your own business?" |
| `household` | Single / Couple / Dependants flag | "Will this be in your name only, or with a partner?" + "Any dependants?" |
| `likely_next_needs` | Vehicle / Travel / Wedding / Reno-Solar / Debt consolidation / Business finance | "Any big purchases or plans coming up in the next 12 months?" |
| `product_preference` | Fixed / Variable / Split / Offset / IO / OO + key dates | Capture during application, not first call |
| `urgency` | Just exploring / Pre-approval / Under contract / Fixed expiring | "Where are you in the process?" |
| `source` | Auto-captured | -- |

**If tags are missing at handoff:** GHL flags it RED. Lifecycle automation cannot fire personalised content. Fix before Booked Out.

---

## Purchase Type Profiles (How to Talk to Each)

cos.yaml `fhl_writing_guidance` is the source of truth for purchase-type writing focus. The underlying human is the same as the Section 2 ICAs (`02-ideal-client-profiles-avatars.md`); this section covers the purchase need only, not the person. This is the SDR-call summary.

### First Home Buyer

**Writing guidance:** explain fundamentals, deposit/LVR basics, up-front costs, pre-approval flow, confidence-building.

**Opener:** "Hey {first_name}, it's {your_first_name} from Fox Home Loans. Saw you're looking at your first home. Quick question, are you still saving the deposit or close to ready?"

**Qualifying questions:**
- Have you spoken to a broker before, or is this your first time?
- Do you have a deposit saved, or working toward it?
- Have you looked into first home buyer grants or stamp duty concessions?
- Would a pre-approval help so you know what you can afford?

### New Purchase (Not First Home)

**Writing guidance:** readiness, borrowing power, offer/contract timing, pre-approval, reducing friction.

**Opener:** "Hey {first_name}, {your_first_name} from Fox Home Loans. Looks like you're moving on a new place. Have you sold your current spot, or running both?"

**Qualifying questions:**
- Have you sold your current property, or is this a second purchase?
- Do you have a property in mind, or still looking?
- Would a pre-approval help you move quickly?
- Is there a timeline you're working to?

### Refinance

**Writing guidance:** triggers, what to compare (rate, fees, features), equity/LVR, "health check" decision path.

**Opener:** "Hey {first_name}, {your_first_name} from Fox Home Loans. You were checking rates. What prompted the look?"

**Qualifying questions:**
- What prompted the refinance look? Rate, features, or something else?
- How long with your current lender?
- Do you know roughly what your property is worth today?
- Want a quick health check on your current loan? No commitment, just to see where you stand.

**Cotality cue:** Refinance leads are the best fit for the Cotality value-add. Offer the free property valuation.

### Investor

**Writing guidance:** cash flow language, long-term strategy, structure/features, risk management WITHOUT giving advice.

**Opener:** "Hey {first_name}, {your_first_name} from Fox Home Loans. You're looking at investment finance. Is this your first investment property?"

**Qualifying questions:**
- First investment, or do you have others?
- Main goal, cash flow or capital growth?
- Residential or commercial?
- How is your current lending structured? We can look at how this fits your broader strategy.

### Commercial

**Writing guidance:** documentation, timelines, deal structure variables, "what to prepare" checklists.

**Opener:** "Hey {first_name}, {your_first_name} from Fox Home Loans. You're looking at commercial property finance. What type of commercial?"

**Qualifying questions:**
- What type of commercial property?
- Owner-occupied or investment?
- Financials ready, or would it help to know what's needed?
- Timeline. In negotiation or still exploring?

**Routing:** Commercial → **Bill Robb** primary.

---

## Booking the Broker Appointment

Mortgage appointments are longer than personal loan calls. Set expectations.

### The script shape

1. Classify Purchase Type (Q1).
2. Capture mandatory tags (Q2).
3. Set the appointment: "Best move from here is a 30-minute appointment with one of our brokers. They'll walk you through what's possible, run the numbers, and answer everything. I've got tomorrow at 10am or Friday at 2pm. Which suits?"
4. Send the calendar invite while still on the call.
5. Tell them what to bring (Purchase Type-specific docs checklist):

**All Purchase Types:**
- Photo ID (driver's licence or passport)
- 2 most recent payslips (PAYG) OR 2 years tax returns + financials (self-employed)
- 3 months bank statements (all accounts)

**FHB additional:** Savings evidence (3-6 months), FHB grant application if eligible.
**Refinance additional:** Current loan statement, fixed rate expiry dates.
**Investor additional:** Rental income evidence, portfolio summary.
**Commercial additional:** 2 years business financials, ATO portal access.

6. Close: "We'll see you on {calendar_date_time}. Cheers, {first_name}."

### Booking rules

- Lock the appointment inside 48 hours of first contact wherever possible.
- High-value (>$800K) → Bill Robb consulted on routing before booking.
- Cross-sell from FFG → preserve broker continuity if possible.

---

## Booking, Reminders and No-Show Recovery

The pre-appointment confirmation, reminders, and no-show recovery now live in the Closer Booking playbook (`09d-closer-booking.md`). They run after you book the appointment and the card exits this pipeline.

---

## Reactivation Conversation Framework

FHL nurture leads who reply at any N stage are colder than fresh enquiries. They've been in nurture for weeks or months.

### Opening rules

- Identify Fox Home Loans in the first sentence.
- Lead with a reframe ("Things have shifted in the property market"), not a pitch.
- Ask one question.
- No urgency. Door open.

### What you do when they reply

1. Acknowledge it has been a while.
2. Ask what changed since the first enquiry.
3. If they sorted it elsewhere → congratulate, offer rate review on the existing loan, close warm. Tag `competitor:settled_elsewhere`.
4. If they stalled → ask what got in the way.
5. If they forgot → restart Q1 classification.

---

## Cross-Sell to FFG

If during qualification or any conversation the lead mentions car finance, equipment, consolidation, personal loan, or business finance → flag for FFG cross-sell.

GHL custom field `likely_next_needs` carries this signal. The cross-sell playbook handles the actual handoff. Your job is the flag.

The ICA-to-Purchase-Type mapping for cross-sell context lives once in Section 2 of the master playbook (`02-ideal-client-profiles-avatars.md`), under "ICA-to-FHL Cross-Sell Mapping". You do not need it to flag. Just flag the need; the cross-sell playbook handles the routing.

---

## Red Dot Protocol (What You See)

GHL puts a coloured dot on every lead based on how urgent your action is.

| Dot | Meaning | Example |
|---|---|---|
| 🔴 RED | Hot. Action now. | A reply just landed. A booked appointment got missed. A high-value lead (>$800K) just came in. |
| 🟡 YELLOW | Warning. SLA approaching or just passed. | A T5 Day 2 call task is 4 hours overdue. |
| 🟢 GREEN | On track. | Lead sitting in N-series nurture. |

### Your SLAs

| Stage | Action | SLA |
|---|---|---|
| Interacting | Read record, action reply, move to FUP | 1 hour business hours |
| FUP (lead has replied) | Call them. They are warm. | 5 minutes |
| T3 (Day 1 morning call) | Call logged in 3CX | 4 hours after stage entry |
| T4 (Day 1 afternoon call + voicemail) | Call + voicemail logged | 4 hours after T3 clears |
| T5 (Day 2 call + voicemail) | Call + voicemail logged | 4 hours after T4 clears |
| T7 (Day 5 call + voicemail) | Call + voicemail logged | 4 hours after T6 fires |
| T9 (Day 9 final + last voicemail) | Final call + voicemail logged | 4 hours after T8 fires |
| Engaged | Pick up the conversation | 1 hour business hours |
| Qualified | Complete handoff brief, book appointment | 4 hours |
| Pre-Appointment no-show | Recovery sequence | 1 hour after missed |
| High-value (>$800K) | Bill Robb notified, you priorise | Immediate |

### Escalation chain

Tier 1: You → Tier 2: **Bill Robb** (Head of Home Loans / Partnerships) → Tier 3: **Rowdie Lang** → Tier 4: **Nathan Drew** (systemic only).

### Business hours

Mon-Fri, 8:30am-5:30pm AEST. Outside hours, dots pause. Resume at 8:30am next business day.

---

## GHL Hygiene

Every lead, every touch.

- Plain English notes. Two to four sentences. "Spoke to {first_name} at 10:30. Refinancing $650K loan, 2 years with current lender, fixed expires March. Curious about variable. Booked Paige for Thursday 2pm."
- Tag Purchase Type + confidence.
- Tag the segmentation fields (employment_band, household, likely_next_needs, urgency).
- Move the stage.
- Log 3CX call recording link in GHL contact.
- If you used Cotality, attach the report ID to the contact.

If tags are incomplete, GHL flags it RED at handoff. Don't let a lead exit Qualified without the full tag set.

---

## Escalation

Call **Bill Robb** if:

- High-value lead (>$800K) needs review.
- Commercial lead with complex deal structure questions.
- Cross-sell from FFG that needs partnership-level handling.

Call **Rowdie** if:

- A reactivation reply gets emotional or threatening.
- Pattern of low-quality leads from a specific source.

Call **Nathan** if:

- A lead mentions a regulator or external complaint.
- Public-figure name in the form.

---

---

## Broker Handoff Brief

Complete this before the lead exits at Booked Out. Lives in GHL contact notes and copies into Infynity (manual entry, no API per cos.yaml).

### Template

```
LEAD HANDOFF: {first_name} {last_name}

Source: {source} | Brand: FHL | Partner: {partner_name if applicable}
Purchase Type: {purchase_type} (confidence: {purchase_type_confidence})
Loan amount band: {loan_amount_band}
Employment: {employment_band}
Household: {household}
Urgency: {urgency}
Likely next needs: {likely_next_needs}

WHAT THEY WANT
[One sentence. Plain English. What they said on the call.]

SITUATION
- Property: {property_address or "not yet identified"}
- Existing lender (if refinance/upgrader): [name]
- Deposit / equity position: [if known]
- Timeline drivers: [contract, fixed expiry, just exploring]

WHAT THEY'VE READ
[Cotality report ID if sent. Any nurture emails they engaged with.]

OBJECTIONS OR FLAGS
[Anything they pushed back on, hesitated on, or asked about. None = "None."]

NEXT STEP
Booked with {broker_first_name} on {calendar_date_time}.
Docs checklist sent (Purchase Type-specific): yes/no.

SDR NOTES
[Two to four sentences in plain English. What you'd want to know if you were taking the appointment.]

{sdr_first_name}, {timestamp}
```

### Worked example

```
LEAD HANDOFF: Sarah Chen (hypothetical example)

Source: fhl_website | Brand: FHL | Partner: --
Purchase Type: Refinance (confidence: high)
Loan amount band: $500K-1M
Employment: PAYG
Household: Couple
Urgency: Fixed expiring soon
Likely next needs: --

WHAT THEY WANT
Refinance off a fixed rate ending in 8 weeks. Wants to know if variable now or roll into another fixed.

SITUATION
- Property: 12 Example St, Brisbane (4000)
- Existing lender: NAB, 5.89% fixed, expires Aug 2026
- Deposit / equity position: approx 30% equity per Cotality (sent on Day 35)
- Timeline drivers: fixed expires 8 weeks

WHAT THEY'VE READ
Cotality report. Read N15 + N19 (rate-check emails). Replied REVIEW on N13.

OBJECTIONS OR FLAGS
Hesitated on broker fee. Asked if there's a way to compare lenders themselves first.

NEXT STEP
Booked with Paige Beveridge on Friday 2pm.
Docs checklist sent (Refinance variant): yes.

SDR NOTES
Sarah's done plenty of homework. Replied to multiple nurture emails before booking. Worth opening with the rate comparison and walking through fee structure transparently. Cotality already shows strong equity position.

[SDR name], 06/05/2026 14:32
```

---

*End of FHL Pre-Sales Handbook.*
