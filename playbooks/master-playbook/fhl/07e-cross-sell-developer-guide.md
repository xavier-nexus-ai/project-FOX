# Cross-Sell Developer Guide (FHL)

**Playbook:** FHL Cross-Sell (FHL-as-origin → FFG)
**Brand folder:** playbooks/master-playbook/fhl/
**Direction:** FHL settled customer → FFG referral
**Version:** 2.0 DRAFT
**Created:** 2026-05-05
**Owner:** James
**Status:** DRAFT

---

## Purpose

The technical spec for building the FHL → FFG cross-sell engine in GoHighLevel. The reverse motion of the FFG → FHL playbook.

FHL customers are the same five ICAs as FFG (Section 2); only the purchase differs. They are deeper in the Fox relationship than a fresh FFG customer. Settling a home loan is a 12-week journey, not a 4-day one. They sit on an 18-month retention lifecycle, not a 12-month nurture spine. So FHL cross-sell is not a parallel email sequence. It is a small set of touchpoints layered on top of the lifecycle.

The 18-month FHL lifecycle itself (welcome, repricing, valuations, annual review) is the **customer success / retention playbook** (suffix `g`), not this document. This guide covers only the cross-sell touchpoints embedded in that lifecycle.

Companion documents:

- **Rep Handbook (08e):** what the FHL broker does when the engine surfaces a moment. Stage names and T-numbers match this guide exactly.
- **Scripts (10e):** every call opener, voicemail, and manual template. This guide points to 10e, it does not hold call copy.

This guide is for the GHL admin and the Njin build team. Not customer-facing.

---

## What This Engine Does

A settled FHL customer is tagged at settlement with one of five Purchase Types: First Home Buyer, New Purchase, Refinance, Investor, or Commercial. The 18-month retention lifecycle runs in parallel (retention playbook).

Cross-sell happens through a short T-spine layered on that lifecycle:

- **Month 6 Half-Year Call (T1/T2):** the FHL broker calls. Proactive. All Purchase Types. New and fixed.
- **Month 9 Momentum Pack (T3-T5):** the system sends one of five segmented packs, a companion SMS, and a conditional click follow-up.
- **Month 12 Anniversary Call (T6/T7):** the FHL broker calls. Proactive. All Purchase Types. Folds in the old annual-review cross-sell question and the Month 12 pack retry.

Plus two branches that can fire any time: a reactive signal the broker hears on a lifecycle call, and the Warm Handover that carries any interested customer across to an FFG broker.

---

## FHL to FFG Cross-Sell: The Whole Flow Explained

Read this first. It is the same picture the FHL broker reads in the handbook. It does not add anything new, it pulls the flow into one place.

### The Core Idea

There are only THREE ways an FHL customer crosses to FFG:

1. **The two fixed calls.** At Month 6 and Month 12 the FHL broker makes a proactive call. If a need surfaces, the broker tags it and an FFG broker takes it.
2. **The Month 9 pack.** The system sends one email pack built for the customer's situation. If they click, an FFG broker calls.
3. **The reactive signal.** On any lifecycle call across the 18 months, the broker hears a car, equipment, business, or debt-tidy need and tags it. An FFG broker calls.

Everything else (fields, scoring, Red Dots, de-dup) is plumbing that supports those three. The FHL broker never pitches FFG. They listen, they tag, the system routes.

### One Picture: The Whole Flow

```
                    FHL HOME LOAN SETTLES
                            |
        Infynity CSV export (weekly) detects settlement
                            |
   System sets fhl_settlement_date + adds Purchase Type to
   fhl_purchase_type_history + adds lifecycle_started signal
                            |
         18-month FHL retention lifecycle starts
                            |
   _________________________|_________________________
  |                  |                |               |
 M6 CALL         M9 PACK          M12 CALL        REACTIVE
 (T1/T2)         (T3-T5)          (T6/T7)         (any LC call)
 broker          system           broker          broker hears
 calls           sends pack       calls           a need, tags it
  |                  |                |               |
  |              waits 14 days        |               |
  |              for a click          |               |
  |              no click -> retry    |               |
  |              folded into M12      |               |
  |__________________|________________|_______________|
                            |
        Need surfaces (call) OR pack click OR signal tag
                            |
          System adds ffg_interest to cross_sell_signals
                            |
              WARM HANDOVER branch fires
                            |
   System creates a task for the right FFG broker queue
   System emails the customer: "expect a call"
                            |
            ===== SYSTEM STOPS. HUMAN STARTS. =====
                            |
        FFG broker calls within 48h (24h if hot)
                            |
        FFG broker logs the outcome in GHL
                            |
   _________________________|_________________________
  |            |               |                |
Applied   Booked Call    Not Interested     No Response
  |            |               |                |
Wait for   Stay in         Suppress 12      Retry at next
settlement handover         months           lifecycle point
  |
FFG loan settles
  |
ffg_converted signal. Customer is now multi-product Fox.
```

### The Flow as a Table

"System" means a GHL automation. "Human" names the Fox role.

| # | Step | Trigger | Owner | What happens | Customer sees | Timing / SLA | Guardrail |
|---|---|---|---|---|---|---|---|
| 1 | Settlement detected | Weekly Infynity CSV shows a settled loan in the last 7 days | System | `fhl_settlement_date` set. Purchase Type added to `fhl_purchase_type_history`. `lifecycle_started` added to `cross_sell_signals`. Raw figures dropped at import. | Nothing yet | Weekly | Sensitive financial snapshot never lands in GHL. |
| 2 | Lifecycle starts | Step 1 done | System | 18-month retention lifecycle begins (retention playbook). Cross-sell is only the touchpoints inside it. | Welcome from FHL broker | M1 onward | `FHL_Operations_Hold` tag pauses all cross-sell. |
| 3 | Half-Year Call (T1/T2) | M6 reached | Human: FHL broker | Broker calls. Proactive. Listens for an FFG need. No pitch. Logs `m6_call_outcome`. | A call from their broker | M6, soft SLA | If a need: tag the signal. If "not now": add `ffg_notinterested`, suppress 12 months. |
| 4 | Pack fires (T3) | `fhl_settlement_date` + 270 days (M9) | System | One of five packs picked from `fhl_purchase_type_history` and emailed. | An email built for their situation | Day 270 | FHL ACR 535038 + FFG ACL 382952 disclaimers. "General information only." |
| 5 | Companion SMS (T4) | Pack sent | System | Short SMS points back to the pack. | An SMS | Day 273 | STOP-to-unsubscribe on the SMS. |
| 6 | Pack wait + follow-up (T5) | Pack sent | System | 14-day click watch. If clicked at Day 7 with no reply, one conditional follow-up SMS. Opens ignored (iOS auto-opens). | Nothing unless they engage, then one SMS | Day 7 after click | One follow-up only. No recycling. |
| 7 | Anniversary Call (T6/T7) | M12 reached | Human: FHL broker | Broker calls. Proactive. The old annual-review cross-sell question lives here now. Logs `m12_call_outcome`. | A call from their broker | M12, soft SLA | Same guardrails as the Half-Year Call. |
| 8 | Reactive signal | Broker hears an FFG need on any lifecycle call | Human: FHL broker | Broker says the bridge line, adds the matching signal to `cross_sell_signals`. | A natural offer to have the asset team call. No pitch. | On the call | Captured in the customer's words. No pressure language. |
| 9 | Paths join | A pack click, a call outcome, or a reactive signal | System | `ffg_interest` added. Warm Handover branch starts. | Nothing yet | Immediate | One signal, one path forward. |
| 10 | Warm handover | `ffg_interest` present | System | GHL task routed to the right FFG broker queue. Intro email to the customer. | "Introducing [FFG broker]. Expect a call within the next business day." | Immediate | Customer is told who calls and roughly when. No surprise calls. |
| 11 | System stops, human starts | Task created | Human: FFG broker | FFG broker calls. FHL broker stays the home loans contact. | A call from the named FFG broker who has their file | 48h. 24h if `ffg_hot`. | A scope conversation, not a sell. |
| 12 | Outcome logged | Call done | Human: FFG broker | Logs Applied / Booked Call / Not Interested / No Response. | Depends on outcome | When the call ends | Not Interested: suppress 12 months. No Response: do not recycle. |
| 13 | Conversion | FFG loan settles (Ambition side) | System | `ffg_converted` added. Exits cross-sell. Multi-product Fox customer. | Their new FFG product, settled | When the FFG deal settles | De-dup on email. Never auto-merge on different emails. |

### The Safety Net (Red Dot Protocol)

Steps 11 and 12 are where a warm customer goes cold if nobody calls. The Red Dot Protocol watches the FFG broker's task: Yellow at 36h (12h if hot), Red at 48h (24h if hot). The FHL broker does not chase the FFG broker. Rowdie owns the escalation. Full table in Section 6.

### One Worked Example (End to End)

A refinance customer, Paige Beveridge their broker, loan settles in March.

1. **Settlement detected.** Weekly Infynity CSV shows it. System sets the settlement date, adds `Refinance` to `fhl_purchase_type_history`, adds `lifecycle_started`. Raw mortgage balance not imported.
2. **Lifecycle starts.** Paige does the Month 1 Welcome. No cross-sell yet.
3. **Month 6, the Half-Year Call (T1).** Paige calls. The customer mentions an old car loan still running at a worse rate. Paige does not pitch. She uses the bridge line, adds `ffg_consolidation` to `cross_sell_signals`, logs `m6_call_outcome = FFG referral`. The Warm Handover branch fires.
4. **System stops, human starts.** An FFG consumer broker calls within 48 hours, file in hand. Short scope call. Logs "Booked Call".
5. **The deal settles.** The customer refinances the car loan through FFG. System adds `ffg_converted`. Multi-product Fox customer. Relationship deeper, locked for the next refinance window.

**Same customer, the planned way instead.** Suppose nothing surfaced at Month 6. At Day 270 the system fires the Refi Savings Accelerator Pack (T3). The customer clicks the consolidation link two days later. System adds `ffg_interest`. From step 9 the flow is identical: warm handover, FFG broker call within 48h, outcome logged. If still nothing, the Month 12 Anniversary Call (T6) is the final proactive touch.

That is the whole flow. Three ways in, one path through, one safety net.

---

## 1. Pipeline Architecture: T-System (Overlay)

The cross-sell pipeline is a T-System overlay on the FHL Customer Lifecycle pipeline (which lives in the retention playbook). One contact, two pipelines, distinct dashboards. The cross-sell spine is short by design: two fixed calls, one pack, two branches.

### 1.1 Stage Type Legend

| Symbol | Meaning |
|---|---|
| ➡️ | Opportunities are automatically added here |
| ⚡️ | Moving a card here triggers an automation |
| ➡️ ⚡️ | Both auto-add and triggers on move |
| 👤 | Manual stage. The broker must action the task. |

### 1.2 T and N Prefixes, and the Stage Rule

- **T-series:** every cross-sell touchpoint. Each call is a T. Each voicemail is a T. Each email is a T. Each SMS is a T. Continuous numbering.
- The FHL cross-sell has no long automated nurture, so there is no N-series here. The 18-month nurture is the retention playbook, not this overlay.
- **Stage rule (two cuts):** a new stage begins when the touchpoint type changes (auto ⚡️ to manual 👤 or back) OR when the month changes. M6, M9, and M12 touchpoints never share a stage.

### 1.3 The FHL Cross-Sell Pipeline

| # | Stage | Type | Description |
|---|---|---|---|
| 1 | Interacting | ➡️ ⚡️ | Any inbound reply auto-moves the card here. First thing the broker sees. 24hr RED dot. Broker actions, then FUP or branch. |
| 2 | FUP | 👤 | Broker-parked card after we have responded. Scheduled follow-up. 24hr YELLOW dot. |
| 3 | T1-T2 | 👤 | M6. Half-Year Call (T1). Voicemail if no answer (T2). |
| 4 | T3-T5 | ⚡️ | M9. Momentum Pack email (T3, Day 270), companion SMS (T4, Day 273), conditional click follow-up SMS (T5, Day 7 after a click with no reply). |
| 5 | T6-T7 | 👤 | M12. Anniversary Call (T6). Voicemail if no answer (T7). Folds the old annual-review cross-sell question and the Month 12 pack retry. |

**Branch stages** (off the spine):

| # | Stage | Type | Description |
|---|---|---|---|
| B1 | Warm Handover | ⚡️ 👤 | `cross_sell_signals` gains `ffg_interest` (pack click, call outcome, or reactive signal). Intro email auto. FFG broker call task. |
| B2 | Reactive Signal | 👤 | FHL broker hears an FFG need on any lifecycle call (LC1 M1, LC3 M6, LC5 M12, LC7 M18) and tags it. Feeds Warm Handover. |

### 1.4 Interacting vs FUP

| Stage | Trigger | Meaning | Broker SLA |
|---|---|---|---|
| Interacting | Inbound reply detected | Their move was last. We act. | Same day. 24hr RED dot. |
| FUP | Broker replied and parked the card with a scheduled follow-up | Our move was last. GHL reminds us. | Task fires on the day. 24hr YELLOW dot. |

If the customer replies while in FUP, the card moves back to Interacting.

### 1.5 Why an Overlay, Not a Standalone

FHL customers are inside an active 18-month lifecycle. A standalone cross-sell pipeline would force the broker to manage two views of the same person. The overlay lets Bill, Paige, and Angel see the cross-sell stage as a column inside their lifecycle dashboard.

### 1.6 Auto-Advance Rule

Manual call stages (T1-T2, T6-T7) auto-advance when the broker logs `No Answer` or `Voicemail Left`. If the broker logs `Connected`, `Booked`, `Not Interested`, or `Referred`, the card does not auto-advance. The broker moves it per the disposition.

### 1.7 What Is NOT a Stage

- **Converted.** `cross_sell_signals` gains `ffg_converted` when an FFG loan settles. Exit event, not a stage.
- **Lost / Won.** GHL statuses. Mark Lost (`Not interested`, `Opted out`) per outcome.
- **The 18-month lifecycle.** That is the retention playbook, a separate pipeline.

### 1.8 Suppression and Unreachable Protocol

- **Opt-out.** Reply STOP applies `SMSOptOut` (Twilio). `FHL_Unsubscribed` = permanent global exclude.
- **Operations hold.** Arrears, default, or a difficult situation applies `FHL_Operations_Hold`. Every cross-sell workflow checks this tag on entry and exits if present. Operations decides re-entry.
- **Not interested.** `ffg_notinterested` suppresses cross-sell for 12 months. The customer stays in the FHL lifecycle as normal.
- **Unreachable.** After the Warm Handover follow-up sequence with no response, do not recycle. Mark the handover closed and let the next lifecycle touchpoint catch them.

---

## 2. Custom Fields

Fields first, tags only where GHL needs one. Signals and routing live in multi-select accumulators so the full history sits on the contact. Sensitive snapshot data (raw mortgage balance, raw card balances) is dropped at import.

### 2.1 Identity and Contact (existing GHL fields, mapped)

| GHL field | Source | Notes |
|---|---|---|
| First Name | Infynity | Personalisation |
| Last Name | Infynity | |
| Email | Infynity | Email channel |
| Phone | Infynity | SMS channel |

### 2.2 Purchase Type (multi-select accumulator)

Accumulates. The latest value is the active one. History is kept so a customer who refinances again keeps the prior type on record.

| Field name | Type | Values | Written by |
|---|---|---|---|
| `fhl_purchase_type_history` | Multi-select (accumulates) | FHB, NewPurchase, Refinance, Investor, Commercial, Unknown | Set at the FHL fact-find / settlement import. Adds a value if it changes later. |

The active Purchase Type = the latest value. Pack selection at M9 reads this. The underlying customer is one of the five shared ICAs; the Purchase Type definitions and the ICA-to-FHL pathway mapping live once in Section 2 of the master playbook (`02-ideal-client-profiles-avatars.md`). This guide does not redefine them.

### 2.3 Signal Accumulator (`cross_sell_signals`)

One multi-select field holds every behavioural and lifecycle signal. Values are added, never removed. This replaces the old Tag Library. Workflows trigger off "field contains value".

| Value | Added when | Effect |
|---|---|---|
| `lifecycle_started` | Settlement import runs | Cross-sell overlay begins |
| `pack_sent` | M9 Momentum Pack fires | Card to T3-T5 |
| `pack_clicked` | Customer clicks any FFG CTA in the pack | Counts toward `ffg_interest` |
| `ffg_interest` | Pack click, M6/M12 call outcome, or reactive signal | Fires Warm Handover (B1) |
| `ffg_hot` | FFG CTA clicked twice in 14 days, or explicit "I want to talk about a car/equipment/loan" | Warm Handover, urgent, 24h SLA |
| `ffg_vehicle` | Vehicle need (CTA click or broker tag) | Routes to FFG vehicle broker |
| `ffg_equipment` | Equipment need | Routes to FFG commercial broker |
| `ffg_business` | Business finance need | Routes to FFG commercial broker |
| `ffg_consolidation` | Debt consolidation need | Routes to FFG consumer broker |
| `ffg_personalloan` | Personal loan CTA click | Routes to FFG consumer broker |
| `ffg_notinterested` | Customer declines | Suppress retry 12 months |
| `ffg_converted` | FFG loan settles (Ambition push) | Exit cross-sell |
| `m6_call_done` | Broker logs the Half-Year Call outcome | Closes T1-T2 |
| `m12_call_done` | Broker logs the Anniversary Call outcome | Closes T6-T7 |
| `sms_active` | Inbound SMS reply | Card to Interacting. Broker personal reply, 24h. |

Behavioural triggers operate on link clicks, not opens. iOS Mail Privacy Protection auto-opens emails, so opens are reported but never used as a workflow signal.

### 2.4 Loan Detail Fields (custom)

| Field name | Type | Source | Used by |
|---|---|---|---|
| `loan_amount` | Currency | Infynity | Personalisation |
| `loan_lender` | Text | Infynity | Repricing context |
| `loan_rate` | Decimal | Infynity | Lifecycle repricing trigger (retention playbook) |
| `loan_product_type` | Single select (Fixed, Variable, Split, IO, OO) | Infynity | Lifecycle context |
| `fixed_rate_expiry_date` | Date | Infynity (if Fixed) | Lifecycle context |
| `property_type` | Single select (Owner Occupied, Investment, Commercial) | Infynity | Reinforces Purchase Type |
| `employment_type` | Single select (PAYG, Self-Employed) | Fact-find | Self-employed cross-sell flag |
| `household_type` | Single select (Single, Couple, Dependents) | Fact-find | Pack tone |
| `likely_next_needs` | Multi-select (Vehicle, Travel, Wedding, Reno/Solar, Debt Consolidation, Business Finance, Equipment) | Fact-find | Pack content emphasis |

### 2.5 Lifecycle Anchors (custom)

| Field name | Type | Source | Used by |
|---|---|---|---|
| `fhl_settlement_date` | Date | Infynity | Drives every workflow timer |
| `fhl_assigned_broker` | User reference | Infynity | Lifecycle + call task ownership |
| `cross_sell_pack_sent_at` | Date | Auto-set when M9 pack fires | Reporting |
| `cross_sell_pack_type` | Single select (mirrors active Purchase Type) | Auto-set | Reporting |
| `ffg_referred_at` | Date | Auto-set on `ffg_interest` | Reporting |
| `ffg_converted_at` | Date | Auto-set on FFG settlement | Reporting |
| `m6_call_outcome` | Single select (Check-in, Future opp, Active opp, FFG referral, Referral mentioned, No answer) | Broker logs at T1 | Reporting, branch routing |
| `m12_call_outcome` | Single select (same options as M6) | Broker logs at T6 | Reporting, branch routing |

### 2.6 UTM Tracking (opportunity + contact)

UTMs replace any single "last source" value. The opportunity holds one UTM trio for the touchpoint that opened it. The contact holds the original acquisition trio plus numbered slots for every later interaction, so we keep the full channel journey and never overwrite it.

**On the opportunity (single trio):**

| Field | Type | Holds |
|---|---|---|
| `utm_medium` | Text | Medium for the touchpoint that opened this cross-sell opportunity |
| `utm_source` | Text | Source for that touchpoint |
| `utm_campaign` | Text | Campaign for that touchpoint |

**On the contact (first touch + numbered slots):**

| Field | Holds | When written |
|---|---|---|
| `utm_1` | medium / source / campaign trio for the original acquisition touch (Infynity / fact-find) | Once, at contact create. Never overwritten. |
| `utm_2` | trio for the second distinct interaction (pack click, SMS reply) | When a second UTM-bearing event lands |
| `utm_3` | trio for the third interaction | Same |
| `utm_4` | trio for the fourth interaction | Same |
| `utm_5` | trio for the fifth interaction | Same. Sixth+ event rolls into `utm_5` (last touch wins). |

Slot 1 is the acquisition source. Slot 5 is the most recent touch. Anything in between is the journey.

Every automated email link carries `utm_medium=email&utm_source=ghl_crosssell_fhl&utm_campaign=momentum_{purchase_type}_{day}`. Each click writes the next empty contact slot (`utm_2` to `utm_5`); it never overwrites `utm_1`.

### 2.7 Consent

| Field name | Type | Notes |
|---|---|---|
| `sms_consent` | Boolean | Captured at FHL application. Checked before any SMS fires. |
| `email_consent` | Boolean | Captured at FHL application. |

### 2.8 Tags We Still Use (the only ones)

| Tag | Why it stays |
|---|---|
| `FHL_Settled` | Infynity integration fires this on settlement. Single entry trigger. |
| `SMSOptOut` | Twilio STOP handling writes a tag. Disables the SMS channel. |
| `FHL_Unsubscribed` | Permanent global suppression. No re-entry. |
| `FHL_Operations_Hold` | Arrears / default / difficult situation. Every workflow checks this tag on entry and exits if present. |

No other tags. Everything else is a field.

---

## 3. Workflows

### 3.1 Settlement Import and Entry

**Trigger:** Tag added, `FHL_Settled` (Infynity push). Guard: exit if `FHL_Operations_Hold` or `FHL_Unsubscribed`.

**Action:** set `fhl_settlement_date`. Derive Purchase Type, add it to `fhl_purchase_type_history`. Add `lifecycle_started` to `cross_sell_signals`. The retention lifecycle starts (retention playbook). The cross-sell overlay schedules the M6 call, the M9 pack, and the M12 call off `fhl_settlement_date`.

### 3.2 M6 Half-Year Call Workflow (NEW)

**Trigger:** `fhl_settlement_date` + 180 days (M6). Guard: skip if `FHL_Operations_Hold` or `FHL_Unsubscribed`.

**Action:**

1. Create a call task assigned to `fhl_assigned_broker`. Title: "Half-Year Call: {First} {Last}, {PurchaseType}, Month 6". Body: loan summary, lifecycle context, suggested talking points by Purchase Type.
2. T1 = the call. Script in 10e. No pitch. The broker listens for an FFG need.
3. T2 = voicemail if no answer. Script in 10e.
4. Broker logs `m6_call_outcome` and the system adds `m6_call_done`.

**Outcome routing:** `FFG referral` → add the matching FFG signal (`ffg_vehicle` / `ffg_equipment` / `ffg_business` / `ffg_consolidation`) and `ffg_interest`, fires B1. `Future opp` → dated FUP task. `Check-in` or `No answer` → no further cross-sell action until M9 pack.

This call is proactive, all Purchase Types. It replaces the old reactive-only treatment of the Month 6 lifecycle touch.

### 3.3 M9 Momentum Pack Workflow

**Trigger:** `fhl_settlement_date` + 270 days (M9). Same guards.

**Logic:**

```
Read latest fhl_purchase_type_history value:

  FHB         → send FHB Momentum Pack,         set cross_sell_pack_type = FHB
  NewPurchase → send New Home Momentum Pack,    set cross_sell_pack_type = NewPurchase
  Refinance   → send Refi Savings Accelerator,  set cross_sell_pack_type = Refinance
  Investor    → send Investor Strategy Pack,    set cross_sell_pack_type = Investor
  Commercial  → send Commercial Equip+Vehicle,  set cross_sell_pack_type = Commercial
  Unknown     → flag Rowdie, send generic intro (one-off)

Add pack_sent. Card to T3-T5.

T3 = pack email (Day 270).
T4 = companion SMS (Day 273).
WAIT 14 days, watch clicks:
  click any FFG CTA            → add pack_clicked + ffg_interest → B1
  click FFG CTA twice in 14d   → add ffg_hot → B1 urgent (24h)
  click but no reply by Day 7  → T5 conditional follow-up SMS
  zero clicks after 14 days    → no retry here. The M12 Anniversary Call is the retry.
```

The Month 9 pack no longer has its own separate Month 12 retry sequence. The fixed M12 Anniversary Call (3.4) is the retry.

### 3.4 M12 Anniversary Call Workflow (NEW)

**Trigger:** `fhl_settlement_date` + 365 days (M12). Same guards.

**Action:** identical structure to 3.2. Title: "Anniversary Call: {First} {Last}, {PurchaseType}, Month 12". T6 = call, T7 = voicemail (10e). Broker logs `m12_call_outcome`, system adds `m12_call_done`.

This call folds in two things that used to be separate: the annual-review cross-sell question, and the Month 12 retry of the pack for customers who did not engage at M9. One fixed call, all Purchase Types.

### 3.5 Reactive Lifecycle Signal (Branch B2)

**Trigger:** FHL broker adds a reactive signal to `cross_sell_signals` on any lifecycle call: `ffg_vehicle`, `ffg_equipment`, `ffg_business`, `ffg_consolidation`, or a general note for Rowdie review.

**Action:** system adds `ffg_interest`, fires a confirmation SMS (Copy Library), enters Warm Handover (3.6). The signal is the broker's judgement, not a system click. This is the primary opportunistic path. The M6 and M12 calls catch the planned moments. The reactive signal catches everything else.

### 3.6 Warm Handover Workflow (Branch B1)

> **Internal policy, Rowdie to resolve.** The GHL task and routing mechanics below are buildable as specified. The handoff *policy* is not. Who owns the customer relationship once FFG takes the conversation, when ownership formally transfers, how credit and commission are split across FHL and FFG, and who makes the call, are internal Fox decisions and still open. Build the plumbing. Do not treat the ownership model as locked until Rowdie signs it off. Tracked in Open Items.

**Trigger:** `cross_sell_signals` gains `ffg_interest` (pack click, M6/M12 call outcome, or reactive signal).

**Action:**

1. GHL task created, routed by signal:
   - `ffg_equipment` or `ffg_business` → FFG commercial broker queue
   - `ffg_vehicle` → FFG vehicle broker queue
   - `ffg_consolidation` or `ffg_personalloan` → FFG consumer broker queue
   - none specific → FFG general queue
2. Internal Slack/Teams notification if integrated.
3. Intro email to the customer (Copy Library): names the FFG broker, sets the expectation.
4. SLA: FFG broker calls within 48 hours (24 hours if `ffg_hot`).
5. FFG broker logs outcome: `Contacted`, `Booked Call`, `Applied`, `Not Interested`, `No Response`.

**Resume:** `Applied` → wait for Ambition settlement push, adds `ffg_converted`. `Not Interested` → add `ffg_notinterested`, suppress 12 months. `No Response` → close handover, next lifecycle touchpoint catches them. `Booked Call` → hold in Warm Handover until conversion confirmed.

The FHL broker stays the home loans contact throughout. The FFG broker owns the cross-sell conversation.

---

## 4. Data Flow: Infynity CSV → GHL

### 4.1 Import Process

Weekly CSV extract from Infynity (locked 27 April 2026 per cos.yaml). LMG aggregator switch under review. Privacy filter at the import layer. Raw sensitive values never land in GHL.

```
Infynity CSV (manual or scheduled export)
  ↓
Privacy filter script (Xavier) - drops sensitive financial snapshots
  ↓
GHL custom fields (upsert by email + last name)
  ↓
Settlement in last 7 days AND not already tagged → apply FHL_Settled
  ↓
Settlement Import and Entry (3.1) fires. Retention lifecycle starts.
M6, M9, M12 cross-sell touchpoints scheduled off fhl_settlement_date.
```

### 4.2 De-Dup with FFG Pipeline

If the contact already exists in the FFG cross-sell pipeline (an FFG customer who became an FHL customer), match on email and merge. They are multi-product Fox. They get FHL lifecycle priority; the FFG cross-sell spine pauses (they have already converted the other direction). De-dup key: email exact. Fallback: last name + phone last 4. Never auto-merge if email differs.

---

## 5. Lead Scoring (Light Layer)

GHL native scoring, surfaces FHL customers ready for an FFG conversation. Same logic as the FFG side for one consistent broker surface.

| Action | Score |
|---|---|
| Click on Momentum Pack | +10 |
| Click on FFG product CTA | +15 |
| SMS reply mentioning an FFG-relevant topic | +20 |
| Call note flagging an FFG signal | +25 (manual broker entry) |
| No engagement 14 days post pack | -5 |
| Unsubscribe | -100 |

**Threshold action:** score ≥ 25 in 30 days → FFG "Worth a call" queue. Score ≥ 40 → urgent FFG task.

---

## 6. Red Dot Protocol (GHL Implementation)

SLA escalation on FHL cross-sell tasks. Yellow is a soft warning in the broker's queue. Red is an external escalation to Rowdie and the broker manager. Same protocol as the FFG-side build for consistency.

### Task SLA Configuration

| Task type | Yellow | Red | Red action |
|---|---|---|---|
| Warm Handover task (FFG broker call) | 36h since created | 48h since created | Notify Rowdie + FFG broker manager |
| Warm Handover with `ffg_hot` | 12h since created | 24h since created | Notify Rowdie + FFG broker manager |
| Reactive signal handover task | 36h since created | 48h since created | Notify Rowdie + FFG broker manager |
| Half-Year Call task (T1) | 5 business days | 10 business days | Notify Rowdie |
| Anniversary Call task (T6) | 5 business days | 10 business days | Notify Rowdie |
| FHL broker SMS reply task (`sms_active`) | 18h since created | 24h since created | Notify Rowdie + FHL manager |
| FUP on customer-set callback date | 24h after the date | 48h after the date | Notify Rowdie |

The two proactive calls (T1, T6) get a softer clock than a Warm Handover. They are planned, not hot. They just must not silently expire.

### Implementation Pattern

Same as FFG side. Three parallel workflow branches on task creation:

```
Branch 1 (primary): wait until broker logs outcome → close task
Branch 2 (yellow):  wait Yellow_Trigger → if no outcome, set yellow, surface in queue
Branch 3 (red):     wait Red_Trigger → if no outcome, fire notification, set red
```

Xavier owns the build pattern. Shared between the FFG and FHL engines so brokers see one consistent SLA surface.

### Cross-Brand Visibility

Red Dots on cross-brand tasks (an FHL contact whose Warm Handover sits with an FFG broker) show in both pipelines so the FHL broker can see whether the FFG broker is on it. If the FFG broker silently lets it Red, the FHL broker is not left guessing. The FHL broker still does not chase. Rowdie owns the escalation.

### Reporting

Red Dot events feed the cross-sell dashboard. Monthly view: Red Dots per broker, per task type, per Purchase Type. Patterns show whether volume exceeds capacity (capacity) or specific brokers need coaching (discipline).

---

## 7. Dependencies and Open Items

| This document feeds into | What it provides |
|---|---|
| 08e Cross-Sell Handbook (FHL) | Stage names, T-numbers, signal definitions, broker moments |
| 10e Cross-Sell Scripts (FHL) | Call openers, voicemails, manual templates |
| 09 Customer Lifecycle (shared) | Cross-references the 18-month FHL lifecycle (retention playbook) |
| 11 KPIs (shared) | Reporting dashboard metrics |
| 14 Tech Stack (shared) | GHL build spec, FHL side |

| This document depends on | Status |
|---|---|
| Tone of Voice gate | PASSED 2026-03-05 |
| FHL 18-month lifecycle plan (Rowdie) | RECEIVED 2026-03-06 (cos.yaml fhl_customer_lifecycle) |
| FHL Purchase Type schema | Locked. Section 2 records the shared ICAs and the ICA-to-FHL mapping. No separate FHL framework needed. |
| Privacy filter | PENDING |
| GHL sub-account access | Provisioned, awaiting Project Plan v1 approval |
| Infynity CSV export cadence | PENDING |
| Broker handoff ownership policy | OPEN, Rowdie to resolve. Task + routing mechanics buildable. Relationship ownership across FHL/FFG, transfer point, credit/commission split, who calls = internal Fox policy, not locked. |

---

## Out of Scope

- **18-month FHL lifecycle build** (welcome, valuations, repricing, annual review). Retention / customer success playbook (suffix `g`).
- **Equity Release / Top-Up offers.** Stay inside the FHL lifecycle as a retention motion, not surfaced as cross-sell.
- **UMI handover from FHL.** Not in current scope. UMI is narrative-only.

---

*This is a draft technical specification. Every workflow and field listed here is a proposal until the Purchase Type derivation logic and FFG broker routing are locked.*

---

# Copy Library - Automated Emails and SMS

All system-fired touchpoints, labelled by T-number to match Section 1. This is what Xavier loads into GHL as templates.

Phone call scripts and voicemails (T1/T2 Half-Year Call, T6/T7 Anniversary Call) live in 10e. Manual broker SMS and follow-up emails live in the handbook (08e).

## Defaults (All Automated Emails)

- **Sender name:** The Fox Home Loans Team
- **Reply-to:** captured into the GHL contact record
- **First-name token:** `{{contact.first_name}}`
- **Length:** 250-400 words for value emails. Under 150 for SMS-companion emails.
- **Format:** HTML with plain text fallback. Single column. One image max. One primary CTA.
- **Send time:** Tuesday-Thursday, 8-10am AEST. Default Wednesday 8:30am.
- **Footer:** standard FHL ACR 535038 disclaimer. Unsubscribe link. FFG ACL 382952 disclaimer when FFG content is included.
- **Voice:** Australian English. Third-grade reading level. No "advice", "guarantee", "financial hardship". No em dashes.

## Defaults (All Automated SMS)

- **Length:** under 160 characters. Never more than 320.
- **Sign-off:** `The Fox Team`
- **Send time:** 12pm-2pm AEST midweek. Never before 9am, never after 8pm.
- **Frequency cap:** maximum 1 SMS per active month per contact (FHL customers tolerate fewer SMS than FFG).
- **Opt-out:** `Reply STOP to unsubscribe` in the first SMS of every sequence.

UTM tags on every link: `?utm_source=ghl&utm_medium=email&utm_campaign=fhl_xsell_{purchase_type}_{day}`

**T-number reference:** T1/T2 = M6 Half-Year Call + voicemail (voice, 10e). T3 = M9 Momentum Pack email (Day 270). T4 = pack companion SMS (Day 273). T5 = conditional pack click follow-up SMS (Day 7 after click, no reply). T6/T7 = M12 Anniversary Call + voicemail (voice, 10e). The pack body varies by Purchase Type. Everything else is common.

---

## T1/T2 - Month 6: Half-Year Call + Voicemail (BROKER)

Voice. Script in 10e. The system has created the broker task with talking points by Purchase Type. Proactive, no pitch, listen for an FFG need. After the call the broker logs `m6_call_outcome` and the system adds `m6_call_done`. If a need surfaces, the broker adds the matching FFG signal and the Warm Handover branch fires.

---

## T3 - Month 9 Momentum Pack Email (Day 270)

One of five, picked from the latest `fhl_purchase_type_history` value.

### 1. First Home Buyer Momentum Pack

**Trigger:** active Purchase Type = FHB AND Day 270 reached.
**Tone:** warm, genuine. They just bought their first home. They are still nervous.

**Subject:** {{contact.first_name}}, the next 12 months in your new home

```
Hey {{contact.first_name}},

You've been in the new place about nine months now. Hopefully it feels like home. The boxes are unpacked, the furniture's in the right rooms, and the repayments are part of the rhythm.

Quick check-in. Most first home buyers we look after end up needing one or two of these things in the first 18 months:

✓ A second car or upgrading the existing one (new commute, growing family)
✓ Furniture to fill the rooms that are still echoey
✓ Solar to take the edge off the power bill
✓ A small reno (kitchen tidy, deck, paint job)
✓ Cleaning up an old credit card or personal loan that didn't get sorted before settlement

If any of that's on your list (or coming soon), our asset finance team at Fox Finance Group handles it day to day. Same group, same approach, same standards we use on the home loan side.

You don't need to do anything right now. We just wanted you to know the option's there. If you want a quick chat about any of it, reply to this email and we'll have someone call you.

Cheers,
The Fox Home Loans Team

Fox Finance Group is an Australian Credit Licensee (ACL 382952). Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### 2. New Home Momentum Pack

**Trigger:** active Purchase Type = NewPurchase AND Day 270.
**Tone:** practical, momentum-led.

**Subject:** {{contact.first_name}}, planning any home upgrades or purchases this year?

```
Hey {{contact.first_name}},

Nine months into the new place. By now you've probably found the things you want to change, the rooms that need work, and the next vehicle you've been thinking about.

A lot of our customers in your spot end up sorting out one or more of these in the first year:

✓ Car upgrade (new commute, family-sized vehicle, end-of-lease swap)
✓ Furniture or appliances for the rooms that are still half-empty
✓ Solar or home upgrades (battery, hot water, ducted air)
✓ A small reno (kitchen, bathroom, deck, paint)
✓ Folding old debts (credit cards, leftover loans) into something cleaner now that the home loan's settled

Our asset finance team handles all of that under Fox Finance Group. Same group as your home loan, same standards.

If you want to talk through any of it, reply to this email and we'll have a chat about what fits. No commitment, no pressure.

Cheers,
The Fox Home Loans Team

Fox Finance Group is an Australian Credit Licensee (ACL 382952). Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### 3. Refi Savings Accelerator Pack

**Trigger:** active Purchase Type = Refinance AND Day 270.
**Tone:** practical, money-led. Refinancers are the highest-conversion FFG cross-sell segment.

**Subject:** {{contact.first_name}}, turn your refinance into extra breathing room

```
Hey {{contact.first_name}},

You refinanced about nine months ago. The repayments dropped, the cash flow's better, and life is hopefully a bit easier.

Here's the question worth asking now: what's that extra money doing?

A lot of our refinance customers use the breathing room to clean up other debt that didn't get included in the refinance. Things like:

✓ Old credit card balances rolling at high rates that could fold into something cheaper
✓ A personal loan from years ago at a worse rate than today's market
✓ A car loan that's nearly paid off but still costing more than it should
✓ Buy-now-pay-later balances that have crept up

Our asset finance team at Fox Finance Group can run the numbers on consolidating any or all of it. The goal is the same as your refinance: less interest, simpler structure, more breathing room.

If that's worth a 15-minute conversation, reply to this email and we'll set it up. No commitment, no pressure.

Cheers,
The Fox Home Loans Team

Fox Finance Group is an Australian Credit Licensee (ACL 382952). Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### 4. Investor Strategy Pack

**Trigger:** active Purchase Type = Investor AND Day 270.
**Tone:** peer-to-peer, sophisticated, short.

**Subject:** {{contact.first_name}}, how to fund the next move without boxing in future goals

```
Hey {{contact.first_name}},

Quick one for the property side of your portfolio.

Nine months in, you've got the new property bedded down. The next 12 months is usually where investors decide how to position for the move after that. A few common moves we see:

✓ Vehicle finance structured outside the home loan (preserves borrowing power)
✓ Equipment finance if you run a business or contracting work
✓ Business loan top-ups for the operating entity
✓ Consolidating any existing personal-side debt into a cleaner structure
✓ Renovation or value-add funding on an existing property

All of it sits under Fox Finance Group's asset and commercial finance team. Same group, separate from your home loan, structured to keep your residential borrowing capacity clear for the next purchase.

If any of that's on your radar, reply to this email. Happy to run through timing for the next 12 months and what your options look like.

Cheers,
The Fox Home Loans Team

Fox Finance Group is an Australian Credit Licensee (ACL 382952). Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### 5. Commercial Equipment and Vehicle Pack

**Trigger:** active Purchase Type = Commercial AND Day 270.
**Tone:** business-to-business, practical, no fluff.

**Subject:** {{contact.first_name}}, while we're sorted on the property side

```
Hey {{contact.first_name}},

Nine months in on the commercial property settlement. The premises are running, the loan's settled, the cash flow's adjusted.

Quick one on the rest of the business finance picture.

Most of our commercial property customers also have one or more of these running:

✓ Commercial vehicle (ute, van, truck) due for replacement in the next 12-24 months
✓ Equipment finance on key business assets
✓ Plant or machinery purchases on the EOFY radar
✓ Cash flow facilities or business loan top-ups for growth

Our asset and commercial finance team at Fox Finance Group handles every one of those. Same group, separate from your commercial property loan, same standards.

EOFY's the natural moment for most of this. If you want to walk through the equipment plan for the next 12 months, reply to this email. We can also line up finance options early so you can move fast when the right unit comes up.

Cheers,
The Fox Home Loans Team

Fox Finance Group is an Australian Credit Licensee (ACL 382952). Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

---

## T4 - Pack Companion SMS (Day 273)

One per Purchase Type, fired three days after the pack.

**FHB:**
```
Hey {{contact.first_name}}, sent you a note about how Fox can help with the next 12 months in your new home. Worth a read when you have 2 mins: [link]
The Fox Team
Reply STOP to unsubscribe.
```

**New Purchase:**
```
Hey {{contact.first_name}}, our asset finance team can help with the upgrades on the to-do list. Worth a read: [link]
The Fox Team
Reply STOP to unsubscribe.
```

**Refinance:**
```
Hey {{contact.first_name}}, your refinance freed up cash flow. Worth a quick read on what to do with it: [link]
The Fox Team
Reply STOP to unsubscribe.
```

**Investor:**
```
Hey {{contact.first_name}}, sent you something on funding the next move without boxing in future goals: [link]
The Fox Team
Reply STOP to unsubscribe.
```

**Commercial:**
```
Hey {{contact.first_name}}, EOFY's coming. Quick read on the rest of the business finance picture: [link]
The Fox Team
Reply STOP to unsubscribe.
```

---

## T5 - Pack Click Follow-Up SMS (Day 7 After Click, No Reply)

Conditional. Fires only if the customer clicked a pack CTA but has not replied within 7 days. The FFG broker should have called before this lands. This is a backup.

**FHB / New Purchase:**
```
Hey {{contact.first_name}}, our team saw you'd had a look at the asset finance options. We'll give you a quick call this week, ok?
The Fox Team
```

**Refinance:**
```
Hey {{contact.first_name}}, our team saw you'd had a look at the consolidation options. Worth 15 mins to run the numbers. We'll book a time, ok?
The Fox Team
```

**Investor / Commercial:**
```
Hey {{contact.first_name}}, our team saw you'd had a look at the asset and commercial finance options. We'll sort a time to walk through the next 12 months, ok?
The Fox Team
```

---

## T6/T7 - Month 12: Anniversary Call + Voicemail (BROKER)

Voice. Script in 10e. System-created broker task. This call folds in the old annual-review cross-sell question and the Month 12 retry of the pack for customers who did not engage at M9. Proactive, all Purchase Types. After the call the broker logs `m12_call_outcome` and the system adds `m12_call_done`. If a need surfaces, add the matching FFG signal and the Warm Handover branch fires.

---

## Warm Handover - Customer Introduction Email

Auto-sends when `cross_sell_signals` gains `ffg_interest` (pack click, M6/M12 call outcome, or reactive signal).

**Subject:** Quick intro, {{contact.first_name}}

```
Hey {{contact.first_name}},

Wanted to quickly introduce {{ffg_broker_first_name}} from our asset finance side at Fox Finance Group. They handle [vehicle / equipment / personal loan / commercial finance] for our home loan customers.

Expect a call from {{ffg_broker_first_name}} within the next business day. They'll have your file already, so it's a short call to scope what you're after.

I'll stay your home loans contact for anything property-side. If anything comes up, ring me direct.

Cheers,
{{fhl_broker_first_name}}
Fox Home Loans

Fox Finance Group is an Australian Credit Licensee (ACL 382952). Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

---

## Reactive Lifecycle SMS (System-Fired After a Manual Broker Signal)

Fires immediately after the FHL broker adds a reactive signal to `cross_sell_signals` on a lifecycle call.

**Vehicle (`ffg_vehicle`):**
```
Hey {{contact.first_name}}, as discussed, our asset finance team will give you a call about the {{vehicle_topic}} in the next day or two. Same group as Fox Home Loans.
The Fox Team
Reply STOP to unsubscribe.
```

**Equipment / Business (`ffg_equipment` / `ffg_business`):**
```
Hey {{contact.first_name}}, our commercial finance team will give you a buzz about the {{equipment_topic}} in the next day or two. Same group as Fox Home Loans.
The Fox Team
Reply STOP to unsubscribe.
```

**Consolidation (`ffg_consolidation`):**
```
Hey {{contact.first_name}}, our asset finance team will give you a call about consolidating things in the next day or two. Worth 15 minutes.
The Fox Team
Reply STOP to unsubscribe.
```

**General (fallback):**
```
Hey {{contact.first_name}}, as discussed on our call, our asset finance team will be in touch in the next day or two.
The Fox Team
Reply STOP to unsubscribe.
```

---

*This is a draft technical specification. Every workflow and field listed here is a proposal until the Purchase Type derivation logic and FFG broker routing are locked.*
