# Cross-Sell Developer Guide (FFG)

**Playbook:** FFG Cross-Sell (FFG-as-origin → FHL)
**Brand folder:** playbooks/master-playbook/ffg/
**Direction:** FFG settled customer → FHL referral
**Version:** 2.0 DRAFT
**Created:** 2026-05-05
**Owner:** James
**Status:** DRAFT

---

## Purpose

The technical spec for building the FFG cross-sell engine in GoHighLevel. Source of truth for Xavier's build. Every field, stage, and workflow ties back to the FFG Post-Settlement Nurture Strategy v2.0 (April 2026, Rowdie).

Companion documents:

- **Rep Handbook (08e):** what the broker does when the system hands them a human. The handbook maps the same journey from the broker's seat. Stage names and T-numbers match this guide exactly.
- **Scripts (10e):** every call opener, voicemail, and manual broker template. This guide points to 10e, it does not hold call copy.

This guide is for the GHL admin and the Njin build team. Not customer-facing.

---

## The Whole Flow Explained

Read this before the technical sections. It is the same picture the broker reads in the handbook.

### The Core Idea

A settled FFG customer is not a finished job. They are the start of a 12-month relationship that should produce a second loan, an FHL referral, or both. The system runs the relationship in the background. It sends the right email and SMS at the right time, watches what the customer does, and taps a broker on the shoulder only when there is a real human moment to handle.

The broker never has to remember to call anyone. The system remembers. The broker works a queue.

### One Picture: The Whole Flow

```
SETTLEMENT (Day 0)
  │  Ambition pushes the settled loan into GHL.
  │  ICA derived. Customer enters the pipeline.
  ▼
M0   T1  Day 3   Welcome email          (auto)
     T2  Day 7   Check-in SMS           (auto)
  ▼
M1   T3  Day 30  Value-drop email       (auto)
  ▼
M3   T4  Day 90  Q1 milestone email     (auto)
     T5  Day 92  Q1 SMS                 (auto)
  ▼
M6   T6  Day 180 Halfway email + FHL seed (auto)
     T7  Day 183 Halfway SMS            (auto)
     T8  Day 180 HALF-YEAR CALL         (BROKER)
     T9          Voicemail if no answer (BROKER)
  ▼
M9   T10 Day 270 FHL warm-up email      (auto)
     T11 Day 273 FHL warm-up SMS        (auto)
  ▼
M12  T12 Day 365 Anniversary email      (auto)
     T13 Day 365 Anniversary SMS        (auto)
     T14 Day 365 ANNIVERSARY CALL       (BROKER)
     T15         Voicemail if no answer (BROKER)
  ▼
M12+ N16 Day 365+ Win-back email 1      (auto)
     N17 Day 365+30 Win-back email 2    (auto)

BRANCHES (fire any time, pull the card off the spine, then return it):
  • Hot Lead      FFG product CTA clicked, M6+    → broker call, 24h
  • FHL Referral  FHL content clicked twice       → 3-email intro + FHL broker
  • Interacting   Any inbound reply (SMS/email)   → broker actions same day
```

Two broker calls are fixed: the Half-Year Call at Month 6 (T8) and the Anniversary Call at Month 12 (T14). Everything else around them is automated. The branches are the only other times a broker is pulled in, and the system decides when, not the broker.

### The Flow as a Table

| Stage | When | Type | What fires | Who acts |
|---|---|---|---|---|
| T1-T2 | M0 | Auto | Welcome email, check-in SMS | System |
| T3 | M1 | Auto | Value-drop email | System |
| T4-T5 | M3 | Auto | Q1 email + SMS | System |
| T6-T7 | M6 | Auto | Halfway email + FHL seed, SMS | System |
| T8-T9 | M6 | Manual | Half-Year Call + voicemail | Broker |
| T10-T11 | M9 | Auto | FHL warm-up email + SMS | System |
| T12-T13 | M12 | Auto | Anniversary email + SMS | System |
| T14-T15 | M12 | Manual | Anniversary Call + voicemail | Broker |
| N16-N17 | M12+ | Auto | Win-back emails | System |
| Hot Lead | Any (M6+) | Manual | Broker follow-up, 24h SLA | Broker |
| FHL Referral | Any | Auto + manual | 3-email FHL intro + FHL broker handover | System + FHL broker |
| Interacting | Any | Manual | Broker actions the reply same day | Broker |

### The Safety Net (Red Dot Protocol)

Every broker task has a clock. Miss the soft window, the task goes Yellow and rises in the broker's queue. Miss the hard window, it goes Red and escalates to Rowdie and the broker manager. The full SLA table is in Section 6. The broker-facing version is in the handbook.

### One Worked Example (End to End)

A PCLRB (prime repeat borrower) settles a $40K unsecured personal loan.

1. Day 0: Ambition pushes the loan. ICA derives to PCLRB. `ica_history` gets `PCLRB`. `cross_sell_signals` gets `settlement_seeded`. Card enters at T1-T2.
2. Day 3: T1 VIP welcome email fires. Day 7: T2 check-in SMS.
3. Day 30 to Day 92: T3, T4, T5 fire on schedule. The customer clicks the rate-tool link in the Day 90 email. `cross_sell_signals` gets `rate_research`. Because it is past M0, the Rate Research branch sends a rate-review email and notes it.
4. Day 180: T6 halfway email + T7 SMS fire. The card moves to T8-T9. A Half-Year Call task lands with the assigned broker. Broker calls (T8), no answer, leaves voicemail (T9). `cross_sell_signals` gets `m6_call_done`.
5. Day 200: customer clicks the FFG "next loan" CTA. `cross_sell_signals` gets `hot_lead`. Card jumps to the Hot Lead branch. Broker task, 24h SLA. Broker calls, customer wants a car loan. Broker books it. Outcome logged.
6. The card returns to the spine at the next scheduled touch. The customer settles a second loan. `cross_sell_signals` gets `repeat_customer`. They exit into the Repeat Customer journey.

That is the whole engine. The rest of this guide is the build detail behind it.

---

## 1. Pipeline Architecture: T-System

One GHL pipeline holds every settled FFG customer. The pipeline uses the **T-System**: every individual touchpoint is its own numbered step, and consecutive touchpoints of the same type are grouped into one visible stage. The broker always knows where a customer is by reading the stage name.

### 1.1 Stage Type Legend

Mandatory on every stage.

| Symbol | Meaning |
|---|---|
| ➡️ | Opportunities are automatically added here (Ambition push, click trigger) |
| ⚡️ | Moving a card here triggers an automation (email, SMS, task) |
| ➡️ ⚡️ | Both auto-add and triggers on move |
| 👤 | Manual stage. The broker must action the task to move the card. |

### 1.2 T and N Prefixes, and the Stage Rule

- **T-series:** direct touchpoints across the 12-month journey. Each email is a T. Each SMS is a T. Each call is a T. Each voicemail is a T. Numbering is continuous from T1.
- **N-series:** post-journey automated nurture (win-back). Numbering continues across the switch (T15 → N16).
- **One T can hold a burst.** The only time multiple sends share one T is when a single SMS touchpoint is split into a quick burst (T2a then T2b a minute apart, read as one message). That is still one T.

**Stage rule (two cuts):**

1. **Type switch.** When the touchpoint type changes (auto ⚡️ to manual 👤 or back), a new stage begins.
2. **Month gap.** This is a 12-month journey, not a 4-day cadence. Touchpoints in different months never share a stage, even when the type is the same. A new month starts a new stage.

So T1 (Day 3 email) and T2 (Day 7 SMS) share the stage T1-T2 (both auto, both Month 0). T3 (Day 30 email) is alone in its stage because it is a new month, even though it is also auto.

### 1.3 The FFG Cross-Sell Pipeline

| # | Stage | Type | Description |
|---|---|---|---|
| 1 | Interacting | ➡️ ⚡️ | Any inbound reply (SMS or email) auto-moves the card here from any stage. First thing the broker sees. 24hr RED dot. Broker actions, then moves to FUP or a branch. |
| 2 | FUP | 👤 | Broker-parked card after we have responded. Scheduled follow-up task. 24hr YELLOW dot from task fire. |
| 3 | T1-T2 | ⚡️ | M0. Day 3 welcome email (T1), Day 7 check-in SMS (T2). |
| 4 | T3 | ⚡️ | M1. Day 30 value-drop email (T3). |
| 5 | T4-T5 | ⚡️ | M3. Day 90 Q1 milestone email (T4), Day 92 Q1 SMS (T5). |
| 6 | T6-T7 | ⚡️ | M6. Day 180 halfway email + FHL seed (T6), Day 183 halfway SMS (T7). |
| 7 | T8-T9 | 👤 | M6. Half-Year Call (T8). Voicemail if no answer (T9). |
| 8 | T10-T11 | ⚡️ | M9. Day 270 FHL warm-up email (T10), Day 273 FHL warm-up SMS (T11). |
| 9 | T12-T13 | ⚡️ | M12. Day 365 anniversary email (T12), Day 365 anniversary SMS (T13). |
| 10 | T14-T15 | 👤 | M12. Anniversary Call (T14). Voicemail if no answer (T15). |
| 11 | N16-N17 | ⚡️ | M12+. Win-back email 1 (N16, Day 365+0), win-back email 2 (N17, Day 365+30). |

**Branch stages** (off the spine, see 1.5):

| # | Stage | Type | Description |
|---|---|---|---|
| B1 | Hot Lead | 👤 | FFG product CTA clicked at M6+. Broker call task, 24h SLA. Returns to spine. |
| B2 | FHL Referral | ⚡️ 👤 | FHL content clicked twice. 3-email FHL intro fires, FHL broker handover task. |

### 1.4 Interacting vs FUP

| Stage | Trigger | Meaning | Broker SLA |
|---|---|---|---|
| Interacting | Inbound reply detected on a card | Their move was last. We act. | Same day. 24hr RED dot. |
| FUP | Broker has replied and parked the card with a scheduled follow-up | Our move was last. GHL reminds us. | Task fires on the scheduled day. 24hr YELLOW dot. |

If the customer replies while the card is in FUP, the card moves back to Interacting. FUP never holds a card with an unread reply.

### 1.5 Behavioural Branch Stages

Branches pull a card off the spine, run a focused intervention, then return it to the next scheduled touchpoint. They fire off a value being added to `cross_sell_signals` (Section 2), not off scattered tags.

- **Hot Lead (B1):** `cross_sell_signals` gains `hot_lead` (FFG product CTA click, M6+). Spine pauses 14 days. Broker call task, 24h SLA. On return, resumes spine.
- **FHL Referral (B2):** `cross_sell_signals` gains `fhl_interest` (FHL content click, twice). Spine pauses 21 days. 3-email FHL Referral sub-sequence fires, FHL broker handover task created.
- **Inbound reply:** card moves to Interacting (stage 1), not a branch. Broker actions, then FUP or branch.

A card can only sit in one branch at a time. If a second signal fires while a branch is active, it queues and fires on return.

### 1.6 Auto-Advance Rule

Manual call stages (T8-T9, T14-T15, Hot Lead) auto-advance when the broker logs a disposition of `No Answer` or `Voicemail Left`. GHL detects the disposition and moves the card on. The next auto stage fires on schedule.

If the broker logs `Connected`, `Booked`, `Not Interested`, or `Repeat Loan`, the card does NOT auto-advance. The broker moves it per the disposition.

### 1.7 What Is NOT a Stage

- **Repeat Customer.** `cross_sell_signals` gains `repeat_customer` when a second loan settles. The card exits this pipeline into the Repeat Customer journey. Not a stage here.
- **Lost / Won.** GHL statuses, not stages. Mark Lost (`Ghosting`, `Opted out`, `Settled elsewhere`) after N17 with no engagement, or on outright decline.
- **FHL conversion.** Tracked in `cross_sell_signals` (`fhl_converted`) and on the FHL side. Exit event, not a stage here.

### 1.8 Suppression and Unreachable Protocol

- **Opt-out.** Reply STOP applies the `SMSOptOut` tag (Twilio handles this). `FFG_Unsubscribed` tag = permanent exclude from every audience, no re-entry.
- **Operations hold.** Arrears, default, or a difficult customer situation applies the `FFG_Operations_Hold` tag. Every cross-sell workflow checks this tag on entry and exits if present. Operations decides re-entry.
- **Unreachable.** After N17 with no engagement: mark Lost (`Ghosting`) or move to the bi-annual dormant nurture if eligible. Never recycle a card to T1.

---

## 2. Custom Fields

Fields first, tags only where GHL needs one. The behavioural and routing signals all live in multi-select accumulator fields so the full journey history sits on the contact and reporting can read it. Fields marked TRANSFORM are derived at import (Ambition CSV → GHL); the raw value never lands in GHL.

### 2.1 Identity and Contact (existing GHL fields, mapped)

| GHL field | Source | Notes |
|---|---|---|
| First Name | Ambition `Applicant First Name` | Personalisation |
| Last Name | Ambition `Applicant Last Name` | |
| Email | Ambition `Applicant Email` | Email channel |
| Phone | Ambition `Applicant Phone` | SMS channel |

### 2.2 ICA and Purchase Type (multi-select accumulators)

These accumulate. The most recently added value is the active one. History is kept so a reclassified repeat customer keeps their prior ICA on record.

| Field name | Type | Values | Written by |
|---|---|---|---|
| `ica_history` | Multi-select (accumulates) | YPMB, EPFB, PCLRB, BAB, PVB, Unknown | Master Entry Workflow at settlement, and again on a repeat loan if the ICA changes |
| `fhl_purchase_type_history` | Multi-select (accumulates) | FHB, NewPurchase, Refinance, Investor, Commercial | Set at the at-settlement call. Adds a value if it changes later. |

The active ICA = the latest value in `ica_history`. The ICA content branch reads this. Full ICA definitions are not repeated here. See Section 2 of the master playbook (`02-ideal-client-profiles-avatars.md`).

### 2.3 Signal Accumulator (`cross_sell_signals`)

One multi-select field holds every behavioural and lifecycle signal. Values are added, never removed. This replaces the old Behavioural Tag and Engagement Tag libraries. Workflows trigger off "field contains value".

| Value | Added when | Effect |
|---|---|---|
| `settlement_seeded` | Master Entry Workflow runs | Card enters pipeline at T1-T2 |
| `fhl_seed_clicked` | First FHL content click (Day 180 seed) | Tracking. Counts toward `fhl_interest`. |
| `fhl_interest` | FHL content clicked twice | Fires FHL Referral branch (B2) |
| `fhl_converted` | FHL apply or call booked | FHL referral metric. Softens FFG cadence. |
| `hot_lead` | FFG product CTA click, M6+ | Fires Hot Lead branch (B1) |
| `rate_research` | Click on the rate-tool link in our email (NOT on-page calculator use, which GHL cannot see) | If M6+, fires Rate Research email |
| `high_engagement` | 3 consecutive emails each clicked | Lifts cadence, notifies broker |
| `low_engagement` | 2 consecutive emails no click and no SMS reply | Switches to SMS-first, reduces email |
| `sms_active` | Any inbound SMS reply | Card to Interacting. Broker personal reply, 24h. No auto-reply. |
| `referral_given` | Referred friend submits via the referral-link mechanism (NOT built, see Open Items) | Fires thank-you + Eftpos workflow |
| `repeat_customer` | Second loan settles (Ambition push) | Exit to Repeat Customer journey |
| `m6_call_done` | Broker logs the Half-Year Call outcome | Closes T8-T9 |
| `m12_call_done` | Broker logs the Anniversary Call outcome | Closes T14-T15 |
| `dormant` | No open, click, or SMS reply for 60 days | Exit active, bi-annual nurture only |
| `win_back` | Day 365+ reached, no engagement 60 days prior | Fires N16-N17 |

Behavioural triggers operate on link clicks, not opens. iOS Mail Privacy Protection auto-opens emails, so opens are reported but never used as a workflow signal.

### 2.4 Loan Detail Fields (custom)

| Field name | Type | Source | Used by |
|---|---|---|---|
| `loan_lender` | Text | Ambition | Repricing, broker handoff |
| `loan_rate` | Decimal | Ambition | Rate review trigger |
| `loan_term_months` | Integer | Ambition | End-of-term return signal |
| `loan_amount_financed` | Currency | Ambition | BAB high-value flag |
| `asset_type` | Single select (Car, Equipment, Trailer, Other) | Ambition | BAB routing |
| `asset_year` | Integer | Ambition | Replacement cycle trigger |
| `asset_make` | Text | Ambition | Personalisation token |
| `asset_model` | Text | Ambition | Personalisation token |
| `business_name` | Text | Ambition | BAB personalisation |
| `asset_backed` | Boolean | Ambition | Cross-sell signal |
| `investment_property` | Boolean | Ambition | FHL Investor pathway |
| `mortgage_balance_band` | Single select (None, <$300K, $300K-$600K, $600K+) | TRANSFORM from raw balance | FHL refinance trigger |
| `credit_cards_count` | Integer | Ambition (count only, never card numbers) | Credit profile flag |
| `personal_loans_count` | Integer | Ambition | EPFB marker |
| `loan_type` | Single select (Personal, Motor Consumer, Personal Unsecured, Chattel Mortgage) | Ambition | ICA derivation, personalisation |
| `loan_tier` | Single select (A, B, C) | Ambition | YPMB vs PCLRB split |
| `age_band` | Single select (Under 30, 30-39, 40-49, 50-59, 60+) | TRANSFORM from DOB | ICA derivation |
| `employment_type` | Single select | Ambition | BAB derivation |
| `residential_status` | Single select (Renting, Mortgaged, Owner Occ, With Parents) | Ambition | FHL pathway |
| `marital_status` | Single select | Ambition | Life-stage messaging |
| `has_dependents` | Boolean | TRANSFORM from Dependents count | Life-stage messaging |

### 2.5 Lifecycle Anchors (custom)

| Field name | Type | Source | Used by |
|---|---|---|---|
| `settlement_date` | Date | Ambition `Remittance Date` | Drives every workflow timer |
| `referrer` | Text | Ambition | Referral thank-you trigger |
| `assigned_broker` | User reference | Ambition | Task routing |
| `fhl_seeded_at` | Date | Auto-set on first FHL content click | Tracking |
| `fhl_converted_at` | Date | Auto-set on FHL apply or call booked | Reporting |
| `m6_call_outcome` | Single select (Check-in, Future opp, Active opp, FHL referral, Referral mentioned, No answer) | Broker logs at T8 | Reporting, branch routing |
| `m12_call_outcome` | Single select (same options as M6) | Broker logs at T14 | Reporting, branch routing |

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
| `utm_1` | medium / source / campaign trio for the original acquisition touch (Ambition pass-through) | Once, at contact create. Never overwritten. |
| `utm_2` | trio for the second distinct interaction (email click, SMS reply) | When a second UTM-bearing event lands |
| `utm_3` | trio for the third interaction | Same |
| `utm_4` | trio for the fourth interaction | Same |
| `utm_5` | trio for the fifth interaction | Same. Sixth+ event rolls into `utm_5` (last touch wins). |

Slot 1 is the acquisition source. Slot 5 is the most recent touch. Anything in between is the journey.

Every automated email link carries `utm_medium=email&utm_source=ghl_crosssell&utm_campaign=nurture_{ica}_{day}`. Each click writes the next empty contact slot (`utm_2` to `utm_5`); it never overwrites `utm_1`.

### 2.7 Consent

| Field name | Type | Notes |
|---|---|---|
| `sms_consent` | Boolean | Captured at loan application. Checked before any SMS workflow fires. |
| `email_consent` | Boolean | Captured at loan application. |

### 2.8 Tags We Still Use (the only ones)

Fields cover the journey. These four tags stay because GHL genuinely needs a tag here, not a field:

| Tag | Why it stays |
|---|---|
| `FFG_Settled` | Ambition integration fires this on settlement. It is the single entry trigger for the Master Entry Workflow. |
| `SMSOptOut` | Twilio STOP keyword handling writes a tag, not a field. Disables the SMS channel. |
| `FFG_Unsubscribed` | Permanent global suppression. Hard-excluded from every audience build. No re-entry. |
| `FFG_Operations_Hold` | Arrears / default / difficult situation. Every workflow checks this tag on entry and exits if present. |

No other tags. Everything else is a field.

---

## 3. Workflows

### 3.1 Master Entry Workflow

**Trigger:** Tag added, `FFG_Settled` (Ambition push on settlement).

**Guard:** if `FFG_Operations_Hold` or `FFG_Unsubscribed` present, exit. No enrolment.

**Logic:**

```
Derive ICA from loan_type + loan_tier + age_band + employment_type:

IF loan_type = "Chattel Mortgage" AND employment_type = self-employed
  → add "BAB" to ica_history
ELSE IF loan_type = "Personal Unsecured" AND loan_tier IN (A,B) AND age_band IN (30-39,40-49,50-59)
  → add "PCLRB" to ica_history
ELSE IF loan_type = "Personal Unsecured"
  → add "EPFB" to ica_history
ELSE IF loan_type = "Motor Consumer" AND loan_tier = "A" AND age_band IN (40-49,50-59)
  → add "PVB" to ica_history
ELSE IF loan_type = "Motor Consumer"
  → add "YPMB" to ica_history
ELSE
  → add "Unknown" to ica_history, notify Rowdie for manual classification

Add "settlement_seeded" to cross_sell_signals.
Enrol in the ICA content branch. Card enters pipeline at T1-T2.
```

**Output:** one ICA value in `ica_history`, `settlement_seeded` set, contact on the spine. End.

### 3.2 ICA Content Branch (×5, content only)

One content set per ICA. Same T-spine for all five. The branch reads the latest `ica_history` value and serves that ICA's copy at each T. The spine, timers, and stage structure are identical across ICAs. Only the email and SMS bodies differ. Copy is in the Copy Library below, labelled by T and ICA.

Timer anchor for every T = `settlement_date`.

| T | Day | Channel | Touchpoint |
|---|---|---|---|
| T1 | 3 | Email | Welcome and Review |
| T2 | 7 | SMS | Check-In |
| T3 | 30 | Email | Value Drop |
| T4 | 90 | Email | Q1 Milestone |
| T5 | 92 | SMS | Q1 SMS |
| T6 | 180 | Email | Halfway + FHL Seed |
| T7 | 183 | SMS | Halfway SMS |
| T8 | 180 | Call | Half-Year Call (3.4) |
| T9 | 180 | Voicemail | Half-Year voicemail |
| T10 | 270 | Email | FHL Warm-Up |
| T11 | 273 | SMS | FHL Warm-Up SMS |
| T12 | 365 | Email | Anniversary |
| T13 | 365 | SMS | Anniversary SMS |
| T14 | 365 | Call | Anniversary Call (3.5) |
| T15 | 365 | Voicemail | Anniversary voicemail |
| N16 | 365+0 | Email | Win-back 1 |
| N17 | 365+30 | Email | Win-back 2 |

**Branch hooks inside the content branch (run after every email send):**

- 7-day wait, check click history. FHL link click → add `fhl_seed_clicked`; second FHL click → add `fhl_interest` (fires B2). FFG product CTA click after Day 180 → add `hot_lead` (fires B1). Rate-tool link click in our email after Day 180 → add `rate_research` (the email-link click, not on-page calculator use).
- 3 consecutive emails each clicked → add `high_engagement`. 2 consecutive with no click and no SMS reply → add `low_engagement`.
- Daily background check: no open, click, or SMS reply for 60 days → add `dormant`.

**Exit conditions:** `repeat_customer` → exit to Repeat Customer journey. `FFG_Unsubscribed` → permanent exit. `dormant` → exit active, bi-annual nurture. Day 365 reached with no `hot_lead` and no `fhl_converted` → add `win_back`, enrol N16-N17.

### 3.3 Behavioural Branch Workflows

> **Build feasibility. Confirm with Xavier before building. Not all of these triggers are GHL-native.**
>
> - **Native, build now:** email link clicks (`fhl_seed_clicked`, `fhl_interest`, `hot_lead`, `rate_research`), consecutive opens / clicks (`high_engagement`, `low_engagement`), inbound SMS reply (`sms_active`) and its auto-acknowledgement. GHL handles all of these out of the box.
> - **Needs instrumentation, do not assume:** `rate_research` fires on a click of the rate-tool *link in our email*, which is trackable. On-page calculator *usage* is not visible to GHL unless the calculator itself is instrumented to post back (dev work, not in scope here).
> - **Mechanism not built:** `referral_given` needs a per-contact referral link, a capture form, and settlement attribution for the $100 Eftpos card. None of that exists yet. Treat the referral branch as design-pending, not buildable as written.
>
> The rest of this section assumes the native triggers only. Anything beyond them is parked in Open Items until Rowdie and Xavier confirm scope.

Each triggers off `cross_sell_signals` containing a value. Each pauses the spine, runs, then returns the card to the next scheduled touchpoint.

| Branch | Trigger value | Action | Notify | Resume |
|---|---|---|---|---|
| High Engagement | `high_engagement` | Pause spine. Interim ICA-aligned SMS. From M6, include broker-call offer. | Assigned broker task: "{First} is engaged. Worth a call." | 30 days, return to spine |
| Low Engagement | `low_engagement` | Pause email. Re-engagement SMS (10e). Engaged in 7 days → resume email. No engagement → quarterly email only. | None | On engagement or 7 days |
| FHL Referral (B2) | `fhl_interest` | Pause spine 21 days. Enrol in FHL Referral sub-sequence (Section below). | FHL broker task: name, ICA, purchase type, history | 21 days or sub-sequence end |
| Hot Lead (B1) | `hot_lead` | Pause spine 14 days. Broker Handoff Workflow (3.7). | Assigned broker, urgent, 24h SLA | Broker outcome or 14 days |
| Rate Research | `rate_research` | If M6+, send Rate Research email (Copy Library) within 7 days. If M0-M6, log only. | Broker if second click in 14 days | Spine continues in parallel |
| Referral Given | `referral_given` | Thank-you email + Eftpos SMS (Copy Library). Increment referral counter. | Assigned broker | Spine continues |
| SMS Active | `sms_active` | Card to Interacting. Pause SMS automation. Auto-acknowledge only (Copy Library). Broker replies personally. | Assigned broker, urgent, 24h SLA | Broker actions, then FUP |
| Dormant | `dormant` | Exit active spine. Bi-annual single educational email only. | None | n/a |
| Repeat Customer | `repeat_customer` | Exit spine. Add new ICA to `ica_history` from the new loan. Enrol in new ICA content branch. | Assigned broker, thank-you task | n/a |

### 3.4 M6 Half-Year Call Workflow (NEW)

**Trigger:** card reaches T8 (Day 180, after T6-T7 auto touches fire). Guard: skip if `FFG_Operations_Hold` or `FFG_Unsubscribed`.

**Action:**

1. Create broker call task assigned to `assigned_broker`. Title: "Half-Year Call: {First} {Last}, {ICA}, Month 6". Body: loan summary, recent engagement (last 3 clicks), FHL purchase type, suggested talking points by ICA.
2. T8 = the call. Broker calls. Script in 10e.
3. T9 = voicemail if no answer. Script in 10e.
4. Broker logs `m6_call_outcome` and adds `m6_call_done` to `cross_sell_signals`.

**Outcome routing (from `m6_call_outcome`):**

- `Active opp` → broker books it, treat as Hot Lead path
- `Future opp` → broker sets a dated FUP task
- `FHL referral` → add `fhl_interest`, fires B2
- `Check-in` or `No answer` → card returns to spine at next scheduled touch

This is a proactive call for every engaged contact, all ICAs. It replaces the old loose "9-12 month proactive call".

### 3.5 M12 Anniversary Call Workflow (NEW)

**Trigger:** card reaches T14 (Day 365, after T12-T13 auto touches fire). Same guards as 3.4.

**Action:** identical structure to 3.4. Title: "Anniversary Call: {First} {Last}, {ICA}, Month 12". T14 = call, T15 = voicemail (10e). Broker logs `m12_call_outcome`, adds `m12_call_done`.

This call folds in what used to be the FFG annual-review touch and the 9-12 month window. One fixed call at Month 12, all ICAs. After it, if no `hot_lead` and no `fhl_converted`, the card moves to N16-N17 win-back.

### 3.6 FHL Referral Sub-Sequence

Standalone three-email warm intro to Fox Home Loans. Triggered when `cross_sell_signals` gains `fhl_interest`.

| Email | Timing | Content | CTA | Exit |
|---|---|---|---|---|
| 1: Warm Intro + Lead Magnet | Day 0 | ICA-specific lead magnet, value first | Lead magnet link | FHL apply or call booked → add `fhl_converted`, exit |
| 2: Education | Day 7 (if no conversion) | FHL process in plain English | FHL apply or book a call | Same exit |
| 3: Social Proof + Apply | Day 14 (if no conversion) | One anonymised story | FHL apply | Sequence ends |

After the sequence the contact resumes the FFG spine where it paused. If `fhl_converted`, the FFG spine continues at quarterly email only until the FHL deal completes.

### 3.7 Broker Handoff Workflow

> **Internal policy, Rowdie to resolve.** The GHL task mechanics below are buildable as specified. The handoff *policy* is not. Who formally owns the customer relationship after handover, when ownership transfers, how credit and commission are split, and who makes the call, are internal Fox decisions and still open. Build the task plumbing. Do not treat the ownership model as locked until Rowdie signs it off. Tracked in Open Items.

**Trigger:** `cross_sell_signals` gains `hot_lead`.

1. Internal GHL task to `assigned_broker`. Title: "FFG Hot Lead: {First} {Last}, {ICA}, Month {months_since_settlement}". Body: contact, last 3 clicks, suggested talking points.
2. Internal Slack/Teams notification if integrated.
3. Spine pauses 14 days.
4. Broker logs outcome: `Contacted`, `Booked Call`, `Applied`, `Not Interested`, `No Response`.
5. No outcome after 14 days → secondary task to broker manager.

**Resume:** `Applied` → exit spine, Ambition push will add `repeat_customer` on settlement. `Not Interested` → resume at next touch. `No Response` → resume at quarterly cadence for 90 days. No outcome after 14 days → resume at next touch, log a flag.

### 3.8 Win-Back Workflow

**Trigger:** `cross_sell_signals` gains `win_back` (Day 365+, no `hot_lead`, no `fhl_converted`, no engagement 60 days).

Two emails, ICA tone applied at send. N16 Day 365+0 pattern interrupt. N17 Day 365+30 final attempt. After N17, add `dormant`. Bi-annual re-engagement email only. No SMS, no proactive broker contact.

### 3.9 Repeat Customer Journey (V2 placeholder)

Out of scope for V1. When `repeat_customer` fires, the contact should enter a separate Repeat Customer pipeline with VIP touchpoints. Build spec to be authored after 90 days of live data.

---

## 4. Data Flow: Ambition CSV → GHL

### 4.1 Import Process

Weekly (daily once stable) CSV extract from Ambition. Privacy filter at the import layer. Raw sensitive values never land in GHL.

```
Ambition CSV
  ↓
Privacy filter script (Xavier)
  ↓ drops Gender, raw DOB, raw Mortgage Balance, Credit Card Balances/Limits, Personal Loan Balances
  ↓ transforms DOB → age_band, Mortgage Balance → mortgage_balance_band, Dependents → has_dependents
GHL custom fields (upsert by email + last name)
  ↓
Settlement in last 7 days AND not already tagged → apply FFG_Settled tag
  ↓
Master Entry Workflow fires (3.1)
```

### 4.2 De-Dup Rule

Match priority: email exact. Fallback: last name + phone last 4 digits. Conflicts logged for manual review. Never auto-merge if email differs.

### 4.3 FHL Data Path

Infynity CSV exports for FHL contacts follow the same import pattern with FHL fields. FHL workflows are out of scope here (FHL 07e + customer success playbook own them). This playbook owns the FFG spine detecting FHL interest and handing the contact across via the FHL Referral sub-sequence.

---

## 5. Lead Scoring (Light Layer)

GHL native lead scoring, surfaces contacts ready for a broker conversation. 30-day rolling window.

| Action | Score |
|---|---|
| Email open | +1 |
| Email click | +5 |
| FHL link click | +10 |
| FFG product CTA click | +10 |
| Calculator or rate tool click | +8 |
| SMS reply | +15 |
| Refer-a-friend submitted | +20 |
| No engagement 14 days | -5 |
| Unsubscribe | -100 |

**Threshold action:** score ≥ 25 in 30 days AND M6+ → push to the "Worth a call" broker queue. Score ≥ 40 → urgent broker task. Scoring runs in parallel to signal triggers. Signals drive the workflow. Score drives broker priority.

---

## 6. Red Dot Protocol (GHL Implementation)

SLA escalation on cross-sell tasks. Yellow is a soft warning inside the broker's queue. Red is an external escalation to Rowdie and the broker manager.

### Task SLA Configuration

| Task type | Yellow | Red | Red action |
|---|---|---|---|
| Hot Lead task (broker call) | 18h since created | 24h since created | Notify Rowdie + broker manager |
| FHL Referral task (FHL broker call) | 36h since created | 48h since created | Notify Rowdie + FHL manager |
| SMS Active task (broker reply) | 18h since created | 24h since created | Notify Rowdie + broker manager |
| Half-Year Call task (T8) | 5 business days | 10 business days | Notify Rowdie |
| Anniversary Call task (T14) | 5 business days | 10 business days | Notify Rowdie |
| FUP task (customer-set callback) | 24h after nominated date | 48h after nominated date | Notify Rowdie + broker manager |

The two proactive calls (T8, T14) get a softer SLA than Hot Lead. They are planned, not hot. The point is they do not silently expire.

### Implementation Pattern

Each task workflow runs three parallel branches on creation:

```
Branch 1 (primary): wait until broker logs outcome → close task
Branch 2 (yellow):  wait Yellow_Trigger → if no outcome, set yellow, surface in queue
Branch 3 (red):     wait Red_Trigger → if no outcome, fire notification, set red
```

GHL native task SLAs do not support multi-stage Yellow/Red out of the box. Use GHL workflows with delayed branches plus internal notification triggers. Xavier owns the build pattern.

### FUP Special Handling

FUP SLA clock anchors on the customer-set callback date, not task creation. The workflow captures the nominated date, schedules Yellow at +24h and Red at +48h from that date. Reschedule re-anchors both. Silent expiry fires the Red Dot.

### Reporting

Every Red Dot logs to the cross-sell reporting dashboard. Monthly view: Red Dots per broker, per task type, per ICA. Repeated Reds on one broker indicate capacity, not discipline. Rowdie escalates to the broker manager.

---

## 7. Dependencies and Open Items

| This document feeds into | What it provides |
|---|---|
| 08e Rep Handbook | Stage names, T-numbers, signal definitions, broker moments |
| 10e Scripts | Call openers, voicemails, manual broker templates |
| 09 Customer Lifecycle (shared) | Lifecycle stages and exit criteria |
| 11 KPIs (shared) | Reporting dashboard metrics |
| 14 Tech Stack (shared) | GHL build spec |

| This document depends on | Status |
|---|---|
| Tone of Voice gate | PASSED 2026-03-05 |
| ICA matrix and definitions (Rowdie) | RECEIVED 2026-04-27 |
| FFG Post-Settlement Nurture Strategy v2.0 (Rowdie) | RECEIVED 2026-04-27 |
| Privacy filter | PENDING |
| GHL sub-account access | Provisioned, awaiting Project Plan v1 approval |
| Settlement Calls script (Doc 6) | BLOCKER: still empty. The at-settlement seed depends on it. |
| Broker handoff ownership policy | OPEN, Rowdie to resolve. Task mechanics buildable. Relationship ownership, transfer point, credit/commission split, who calls = internal Fox policy, not locked. |
| Market-pulse content (PCLRB Day 30, T3) | OPEN, Rowdie to resolve. Ships static evergreen by default. Decision: keep static, or commit to an intermittently-updated market note and at what cadence. Dynamic build parked until decided. |
| Behavioural trigger feasibility | OPEN, Xavier to confirm. Native triggers (email click, open, inbound SMS) buildable. On-page calculator use and referral attribution are NOT GHL-native. Scope each before build. |
| Referral-link mechanism (Eftpos) | OPEN, Rowdie + Xavier. Per-contact referral link, capture form, and settlement attribution for the $100 Eftpos card do not exist. Referral branch is design-pending, not buildable as written. |

---

# Copy Library - Automated Emails and SMS

All system-fired touchpoints live here, labelled by T-number to match the pipeline in Section 1. This is the content Xavier loads into GHL as templates. Every email and SMS below is fired by workflow logic.

Phone call scripts and voicemails (T8/T9 Half-Year Call, T14/T15 Anniversary Call) live in the script library (10e). Manual broker SMS and follow-up emails live in the handbook (08e).

## Defaults (All Automated Emails)

- **Sender name:** The Fox Finance Team
- **Reply-to:** captured into the GHL contact record
- **First-name token:** `{{contact.first_name}}`
- **Length:** 250-400 words for value emails. Under 150 for milestone or SMS-companion emails.
- **Format:** HTML with plain text fallback. Single column. One image max. One primary CTA.
- **Send time:** Tuesday-Thursday, 8-10am AEST. Default Wednesday 8:30am.
- **Footer:** standard FFG ACL 382952 disclaimer. Unsubscribe link. FHL ACR 535038 disclaimer when FHL content is included.
- **Voice:** Australian English. Third-grade reading level. No "advice", "guarantee", "financial hardship". No em dashes.

## Defaults (All Automated SMS)

- **Length:** under 160 characters. Never more than 320.
- **Sign-off:** `, The Fox Team`
- **Send time:** 12pm-2pm AEST midweek. Never before 9am, never after 8pm.
- **Frequency cap:** maximum 2 SMS per active month per contact.
- **Opt-out:** `Reply STOP to unsubscribe` in the first SMS of every sequence.

UTM tags on every link: `?utm_medium=email&utm_source=ghl_crosssell&utm_campaign=nurture_{ica}_{day}`. See Section 2.6.

**T-number reference:** T1 = Day 3 email, T2 = Day 7 SMS, T3 = Day 30 email, T4 = Day 90 email, T5 = Day 92 SMS, T6 = Day 180 email, T7 = Day 183 SMS, T10 = Day 270 email, T11 = Day 273 SMS, T12 = Day 365 email, T13 = Day 365 SMS, N16/N17 = win-back. T8/T9 (Half-Year Call) and T14/T15 (Anniversary Call) are voice, scripts in 10e. The same T applies across all five ICAs; only the body changes.

---

## ICA 1: YPMB (Young Practical Motor Borrower)

Theme: credit confidence and financial growth. Pathway: First Home Buyer (long seed).

### T1 - Day 3: Welcome and Review (Email)

**Subject:** {{contact.first_name}}, you just did something worth celebrating
**Preview text:** A quick thanks, a small ask, and one thing that might surprise you about your loan.

```
Hey {{contact.first_name}},

Quick one to say thanks. Getting your car loan over the line was a real moment, and we're stoked to have helped sort it.

A few people have asked us what to do now the loan's settled, so here's the short version:

✓ First repayment lands on {{custom.first_repayment_date}}. Set the reminder if you haven't.
✓ Anything looks off, ring us. We'd rather hear it now than later.
✓ Every repayment is also building your credit history, which is a much bigger deal than most people realise.

That last one is the bit we want you to hold onto. Most car loan customers don't think about credit. The smart ones do. We'll send you something useful on that in a few weeks.

One small ask: if the experience was a good one, a quick Google review goes a long way for our team. Two minutes max.

[Leave a Google review →]

Cheers,
The Fox Finance Team
```

### T2 - Day 7: First Check-In (SMS)

```
Hey {{contact.first_name}}, just checking in, how's the new car going? Any questions about the loan, give us a buzz on 1300 665 906.
The Fox Team
Reply STOP to unsubscribe.
```

### T3 - Day 30: Credit Builder (Email)

**Subject:** Did you know your loan is building your credit score?

```
Hey {{contact.first_name}},

Most car loan customers don't realise this until later, so we wanted to flag it now.

Every time you make a repayment on time, it's logged on your credit file. Three months of consistent repayments starts to shift the picture. Twelve months changes it properly.

Why does this matter?

Strong credit opens options most people miss:

- Better rates on the next loan (sometimes 2-3% lower)
- Bigger borrowing capacity when you need it
- A real shot at a home loan when the timing's right

You don't need to do anything different. Just keep paying on time, like you're already doing. The system does the rest.

One practical tip: if you can swing an extra $20 into the repayment now and then, it cuts the balance faster and lifts your score profile a touch quicker. Not magic, just maths.

Want to read more on how this works?

[How responsible repayments build credit history →]

No rush. We'll check in again in a couple of months.

Cheers,
The Fox Finance Team
```

### T4 - Day 90: Q1 Milestone (Email)

**Subject:** 3 months in, here's what's changed for you

```
Hey {{contact.first_name}},

You've just hit your first quarter with the loan. That's worth a pause.

Here's what 3 months of repayments has done:

- {{custom.repayments_count}} repayments logged on your credit file
- Roughly {{custom.principal_paid}} chipped off the principal
- A growing track record that lenders pay attention to

Most people don't notice this until they go to apply for the next thing. Then they see it. We're flagging it now so you've got the picture.

Quick budgeting tip while we're here: most customers we see who run into trouble do it in months 4-9, when the novelty wears off and the spending creeps. The trick is keeping the loan repayment as the first thing out of the account, not the last.

You're tracking well. Keep going.

Cheers,
The Fox Finance Team
```

### T5 - Day 92: Q1 SMS

```
Hey {{contact.first_name}}, 3 months with your new car, hope it's been worth every repayment. Quick progress update sent your way: [link]
The Fox Team
```

### T6 - Day 180: Halfway Point + FHL Seed (Email)

**Subject:** You're halfway through, and your options are growing

```
Hey {{contact.first_name}},

Six months down on the car loan. That's a real milestone, and we want to mark it properly.

Here's where you're sitting:

- Six months of clean repayment history on your credit file
- Roughly {{custom.principal_paid}} of the loan paid down
- Borrowing power is meaningfully different to where it was when we first met

Now here's the thing we wanted to plant a seed on. We've worked with a lot of car loan customers who, six months in, started thinking about something they wouldn't have thought about before. A place of their own.

Not now. Not next month. Maybe not even next year. But the same maths that's been quietly working on your credit score is also working on your housing options.

If you have ever wondered what it takes to buy your first home (deposit, lender expectations, repayments), our home loans team put together a plain-English guide. It's not a sales pitch. It's just the breakdown.

[Read the First Home Buyer Guide →]

No rush. No follow-up. Just something to keep on hand for when the thought crosses your mind.

Cheers,
The Fox Finance Team

This email contains general information only and does not constitute financial advice. Fox Home Loans is an Australian Credit Representative (ACR 535038).
```

### T7 - Day 183: Halfway SMS

```
Hey {{contact.first_name}}, 6 months down, your credit's growing. We've put together something that might surprise you: [link]
The Fox Team
```

### T8/T9 - Day 180: Half-Year Call + Voicemail (BROKER)

Voice. Script in 10e. The system has created the broker task. Talking points by ICA are in the task body. After the call the broker logs `m6_call_outcome` and the system adds `m6_call_done`.

### T10 - Day 270: FHL Warm-Up (Email)

**Subject:** What does it take to buy your first home?

```
Hey {{contact.first_name}},

Last time we wrote, we mentioned that your credit had grown to a point where it was worth thinking about home ownership. Some of you replied. Most of you opened it and parked the thought.

This one's for the parkers.

Here's the actual sequence, start to finish, for a first home buyer in Queensland in 2026:

1. Deposit. Most lenders want 5-20% of the property price. The First Home Guarantee can drop that floor.
2. Up-front costs. Stamp duty (often $0 for first home buyers under the threshold), conveyancing, building inspection. Budget around $3-5K depending on the state.
3. Pre-approval. Lender confirms the maximum they'd lend you. No commitment, no impact on your credit if it's done right.
4. Property hunt. Pre-approval makes you a serious buyer.
5. Offer accepted. Conveyancer takes over.
6. Settlement. Keys in hand.

That's it. Five steps, six if you count moving in.

The bit most people get stuck on is the deposit. Our home loans team has a borrowing power calculator that shows you what is achievable based on your current situation, not the situation you think you need to be in.

[Try the borrowing power calculator →]

If that throws up a number that interests you, the next step is a chat with our home loans team. No commitment, no pressure. Just a conversation about what's possible.

Cheers,
The Fox Finance Team

Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### T11 - Day 273: FHL Warm-Up SMS

```
Hey {{contact.first_name}}, ever wondered what it takes to buy your first home? We break it down here: [link]
The Fox Team
```

### T12 - Day 365: Anniversary + Return Pitch (Email)

**Subject:** One year ago, you made a great decision. Here's what's next.

```
Hey {{contact.first_name}},

One year ago today (give or take), the car loan settled. Worth marking.

Here's what has happened in 12 months:

- 12 months of clean credit history
- Roughly {{custom.principal_paid}} paid down on the loan
- Borrowing power that's meaningfully different to the day we met

A few things worth thinking about as you head into year two.

If the car's been good but you've outgrown it, a refinance to release equity or a step-up to a different loan is a real option. Better credit means better rates.

If you're starting to think about a home, our home loans team is the next conversation. They've helped hundreds of people in your exact spot.

If everything's tracking and you don't need anything, that's also fine. We'll keep being useful in the background.

Whichever it is, here's where we'd start a conversation:

[Talk to our home loans team →]

[Or chat to us about a finance refresh →]

Cheers,
The Fox Finance Team

Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### T13 - Day 365: Anniversary SMS

```
Hey {{contact.first_name}}, it's been exactly one year since your loan settled. We're proud of you, and we'd love to help with whatever's next: [link]
The Fox Team
```

### T14/T15 - Day 365: Anniversary Call + Voicemail (BROKER)

Voice. Script in 10e. System-created broker task. Folds the old annual review and the 9-12 month window into one fixed Month 12 call. After it the broker logs `m12_call_outcome` and the system adds `m12_call_done`.

### N16/N17 - Day 365+: Win-Back

See Win-Back below.

---

## ICA 2: EPFB (Established Personal Finance Borrower)

Theme: financial momentum and life-stage planning. Pathway: New Purchase or Refinance.

### T1 - Day 3: Welcome and Review (Email)

**Subject:** {{contact.first_name}}, thanks for trusting us with this

```
Hey {{contact.first_name}},

Quick one to say thanks. We know there were probably a few options on the table for sorting out the {{custom.loan_purpose}}, and you went with us. Appreciated.

Three things to lock in:

✓ First repayment is {{custom.first_repayment_date}}. Set the reminder.
✓ If anything looks off when the direct debit hits, ring us first, not the bank.
✓ Keep our number handy: 1300 665 906.

We won't drown you in emails. We check in at three months, six months, and a year. Only when there is something useful to say.

If the experience was a good one, a Google review takes two minutes and helps our team a lot.

[Leave a Google review →]

Cheers,
The Fox Finance Team
```

### T2 - Day 7: Quick Check-In (SMS)

```
Hey {{contact.first_name}}, hope everything's settled in nicely with your loan. Give us a call if anything comes up.
The Fox Team
Reply STOP to unsubscribe.
```

### T3 - Day 30: Financial Clarity (Email)

**Subject:** Three things that make a personal loan work for you (not against you)

```
Hey {{contact.first_name}},

Most personal loan customers we see could be getting more from their loan. They're paying on time, but they're missing the small moves that compound.

Three things worth knowing:

1. Extra repayments. Most personal loans let you make additional repayments without penalty. Even $50 a month off the principal saves real money over the term. Check your loan terms or give us a buzz to confirm.

2. Redraw, if your loan has it. Some personal loans give you access to extra repayments back as a redraw. Useful safety net. Worth knowing whether yours does.

3. Loan health check. If your situation changes (pay rise, new job, baby, anything), let us know. Sometimes a quick conversation reveals an opportunity to consolidate, restructure, or simply make the loan work better.

That's it. No CTA, no pitch. Just useful.

If you want to model the impact of an extra $50 or $100 a month, here's our calculator:

[Loan repayment calculator →]

Cheers,
The Fox Finance Team
```

### T4 - Day 90: Q1 Progress (Email)

**Subject:** {{contact.first_name}}, 3 months in, how's it tracking?

```
Hey {{contact.first_name}},

Three months down. Time for a quick check.

By now, the loan's part of the rhythm. Direct debit fires, money goes out, life keeps moving. The {{custom.loan_purpose}} you took the loan out for is hopefully sorted.

Quick question worth sitting with: what are you working toward next?

We ask because the customers who get the most out of working with us are the ones who treat the loan as one move in a longer plan, not the whole plan. A renovation. A wedding. A car. A house. Sometimes all four over a few years.

If you've got something on the horizon, even something fuzzy, we can help you map the order. Sometimes the order matters more than the move itself.

No commitment. Just a conversation.

[Reply with a quick "yeah, I've got something" if so →]

Cheers,
The Fox Finance Team
```

### T5 - Day 92: Q1 SMS

```
Hey {{contact.first_name}}, just hitting your 3-month mark, we hope the loan's making a difference. Anything we can help plan for next? [link]
The Fox Team
```

### T6 - Day 180: Mid-Year Review + FHL Seed (Email)

**Subject:** You're halfway there, what does the next 6 months look like?

```
Hey {{contact.first_name}},

How's it going? The {{custom.loan_purpose}} is sorted (we hope). The repayment rhythm is locked.

Quick mid-year review prompt: how are things tracking against what you wanted six months ago?

Two questions worth sitting with:

1. Could a consolidation save more? If you've still got a credit card, a buy-now-pay-later, or another debt running, sometimes folding it into one tidier setup makes the maths work better. Sometimes not. We can run the numbers.

2. Is home ownership (or refinancing the one you have) worth a conversation? Whether you're renting and wondering if the deposit's closer than you think, or you're already a homeowner and the rate environment's shifted since you locked in, our home loans team is worth a chat. Not a pitch. A health check.

[Try the home loan health check →]

[Or apply →]

If neither applies right now, no problem. Just keep us in mind for when something does.

Cheers,
The Fox Finance Team

Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### T7 - Day 183: Mid-Year SMS

```
Hey {{contact.first_name}}, 6 months in, have you thought about your next financial goal? We'd love to help you plan it. [link]
The Fox Team
```

### T8/T9 - Day 180: Half-Year Call + Voicemail (BROKER)

Voice. Script in 10e. Broker task created by the system. Logs `m6_call_outcome`, system adds `m6_call_done`.

### T10 - Day 270: Next Chapter (Email)

**Subject:** What would your finances look like in 12 months if you made one smart move now?

```
Hey {{contact.first_name}},

Right around the 9-month mark is when we see customers start asking the bigger question. Not "how do I keep up with this loan", but "what's the next move".

For someone who took out a personal loan to consolidate, the next move is usually a vehicle upgrade or a home renovation. Cash flow is freed, options open up.

For someone who took out a loan for a renovation, wedding, or travel, the next move is often a property conversation. Either the first one or the next one.

Whatever your version is, the one move that compounds the most is being financially organised before you need to be. Pre-approval. Equity check. A plan, not a panic.

If a home loan, or refinancing your current one, is part of the picture, the Fox Home Loans team can run the numbers without commitment.

[Talk to the home loans team →]

If something else is on the horizon, reply to this email or give us a buzz. We'll work it out together.

Cheers,
The Fox Finance Team

Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### T11 - Day 273: Next Chapter SMS

```
Hey {{contact.first_name}}, have you ever wondered what your next financial move should be? We think we know. [link]
The Fox Team
```

### T12 - Day 365: Anniversary (Email)

**Subject:** A year ago you made a decision. Here's what you can do with that momentum.

```
Hey {{contact.first_name}},

One year ago, you trusted us to help you sort the {{custom.loan_purpose}}. That's worth marking.

In 12 months you've:

- Built a year of clean repayment history (which lenders weight heavily)
- Paid down roughly {{custom.principal_paid}} of the loan
- Probably learned a thing or two about how this whole finance thing works

Here's the question we'd put to you for year two: what's the next goal?

Three real options most customers in your spot are weighing:

1. Another life-event loan (vehicle, renovation, home upgrade) using your better borrowing position
2. A first home or an upgrade. Our home loans team has helped hundreds of personal loan customers move into property
3. Refinance the original loan if you've found a better rate or want to restructure

Or none of the above, in which case keep the loan rolling and we'll check in next year.

Whatever it is, we're here.

[Talk to the home loans team →]

[Or chat to us about a personal finance refresh →]

Cheers,
The Fox Finance Team

Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### T13 - Day 365: Anniversary SMS

```
Happy one-year mark, {{contact.first_name}}. It's been great having you with us. What are you working toward next?
The Fox Team [link]
```

### T14/T15 - Day 365: Anniversary Call + Voicemail (BROKER)

Voice. Script in 10e. System-created broker task. Logs `m12_call_outcome`, system adds `m12_call_done`.

---

## ICA 3: PCLRB (Prime Convenience-Led Repeat Borrower)

Theme: VIP intelligence and proactive preparation. Pathway: New Purchase, Refinance, or Investor. Tone: peer-to-peer.

### T1 - Day 3: VIP Welcome Back (Email)

**Subject:** {{contact.first_name}}, good to have you back

```
Hey {{contact.first_name}},

Quick one. Loan's settled, paperwork's done, and we're glad you came back to us {{custom.loan_count_text}}.

You know the drill, but for the record:

✓ First repayment {{custom.first_repayment_date}}
✓ Anything off, ring us direct: 1300 665 906
✓ We'll keep the contact light. You'll hear from us when there's something worth knowing.

Two minutes for a Google review when you've got a moment? Helps the team.

[Google review →]

Cheers,
The Fox Finance Team
```

### T2 - Day 7: Personal Check-In (SMS)

```
Hey {{contact.first_name}}, just making sure everything settled smoothly. Always here if you need anything.
The Fox Team
Reply STOP to unsubscribe.
```

### T3 - Day 30: Staying Ready (Email)

**Subject:** A quick one for when your next move comes up

```
Hey {{contact.first_name}},

Quick one, nothing to action.

You know how this works. The people who move fastest when an opportunity comes up are the ones who were ready before they needed to be. File current. Pre-approval sorted. No scramble.

So treat this as a marker. Whenever the next thing is on the horizon, a new vehicle, a property move, a refinance question, the first call is the easy one. We pull your file, tell you where you stand, you decide from there. No commitment, no credit impact just to ask.

Nothing to do today. Just know the door is open and the groundwork is quick.

Cheers,
The Fox Finance Team
```

**Build note (default = static).** This email ships static and evergreen. It carries no live market data, so it never goes stale and needs no feed. An optional V2 could replace it with a periodically-updated market note (rate environment, lender policy, broker observations), but only if Rowdie commits to maintaining those inputs on a set cadence. Do not build the dynamic version until that call is locked. See Open Items.

### T4 - Day 90: Exclusive Update (Email)

**Subject:** Your 3-month update, and something worth knowing

```
Hey {{contact.first_name}},

Three-month mark. Quick update.

Loan tracking as expected.

One thing worth flagging for someone in your position: pre-approval readiness.

Most repeat customers we see in your bracket end up doing one of two things in the next 6-12 months: another asset purchase, or a property conversation. Both move faster when we've got the paperwork already in motion.

If you're thinking about anything (or even thinking about thinking about it), the smart play is a 15-minute call. We get the basics on file. When the timing's right, we move.

[Book 15 minutes →]

Or just reply to this email if it's easier.

Cheers,
The Fox Finance Team
```

### T5 - Day 92: Q1 SMS

```
Hey {{contact.first_name}}, 3 months in. Any changes coming up that we should help plan for? Always happy to chat.
The Fox Team
```

### T6 - Day 180: Equity and Opportunity (Email)

**Subject:** The one question worth asking at the halfway mark

```
How's it going {{contact.first_name}}?

One question worth sitting with at the halfway mark: is your money working as hard as it should be?

Two specific angles for you.

If you're a homeowner, the rate environment has shifted enough since your last home loan review that a health check is probably worth 15 minutes. We can pull up what you're on, what the market's at, and what is achievable. No commitment.

[Home loan health check →]

If you have equity sitting idle, it is worth a conversation. Investment property, smart refinance, or funding the next purchase without touching cash flow.

[Talk to the investment team →]

If neither applies, no problem. We'll keep watching the market for you.

Cheers,
The Fox Finance Team

Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### T7 - Day 183: Halfway SMS

```
Hey {{contact.first_name}}, mid-year already. We've been watching the market, there's something worth knowing. [link]
The Fox Team
```

### T8/T9 - Day 180: Half-Year Call + Voicemail (BROKER)

Voice. Script in 10e. PCLRB is the highest-value ICA. Treat this call as a priority. Broker task created by the system. Logs `m6_call_outcome`, system adds `m6_call_done`.

### T10 - Day 270: Pre-Approval Ready (Email)

**Subject:** Ready before you need to be, here's why that matters

```
{{contact.first_name}}, quick question.

Statistically, the next few months are when most of our repeat customers come back to us with the next thing.

You don't have one yet? Fine.

But the smart move is to be ready before you need to be. Here's why.

When the right deal, vehicle, or property pops up, the difference between getting it and missing it is usually 48 hours. Pre-approved customers move. Everyone else scrambles for paperwork while the opportunity disappears.

Pre-approval with us takes 30 minutes once we've got your file. There's no commitment, no impact on your credit, no obligation to use it.

If property is on the radar at all, even softly, our home loans team works with investors and upgraders every week. Same logic. Be ready first.

[Get pre-approved →]

[Or just have a chat →]

Cheers,
The Fox Finance Team

Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### T11 - Day 273: Pre-Approval SMS

```
Hey {{contact.first_name}}, are you ready for whatever's next? Let's make sure you're pre-approved before you need it.
The Fox Team [link]
```

### T12 - Day 365: Anniversary (Email)

**Subject:** {{contact.first_name}}, one year on, here's the year-two picture

```
Hey {{contact.first_name}}, mate.

One year on. Worth a proper look at the year-two picture.

Three things worth a number on:

1. Rate comparison on your current loan. Is there anything materially better available?
2. Pre-approval refresh. If the goalposts have moved (income, position, equity), let's update the picture.
3. Investment property review, if relevant. Equity, cash flow, and timing.

The customers who act on this usually find one or two things worth doing in the next 90 days.

[Talk to the team →]

Or reply to this email and we'll work out a time.

Cheers,
The Fox Finance Team

Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### T13 - Day 365: Anniversary SMS

```
{{contact.first_name}}, one year in. We'll look at your loan, your rate, and what's next. Worth a call?
The Fox Team [link]
```

### T14/T15 - Day 365: Anniversary Call + Voicemail (BROKER)

Voice. Script in 10e. This is the proper annual review for PCLRB, now delivered as the fixed Month 12 broker call. Highest-value ICA, priority call. Logs `m12_call_outcome`, system adds `m12_call_done`.

---

## ICA 4: BAB (Business Asset Borrower)

Theme: business growth, tax efficiency, practical tools. Pathway: Commercial Property + Residential (Low Doc). Tone: practical, no fluff.

### T1 - Day 3: Business Welcome (Email)

**Subject:** {{contact.first_name}}, your {{custom.asset_type}} is working, let's make sure your finance is too

```
Hey {{contact.first_name}},

Loan's settled. {{custom.asset_type}} is on the road. Quick wrap-up so the finance side is sorted in your head.

Three things worth confirming:

1. Repayment cycle. {{custom.first_repayment_date}}. Aligned with your {{custom.payment_cycle}} cash flow as discussed.
2. Tax setup. Loan structure is {{custom.loan_structure}}, which means {{custom.tax_implication}}. Worth flagging to your accountant at your next catch-up.
3. Asset write-off. If you haven't already, check whether the {{custom.asset_type}} qualifies for the Instant Asset Write-Off this financial year. Your accountant will know.

That's the operational stuff. We'll keep the contact useful (tax timing, equipment cycles, EOFY) and skip the marketing fluff.

If the experience was a good one, a Google review helps our team a lot.

[Google review →]

Cheers,
The Fox Finance Team
```

### T2 - Day 7: Quick Check-In (SMS)

```
Hey {{contact.first_name}}, all settled with the {{custom.asset_type}}? Give us a call if the paperwork throws anything up.
The Fox Team
Reply STOP to unsubscribe.
```

### T3 - Day 30: Tax and Structure (Email)

**Subject:** Are you claiming everything you're entitled to on the {{custom.asset_type}}?

```
Hey {{contact.first_name}},

Quick one for the business owners. Three things to ask your accountant at your next meeting:

1. ATO deductibility on your loan structure. Chattel mortgage, finance lease, and CHP all behave differently at tax time. Make sure your accountant has the loan documents and is treating it correctly. We can resend if needed.

2. Instant Asset Write-Off eligibility. Threshold for FY2026 is currently $20,000 per asset for businesses turning over under $10M. The {{custom.asset_type}} may or may not qualify depending on cost and use. Worth confirming.

3. Depreciation method. Diminishing value vs prime cost makes a real difference over the asset's life. If your accountant hasn't asked, raise it.

Three questions, one meeting, potentially thousands in tax saved.

Here's a useful reference your accountant may already have:

[ATO business deductions guide →]

We'll be back at the 90-day mark with a cash flow framework you can use.

Cheers,
The Fox Finance Team
```

### T4 - Day 90: Cash Flow Framework (Email)

**Subject:** Three months in, is your business finance working as hard as the asset?

```
Hey {{contact.first_name}},

Three months in. The {{custom.asset_type}} is generating return (we hope). The repayment rhythm is locked.

Quick framework worth running through this quarter.

1. Payment calendar. Map every business loan, lease, and finance commitment against the income calendar. Any cash flow tightness in any month? That's where you reshape, not when the bill arrives.

2. Asset utilisation. Is the {{custom.asset_type}} generating the return you scoped at purchase? If not, that's data. Either the asset's wrong, the use case is wrong, or the costing was off.

3. Forward equipment plan. What's coming up in the next 6-12 months? Replacement, additional capacity, anything else. Knowing now means we can structure ahead.

If the third one's open, that's our wheelhouse. Don't wait until the truck blows up to start the conversation.

[Book a 15-minute equipment plan call →]

Cheers,
The Fox Finance Team
```

### T5 - Day 92: Q1 SMS

```
Hey {{contact.first_name}}, 3 months in, how's the {{custom.asset_type}} performing? Worth a quick check on your finance structure. [link]
The Fox Team
```

### T6 - Day 180: EOFY Checklist (Email)

**Subject (EOFY variant):** EOFY is {{custom.weeks_to_eofy}} weeks away, your business finance checklist

```
Hey {{contact.first_name}},

EOFY's coming up. Here's the checklist for business asset owners worth running through with your accountant before June 30:

✓ Instant Asset Write-Off: confirm the {{custom.asset_type}} eligibility and any other gear bought this FY
✓ Depreciation review: make sure assets are being treated correctly
✓ GST claim cycle: chattel mortgage GST claim is at purchase; lease is across the term. Different cash flow.
✓ Year-end equipment review: anything else you need to action before June 30 to claim this FY?
✓ Loan structure review: is your current setup still the right fit for the way the business is moving?

Three questions to put to your accountant this month:

1. Should I bring forward any equipment purchases to claim this FY?
2. Is my current loan structure still the most tax-effective?
3. Are there any other deductions I'm missing on the existing finance?

If any of that surfaces a need to finance something before June 30, we move fast. Pre-approval and settlement inside two weeks for most asset types.

[EOFY equipment chat →]

While we're talking longer-term: a few of our business customers ask whether they can get a residential home loan as a self-employed borrower. The short answer is yes. You don't need two years of tax returns. Low doc and alt doc options accept BAS statements or an accountant's letter.

[Self-employed home loans →]

[Or commercial property →]

Cheers,
The Fox Finance Team

Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

(Mid-year variant for Jul-Dec settlements: same structure, framed as mid-year stocktake rather than EOFY rush.)

### T7 - Day 183: EOFY SMS

```
Hey {{contact.first_name}}, EOFY checklist is ready, anything we can help sort for the business before June 30? [link]
The Fox Team
```

### T8/T9 - Day 180: Half-Year Call + Voicemail (BROKER)

Voice. Script in 10e. For BAB, time this against the EOFY cycle where it lands close. Broker task created by the system. Logs `m6_call_outcome`, system adds `m6_call_done`.

### T10 - Day 270: New FY Planning (Email)

**Subject:** New financial year, and smart business owners are already planning

```
Hey {{contact.first_name}},

New FY's underway. The smart business owners we work with are already planning the next 12 months of asset moves.

Three things worth doing this quarter:

1. Equipment audit. What's due for replacement or upgrade in the next 12 months? Vehicles, gear, machinery. Don't wait for breakdowns.

2. Cash flow forecast. Map next year's income against next year's commitments. Any tight months get planned for now.

3. Pre-approval readiness. If a vehicle, equipment purchase, or property is on the horizon, getting the file in front of us now means we can move fast when the right opportunity lands.

If owning your own premises or buying a home as a self-employed borrower is on the roadmap, the Fox Home Loans team has a path forward that doesn't require tax returns.

[Commercial property →]

[Residential low doc →]

Or just give us a buzz to talk through what's coming.

Cheers,
The Fox Finance Team

Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### T11 - Day 273: New FY SMS

```
Hey {{contact.first_name}}, new FY is here, are you set up for the year ahead? Worth a chat about your equipment plans.
The Fox Team [link]
```

### T12 - Day 365: Annual Business Review (Email)

**Subject:** One year on, your business finance deserves a proper review

```
Hey {{contact.first_name}},

One year ago you got the {{custom.asset_type}} financed. Time for the annual review.

Here's what's worth a look:

1. Rate comparison on the current loan. Is there anything materially better available?
2. Replacement timeline review. Is the {{custom.asset_type}} on track, or are we starting to plan the next one?
3. Business growth check. New equipment, second vehicle, premises, anything else on the horizon?
4. Pre-approval refresh for whatever's next.

The customers who act on this usually walk out with one or two things worth doing in the next 90 days.

[Talk to the team →]

While we're at it: from commercial property to a home loan without tax returns, Fox Home Loans covers every stage of business growth and personal wealth building.

[Commercial property →]

[Self-employed home loans →]

Cheers,
The Fox Finance Team

Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### T13 - Day 365: Annual Review SMS

```
Hey {{contact.first_name}}, one year with the {{custom.asset_type}}. Time for the annual review. Let's set you up for the year ahead.
The Fox Team [link]
```

### T14/T15 - Day 365: Anniversary Call + Voicemail (BROKER)

Voice. Script in 10e. The annual business review delivered as the fixed Month 12 broker call. Logs `m12_call_outcome`, system adds `m12_call_done`.

---

## ICA 5: PVB (Prime Vehicle Borrower)

Theme: finance intelligence and strategic readiness. Pathway: New Purchase, Refinance, Investor. Tone: factual, peer-level.

### T1 - Day 3: Settlement Confirmation (Email)

**Subject:** {{contact.first_name}}, all settled, a couple of things worth knowing

```
Hey {{contact.first_name}},

Loan's settled. {{custom.asset_make}} {{custom.asset_model}} on the road. Quick reference.

Loan summary:
- Amount financed: {{custom.amount_financed}}
- Term: {{custom.loan_term_months}} months
- Rate: {{custom.loan_rate}}
- Comparison rate: {{custom.comparison_rate}}
- Balloon: {{custom.balloon_amount}} at end of term
- First repayment: {{custom.first_repayment_date}}

One practical tip most customers in your spot don't act on: extra repayments inside the structure of this loan can shave real interest off if your loan allows it. Worth checking the terms.

When you're ready for the next vehicle, drop us a line first. Pre-approval before you walk into a dealership saves the haggle.

If the experience was a good one, a quick Google review helps the team.

[Google review →]

Cheers,
The Fox Finance Team
```

### T2 - Day 7: Brief Check-In (SMS)

```
Hey {{contact.first_name}}, just confirming everything's settled smoothly. Give us a call before your next purchase, we'll have you pre-approved fast.
The Fox Team
Reply STOP to unsubscribe.
```

### T3 - Day 30: Finance Structure Facts (Email)

**Subject:** How your loan structure affects what you really pay

```
Hey {{contact.first_name}},

Most vehicle finance customers don't run the numbers on their own loan after settlement. Worth doing once. Here's the framework.

Your structure: {{custom.loan_structure}}.

Comparison rate vs headline rate. The difference for your loan is {{custom.comparison_rate_delta}}. Over the term, that converts to roughly {{custom.total_interest_estimate}} in interest.

Balloon payment. Yours is {{custom.balloon_amount}} at month {{custom.loan_term_months}}. Three options at maturity:
1. Pay it out (cash or refinance)
2. Roll into the next vehicle (most common)
3. Refinance the residual on a new term

We'll start the next-vehicle conversation around the 6-month call. No pressure before then.

Extra repayments. Most consumer vehicle loans allow extra repayments without penalty. If yours does and the cash flow allows, $50-100 per fortnight chips away the principal noticeably over the term.

That's the structural read. No CTA. Just useful.

Cheers,
The Fox Finance Team
```

### T4 - Day 90: Loan Health Check (Email)

**Subject:** Three months in, is your loan structure still optimal?

```
Hey {{contact.first_name}},

Three-month check-in. Here's the framework worth running through.

1. Repayment opportunities. Are you using extra repayments if available? On a {{custom.amount_financed}} loan over {{custom.loan_term_months}} months, an extra $200/month can save ~{{custom.savings_estimate}} in interest.

2. Balloon planning. {{custom.balloon_amount}} matures at month {{custom.loan_term_months}}. We start that conversation properly at the 6-month call. Worth knowing what the options are now.

3. Refinancing trigger. If lender rates have moved more than 0.75% since you settled, it's worth a 15-minute number-crunch on whether refinancing makes sense. Includes break costs, fees, and net saving.

If any of that's worth a deeper conversation, here's our calendar:

[Book 15 minutes →]

Cheers,
The Fox Finance Team
```

### T5 - Day 92: Q1 SMS

```
Hey {{contact.first_name}}, 3-month loan health check, worth a quick read if you're planning your next purchase. [link]
The Fox Team
```

### T6 - Day 180: Equity and Rate Review (Email)

**Subject:** Could your money be working harder right now?

```
How's it going {{contact.first_name}}?

Two things worth a number on at the six-month mark.

1. Rate comparison. Rates move. If yours has not had a look since you settled, it is worth a quick check. We can run a refinance opportunity assessment and tell you whether a move stacks up after break costs and fees.

2. Equity angle (if you're a homeowner). If you've got equity sitting idle in your property, the question worth asking is whether it could be funding the next vehicle, an investment property, or simply reducing your overall loan costs. Our home loans team runs the numbers without commitment.

[Investment property →]

[Home loan health check →]

If neither applies right now, no stress. We watch the market for you and flag anything worth knowing.

Cheers,
The Fox Finance Team

Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### T7 - Day 183: Mid-Year SMS

```
Hey {{contact.first_name}}, mid-year rate check, the market has moved. Might be worth a look. [link]
The Fox Team
```

### T8/T9 - Day 180: Half-Year Call + Voicemail (BROKER)

Voice. Script in 10e. For PVB with a balloon, begin balloon planning on this call. Broker task created by the system. Logs `m6_call_outcome`, system adds `m6_call_done`.

### T10 - Day 270: Pre-Approval Ready Before You Need It (Email)

**Subject:** The smartest thing to do before buying your next car

```
{{contact.first_name}}, quick question.

Statistically, the next 6 months is when most premium-vehicle customers start looking at their next purchase.

The smartest thing you can do before walking into a dealership is be pre-approved. Here's why:

1. Speed. Pre-approval means you can act when the right car appears. Dealers know who's a serious buyer.
2. Negotiating power. Pre-approved customers walk in already strong. Dealer finance often gets used as a closing tool, not a financing tool. Your pre-approval kills that.
3. No surprises. The pre-approval is run on real numbers, not dealer-side promises.

It takes 30 minutes once we've got your file. Costs nothing. No commitment to use it.

[Get pre-approved →]

While we're at it, if an investment property is part of the plan, the Fox Home Loans team works with vehicle finance customers like you every week. Worth a quick conversation if the timing's right.

[Investment property →]

Cheers,
The Fox Finance Team

Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### T11 - Day 273: Pre-Approval SMS

```
Hey {{contact.first_name}}, thinking about your next vehicle? Get pre-approved first, we can have it sorted fast.
The Fox Team [link]
```

### T12 - Day 365: Anniversary + Next Vehicle (Email)

**Subject:** {{contact.first_name}}, one year on, and your next purchase window is opening

```
Hey {{contact.first_name}}, mate.

One year on. Worth a proper look.

Three things on the table:

1. Loan anniversary check. Rate environment, balloon planning, refinance options. We crunch the numbers and tell you whether anything's worth acting on.

2. Next vehicle timing. {{custom.balloon_amount}} balloon matures at month {{custom.loan_term_months}}. Most premium customers upgrade every 2-3 years. If you're inside that window, pre-approval for the next vehicle (and the residual rollover) takes the stress out of it.

3. Investment property, if relevant. Equity from your home, paired with the cash flow we already have on file, makes you a serious investment property candidate.

[Talk to the team →]

Cheers,
The Fox Finance Team

Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### T13 - Day 365: Anniversary SMS

```
Hey {{contact.first_name}}, one year in, we can have you pre-approved for your next vehicle before you even step into a dealership. Worth a call?
The Fox Team [link]
```

### T14/T15 - Day 365: Anniversary Call + Voicemail (BROKER)

Voice. Script in 10e. Annual review plus next-vehicle and balloon planning, delivered as the fixed Month 12 broker call. Logs `m12_call_outcome`, system adds `m12_call_done`.

---

## FHL Referral Sub-Sequence (3 Emails)

Triggered when `cross_sell_signals` gains `fhl_interest`. Three automated emails. ICA-tailored for the lead magnet only. Common structure for emails 2 and 3.

### Email 1: Warm Intro + Lead Magnet (Day 0)

**Subject:** Glad you're having a look, here's something useful

```
Hey {{contact.first_name}},

Saw you were poking around the home loans content we sent. Thought we'd give you something more useful than another email.

For someone in your position, the most useful first step is {{ica.lead_magnet_description}}. We've put it together for you below.

[{{ica.lead_magnet_cta}} →]

No call, no pressure, no follow-up unless you reply. Take your time. When you're ready (if you ever are), we're here.

Cheers,
The Fox Finance Team

Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

**ICA-specific lead magnets:**

| ICA | Lead magnet | URL |
|---|---|---|
| YPMB | First Home Buyer deposit + borrowing power guide | foxhomeloans.com.au/first-home-buyer-guide/ |
| EPFB | Refinance savings calculator | foxhomeloans.com.au/refinance-calculator/ |
| PCLRB | Home loan health check + rate comparison tool | foxhomeloans.com.au/health-check/ |
| BAB | Self-employed home loan guide ("Can a business owner get a home loan without tax returns?") | foxhomeloans.com.au/self-employed-guide/ |
| PVB | Investment property borrowing power calculator | foxhomeloans.com.au/investment-calculator/ |

### Email 2: Education (Day 7, only if no conversion)

**Subject:** How Fox Home Loans works (the short version)

```
Hey {{contact.first_name}},

If you opened the {{ica.lead_magnet_short_name}} we sent last week and the next move is unclear, here's how the process works.

Five steps. That's it.

1. Enquire. Phone, email, or our online form. Takes 5 minutes. No commitment, no credit impact.
2. Speak with an expert. 30-minute conversation. We figure out what you need (not what we want to sell).
3. Pre-approval. We submit to a lender. No hard credit pull until you say go.
4. Sign documents. Plain English. We walk through every page.
5. Settle. Funds move. You move.

That's it. We don't have a clever sales process. We just have a team that does this every day.

If you're ready, here's where to start:

[Talk to the Fox Home Loans team →]

[Or book a discovery call →]

Cheers,
The Fox Finance Team

Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

### Email 3: Social Proof + Apply CTA (Day 14, only if no conversion)

**Subject:** One short story before we wrap this up

```
Hey {{contact.first_name}},

Last one from us on the home loans side for now.

A quick story. {{social_proof.customer_name_anonymised}} settled an FFG car loan with us about 18 months back. They were renting at the time. Fast forward, last month they settled their first home with the Fox Home Loans team. Same broker. Same group. Different chapter.

Their words, not ours: "I didn't think I was a home buyer. The Fox Home Loans team showed me I was. Three months later we had the keys."

That's not every story. But it's a real one.

If anything's stirring for you on this, even a small thought, here's where to land:

[Ready when you are →]

Or just reply to this email. We're here.

Cheers,
The Fox Finance Team

Fox Home Loans is an Australian Credit Representative (ACR 535038). This content is general information only and does not constitute financial advice.
```

(Social proof story placeholder. Use a real anonymised case before production.)

---

## Broker Handoff - Internal GHL Task Template

Auto-generated when `cross_sell_signals` gains `hot_lead`. Sent to `assigned_broker`.

```
TASK: FFG Hot Lead, {{contact.first_name}} {{contact.last_name}}

ICA: {{ica_active}}
Loan settled: {{settlement_date}} (Month {{months_since_settlement}})
Lender: {{loan_lender}} | Amount: {{amount_financed}} | Rate: {{loan_rate}}

What just happened:
- Clicked CTA on {{cta_page_url}} at {{click_timestamp}}
- Recent engagement: {{recent_engagement_summary}}
- FHL purchase type: {{fhl_purchase_type_active}} (or "not seeded")

Suggested talking points:
- {{ica_specific_talking_point_1}}
- {{ica_specific_talking_point_2}}
- {{ica_specific_talking_point_3}}

SLA: call within 24 hours. Log outcome in pipeline note.
Yellow at: 18 hours. Red at: 24 hours (escalates to Rowdie + broker manager).
```

---

## Win-Back Sequence (Shared, ICA Tone Applied)

Two automated emails. ICA tone applied at send time via dynamic content blocks. Triggered when `cross_sell_signals` gains `win_back`.

### N16 - Day 365+0: Pattern Interrupt (Email)

**Subject:** Still here if you need us, {{contact.first_name}}

```
Hey {{contact.first_name}},

Quick note. We haven't heard from you in a while. No big deal, life gets busy and email's noisy.

Just flagging that we're still here. Whatever the next financial thing is (vehicle, home, business, refinance), we'd be glad to be the first call.

If we're not the right fit any more, no problem. You can unsubscribe at the bottom and we'll stop sending.

If we are still useful, give us a buzz when the time's right.

Cheers,
The Fox Finance Team
```

### N17 - Day 365+30: Final Attempt (Email)

**Subject:** One thing before we go quiet

```
Hey {{contact.first_name}},

Last one from us for a while.

A year on, the customers we hear back from usually fall into one of three buckets:

1. "Everything's good, all sorted, talk in a year." Great. We'll stop emailing.
2. "Actually, I've got something coming up." Brilliant. Reply and we'll sort it.
3. "Not the right fit any more." All good. The unsubscribe link is at the bottom.

Whichever it is, thanks for trusting us with the original loan. We hope it served you well.

If you ever need us, you know where we are.

Cheers,
The Fox Finance Team
```

After N17: add `dormant`. Bi-annual re-engagement email only. No SMS. No proactive broker contact.

---

## Behavioural Branch Touchpoints

### Low Engagement Re-Engagement SMS

Fires when `cross_sell_signals` gains `low_engagement` (2 consecutive emails no click).

```
Hey {{contact.first_name}}, just checking we still have the right details. If email isn't the right way, reply with what works (phone, message, or something else).
The Fox Team
Reply STOP to unsubscribe.
```

### Rate Research Email (M6+)

Fires when `cross_sell_signals` gains `rate_research` at M6+.

**Subject:** {{contact.first_name}}, you've been looking at rates, here's a real read

```
Hey {{contact.first_name}},

Saw you'd been on the rate calculator. Most customers who check in on rates are weighing one of three things:

1. Should I refinance the existing loan?
2. Could I get a better rate now than when I settled?
3. Am I about to take on something new and want to know what's possible?

We can run a rate review on your existing loan in 15 minutes. We pull what you're on, what the market's at, and what the move would save (after break costs and fees).

[Book a 15-minute rate review →]

Cheers,
The Fox Finance Team
```

### SMS Active Acknowledgement (Auto-SMS)

Fires the moment an inbound SMS reply lands (`cross_sell_signals` gains `sms_active`). The real reply comes from the broker manually using the response scripts in 10e.

```
Got it, {{contact.first_name}}, one of the team will be in touch within the next business day.
The Fox Team
```

### Referral Given - Thank-You (Email + SMS)

Fires when `cross_sell_signals` gains `referral_given`.

**Email subject:** {{contact.first_name}}, thank you (genuinely)

```
Hey {{contact.first_name}},

You just sent {{referred_first_name}} our way. We don't take that lightly.

Here's what happens now:

1. Our team reaches out to {{referred_first_name}} within the next business day.
2. We treat them the way we'd want our own family treated.
3. When their loan settles, your $100 Eftpos card lands within 7 days. We'll text you when it's on the way.

Word of mouth is the reason this business works. Thank you for being part of it.

Cheers,
The Fox Finance Team
```

**SMS (same day):**

```
Hey {{contact.first_name}}, thanks for sending {{referred_first_name}} our way. We'll look after them like family.
The Fox Team
```

---

*This is a draft technical specification. Every workflow and field listed here is a proposal until the privacy filter and ICA derivation logic are locked.*
