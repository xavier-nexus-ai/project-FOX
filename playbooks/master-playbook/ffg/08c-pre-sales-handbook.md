# FFG Pre-Sales Handbook

**Brand:** Fox Finance Group (asset finance)
**Playbook:** Pre-Sales SDR (suffix c)
**Version:** 1.1
**Created:** 2026-05-05
**Owner:** James
**Status:** Draft

---

## Purpose

Day-to-day manual for the FFG SDR. The pipeline automation does the heavy lifting. This handbook covers what you do as a human between the automated touches.

You are the first voice the lead hears. The closing team converts at 95%+ once the lead is on the phone. Your job is to get them there, qualified and warm, with the right information attached.

**Convention:** ICAs are defined once in Section 2 of the master playbook (`02-ideal-client-profiles-avatars.md`). This playbook names them and points back. It never redefines them.

---

## Your Day

The FFG pipeline runs on T-System (touchpoint-per-stage). You see your tasks per stage. The developer guide has the full pipeline map.

- **Interacting** (➡️⚡️). Replies land here first. 24hr RED dot. Action and move to FUP.
- **FUP** (👤). Your follow-up parking with a 24hr task reminder.
- **T-stages** (T1 to T14). 4-day direct cadence. Auto stages (⚡️) fire automation. Manual stages (👤) create call tasks for you.
- **N-stages** (N15 to N22). Automated nurture from Day 7 to Day 180. You don't touch these unless the lead replies (then card jumps to Engaged and lands on your plate).
- **Engaged**. Re-entry from any T or N stage. SDR takes over.
- **Qualified**. All fields captured, ICA confirmed, ready to book the broker call.
- **Booked Out**. Card exits to the Closer Pipeline.

| Block | What you are doing |
|---|---|
| Hour 1 (start of shift) | Action Interacting (24hr RED) replies. Speed-to-contact tasks first. |
| Hours 2-4 | T-stage manual calls (T3 / T4 / T5 Day 1, T7 / T8 Day 2, T10 / T11 Day 3, T13 Day 4 final). |
| Hours 5-6 | Engaged stage replies from N-series leads + reactivation cohort SMS replies. |
| Hour 7 | Booking confirmations for tomorrow + customer care call list. |
| End of shift | Update notes in GHL. Tag every lead. Log dispositions. |

GHL tells you what to do next. If the system is quiet, work the Reactivation reply queue, then the Customer Care call list (cos.yaml: 41 inquiries last month from outbound care calls, no automation).

---

## Rules of the Road

### 1. Speed kills hesitation

A lead that filled the form 5 minutes ago is hot. SMS goes out automatically inside 5 minutes (T2). Your call goes out inside 15 minutes (T3). Treat any lead older than 24 hours as cooler. Same effort, less expectation.

### 2. We are the guide. They are the hero.

We do not sell. We help them sort their finance. Customer is the hero. We are the knowledgeable mate who walks beside them. StoryBrand framing in the tone-of-voice guide.

## Handling Inbound Leads by Lead Magnet

Four magnets. Same process shape. Different opening hook.

### Commercial Vehicle

**Likely ICA:** Business Asset Borrower
**App type:** Commercial
**What they want:** A vehicle for the business, often EOFY or replacement-cycle pressure.

**Opener (call or SMS):**
"Hey {first_name}, it's {your_first_name} from Fox Finance Group. You grabbed our commercial vehicle guide. Quick check, are you looking at a specific vehicle or still working out the budget side?"

**Qualifying questions:**
- ABN registered, how long?
- Vehicle type, age, kilometres if known.
- Use case: own use, mixed, sub-contracted?
- Approximate value.
- Time pressure: this month, this quarter, EOFY?

**Tag in GHL:** `app_type:commercial`, `loan_type:chattel_mortgage`, `primary_ica:business_asset` (low confidence until confirmed).

### Commercial Equipment

**Likely ICA:** Business Asset Borrower
**App type:** Commercial
**What they want:** Equipment finance, often for replacement, growth, or EOFY tax timing.

**Opener:**
"Hey {first_name}, it's {your_first_name} from Fox Finance Group. You picked up our commercial equipment guide. Are you looking at a specific piece of gear or sizing up your options?"

**Qualifying questions:**
- ABN length.
- Equipment type and approximate value.
- New or used.
- Replacement or addition to the fleet?
- Time pressure.

**Tag in GHL:** Same as commercial vehicle.

### Consumer Personal

**Likely ICA:** Established Personal Finance OR Prime Convenience Repeat
**App type:** Consumer
**What they want:** A personal loan. Could be debt consolidation, home improvement, planned spending.

**Opener:**
"Hey {first_name}, it's {your_first_name} from Fox Finance Group. You grabbed our consumer personal loan guide. What's the loan helping you sort out?"

**Qualifying questions:**
- Loan purpose.
- Approximate amount.
- Employment type and length.
- Renting, mortgaged, or other?
- Existing loans or credit cards?

**Routing split:** Loan amount $30K+, full-time, mortgaged → Prime Convenience Repeat (highest-value ICA, **fast-track pool**). Otherwise → Established Personal Finance.

### Consumer Vehicle

**Likely ICA:** Young Practical Motor OR Prime Vehicle
**App type:** Consumer
**What they want:** A car loan.

**Opener:**
"Hey {first_name}, it's {your_first_name} from Fox Finance Group. You picked up our consumer vehicle guide. Have you got a car in mind or still shopping?"

**Qualifying questions:**
- Vehicle type, age, approximate price.
- New or used.
- Trade-in?
- Employment type and length.
- Renting, mortgaged, with parents?
- Approximate age band (you can read it without asking).

**Routing split:** Age 40+, full-time, mortgaged → Prime Vehicle. Otherwise → Young Practical Motor.

---

## ICA Tagging at Qualification

You will not be 100% sure on the first call. Best-guess from form plus conversation. Set `ica_confidence` to `medium` once you have spoken, `high` once the broker confirms.

> **ICA reference.** Full ICA definitions (who they are, what they value, FHL pathway, return-loan signal) live once in Section 2 of the master playbook (`02-ideal-client-profiles-avatars.md`). This handbook names the ICA and points back. It never redefines it. The five FFG ICAs are YPMB, EPFB, PCLRB, BAB, PVB. PCLRB is the highest-value ICA: fast-track them to the broker pool (Brad-tier).

The quick tells you use to tag the picklist, plus the tie-break order when two seem possible:

| Quick tell on the call | Tag |
|---|---|
| First or second car, young, light credit file | YPMB |
| Personal loan or consolidation, mid-life, full-time | EPFB |
| $30K+ unsecured, mortgaged, repeat or referral | PCLRB (fast-track) |
| Self-employed, ABN, asset finance | BAB |
| Vehicle finance, 40+, mortgaged, wants it smooth | PVB |

Tie-break order: BAB → PVB → YPMB → PCLRB → EPFB.

Wrong tag fires the wrong post-call sequence. Take the extra 30 seconds.

---

## Booking the Broker Call (BAMFAM)

Book A Meeting From A Meeting. Never end a call without the next step locked.

### The script shape

1. Ask the qualifying questions.
2. Confirm what they want.
3. Set the broker call: "Best move from here is a quick chat with one of our brokers. They'll walk you through your options. I've got a 15 minute slot today at 2pm or tomorrow at 10am. Which works?"
4. Send the calendar invite while still on the call. Confirm they have it.
5. Tell them what to expect: "{broker_first_name} will call you on this number. They'll have your details so you don't repeat yourself."
6. Close: "Anything you want to read before the call, the guide you grabbed has the basics. Cheers, {first_name}."

### Booking rules

- Lock the broker call inside 24 hours from first contact wherever possible.
- Prime Convenience Repeat → broker call same day if the slot exists.
- Commercial leads → broker call inside 48 hours unless the lead pushes back. Don't lose them to a dealer.
- Send the SMS confirmation within 60 seconds of booking. GHL workflow handles it. Confirm it sent.

---

## Reactivation Conversation Framework (Lead Market Recapture)

Reactivation leads are colder. They asked about finance somewhere in the last 6-12 months and never settled with us. They might have settled elsewhere. They might have stalled. They might have forgotten.

### Opening rules

- Identify Fox in the first sentence. No mystery.
- Lead with a reframe, not a pitch ("Things have shifted since we last chatted").
- Ask one question. Make it easy to reply.
- No pressure. No urgency. Door open.

### What you do when they reply

1. Acknowledge it has been a while.
2. Ask what changed since they first looked. ("Did you sort it out somewhere else?" is a fair question.)
3. If they sorted it elsewhere, congratulate, offer rate review on the existing loan, close warm. Tag `competitor:settled_elsewhere`.
4. If they stalled, ask what got in the way. Then offer the next step.
5. If they forgot, restart the qualification flow.

### What you don't do

- Pretend the gap didn't happen.
- Use guilt ("you never got back to us"). Never.
- Push for a booking on first reply. Build trust first.

---

## Customer Care Calls (Existing FFG Book)

41 new inquiries last month from outbound care calls with no automation (cos.yaml). Use the rate-drop refinance hook. Cross-sell openings: car loan, personal loan, consolidation, home loan (FHL handoff).

ICA personalisation for Customer Care calls:

- Young Practical Motor: "How's the car going? With recent rate drops, refinancing could save you money."
- Business Asset: "Any equipment needs coming up? EOFY is a good time to look at tax-effective financing."
- Prime Vehicle: "Time for an upgrade? We can make it smooth and easy."
- Prime Convenience Repeat: "Quick check-in. Need anything? We can fast-track for you."
- Established Personal: "Just touching base. Any big plans coming up we can help with?"

If they mention property, investment, or home loan: flag for **FHL cross-sell**. The ICA-to-FHL Purchase Type mapping lives once in Section 2 of the master playbook (`02-ideal-client-profiles-avatars.md`), under "ICA-to-FHL Cross-Sell Mapping". Cross-sell logic itself is owned by the cross-sell playbook, not this one. Your job is the flag.

---

## Red Dot Protocol (What You See)

GHL puts a coloured dot on every lead based on how urgent your action is.

| Dot | Meaning | Example |
|---|---|---|
| 🔴 RED | Hot. Action now. Missing the SLA escalates fast. | A reply just landed at Interacting. A booked lead missed their call. |
| 🟡 YELLOW | Warning. SLA is approaching or has just passed. | A T7 Day 2 call task is 4 hours overdue. |
| 🟢 GREEN | On track. No action needed right now. | A lead is sitting in N-series nurture and the system has it. |

### Your SLAs (the ones that drive your day)

| Stage | What you need to do | SLA |
|---|---|---|
| Interacting | Read the record, action the reply, move to FUP. | 1 hour business hours |
| FUP (lead has replied) | Call them. They are warm. | 5 minutes |
| T3 (Day 1 morning call) | Call logged in 3CX. | 4 hours after stage entry |
| T4 (Day 1 lunch call) | Call logged. | 4 hours after T3 clears |
| T5 (Day 1 5pm call + voicemail) | Call + voicemail logged. | 4 hours after T4 clears |
| T7-T8 (Day 2 calls) | Call attempts logged. | 6 hours each after T6 fires |
| T10-T11 (Day 3 calls) | Call attempts logged. | 6 hours each after T9 fires |
| T13 (Day 4 final call + voicemail) | Final call + voicemail logged. | 8 hours after T12 fires |
| Engaged (re-entry from nurture) | Pick up the conversation. | 1 hour business hours |
| Qualified | Complete the handoff brief, book the broker call. | 4 hours |
| Reactivation reply | Reply within 30 min if intent is in the message. | 30 minutes |

### What happens if you miss

- First miss: GHL dashboard alert to you. Action the task.
- Second miss: alert to **Sam Drew** (Head of Asset & SME). He'll check in.
- Third miss: alert to Rowdie. Pattern of breaches is a coaching conversation.

The dot system is not punishment. It's the safety net that catches a lead before they go cold. Action the dots and you stay green.

### Business hours

Mon-Fri, 8:30am-5:30pm AEST. Outside hours, dots pause. They resume at 8:30am next business day. Speed-to-contact applies inside business hours.

---

## GHL Hygiene

Every lead, every touch.

- Update the contact record with what happened, in plain English. Two sentences. "Spoke to {first_name} at 11:15. Wants a $25K personal loan for kitchen reno, full-time, mortgaged. Booked Brad for tomorrow 10am."
- Tag the ICA + confidence.
- Move the stage.
- Log call recording link from 3CX into the GHL contact under `call_recordings` (Ambition link auto-syncs per cos.yaml).
- Magnet status: did they read it? Reference it in your follow-up.

If you skip the notes, the broker walks into the call cold. That breaks the whole point of pre-sales. Don't break it.

---

## What Good Looks Like

Brad is the benchmark. 70-80% of his settlements come from repeat or referral business. He is not a SDR, he is a closer, but the standard he expects from the SDR who hands him a lead is:

- ICA tagged, confidence at least medium.
- Notes in plain English, two to four sentences.
- Loan purpose, amount, employment, residential status captured.
- Magnet (if any) referenced so he knows what they have already read.

Hand a Brad-quality brief on every lead.

---

## Escalation

Call **Rowdie** if:

- Multiple lead magnet leads from the same source feel suspicious (bot signups, spam).
- A broker complains about lead quality two days running.

Call **Nathan** if:

- A lead mentions a regulator or external complaint.
- A media or public-figure name appears in the form.

---

---

## Broker Handoff Brief

Complete this before the lead exits at Booked Out. Lives in GHL contact notes and copies into Ambition.

### Template

```
LEAD HANDOFF: {first_name} {last_name}

Source: {source} | Magnet: {lead_magnet_taken} | Brand: FFG
ICA: {primary_ica} (confidence: {ica_confidence})
App type: {app_type} | Loan type: {loan_type}
Loan amount band: {loan_amount_band}

WHAT THEY WANT
[One sentence. Plain English. What they said on the call.]

SITUATION
- Employment: {employment_type}
- Residential: {residential_status}
- Other relevant: [marital, dependants, time pressure, anything they flagged]

WHAT THEY'VE READ
[Magnet name and any Fox content they engaged with.]

OBJECTIONS OR FLAGS
[Anything they pushed back on, hesitated on, or asked about. None = "None."]

NEXT STEP
Booked with {broker_first_name} on {calendar_date_time}.
{broker_first_name} to call on {phone_number}.

SDR NOTES
[Two to four sentences in plain English. What you'd want to know if you were the one taking the call.]

{sdr_first_name}, {timestamp}
```

### Worked example

```
LEAD HANDOFF: Jamie Carter (hypothetical example)

Source: ffg_website | Magnet: consumer_personal | Brand: FFG
ICA: Established Personal Finance Borrower (confidence: medium)
App type: Consumer | Loan type: Personal Loan
Loan amount band: $15-30K

WHAT THEY WANT
A $25K personal loan to consolidate three smaller debts into one repayment.

SITUATION
- Employment: Full-time, 4 years same role
- Residential: Renting, looking to buy in 2 years
- Other relevant: Wants to clean up the credit file before applying for a home loan

WHAT THEY'VE READ
Personal loan guide. Mentioned secured vs unsecured loans.

OBJECTIONS OR FLAGS
Worried about hit to credit file from the consolidation.

NEXT STEP
Booked with Brad on Tuesday 11am.
Brad to call on 0412 345 678.

SDR NOTES
Jamie's already done the homework. Wants to consolidate cleanly and protect the credit file for a home loan in 2 years. Worth setting expectations on credit-file impact early on the call.

Sam, 06/05/2026 14:32
```

---

*End of FFG Pre-Sales Handbook.*
