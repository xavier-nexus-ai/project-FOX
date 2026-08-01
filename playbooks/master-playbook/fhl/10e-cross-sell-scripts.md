# Cross-Sell Scripts (FHL)

**Playbook:** FHL Cross-Sell (FHL-as-origin → FFG)
**Brand folder:** playbooks/master-playbook/fhl/
**Direction:** FHL settled customer → FFG referral
**Version:** 2.0 DRAFT
**Owner:** James
**Status:** DRAFT

---

## How To Use This

Voice scripts only. Phone calls and voicemails.

- **Automated emails and SMS sequences** → Copy Library
- **Manual broker SMS and follow-up emails** → Broker Handbook
- **This document** → what to say on calls and what to leave on voicemail

The FHL cross-sell is embedded in lifecycle calls, not in standalone cross-sell calls. Most of these scripts are one question or one bridge line inside an existing conversation — not a full call structure.

Scripts are written for natural speech. Read them aloud before using. Adapt the phrasing to your voice.

---

## 1. Annual Review Cross-Sell (Month 12 — LC5 Call)

**When:** the Month 12 Annual Review lifecycle call. This question comes near the end of the call, after the home loan strategy discussion is complete.

**Purpose:** surface any FFG-relevant needs the Month 9 Momentum Pack did not convert. One question, not a pitch.

### 1.1 The Question

> "Quick one before we wrap up. Is there anything else on the financial to-do list this year that I should flag to my team? Car upgrade, business gear, debt to clean up, anything else?"

### 1.2 Routing Based on Their Answer

| They say | Tag you apply | What happens next |
|---|---|---|
| "Looking at a new car / ute / van" | `Lifecycle_FFGSignal_Vehicle` | FFG vehicle broker call within 48h |
| "Need equipment / truck / gear for the business" | `Lifecycle_FFGSignal_Equipment` | FFG commercial broker call within 48h |
| "Thinking about consolidating" | `Lifecycle_FFGSignal_Consolidation` | FFG consumer broker call within 48h |
| "Business expansion / second loan" | `Lifecycle_FFGSignal_Business` | FFG commercial broker call within 48h |
| "Maybe in 6 months" | `FFG_Interest` (deferred) | Auto-trigger at 6 months from today |
| "Nothing right now" | No tag | Return to standard lifecycle |

**If they say yes to anything:** do not pitch the product yourself. Acknowledge it and hand it over cleanly.

> "Leave that with me. I'll have one of our asset finance team give you a call in the next day or two. They handle the [vehicle / equipment / loan] side. I'll stay your home loans contact."

Then apply the relevant tag in GHL on the call or immediately after.

### 1.3 Voicemail (Annual Review)

This is not a standalone call — it is always booked in advance. If the customer no-shows, leave this voicemail:

> "Hey [first name], it's [name] from Fox Home Loans. We had the annual review booked for today — just trying to reach you. I'll send through a quick email with the key things we were going to cover. Give me a call back on [FHL number] when you get a chance, or reply to the email and we can reschedule. No stress. Talk soon."

---

## 2. Reactive Lifecycle Cross-Sell Call Language

**When:** any lifecycle call (LC1, LC3, LC5, LC7) where the customer mentions a vehicle, equipment, business finance, or debt consolidation need. You have spotted the FFG signal in conversation.

**Purpose:** bridge cleanly to the FFG team. Do not pitch the product. Make the handover feel natural.

### 2.1 Universal Bridge Line

> "Sounds like a chat with our [asset finance / commercial finance] team would be useful. Do you want me to have one of them give you a call this week? They handle the loan side from there — I stay your home loans contact."

Wait for their answer before tagging.

### 2.2 Per-Signal Variants

| Customer signal | Bridge line variant |
|---|---|
| Vehicle | "Our asset finance team handles car and ute loans. Same group, different team. Want me to flag it to them?" |
| Equipment / business gear | "We have a commercial finance team that does equipment and business assets. It's the same Fox group. Worth having them give you a call?" |
| Debt consolidation | "Our team on the personal finance side can run the numbers on consolidating that. Might be worth 15 minutes. Want me to set it up?" |
| Business expansion | "The commercial finance team handles that kind of thing — vehicles, equipment, business loans. Want me to have them reach out?" |

### 2.3 If They Say "Not Right Now"

> "All good, no rush. I'll note it and we can revisit."

Apply `FFG_NotInterested`. They will not be re-pushed for 12 months. Do not apply any FFG tags.

### 2.4 If They Say "Send Me an Email First"

> "No worries, I'll have them shoot you an email today and then give you a ring if you want to go further."

Apply `FFG_Interest`. The warm handover email fires automatically and the FFG broker gets a task.

### 2.5 Voicemail for Reactive Handover Follow-Up

Used by the FFG broker when the FHL broker has logged a reactive signal and the FFG broker is making the outbound call.

> "Hey [first name], it's [FFG broker name] from Fox Finance Group. [FHL broker first name] from our home loans team mentioned you'd been thinking about [vehicle / equipment / consolidation / business finance] and thought I'd reach out. Happy to have a quick chat about what that could look like. Give me a call on [FFG number] or I'll try you again [time]. No pressure. Cheers."

---

## 3. Warm Handover Call (FFG Broker Outbound — FHL-Referred Contact)

**When:** the FFG broker calls a customer who has been handed over from FHL — either via a Momentum Pack click or a reactive lifecycle tag.

**Purpose:** introduce the FFG broker, acknowledge the FHL relationship, and qualify the need. Short call. The FHL broker has already built the trust.

### 3.1 Call Opener

> "Hey [first name], it's [FFG broker name] from Fox Finance Group. [FHL broker first name] from our home loans team mentioned you might be thinking about [vehicle / equipment / personal loan / consolidation] and suggested I give you a call. I handle the asset finance side for our home loan customers. How are you going?"

Then:

> "So [FHL broker first name] said you're looking at [topic]. What does that look like for you?"

Listen. Then qualify the need and begin a normal discovery conversation.

### 3.2 Voicemail (Warm Handover)

> "Hey [first name], it's [FFG broker name] from Fox Finance Group. [FHL broker first name] from our home loans team thought it was worth me reaching out — mentioned you'd been thinking about [topic]. Happy to have a quick chat about it. Give me a call on [FFG number] or I'll try again [time]. No rush. Cheers."

---

## Dependencies

| Feeds into | What |
|---|---|
| 8e Cross-Sell Handbook (FHL) | Procedural instructions for each broker moment |
| 7e Developer Guide (FHL) | Workflow triggers and task SLA configuration |

| Depends on | Status |
|---|---|
| Tone of Voice gate | PASSED 2026-03-05 |
| FHL 18-month lifecycle plan (Rowdie) | RECEIVED 2026-03-06 |
| FFG broker routing queues | PENDING |

---

*Scripts are a starting point. Brokers refine the language in week one of live use. Lock after 30 days of real conversations.*
