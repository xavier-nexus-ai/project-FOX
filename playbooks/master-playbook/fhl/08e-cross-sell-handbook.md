# Cross-Sell Rep Handbook (FHL)

**Playbook:** FHL Cross-Sell (FHL-as-origin → FFG)
**Brand folder:** playbooks/master-playbook/fhl/
**Direction:** FHL settled customer → FFG referral
**Version:** 2.0 DRAFT
**Created:** 2026-05-05
**Owner:** James
**Status:** DRAFT

---

## Purpose

What you do when the cross-sell engine surfaces a moment to hand a customer to FFG. You do not pitch FFG. You listen on calls, you log the signal, the system routes it, an FFG broker takes the conversation. You stay the trusted home loans contact.

Where the rest lives, do not relearn it here:

- **Pipeline + build detail:** Developer Guide 07e. The pipeline below matches it exactly.
- **What to say (openers, voicemails, talk-track, per-Purchase-Type language):** Scripts 10e.
- **Who the customers are, ICA-to-FHL mapping, FHL writing guidance:** Section 2 of the master playbook (`02-ideal-client-profiles-avatars.md`). FHL shares the five FFG ICAs; Purchase Type is the operating overlay. This handbook names them and points back. It never redefines them.

The 18-month FHL lifecycle (welcome, repricing, valuations, annual review) is the retention playbook, not this. This handbook is only the cross-sell pieces layered on it. Read it once, then keep it open.

---

## The Client Journey

The cross-sell journey layered on the 18-month lifecycle. Most of it is the system. You act at the bold BROKER lines and whenever you hear a signal on any call. T-numbers match the pipeline below and the Developer Guide.

| When | T | What happens | Who |
|---|---|---|---|
| Day 0 | n/a | Home loan settles. Infynity export detects it. Purchase Type recorded. 18-month lifecycle starts. | System |
| Month 6 | T1 | **Half-Year Call.** You call. Proactive. All Purchase Types. Listen for an FFG need. | **YOU** |
| Month 6 | T2 | Voicemail if no answer. | **YOU** |
| Day 270 | T3 | Momentum Pack email sends. One of five, picked for their Purchase Type. | System |
| Day 273 | T4 | Pack companion SMS sends. | System |
| Day 270 +7 | T5 | Conditional follow-up SMS, only if they clicked but did not reply. | System |
| Month 12 | T6 | **Anniversary Call.** You call. Proactive. All Purchase Types. The old annual-review cross-sell question lives here now. | **YOU** |
| Month 12 | T7 | Voicemail if no answer. | **YOU** |

**Branches.** These fire any time, pull the card out, hand it on, then close:

| Branch | Fires when | What happens |
|---|---|---|
| Reactive Signal | You hear an FFG need on any lifecycle call (LC1 M1, LC3 M6, LC5 M12, LC7 M18) and log it | System confirms by SMS, fires Warm Handover |
| Warm Handover | `ffg_interest` set (pack click, your call outcome, or a reactive signal) | System creates an FFG broker task + intro email. FFG broker calls within 48h. You stay the home loans contact. |
| Interacting | Customer replies to any SMS or email | You action it same day. |

The system sends the pack and watches for clicks. You make two proactive calls and listen on every lifecycle call. The FFG broker takes any real cross-sell conversation.

---

## The Pipeline

The same overlay pipeline the system runs (full build in 07e). It sits on top of the 18-month lifecycle pipeline. You read a contact's cross-sell stage to know exactly where they are. This is the technical view of the journey above.

**Stage type:** ➡️ auto-added · ⚡️ moving here fires automation · 👤 manual, you action the task.

| # | Stage | Type | What it means |
|---|---|---|---|
| 1 | Interacting | ➡️ ⚡️ | Any inbound reply lands here. First thing you see. 24hr RED dot. Action, then FUP or a branch. |
| 2 | FUP | 👤 | You parked it with a scheduled follow-up. 24hr YELLOW dot when the task fires. |
| 3 | T1-T2 | 👤 | M6. Half-Year Call, voicemail if no answer. |
| 4 | T3-T5 | ⚡️ | M9. Momentum Pack email (Day 270), companion SMS (Day 273), conditional follow-up SMS (Day 7 after a click, no reply). |
| 5 | T6-T7 | 👤 | M12. Anniversary Call, voicemail if no answer. Folds the old annual-review question and the Month 12 pack retry. |
| B1 | Warm Handover | ⚡️ 👤 | `ffg_interest` set. Intro email auto. FFG broker call task. |
| B2 | Reactive Signal | 👤 | You hear an FFG need on a lifecycle call and log it. Feeds Warm Handover. |

A card sits in one stage at a time. Any inbound reply moves it to Interacting from wherever it is.

---

## Context You Already Have

Two pieces of context are not repeated here because they live in one place:

- **Purchase Type.** Every customer carries an active Purchase Type in `fhl_purchase_type_history`. The underlying human is one of the five FFG ICAs in **Section 2** (`02-ideal-client-profiles-avatars.md`); the ICA-to-FHL pathway mapping and FHL writing guidance live there too. Do not redefine the customer here. This is the operating quick-reference for which FFG product fits each Purchase Type:

  | Purchase Type | What FFG could help with |
  |---|---|
  | FHB | Car upgrade, furniture, solar, small renos, occasional consolidation |
  | NewPurchase | As FHB plus more reno funding, often a new family vehicle |
  | Refinance | Debt consolidation, refinance of an old car or personal loan, fund a planned purchase. Highest FFG conversion. |
  | Investor | Vehicle, equipment (if self-employed), business finance, investment-related personal loans |
  | Commercial | Commercial vehicle, equipment, business loan top-ups, EOFY asset purchases |

  If a call shows the type has changed (refinanced again, bought an investment), add the corrected value to `fhl_purchase_type_history`; it accumulates and the system picks up the new one.

- **What to say.** Every opener, voicemail, response script, and the per-Purchase-Type talk-track lives in **Scripts 10e**. This handbook tells you when to act and what to log. 10e tells you what to say.

---

## Your Moments

The manual stages from the journey, expanded. The words for each are in 10e.

### 1. Half-Year Call (Month 6, T1/T2)

Fixed. Every customer gets a proactive call at Month 6, all Purchase Types. Not a pitch. A relationship call where you also listen for an FFG-relevant need. Script and per-Purchase-Type questions in 10e.

**Before you call:** open the contact. Active Purchase Type, the loan, lifecycle context. 60 seconds.

**On the call:** if they mention a car, equipment, business finance, or a debt to tidy up, do not pitch. Use the bridge line (10e), then log it.

**Log the outcome** in `m6_call_outcome`: `Check-in`, `Future opp` (log the need + date), `Active opp`, `FFG referral` (add the matching FFG signal: `ffg_vehicle`, `ffg_equipment`, `ffg_business`, or `ffg_consolidation`), `Referral mentioned`, `No answer` (voicemail left, T2). Logging it adds `m6_call_done`. Skip it and the system cannot close the call out.

### 2. The Month 9 Momentum Pack (System-Driven)

The planned cross-sell. The system fires it at Day 270. You do nothing for the send. One of five packs by Purchase Type, a companion SMS at Day 273, one conditional follow-up SMS around Day 7 if they click but do not reply.

- If they click an FFG CTA, `ffg_interest` is set automatically, the Warm Handover fires, an FFG broker gets the task. No action from you.
- If they mention the pack on a lifecycle call, confirm and route (script in 10e), then add `ffg_interest`.
- If they ignore it, do not raise it unprompted. Let it work or not.

**Golden rule from Rowdie:** "Must NOT feel like lead generation. Must feel like: we prepared options based on what customers like you typically need next."

### 3. Reactive Lifecycle Signal (You Spot It, You Log It)

The opportunistic cross-sell. Any lifecycle call, any time. Most common at LC1 (M1), LC3 (M6), LC5 (M12), LC7 (M18).

| Customer says something like | Add this signal | Routes to |
|---|---|---|
| "Looking at a new car / ute / van" | `ffg_vehicle` | FFG vehicle broker |
| "Need a truck / equipment / new gear" | `ffg_equipment` | FFG commercial broker |
| "Thinking about expanding the business / premises / second business loan" | `ffg_business` | FFG commercial broker |
| "Want to consolidate the credit cards / personal loans" | `ffg_consolidation` | FFG consumer broker |
| Anything else FFG-relevant | General note for Rowdie review | Manual review |

Bridge line and the "not right now" / "send me an email" responses in 10e. If yes: add the signal on the call or right after. The system confirms by SMS, the FFG broker follows up within 48 hours (24 if urgent). If no: add `ffg_notinterested`; not re-pushed for 12 months; you stay the relationship.

### 4. Anniversary Call (Month 12, T6/T7)

Fixed. Folds in the old annual-review cross-sell question and the Month 12 retry for customers who did not engage with the M9 pack. One proactive call, all Purchase Types. Script in 10e.

**Before you call:** same prep as the Half-Year Call, plus check what came out of the Month 6 call (`m6_call_outcome`) and whether they engaged with the M9 pack. If not, this is the warm retry. The Annual Review is home loan strategy first; the cross-sell question is one part of the call, not the whole thing.

**Log the outcome** in `m12_call_outcome` (same options as the Half-Year Call). Logging it adds `m12_call_done`.

### 5. Warm Handover (Your Part Is Small)

When `ffg_interest` is set, the system creates an FFG broker task and sends the customer an intro email naming the FFG broker. The FFG broker calls within 48 hours (24 if hot).

**Your job:** stay the home loans contact. You introduce, you do not close. If they come back to you on the FFG side, point them to the FFG broker. **Hand-back rule:** if a customer in a handover wants to talk home loan instead, that is yours, take it; the FFG side pauses.

### 6. SMS Reply (Interacting)

The customer replied to an automated SMS. `cross_sell_signals` gained `sms_active`. The card moved to Interacting. The system paused SMS automation and sent a one-line acknowledgement only.

**SLA:** personal phone or SMS reply within 24 hours. Never auto-respond beyond the acknowledgement. Scripts in 10e. Once actioned, move the card to FUP with a dated task or into a branch.

---

## Rules

### Common Situations

| Situation | What you do |
|---|---|
| Already has a car / personal loan elsewhere | Do not push. Note it for Rowdie. Plant the seed: "When it comes up for refinance, we can run the numbers. No rush." |
| "I don't want any more loans" | Add `ffg_notinterested`. Suppressed 12 months. They stay in the FHL lifecycle. |
| Going through something difficult | Apply `FHL_Operations_Hold` tag. Every workflow checks it and exits. Never write "hardship", use "circumstances have changed". Operations decides re-entry. |
| Asks about refinancing their FFG loan through you | If it involves secured property or home-equity restructure, take it. Otherwise add `ffg_interest`; the FFG broker handles it. |
| FHL loan off-track (arrears, default risk) | Apply `FHL_Operations_Hold` tag. Operations takes over. No handover, no pack. Hold until resolved. |

### Red Dot Protocol

A Red Dot fires when an SLA is missed. Yellow = soft warning, task rises in your queue. Red = escalation to Rowdie and the broker manager.

| Task | Yellow at | Red at |
|---|---|---|
| Warm Handover → FFG broker call | 36 hours | 48 hours |
| Warm Handover marked hot (`ffg_hot`) | 12 hours | 24 hours |
| Half-Year Call task (T1) | 5 business days | 10 business days |
| Anniversary Call task (T6) | 5 business days | 10 business days |
| SMS reply (Interacting) | 18 hours | 24 hours |
| FUP on a customer-set callback date | 24h after the date | 48h after the date |

Most cross-sell tasks belong to the FFG team. If a Red fires on an FFG broker's Warm Handover, do not do their job; Rowdie sees the escalation and the FFG manager is on it. Cross-brand Red Dots show in your pipeline too so you can see it is handled. You still do not chase. Your own tasks (SMS reply, your calls, FUPs): action immediately, log the moment you finish. FUP SLA runs from the date you nominated; reschedule with a one-line note rather than let it expire.

### What Good Looks Like

1. Month 9 pack click rate 8%+ across all Purchase Types within 90 days of build live.
2. Reactive signals and call referrals fire 3-5 per month per FHL broker within 90 days.
3. Cross-sell to a settled FFG deal hits 12%+ of handovers within 6 months.
4. You log call outcomes 95%+ of the time. The system only learns from what you tell it.

### Not Covered Here

- The 18-month FHL lifecycle (welcome, valuations, repricing, annual review). Customer success / retention playbook.
- FHL pre-sales conversion and the fact-find call structure (pre-sales SDR playbook).
- UMI handovers from FHL (out of scope; UMI is narrative-only).

---

## Quick Reference

**Signals you log in `cross_sell_signals`** (a multi-select field, not a tag):

| What you see / do | The signal |
|---|---|
| Customer mentions a vehicle on a call | `ffg_vehicle` |
| Customer mentions equipment / gear | `ffg_equipment` |
| Customer mentions business expansion | `ffg_business` |
| Customer mentions debt consolidation | `ffg_consolidation` |
| Customer engages with the M9 pack | `ffg_interest` (system adds it on click) |
| Customer says "not interested" | `ffg_notinterested` (suppresses 12 months) |
| Customer asks about an FFG product on your call | `ffg_interest` (hand to FFG broker) |
| Half-Year Call done | Log `m6_call_outcome`. System adds `m6_call_done`. |
| Anniversary Call done | Log `m12_call_outcome`. System adds `m12_call_done`. |
| Inbound SMS reply | `sms_active`. Personal reply within 24h. |

**Tags (the only ones you ever apply):** `FHL_Unsubscribed` (take me off the list), `SMSOptOut` (stop texting, email fine), `FHL_Operations_Hold` (arrears / default / difficult). Everything else is a field.

---

*This is a draft handbook. Every script line referenced lives in 10e and is a starting point. FHL brokers refine the language in week one of live use. Lock the scripts after 30 days of real conversations.*
