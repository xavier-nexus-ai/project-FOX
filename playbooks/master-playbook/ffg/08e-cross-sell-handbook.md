# Cross-Sell Rep Handbook (FFG)

**Playbook:** FFG Cross-Sell (FFG-as-origin → FHL)
**Brand folder:** playbooks/master-playbook/ffg/
**Direction:** FFG settled customer → FHL referral
**Version:** 2.0 DRAFT
**Created:** 2026-05-05
**Owner:** James
**Status:** DRAFT

---

## Purpose

What you do when the cross-sell engine hands you a human. The system runs the journey: it sends every email and SMS and watches what the customer does. It only taps you when there is a real conversation to have. The customer arrives warm. You land the conversation, you do not start the relationship from scratch.

Where the rest lives, do not relearn it here:

- **Pipeline + build detail:** Developer Guide 07e. The pipeline below matches it exactly.
- **What to say (openers, voicemails, talk-track, per-ICA language):** Scripts 10e.
- **Who the ICAs are:** Section 2 of the master playbook (`02-ideal-client-profiles-avatars.md`).

Read this once cover to cover. Then keep it open in another tab.

---

## The Client Journey

The whole 12-month journey for every settled FFG customer. Most of it is automated. You act only at the bold BROKER lines and the branches. Read it so you know what the customer has already had before you pick up the phone. T-numbers match the pipeline below and the Developer Guide.

| When | T | What happens | Who |
|---|---|---|---|
| Day 0 | n/a | Loan settles. Ambition pushes it to GHL. ICA derived. Customer enters the pipeline. | System |
| Day 0 | n/a | **At-settlement seed call.** You ask the FHL purchase-type question on the standard settlement call. | **YOU** |
| Day 3 | T1 | Welcome + review email sends. | System |
| Day 7 | T2 | Check-in SMS sends. | System |
| Day 30 | T3 | Value-drop email sends (varies by ICA). | System |
| Day 90 | T4 | Q1 milestone email sends. | System |
| Day 92 | T5 | Q1 SMS sends. | System |
| Day 180 | T6 | Halfway email sends. Carries the first FHL seed. | System |
| Day 183 | T7 | Halfway SMS sends. | System |
| Month 6 | T8 | **Half-Year Call.** You call. Proactive. All customers. | **YOU** |
| Month 6 | T9 | Voicemail if no answer. | **YOU** |
| Day 270 | T10 | FHL warm-up email sends. | System |
| Day 273 | T11 | FHL warm-up SMS sends. | System |
| Day 365 | T12 | Anniversary email sends. | System |
| Day 365 | T13 | Anniversary SMS sends. | System |
| Month 12 | T14 | **Anniversary Call.** You call. Proactive. All customers. | **YOU** |
| Month 12 | T15 | Voicemail if no answer. | **YOU** |
| Day 365+ | N16 | Win-back email 1 (only if no engagement). | System |
| Day 365+30 | N17 | Win-back email 2 (only if no engagement). | System |

**Branches.** These fire any time the customer does something, pull the card out of the spine, hand it to you, then put it back:

| Branch | Fires when | What you do |
|---|---|---|
| Hot Lead | Customer clicks an FFG product CTA, Month 6+ | Call within 24h. See Your Moments. |
| FHL Referral | Customer clicks FHL content twice | FHL team calls within 48h. You are the introducer. |
| Interacting | Customer replies to any SMS or email | Action it same day. |

The system does the steady work. You do the four to six moments where a human matters.

---

## The Pipeline

The same pipeline the system runs (full build in 07e). You read a contact's stage to know exactly where they are in the journey. This is the technical view of the journey above.

**Stage type:** ➡️ auto-added · ⚡️ moving here fires automation · 👤 manual, you action the task.

| # | Stage | Type | What it means |
|---|---|---|---|
| 1 | Interacting | ➡️ ⚡️ | Any inbound reply lands here. First thing you see. 24hr RED dot. Action, then move to FUP or a branch. |
| 2 | FUP | 👤 | You parked it with a scheduled follow-up. 24hr YELLOW dot when the task fires. |
| 3 | T1-T2 | ⚡️ | M0. Day 3 welcome email, Day 7 check-in SMS. |
| 4 | T3 | ⚡️ | M1. Day 30 value-drop email. |
| 5 | T4-T5 | ⚡️ | M3. Day 90 Q1 email, Day 92 Q1 SMS. |
| 6 | T6-T7 | ⚡️ | M6. Day 180 halfway email + FHL seed, Day 183 SMS. |
| 7 | T8-T9 | 👤 | M6. Half-Year Call, voicemail if no answer. |
| 8 | T10-T11 | ⚡️ | M9. Day 270 FHL warm-up email, Day 273 SMS. |
| 9 | T12-T13 | ⚡️ | M12. Day 365 anniversary email, SMS. |
| 10 | T14-T15 | 👤 | M12. Anniversary Call, voicemail if no answer. |
| 11 | N16-N17 | ⚡️ | M12+. Win-back emails (only if no engagement). |
| B1 | Hot Lead | 👤 | FFG product CTA clicked M6+. Your call, 24h. Returns to the spine after. |
| B2 | FHL Referral | ⚡️ 👤 | FHL content clicked twice. 3-email FHL intro fires, FHL broker handover. |

A card sits in one stage at a time. Any inbound reply moves it to Interacting from wherever it is.

---

## Context You Already Have

Two pieces of context are not repeated in this handbook because they live in one place:

- **ICA.** Every contact carries an active ICA in `ica_history`. Full ICA detail (who they are, what they value, FHL pathway, return-loan signal) is **Section 2 of the master playbook**. Do not relearn it here. PCLRB is the highest-value ICA, prioritise them on the Half-Year and Anniversary calls. If a call shows the ICA is wrong, add the corrected value to `ica_history`; it accumulates and the system picks up the new one.
- **What to say.** Every opener, voicemail, response script, and the per-ICA talk-track lives in **Scripts 10e**. This handbook tells you when to act and what to log. 10e tells you what to say.

---

## Your Moments

The manual stages from the journey, expanded. This is your actual job. The words for each are in 10e.

### 1. At-Settlement Seed (Settlement Day)

Your first chance to plant the FHL flag. You are not selling FHL. You are identifying purchase type so the system can send the right FHL content at Day 180 and Day 270.

**When:** the settlement call you already make today, after the standard FFG settlement wrap-up. Script in 10e.

**What to log** in `fhl_purchase_type_history`:

| They say | Log this value |
|---|---|
| "I own one." (owner-occupied) | `Refinance` |
| "I own a few." | `Investor` |
| "I rent." / "I'm with parents." | `FHB` |
| "I'm thinking about buying." | `NewPurchase`. Also add `fhl_interest` to `cross_sell_signals` now. |

For BAB: also ask whether they own or lease their business premises. Log `Commercial` or `NewPurchase`.

Adding `fhl_interest` fires the FHL Referral branch. An FHL broker task lands within the hour.

**Why it matters:** without your purchase-type log the system guesses which FHL content to send. With it, Day 180 and Day 270 are right for them.

### 2. Half-Year Call (Month 6, T8/T9)

Fixed. Every engaged customer gets a proactive call at Month 6, after the Day 180 email and SMS have landed. Script and per-ICA questions in 10e.

**Before you call:** open the contact. Active ICA, the loan, recent clicks, FHL-seeded or not. 90 seconds. It changes the call.

**The goal is not to close.** It is to surface the next opportunity and be the broker who called when nothing was wrong.

**Log the outcome** in `m6_call_outcome`: `Check-in`, `Future opp` (log the need + a date), `Active opp`, `FHL referral` (add `fhl_interest`), `Referral mentioned`, `No answer` (voicemail left, T9). Logging it adds `m6_call_done`. Skip it and the system cannot move the card on.

### 3. Hot Lead Branch Fired

`cross_sell_signals` gained `hot_lead`. The customer clicked an FFG product CTA at Month 6+. The system paused their journey 14 days. Your move.

**SLA:** call within 24 hours. Cooling drops conversion fast.

**Before you call:** open the contact. Loan, active ICA, which CTA they clicked, FHL purchase type, recent SMS. 90 seconds. Opener and voicemail in 10e.

**Route on what they tell you:**

| Their answer | What to do |
|---|---|
| "Thinking about a new car / consolidating / upgrading equipment." | Discovery on the new need. Standard FFG sales script. Warm pre-approval. |
| "Just having a look." | "Fair enough, what got you looking?" Listen. Log a 30-day FUP. |
| "Actually I was looking at home loans." | Add `fhl_interest`. Hand to FHL. Stay the introducer. |
| "Not interested, please stop." | Apply the `FFG_Unsubscribed` tag. Log the reason. |

**Log the outcome** in the pipeline note: `Contacted`, `Booked Call`, `Applied`, `Not Interested`, `No Response`. Manual Hot Lead SMS in 10e if you cannot reach them.

### 4. FHL Referral Branch Fired

`cross_sell_signals` gained `fhl_interest`. The customer clicked FHL content twice. The 3-email FHL Referral sub-sequence is running. An FHL broker task has landed.

**SLA:** FHL broker calls within 48 hours. The emails are the safety net, the call is the conversion.

**Who calls:** the FHL team owns this. The FFG broker is the introducer, not the closer. Routing and voicemail in 10e.

**Hand-back rule:** if they say "actually I want to talk about my car loan," add `hot_lead` and hand to the FFG broker. Never push someone toward a product they have signalled away from.

### 5. SMS Reply (Interacting)

The customer replied to an automated SMS. `cross_sell_signals` gained `sms_active`. The card moved to Interacting. The system paused SMS automation and sent a one-line acknowledgement only.

**SLA:** personal phone or SMS reply within 24 hours. An SMS reply is the highest-intent signal in this system. Treat it like a missed phone call.

**The rule:** never auto-respond beyond the system acknowledgement. The reply comes from you. Response scripts in 10e. Once actioned, move the card to FUP with a dated task or into a branch.

### 6. Anniversary Call (Month 12, T14/T15)

Fixed. Folds in the old loose "9-12 month" call and the annual review. Every customer gets one proactive call at Month 12, after the Day 365 email and SMS have landed. Script in 10e. For PCLRB and BAB this is the proper annual review. For PVB with a balloon it is the balloon-planning call.

**Before you call:** same 90-second prep, plus check what came out of the Month 6 call (`m6_call_outcome`) and pick up there.

**Log the outcome** in `m12_call_outcome` (same options as the Half-Year Call). Logging it adds `m12_call_done`. After this call, if nothing is live, the system moves the customer into win-back. This is the last proactive human touch in year one. Make it count.

---

## Rules

### Refer-A-Friend

The Day 3 email mentions refer-a-friend with the $100 Eftpos card. When live, the system adds `referral_given` when a referred friend submits a unique link. The referral-link and Eftpos mechanism is still being finalised (07e Open Items). Until confirmed live, log referrals manually and do not promise an automated card timeline.

When a customer refers: thank-you SMS or call within 24 hours; note the referrer in GHL; reference it next time ("how are they finding the loan?"). When a referred friend lands: their record links to the referrer; the first call references them ("[referrer] sent you my way"); after settlement the referrer gets the thank-you. Templates in 10e.

### Common Situations

| Situation | What you do |
|---|---|
| "Take me off the list" | Apply `FFG_Unsubscribed` tag. No re-entry. Note the reason. Confirmation SMS within an hour (10e). |
| "Stop texting, email is fine" | Apply `SMSOptOut` tag only. They stay in the email sequence. |
| A question the system can't answer | Answer it yourself. Never redirect to a portal or form. The human moments must feel personal. |
| Situation changed (job, divorce, difficult) | Update GHL fields. Never write "hardship", use "circumstances have changed". If serious, see below. |
| Loan defaulted or in arrears | Apply `FFG_Operations_Hold` tag. Every workflow checks it and exits. Operations decides re-entry. |
| Booked an FHL call, then asks about a car loan | Answer it. Add `hot_lead`. Hand to the FFG broker. FHL conversation continues in parallel. |

### Red Dot Protocol

A Red Dot fires when an SLA is missed. Yellow = soft warning, task rises to the top of your queue. Red = escalation to Rowdie and the broker manager, visible above your head until closed.

| Task | Yellow at | Red at |
|---|---|---|
| Hot Lead branch → broker call | 18 hours | 24 hours |
| FHL Referral branch → FHL broker call | 36 hours | 48 hours |
| SMS reply (Interacting) → broker reply | 18 hours | 24 hours |
| Half-Year Call task (T8) | 5 business days | 10 business days |
| Anniversary Call task (T14) | 5 business days | 10 business days |
| FUP on a customer-set callback date | 24h after the date | 48h after the date |

The two proactive calls get a softer clock than a Hot Lead. They are planned, not hot. They just must not silently expire. FUP SLA runs from the date you nominated, not the date you logged it. Reschedule with a one-line note rather than let it expire. Repeated roll-overs are a capacity issue, flag it to your manager.

### What Good Looks Like

1. Hot Lead → second loan rate hits 30%+ within 90 days of build live (the pre-existing FFG repeat benchmark, matched with less of your time).
2. FHL referrals fire 5-10 per month minimum within 90 days (currently zero from automation).
3. Your Half-Year and Anniversary call lists are warm conversations, not cold ones.
4. You log call outcomes 95%+ of the time. The system only learns from what you tell it.

### Not Covered Here

- The FFG sales process for new lead conversion (Pre-Sales SDR Playbook + FFG sales scripts).
- The FHL 18-month lifecycle for FHL-originated customers (customer success playbook).
- UMI cross-sell (out of scope; UMI broker-referred clients cannot be cross-sold).
- Insurance cross-sell at loan packaging (Insurance Introduction Call script in FFG sales scripts).

---

## Quick Reference

**Signals you log in `cross_sell_signals`** (a multi-select field, not a tag):

| What you see / do | The signal |
|---|---|
| Hot Lead task lands | `hot_lead`. Call within 24h. Log outcome. |
| FHL Referral task lands (FHL team) | `fhl_interest`. FHL broker calls within 48h. You introduce only. |
| Inbound SMS reply | `sms_active`. Personal reply within 24h. Never auto. |
| You surface an FHL need on a call | Add `fhl_interest`. Hand to FHL. |
| Customer refers a friend | `referral_given`. Thank-you within 24h (log manually until mechanism live). |
| Half-Year Call done | Log `m6_call_outcome`. System adds `m6_call_done`. |
| Anniversary Call done | Log `m12_call_outcome`. System adds `m12_call_done`. |
| Customer goes quiet | `dormant`. No action. System handles re-engagement. |

**Tags (the only ones you ever apply):** `FFG_Unsubscribed` (take me off the list), `SMSOptOut` (stop texting, email fine), `FFG_Operations_Hold` (arrears / default / difficult). Everything else is a field.

---

*This is a draft handbook. Every script line referenced lives in 10e and is a starting point. Brokers refine the language in week one of live use. Lock the scripts after 30 days of real conversations.*
