# Cross-Sell Scripts (FFG)

**Playbook:** FFG Cross-Sell (FFG-as-origin → FHL)
**Brand folder:** playbooks/master-playbook/ffg/
**Direction:** FFG settled customer → FHL referral
**Version:** 2.0 DRAFT
**Owner:** James
**Status:** DRAFT

---

## How To Use This

Voice scripts only. Phone calls and voicemails.

- **Automated emails and SMS sequences** → Copy Library
- **Manual broker SMS templates and follow-up emails** → Broker Handbook
- **This document** → what to say on calls and what to leave on voicemail

Scripts are written for natural speech. Read them aloud before using. Adapt the exact words to your voice — do not read verbatim. The structure is non-negotiable. The phrasing is a starting point.

---

## 1. At-Settlement Seed Call

**When:** the settlement call you make today as part of the standard FFG settlement process. This question comes after the standard settlement wrap-up points.

**Purpose:** identify FHL purchase type and log it. You are not selling FHL. You are planting a seed the system will grow over the next 12 months.

### 1.1 The Question

```script
"Mate, before we wrap up, quick one. Do you currently own a property, or is that something on the horizon?"
```

### 1.2 Response Pathways

| They say | Log in `fhl_purchase_type` | What you say |
|---|---|---|
| "I own one." (single, owner-occupied) | `Refinance` | ```script "Good on you. Just so you know, our home loans team does a free property and loan health check for our customers at the six-month mark. Nothing pushy, just making sure you're on the best deal. We'll be in touch." ``` |
| "I own a few." (investor) | `Investor` | ```script "Nice. Our home loans team works with a lot of investors. As your finance situation develops over the next year, we'll loop you in on anything worth knowing." ``` |
| "I rent." / "I'm with parents." | `FHB` | ```script "All good. Down the track when buying becomes part of the plan, we have a home loans team that helps first home buyers all the time. We'll send you a couple of useful things over the next few months. No pressure." ``` |
| "I'm thinking about buying." | `New Purchase` | ```script "Right time to start the conversation. Our home loans team can run pre-approval numbers without it impacting your credit score. Want me to ping them now?" ``` |

**If they say "I'm thinking about buying":** apply tag `FHL_Interest` manually now. The FHL Referral Workflow fires and an internal task lands with the FHL broker within the hour.

### 1.3 BAB Extension

For Business Asset Borrowers — also ask:

```script
"One more quick one. Do you own your business premises or are you leasing?"
```

| They say | Log in `fhl_purchase_type` |
|---|---|
| "I own them." | `Commercial` |
| "I'm leasing." / "Haven't bought yet." | `New Purchase` |

### 1.4 Voicemail (At-Settlement)

Used when the customer does not answer the settlement call.

```script
"Hey [first name], it's [your name] from Fox. Just calling to say your loan has settled — congratulations. Everything is in order from our end. I'll send you an email now with the details. And I'll try you again [tomorrow / in a couple of days] to do a quick wrap-up. Looking forward to it. Speak soon."
```

The purchase-type question waits for the next contact attempt. Do not leave it on voicemail.

---

## 2. Hot Lead Call (FFG_HotLead Task)

**When:** a `FFG_HotLead` task lands in your queue. The customer clicked an FFG product CTA in months 7-12. SLA is 24 hours.

**Before you call:** open their GHL contact. Check the original loan (lender, amount, ICA tag), which email they clicked, FHL purchase type, and any recent SMS replies. Takes 90 seconds. Changes the conversation.

### 2.1 Universal Opener

```script
"Hey [first name], it's [your name] from Fox. How are you going? Listen, we noticed you were poking around on [the page they clicked] over the weekend. Wanted to check in. Anything happening on the [car/business/loan] front?"
```

You are not pretending you do not know they clicked. You are showing you noticed and following up. That is the relationship Fox is selling.

### 2.2 Per-ICA Opener Lines

Use after the universal opener, based on the ICA tag.

| ICA | What to say |
|---|---|
| YPMB | ```script "Your credit's had a year to grow. The bigger loan we couldn't quite get you over the line for back then might be on the table now." ``` |
| EPFB | ```script "You've paid down the [debt consolidation / renovation] loan a fair bit. Cash flow's freed up. What's the next thing on the list?" ``` |
| PCLRB | ```script "You know how this works. Tell me what you're thinking and I'll have options to you by Friday." ``` |
| BAB | ```script "How's the [asset] performing? Any other equipment on the horizon?" ``` |
| PVB | ```script "Looking at the next vehicle? We can have you pre-approved before you walk into a dealership. Saves you the haggle." ``` |

### 2.3 Routing Based on Their Answer

| They say | What to do |
|---|---|
| "Yeah, thinking about [new car / debt consolidation / equipment upgrade]." | Discovery on the new need. CLOSER framework applies. Treat as a warm pre-approval conversation. |
| "Just having a look, no plans yet." | ```script "Fair enough. What got you looking?" ``` Listen. Log a callback for 30 days. Keep them warm. |
| "Actually I was looking at home loans." | Apply `FHL_Interest` tag. Hand to the FHL team. Stay involved as the introducer. |
| "I'm not interested, please stop." | Apply `FFG_Unsubscribed`. Log the reason. Move on. |

**Log the outcome in GHL:** `Contacted`, `Booked Call`, `Applied`, `Not Interested`, `No Response`.

### 2.4 Voicemail (Hot Lead)

```script
"Hey [first name], it's [your name] from Fox. Just trying to reach you — we noticed you'd been having a look at [topic] and wanted to make sure you had everything you needed. No rush, no pressure. Give me a call back on [number] when you get a chance, or reply to the email we'll send through. Talk soon."
```

Send the manual Hot Lead SMS within 30 minutes of leaving this voicemail.

---

## 3. FHL Interest Call (FHL Broker)

**When:** the `FHL_Interest` task lands in the FHL broker queue. SLA is 48 hours. The original FFG broker is the introducer — not the closer.

### 3.1 Call Opener

```script
"Hey [first name], it's [name] from the home loans side at Fox. [FFG broker first name] mentioned you settled with them on [vehicle/loan] last year and you've been having a look at the home loans content we've been sending through. Wanted to introduce myself properly before any of that became a real thing. How's it all going?"
```

### 3.2 Conversation Direction by ICA and Purchase Type

| ICA + Pathway | Focus |
|---|---|
| YPMB → FHB | First home buyer fundamentals. Deposit. LVR. Pre-approval. Borrowing power. Long sales cycle. Confidence-building. |
| EPFB → New Purchase | Readiness check. Borrowing power. Pre-approval timing. |
| EPFB → Refinance | Health check. Rate review. Equity check. |
| PCLRB → New Purchase | Same as EPFB but faster. Sophisticated buyer. |
| PCLRB → Refinance | Rate movement. Lender changes. What they could be on instead. |
| PCLRB → Investor | Cash flow language. Long-term strategy. |
| BAB → Commercial | Documentation. Timelines. Deal structure. |
| BAB → Residential (low doc) | Self-employed pathway. BAS statements. Accountant letter. No tax returns required. |
| PVB → New Purchase / Refinance / Investor | Same as PCLRB. Sophisticated. Tighter sales cycle. |

**Hand-back rule:** if the customer says "actually I want to talk about my car loan," apply `FFG_HotLead` and hand back to the FFG broker. Never push someone toward a product they have signalled away from.

### 3.3 Voicemail (FHL Interest Call)

```script
"Hey [first name], it's [name] from the home loans team at Fox. [FFG broker first name] from our asset finance side mentioned you'd been having a look at the home loans content we've been sending through. Wanted to reach out and introduce myself before things got serious. Give me a call back on [FHL number] or reply to the email we'll send through. No rush. Talk soon."
```

---

## 4. Nine-to-Twelve Month Proactive Call

**When:** PCLRB, PVB, and BAB only. Contacts flagged as engaged but not yet hot in the lead score dashboard ("Worth a call" queue).

**Cadence:** 30 minutes per broker per week. Five to eight calls. Focused on the engaged middle — not the cold and not the hot.

**Purpose:** surface the next opportunity and be remembered as the broker who called when nothing was wrong. The goal is not to close. It is to be the default when something does come up.

### 4.1 Universal Opener

```script
"Hey [first name], it's [name] from Fox. Just calling to check in. It's been about [time since settlement] since we sorted out the [vehicle/loan] for you. How's that all going?"
```

Listen. Then ask the per-ICA question below.

### 4.2 Per-ICA Questions

| ICA | The one question that opens it up |
|---|---|
| PCLRB | ```script "What's the next thing on the to-do list — for the family, the household, the lifestyle? Anything in the next 6-12 months we should be on top of?" ``` |
| PVB | ```script "When are you planning to upgrade the [vehicle]? We can get you pre-approved before you start looking. Saves the haggle at the dealership." ``` |
| BAB | ```script "How's the business going? Anything coming up in the next 6 months — replacement gear, new vehicle, anything we should be ready for?" ``` |
| EPFB | ```script "Now that the [original loan purpose] is sorted, what's next on the financial plan?" ``` |
| YPMB | ```script "How's the [car] going? Everything running well?" ``` (Pure check-in. Do not pitch unless they open it.) |

### 4.3 Log Every Call

Outcome dropdown in GHL:
- `Check-in only` — no opportunity surfaced
- `Future opportunity` — log specific need + date to follow up
- `Active opportunity` — convert into a pre-approval conversation now
- `FHL referral` — apply `FHL_Interest` tag, hand to FHL team
- `Refer-a-friend mentioned` — log it, follow up

### 4.4 Voicemail (Proactive Call)

```script
"Hey [first name], it's [name] from Fox. Just checking in — it's been about [time] since we sorted the [vehicle/loan] for you. Wanted to make sure everything's still going well and see if there's anything on the horizon we can help with. Give me a call back on [number] when you get a moment. No rush. Chat soon."
```

---

## 5. SMS Active Response (FFG_SMSActive Task)

**When:** a customer has replied to an automated SMS. The system has paused all SMS automation. SLA is 24 hours. A task is in your queue.

**The rule:** never auto-respond beyond the system's acknowledgement. The actual reply must be personal — by phone or by personal SMS.

### 5.1 If They Asked a Specific Question (SMS reply)

```script
"Hey [name], just got your message. [Direct answer to their question]. Want me to give you a quick call to walk through it?
[Your name]"
```

### 5.2 If They Said Something Generic — "Yes" / "Interested" (SMS reply)

```script
"Hey [name], thanks for getting back. What was the bit that caught your eye? Happy to call now or pick a time that suits.
[Your name]"
```

### 5.3 If It Is a Complaint or Concern

Phone call. Today. Not SMS. The system flag is enough — do not pile on with text.

### 5.4 Voicemail (After Missed Call on SMSActive)

```script
"Hey [name], it's [your name] from Fox — I saw your message and wanted to give you a call back personally. I'll try you again [time / tomorrow morning]. You can also reply to my SMS and I'll come straight back to you. Cheers."
```

---

## Dependencies

| Feeds into | What |
|---|---|
| 8e Rep Handbook | Procedural instructions for each broker moment |
| 7e Developer Guide | Workflow triggers and SLA configuration |

| Depends on | Status |
|---|---|
| Tone of Voice gate | PASSED 2026-03-05 |
| FFG Post-Settlement Nurture Strategy v2.0 | RECEIVED 2026-04-27 |
| Settlement Calls script (Doc 6) | BLOCKER: still empty |

---

*Scripts are a starting point. Brokers refine the language in week one of live use. Lock after 30 days of real conversations.*
