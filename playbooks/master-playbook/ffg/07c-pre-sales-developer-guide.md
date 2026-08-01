# FFG Pre-Sales Developer Guide

**Brand:** Fox Finance Group (asset finance)
**Playbook:** Pre-Sales SDR (suffix c)
**Version:** 1.2
**Created:** 2026-05-05
**Owner:** James
**Status:** Draft

---

## Purpose

How an FFG asset finance lead moves from first click to a broker call. The build sits in GoHighLevel. TypeForm captures, Zapier routes, GHL holds the pipeline, 3CX takes the call, Ambition holds the deal once a broker takes ownership.

The SDR-facing companion is the handbook. The script library holds the voice scripts.

In scope: FFG asset finance pre-sale lead nurture and four lead magnets (commercial vehicle, commercial equipment, consumer personal, consumer vehicle).

Reactivation runs as its own pipeline. See the separate Reactivation Developer Guide.

**Convention:** ICAs are defined once in Section 2 of the master playbook (`02-ideal-client-profiles-avatars.md`). This playbook names them and points back. It never redefines them.

---

## Pipeline Architecture: T-System

T-System (touchpoint-per-stage). Automated and manual touches are grouped into linked stages so a single pipeline card moves through the cadence in one continuous flow. Auto stages fire on entry. Manual stages need SDR action. After T14, leads who never replied move into the N-series automated nurture. The transition is automatic. **Never recycle a card back to T1.**

### Stage type legend

| Symbol | Meaning |
|---|---|
| ➡️ | Opportunities are automatically added (webhook, Zapier, form trigger) |
| ⚡️ | Moving a card here triggers an automation (email, SMS, task) |
| 👤 | Manual stage. SDR must action the task to move the card. |

### T and N prefixes

- **T-series (T1 to T14):** direct touchpoints, the active 4-day cadence.
- **N-series (N15 to N22):** post-cadence automated nurture, Day 7 to Day 180.

Numbering is continuous. T14 is the last direct touch. N15 is the first nurture touch.

### FFG Pre-Sale SDR Pipeline

Linked stages keep the card moving without dropping it between automated and manual touches.

| # | Stage | Type | Description |
|---|---|---|---|
| 1 | Interacting | ➡️ ⚡️ | Inbound reply detected. 24hr RED dot. SDR actions and either books the broker call (card exits to Closer Pipeline) or moves to FUP. |
| 2 | FUP | 👤 | SDR-parked card after we've responded. Scheduled follow-up task. 24hr YELLOW dot from task fire time. |
| 3 | T1-T2 | ⚡️ | Day 1. Auto email (T1) then auto SMS pair (T2a + T2b). T1 and T2 are the only touches that vary based on input (magnet or generic enquiry). |
| 4 | T3-T5 | 👤 | Day 1. Three manual SDR call attempts: morning, lunch, 5pm. T5 leaves a voicemail. |
| 5 | T6 | ⚡️ | Day 1, 5:30pm. Auto SMS pair after no-answer cycle. |
| 6 | T7-T8 | 👤 | Day 2. Two manual SDR call attempts: morning, afternoon. |
| 7 | T9 | ⚡️ | Day 2, 5pm. Auto SMS check-in. |
| 8 | T10-T11 | 👤 | Day 3. Two manual SDR call attempts: morning, afternoon. |
| 9 | T12 | ⚡️ | Day 3, 5pm. Auto SMS pair. |
| 10 | T13 | 👤 | Day 4 morning. SDR final call + breakup voicemail. |
| 11 | T14 | ⚡️ | Day 4, 5pm. Auto breakup email. Door-open language. |
| 12 | N15-N22 | ⚡️ | Day 7 to Day 180. Eight automated nurture touches. |

A booked broker call exits the card to the Closer Pipeline. There is no Engaged, Qualified, or Booked Out stage inside this pipeline. Any inbound reply moves the card to Interacting (see below).

### Interacting vs FUP

Stage 1 and Stage 2. Both stay. They are not interchangeable.

| Stage | What it holds | Who moves the card here | SDR SLA |
|---|---|---|---|
| 1. Interacting | Leads actively interacting. The lead's reply was the last action. We owe them a response. | GHL, automatically, on any inbound reply | Action same day. 24hr RED dot. |
| 2. FUP | Follow-ups. Our response was the last action. We are waiting on the lead, with a scheduled follow-up task. | SDR, manually, after responding | Task fires on the scheduled day. 24hr YELLOW dot if not actioned. |

**Auto-move rule (GHL workflow):**

- Any inbound reply (email or SMS) from a lead in this pipeline moves the card to Interacting automatically. The SDR does not move it.
- This applies from any stage. If the card is in FUP and the lead replies, it moves FUP to Interacting. FUP never holds a card with an unread reply.
- The card stays in Interacting until the SDR actions it: book the broker call (card exits to the Closer Pipeline) or respond and park it in FUP with a scheduled follow-up.

Rule of thumb: Interacting = "their move was last, we act". FUP = "our move was last, GHL reminds us".

### Auto-Advance Rule

Manual call stages (T3-T5, T7-T8, T10-T11, T13) auto-advance when the SDR logs a disposition of `No Answer` or `Voicemail Left`. GHL detects the disposition and moves the card forward. The next auto stage fires on schedule.

If the SDR logs `Connected`, `Booked`, `Not Interested`, or `Wrong Number`, the card does NOT auto-advance. SDR moves it manually per disposition.

### What is NOT a stage

- **Booked / SQL.** Booked exits to Closer Pipeline.
- **Lost / Won.** GHL statuses, not stages. Mark Lost (`Ghosting`) after N22 with no reply, or if the lead declines outright.
- **No-Show Recovery.** Sub-flow inside the Closer Pipeline. SDR assists when called in.

### Unreachable Lead Protocol

After N22 with no reply:

1. Mark **Lost** with reason `Ghosting`, or
2. Move to the Reactivation Pipeline cohort if eligible.

**Never recycle to T1.**

---

## UTM Tracking

UTMs replace the old lead source field. The opportunity holds the UTM trio (medium, source, campaign) for the touchpoint that created it. The contact holds the same trio for the first touch PLUS numbered slots for every subsequent interaction, so we can see every channel a lead has touched over time.

### What we capture

**On the opportunity (single trio):**

| Field | Example |
|---|---|
| `utm_medium` | `cpc`, `social`, `email`, `phone`, `referral` |
| `utm_source` | `google`, `facebook`, `instagram`, `direct`, `partner_name` |
| `utm_campaign` | `commercial_vehicle_magnet_2026`, `eofy_promo`, `brand` |

**On the contact (first touch + numbered slots):**

| Field | Holds | When written |
|---|---|---|
| `utm_1` | medium / source / campaign trio for the original first touch | Once, at first contact create. Never overwritten. |
| `utm_2` | trio for the second distinct interaction (next form submit, click, SMS reply, call) | When a second UTM-bearing event lands |
| `utm_3` | trio for the third interaction | Same |
| `utm_4` | trio for the fourth interaction | Same |
| `utm_5` | trio for the fifth interaction | Same. Sixth+ event rolls into `utm_5` (last touch wins). |

Slot 1 is the acquisition source. Slot 5 is the most recent touch. Anything in between is the journey.

### How it works

1. TypeForm captures UTMs from URL parameters and writes them to hidden fields.
2. Zapier passes UTMs into GHL on contact create or update.
3. On contact create: opportunity UTM trio writes fresh. Contact `utm_1` writes once.
4. On contact update: opportunity UTM trio updates per opportunity. Contact `utm_1` stays locked. The next empty slot (`utm_2`, then `utm_3`, etc.) takes the new trio. Once `utm_5` is full, new events overwrite `utm_5`.
5. Phone-only leads get `utm_medium = phone`, `utm_source = inbound_3cx`. Campaign field stays blank or gets the call-tag if one applies.

### Speed-to-contact

Speed-to-contact target is under 5 minutes for any inbound through TypeForm or website chat. SMS first (T2 auto), call second (T3 SDR within 15 min).

### TypeForm setup

Five forms minimum, conditional logic on. 70% completion baseline (cos.yaml). Required capture per form:

- First name, last name
- Mobile (Australian format validation)
- Email
- Loan purpose (drives ICA best-guess)
- Approximate loan amount (drives ICA tier)
- Employment type (full-time, casual, self-employed). Drives `app_type` (Consumer vs Commercial).
- Consent to contact (Yes / No)
- UTMs (`utm_medium`, `utm_source`, `utm_campaign`) auto-passed from URL params

Magnet forms add magnet-specific qualifying questions. The handbook covers SDR handling per magnet.

### Zapier flow

One Zap per TypeForm. Each Zap:

1. TypeForm submission triggers.
2. Create or update GHL contact (match on email + mobile).
3. Write UTM trio to opportunity. Write trio to contact `utm_1` if new contact, or to the next empty `utm_2`/`utm_3`/`utm_4`/`utm_5` slot if returning.
4. Apply tags from form answers (`brand:ffg`, magnet, ICA best-guess).
5. Move card to T1 stage and fire workflow `entry_pre_sale_ffg`.
6. Push to Slack `#fox-new-leads` for visibility.

Document every Zap. One owner per Zap.

---

## ICA Tagging at Lead Capture (FFG 5-Profile Framework)

At pre-sale we cannot confirm the ICA. We make a best-guess from form data and set `ica_confidence` to `low` until the SDR confirms on the call. The best-guess logic below is operational routing, not a profile. Full ICA definitions live once in Section 2 of the master playbook (`02-ideal-client-profiles-avatars.md`): YPMB, EPFB, PCLRB, BAB, PVB. This guide names them, it does not redefine them.

### Best-guess logic

| Form signal | Likely ICA | Confidence |
|---|---|---|
| Loan purpose = car, age under 30, employment casual or part-time | Young Practical Motor Borrower | Low |
| Loan purpose = personal loan or debt consolidation, age 30-59, full-time | Established Personal Finance Borrower | Low |
| Loan purpose = personal loan, amount $30K+, full-time, mortgaged | Prime Convenience-Led Repeat Borrower | Low |
| Loan purpose = equipment or business vehicle, employment self-employed | Business Asset Borrower | Low |
| Loan purpose = car, age 40-59, full-time, mortgaged | Prime Vehicle Borrower | Low |

SDR confirms on first contact. Confidence flips to `high` and the matching post-call sequence applies. Routing priority breaks ties:

1. Business Asset Borrower
2. Prime Vehicle Borrower
3. Young Practical Motor Borrower
4. Prime Convenience-Led Repeat Borrower
5. Established Personal Finance Borrower

### GHL custom-field set

- `primary_ica` (picklist, 5 options)
- `ica_confidence` (low, medium, high)
- `app_type` (Consumer, Commercial)
- `loan_type` (picklist)
- `loan_amount_band` ($0-15K, $15-30K, $30-50K, $50K+)
- `age_band` (picklist)
- `employment_type` (picklist)
- `residential_status` (renting, mortgaged, owner, with parents)
- `marital_band` (single, partnered)
- `dependants_flag` (Yes, No)
- `business_name` (text, Commercial only)
- `lead_magnet_taken` (multi-select)
- `utm_medium`, `utm_source`, `utm_campaign` (opportunity)
- `utm_1` through `utm_5` (contact, numbered slots, see UTM Tracking section)

Privacy filter applies to all sensitive raw values at import.

---

## Lead Magnet Pre-Sale Flow

Four magnets locked: commercial vehicle, commercial equipment, consumer personal, consumer vehicle.

A magnet lead runs the same pipeline as a generic enquiry. The only difference is the content of T1 and T2. The magnet name and link merge into one template. Everything from T3 onwards is identical, no matter the input.

The magnet form must capture enough to split the lead later (loan amount band + employment type + age band).

### Magnet-to-ICA mapping

| Magnet | Default ICA best-guess | App type |
|---|---|---|
| Commercial vehicle | Business Asset Borrower | Commercial |
| Commercial equipment | Business Asset Borrower | Commercial |
| Consumer personal | Established Personal Finance OR Prime Convenience Repeat (split by amount) | Consumer |
| Consumer vehicle | Young Practical Motor OR Prime Vehicle (split by age + employment) | Consumer |

---

## Speed-to-Contact Triggers

| Source | First touch (SMS) | SDR call attempt |
|---|---|---|
| TypeForm submission | Within 5 minutes, automated (T2) | Within 15 minutes, manual (T3) |
| Phone call missed | Within 2 minutes, automated SMS | Same hour, manual callback |
| Lead magnet opt-in | Within 5 minutes, automated SMS (T2) | Day 1, manual (T3) |

Test the 5-minute trigger weekly. A missed speed-to-contact is a leak. Log it as an incident, not a feature.

---

## N-Series: Post-Cadence Nurture (N15 to N22)

Eight automated touches across Day 7 to Day 180. Mix of email and SMS.

| N# | Day | Action | Channel | Notes |
|---|---|---|---|---|
| N15 | Day 7 | "One thing worth knowing" value-drop email | Email | One tip from the magnet (or generic if no magnet). No pitch. |
| N16 | Day 14 | Rate or market update email | Email | What has shifted. Plain language. |
| N17 | Day 21 | "30-second rate-review" tip email | Email | Action they can take with their existing lender. Trust-building. |
| N18 | Day 30 | Customer story email (anonymised) | Email | Short story of someone in similar shoes who sorted it. |
| N19 | Day 45 | Light SMS check-in | SMS | "Things have shifted. I'll send a quick rundown, ok?" Reply STOP to opt out. |
| N20 | Day 90 | Quarterly market update email | Email | Day 90 clears the legal lead market cooling threshold. |
| N21 | Day 120 | "If you've been thinking about it" email | Email | Soft re-engagement. |
| N22 | Day 180 | Final breakup email | Email | Door-open. Move to Lost or Reactivation cohort. |

Any reply at any N stage moves the card back to Interacting. SDR takes over. Pause N-workflow.

---

## Broker Handoff

Lead assignment and broker routing is Fox internal policy, not something this playbook defines. Rowdie to advise. The process for moving a booked lead from the pre-sale pipeline into broker ownership is not documented yet.

---

## Red Dot Protocol (FFG)

Stage-based SLA enforcement. Every active stage has a target time. Breach the target → dot goes RED or YELLOW. Dot escalates if the dot itself isn't actioned. GHL workflows + native task SLAs run this. No external tooling required.

### Dot legend

- 🔴 **RED dot** = high priority, fast SLA, immediate breach matters (warm leads, replies, missed bookings).
- 🟡 **YELLOW dot** = medium priority, longer SLA, breach is warning.
- 🟢 **GREEN dot** = on track, no action needed.

### SLAs by stage

| Stage | SLA | Dot | Tier 1 alert | Tier 2 alert |
|---|---|---|---|---|
| Interacting (reply detected) | 1 hour (business hours) | 🔴 | SDR at 1hr | Sam Drew at 2hr |
| FUP (waiting on lead) | 24 hours from task fire | 🟡 | SDR at 24hr | Sam Drew at 48hr |
| T3-T5 (Day 1 calls) | 4 hours each after the previous clears | 🟡 | SDR | -- |
| T7-T8 (Day 2 calls) | 6 hours each after T6 fires | 🟡 | SDR | -- |
| T10-T11 (Day 3 calls) | 6 hours each after T9 fires | 🟡 | SDR | -- |
| T13 (Day 4 final call) | 8 hours after T12 fires | 🟡 | SDR | -- |
| Reply from N-series (lands in Interacting) | 1 hour business hours | 🔴 | SDR | Sam Drew at 2hr |
| Online form completed (no contact yet) | 24 hours | 🔴 | SDR | Sam Drew at 24hr |

### Escalation chain (FFG)

Tier 1: SDR → Tier 2: **Sam Drew** (Head of Asset & SME) → Tier 3: **Rowdie Lang** → Tier 4: **Nathan Drew** (systemic issues only).

### GHL implementation

GHL native tasks + workflow timers. Every 15 minutes during business hours, the watcher workflow runs:

1. Query open tasks where `due_at` has passed.
2. For each, compare elapsed time vs the stage SLA above.
3. If breached and `tier_1_notified = false`: GHL notification + dashboard flag to assigned SDR. Set `tier_1_notified = true`.
4. If breached by 2x and `tier_2_notified = false`: notify Sam Drew (email + GHL). Set escalated.
5. If breached by 3x: notify Rowdie.
6. Tier 4 (Nathan) reserved for systemic patterns, not single breaches.

### Business hours

Business hours: **Mon-Fri, 8:30am-5:30pm AEST** (Australia/Brisbane). Outside hours, dots pause and resume at 8:30am next business day.

### Lost reasons (mark Lost, not stage)

Standard list of reasons when marking Lost:

- `Ghosting`, no reply after N22.
- `Settled elsewhere`, lead confirms they sorted it with a competitor.
- `Not a fit`, application would not pass any FFG lender.
- `Spam / bot`, quality-control flag.
- `Opted out`, STOP / unsubscribe.

---

## Automated Scripts (System-Fired Touchpoints)

All automated email and SMS that fire without an SDR pressing send. Voice scripts cover call openers and voicemails.

Brand sender: **Fox Finance Group**. All emails end with the standard ABN + ACL footer.

T1 and T2 are the only touches that vary based on input. The magnet branch swaps the T1 email body for the magnet delivery and tweaks the first T2 SMS to reference the magnet. Everything from T6 onwards is identical across both paths.

**SMS pair timing rule:** wherever an automated SMS pair fires (T2, T6, T9, T12), the second SMS lands one minute after the first. The lead reads them as a single burst. Do not space pairs further apart.

### Compliance footers (apply to every automated send)

These are mandatory on every automated touchpoint. The script templates below show them inline, but the rule is universal — if a new template is added later, these still apply.

- **Every SMS:** must end with `Reply STOP to opt out.` Twilio's STOP keyword handling must be configured so opt-outs flow back into GHL and disable the SMS channel for that contact.
- **Every email:** must include an unsubscribe link in the footer. Australian Spam Act compliance. The standard FFG ABN + ACL footer block already includes this — confirm it renders in every template before launch.
- **First SMS in any new sequence:** the opt-out line must appear in the first send, not just later ones.

Build sign-off should verify both rules on each template before workflows go live.

### T1 auto email (Day 1, 0 min)

Generic enquiry path. Subject: `Got your enquiry, {first_name}`

```
Hey {first_name},

{sdr_first_name} from Fox Finance Group here. Got your enquiry.

I'll give you a quick bell shortly. No impact on your credit score, no commitment.

Cheers,
{sdr_first_name}
Fox Finance Group
{phone}
```

Magnet path. One template, any magnet. Subject: `Your {magnet_name} is here, {first_name}`

```
Hey {first_name},

{sdr_first_name} from Fox Finance Group. Your {magnet_name} is here: {magnet_link}.

I'll give you a quick bell shortly to talk through your options. No impact on your credit score, no commitment.

Cheers,
{sdr_first_name}
Fox Finance Group
{phone}
```

`{magnet_name}` is the magnet's customer-facing name, set at opt-in (for example "Commercial Vehicle Finance Guide"). It carries the asset type in the name, so the same template works for a guide, a calculator, or a video. `{magnet_link}` is the download or tool URL. Both write to the contact from the TypeForm magnet config. Add a magnet by adding its name and link in the config. No new template, no workflow change.

Current magnets: commercial vehicle, commercial equipment, consumer personal loan, consumer vehicle (cos.yaml).

### T2 auto SMS pair

T2a (Day 1, +5 min):

```
Hey {first_name}, {sdr_first_name} from Fox Finance Group. Got your enquiry.
```

T2b (Day 1, +6 min):

```
I'll give you a call shortly, ok?
```

For magnet leads, T2a swaps to reference the magnet:

```
Hey {first_name}, {sdr_first_name} from Fox Finance Group. Your {magnet_name} just landed in your inbox.
```

T2b stays the same.

### T6 auto SMS pair (Day 1, 5:30pm and 5:31pm)

T6a:

```
Hey {first_name}, tried to reach you today again about your enquiry.
```

T6b:

```
{first_name}, would you like to proceed through SMS?
```

### T9 auto SMS pair (Day 2, 5pm and 5:01pm)

By this point the SDR has already introduced themselves at T1 / T2 / T6, so the check-in skips the intro and gets straight to the message.

T9a:

```
Hey {first_name}, just checking in on your enquiry. No stress, no rush.
```

T9b:

```
I'll give you a quick bell tomorrow morning to walk you through it, ok?
```

### T12 auto SMS pair (Day 3, 5pm and 5:01pm)

T12a:

```
You just got a call from me.
```

T12b:

```
If you'd still like to chat, give me a quick reply.
```

### T14 auto breakup email (Day 4, 5pm)

Subject: `Door's always open, {first_name}`

```
Hi {first_name},

I'll stop the calls and emails for now. Things move on, we get it.

If you'd still like to sort your {product}, we're on {phone} or you can grab a time here: {booking_link}.

The door's always open. No expiry.

Cheers,
{sdr_first_name}
Fox Finance Group
```

---

### Booking Confirmation, Reminders and No-Show Recovery

The booking confirmation SMS + email, the pre-call reminders, and the no-show recovery sequence now live in the Closer Booking playbook (`09d-closer-booking.md`). They fire after the SDR books the broker call and the card exits this pipeline.

---

### N-Series Nurture Scripts (N15 to N22)

**N15. Day 7 email**

Subject: `One thing worth knowing, {first_name}`

```
Hi {first_name},

If you're sorting any kind of finance, the most useful thing you can do is have your last three months of bank statements ready. Doesn't matter which lender you go with, they all want to see them.

Once we know your situation, we can match you to a lender that fits. Two minutes on the phone usually does it.

Reply here or grab a time: {booking_link}

Cheers,
{sdr_first_name}
Fox Finance Group
```

**N16. Day 14 email**

Subject: `Quick update on what's moved, {first_name}`

```
Hi {first_name},

A quick rundown on what's shifted in the last fortnight:
- Lender appetite has changed in a few categories
- Rates have moved on some products
- A couple of lenders have new offers worth a look

If you'd like a current snapshot for your situation, hit reply. No pressure, just helpful info.

Cheers,
{sdr_first_name}
Fox Finance Group
```

**N17. Day 21 email**

Subject: `A 30-second move that often pays off`

```
Hi {first_name},

If you've got an existing personal or car loan running, here's something most people don't think to do:

Ring your lender, ask for a rate review, and mention what newer customers are being offered. A fair few will match it.

If they don't, we can take a look at what else is around. No obligation, just a second opinion.

Reply or ring us on {phone}.

Cheers,
{sdr_first_name}
Fox Finance Group
```

**N18. Day 30 email**

Subject: `How a recent client sorted theirs`

```
Hi {first_name},

Quick story.

A client came to us a while back wanting to consolidate a few loans into one. They were paying more than they needed to.

We sorted it in a fortnight. One repayment. Lower total interest. No drama.

If your situation looks anything like that, hit reply and I'll see what's possible for you.

Cheers,
{sdr_first_name}
Fox Finance Group
```

**N19. Day 45 SMS**

```
Hi {first_name}, {sdr_first_name} from Fox Finance Group. Things have shifted on rates and lender options lately. I'll send you a quick rundown, ok? Reply STOP if you'd rather not.
```

**N20. Day 90 email**

Subject: `A quarter on, {first_name}, here's what's changed`

```
Hi {first_name},

It's been a few months since you first got in touch. A lot has moved on rates and lender options in that time.

If your situation has changed, or you're back in the market, hit reply and I'll send you a current snapshot for what fits your circumstances.

If you've sorted it elsewhere, all good. We can still help you check whether your current deal stacks up.

Cheers,
{sdr_first_name}
Fox Finance Group
```

**N21. Day 120 email**

Subject: `If you've been thinking about it`

```
Hi {first_name},

Sometimes the right time isn't day one. Sometimes it's four months later when something shifts.

If you're back to thinking about your {product}, we're here. Two-minute call, we can work out what makes sense for your situation today.

Reply here or ring us on {phone}.

Cheers,
{sdr_first_name}
Fox Finance Group
```

**N22. Day 180 email**

Subject: `Last one from us, {first_name}`

```
Hi {first_name},

I'll stop filling your inbox.

If your situation changes down the track, we're on {phone} and the door's always open. No expiry, no hard feelings.

All the best.

Cheers,
{sdr_first_name}
Fox Finance Group
```

After N22: mark Lost (`Ghosting`) or move to Reactivation Pipeline. Never recycle to T1.

---

*End of FFG Pre-Sales Developer Guide.*
