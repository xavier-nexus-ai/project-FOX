# FHL Pre-Sales Developer Guide

**Brand:** Fox Home Loans (mortgages, refinance, investment property, commercial property)
**Playbook:** Pre-Sales SDR (suffix c)
**Version:** 1.2
**Created:** 2026-05-05
**Owner:** James
**Status:** Draft

---

## Purpose

How an FHL home loan lead moves from first click to a broker call. The build sits in GoHighLevel. TypeForm captures, Zapier routes, GHL holds the pipeline, 3CX takes the call, **Infynity** holds the deal once a broker takes ownership.

FHL pre-sale is different from FFG. The mortgage decision cycle is weeks to months, not days. The cadence stretches further. The classification is by **Purchase Type** (FHB, New Purchase, Refinance, Investor, Commercial). Purchase Type is the FHL operating overlay on the shared ICAs (Section 2); it is not a separate customer framework. The data spine is harder because Infynity has no API.

The SDR-facing companion is the handbook. The FHL script library holds the voice scripts.

In scope: FHL pre-sale lead nurture across all five Purchase Types.

**Convention:** FHL shares the five FFG ICAs. They are defined once in Section 2 (`02-ideal-client-profiles-avatars.md`). Purchase Type is the FHL operating overlay. This playbook names them and points back. It never redefines them.

---

## Pipeline Architecture: T-System (FHL Variant)

T-System (touchpoint-per-stage). Same methodology as FFG. Different cadence and stage count to match the longer mortgage consideration cycle. Automated and manual touches are grouped into linked stages so a single pipeline card moves through the cadence in one continuous flow.

### Stage type legend

| Symbol | Meaning |
|---|---|
| ➡️ | Opportunities are automatically added (webhook, Zapier, form trigger) |
| ⚡️ | Moving a card here triggers an automation (email, SMS, task) |
| 👤 | Manual stage. SDR must action the task. |

### T and N prefixes

- **T-series (T1 to T12):** direct touchpoints. FHL active cadence runs **Day 1 to Day 16** (longer than FFG's 4 days, mirrors existing FHL SendGrid "No Customer Contact" schedule of Instant, Day 2, 5, 9, 16).
- **N-series (N13 to N22):** post-cadence automated nurture, **Day 21 to Day 270**. Long-tail because mortgage consideration is 3-6 months.

### FHL Pre-Sale SDR Pipeline

Linked stages keep the card moving without dropping it between automated and manual touches.

| # | Stage | Type | Description |
|---|---|---|---|
| 1 | Interacting | ➡️ ⚡️ | Inbound reply detected. 24hr RED dot. SDR actions and either books the appointment (card exits to Closer Pipeline) or moves to FUP. |
| 2 | FUP | 👤 | SDR-parked card after we've responded. Scheduled follow-up task. 24hr YELLOW dot from task fire time. |
| 3 | T1-T2 | ⚡️ | Day 1. Auto email (T1) then auto SMS pair (T2a + T2b). T1 and T2 are the only touches that vary based on input (Purchase Type if known at intake). |
| 4 | T3-T5 | 👤 | Day 1 morning, Day 1 afternoon (voicemail), Day 2 morning (voicemail). Three manual SDR calls. |
| 5 | T6 | ⚡️ | Day 2 afternoon. Auto SMS pair after no-answer cycle. |
| 6 | T7 | 👤 | Day 5. SDR call attempt + breakup voicemail. |
| 7 | T8 | ⚡️ | Day 5 same day. Auto email with booking link. |
| 8 | T9 | 👤 | Day 9. SDR final call + "your file stays open" voicemail. |
| 9 | T10-T11 | ⚡️ | Day 9 same day. Auto email (T10) then auto SMS pair (T11a + T11b). |
| 10 | T12 | ⚡️ | Day 16. Final auto email (matches existing FHL "No Customer Contact" Day 16). |
| 11 | N13-N22 | ⚡️ | Day 21 to Day 270. Ten automated nurture touches, Purchase Type-targeted. |

A booked broker appointment exits the card to the Closer Pipeline. There is no Engaged, Qualified, or Booked Out stage inside this pipeline. Any inbound reply moves the card to Interacting (see below).

### Interacting vs FUP

Stage 1 and Stage 2. Both stay. They are not interchangeable.

| Stage | What it holds | Who moves the card here | SDR SLA |
|---|---|---|---|
| 1. Interacting | Leads actively interacting. The lead's reply was the last action. We owe them a response. | GHL, automatically, on any inbound reply | Action same day. 24hr RED dot. |
| 2. FUP | Follow-ups. Our response was the last action. We are waiting on the lead, with a scheduled follow-up task. | SDR, manually, after responding | Task fires on the scheduled day. 24hr YELLOW dot if not actioned. |

**Auto-move rule (GHL workflow):**

- Any inbound reply (email or SMS) from a lead in this pipeline moves the card to Interacting automatically. The SDR does not move it.
- This applies from any stage. If the card is in FUP and the lead replies, it moves FUP to Interacting. FUP never holds a card with an unread reply.
- The card stays in Interacting until the SDR actions it: book the appointment (card exits to the Closer Pipeline) or respond and park it in FUP with a scheduled follow-up.

Rule of thumb: Interacting = "their move was last, we act". FUP = "our move was last, GHL reminds us".

### Auto-Advance Rule

Manual call stages (T3-T5, T7, T9) auto-advance when the SDR logs a disposition of `No Answer` or `Voicemail Left`. GHL detects the disposition and moves the card forward.

If the SDR logs `Connected`, `Booked`, `Not Interested`, or `Wrong Number`, the card does NOT auto-advance. SDR moves it manually per disposition.

### What is NOT a stage

- **Booked / SQL.** Booked exits to Closer Pipeline.
- **Lost / Won.** GHL statuses, not stages.
- **No-Show Recovery.** Sub-flow inside Closer Pipeline.

### Unreachable Lead Protocol

After N22 (Day 270) with no reply:

1. Mark **Lost** with reason `Ghosting`, or
2. Move to long-tail "Cold Lead" nurture (existing FHL automation: 7 emails over 2 years, 55.7% open rate). Catch-all only. Do not actively re-pipeline.

**Never recycle to T1.**

---

## UTM Tracking

UTMs replace the old lead source field. The opportunity holds the UTM trio (medium, source, campaign) for the touchpoint that created it. The contact holds the same trio for the first touch PLUS numbered slots for every subsequent interaction, so we can see every channel a lead has touched over time.

### What we capture

**On the opportunity (single trio):**

| Field | Example |
|---|---|
| `utm_medium` | `cpc`, `social`, `email`, `phone`, `referral`, `cross_sell` |
| `utm_source` | `google`, `facebook`, `fhl_website`, `direct`, `ffg`, `partner_name` |
| `utm_campaign` | `fhb_grants_2026`, `refinance_q1`, `brand` |

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
6. Cross-sell from FFG: `utm_medium = cross_sell`, `utm_source = ffg`, campaign = the FFG playbook reference.
7. Partner referrals (real estate agent, conveyancer): `utm_medium = referral`, `utm_source = partner_name`.

### Speed-to-contact

Speed-to-contact target is under 5 minutes inside business hours. Mortgage leads tend to research before they enquire, they're warm.

### TypeForm setup (FHL)

FHL TypeForm captures Purchase Type signal at intake where possible:

- First name, last name
- Mobile (Australian format validation)
- Email
- "What brings you to Fox Home Loans today?" (drives Purchase Type best-guess: Buying first home / Buying a home / Looking at rates / Investment property / Commercial property / Not sure)
- Approximate loan amount or property price
- Employment type (PAYG / self-employed)
- Timeline (just exploring / pre-approval / under contract / fixed expiring soon)
- Consent to contact (Yes / No)
- UTMs (`utm_medium`, `utm_source`, `utm_campaign`) auto-passed from URL params

### Zapier flow

1. TypeForm submission triggers.
2. Create or update GHL contact (match on email + mobile).
3. Write UTM trio to opportunity. Write trio to contact `utm_1` if new contact, or to the next empty `utm_2`/`utm_3`/`utm_4`/`utm_5` slot if returning.
4. Apply tags from form answers (`brand:fhl`, Purchase Type best-guess).
5. Move card to T1 stage and fire workflow `entry_pre_sale_fhl`.
6. Push to Slack `#fox-new-leads-fhl` for visibility.

---

## Purchase Type Tagging at Lead Capture (FHL)

FHL classifies by **Purchase Type** for day-to-day work: FHB, New Purchase, Refinance, Investor, Commercial. The underlying customer is the same human as the five FFG ICAs in Section 2 of the master playbook (`02-ideal-client-profiles-avatars.md`); only the purchase differs. The ICA-to-FHL mapping lives once in Section 2. This guide keeps Purchase Type as its operating overlay and points back for the human profile. It never redefines either. Five categories per cos.yaml `fhl_purchase_type_mapping`.

### Best-guess from form data

| Form signal | Likely Purchase Type | Confidence |
|---|---|---|
| "Buying first home" | First Home Buyer | Medium |
| "Buying a home" + already owns property | New Purchase | Low |
| "Looking at rates" / "Checking options" + has existing mortgage | Refinance | Medium |
| "Investment property" | Investor | Medium |
| "Commercial property" | Commercial | High |
| "Not sure / exploring" | New Purchase (default) | Low |

SDR confirms on first call via the Q1 decision tree. Confidence flips to `high` once confirmed and the matching post-call sequence applies.

### Q2: Segmentation tag capture (during qualification)

These tags drive every downstream lifecycle touchpoint. SDR MUST capture during the qualification call.

| Tag | What to capture | Used at |
|---|---|---|
| `purchase_type` | FHB / New Purchase / Refinance / Investor / Commercial | Every lifecycle touchpoint |
| `employment_band` | PAYG / Self-employed | Repricing approach varies |
| `household` | Single / Couple / Dependants flag | Cross-sell targeting |
| `likely_next_needs` | Vehicle, equipment, consolidation, other | FFG cross-sell flagging |
| `product_preference` | Fixed / Variable / Split / Offset / IO / OO + key dates | Action Window triggers |
| `urgency` | Just exploring / Pre-approval needed / Under contract / Fixed expiring | Nurture intensity |

### GHL custom-field set

- `purchase_type` (picklist, 5 options + "Not yet classified")
- `purchase_type_confidence` (low, medium, high)
- `employment_band` (PAYG, Self-employed)
- `household` (single, couple, with dependants)
- `likely_next_needs` (multi-select)
- `product_preference` (multi-select)
- `urgency` (picklist)
- `loan_amount_band` ($0-500K, $500K-1M, $1M-2M, $2M+)
- `utm_medium`, `utm_source`, `utm_campaign` (opportunity)
- `utm_1` through `utm_5` (contact, numbered slots, see UTM Tracking section)
- `partner_name` (text, populated when partner referral)

---

## Speed-to-Contact Triggers (FHL)

| Source | First touch (SMS) | SDR call attempt |
|---|---|---|
| TypeForm submission | Within 5 minutes, automated (T2) | Within 30 minutes, manual (T3) |
| Phone call missed | Within 2 minutes, automated SMS | Same hour, manual callback |
| Cross-sell from FFG | Within 5 minutes, automated SMS | Same business day, manual |
| Real estate / conveyancer referral | Within 5 minutes, automated SMS + tag partner | Same business day, prioritised |

FHL allows a slightly longer first-call window than FFG (30 min vs 15 min) because the SDR often needs to review the property and amount context before calling. Speed still matters.

---

## N-Series: Post-Cadence Nurture (N13 to N22, FHL)

Ten automated touches across Day 21 to Day 270. Purchase Type-targeted. Mortgage decisions take time. The job is to stay useful and present without pushing.

### Short-term nurture (Weeks 3-4)

| N# | Day | Channel | Content theme | Purchase Type personalisation |
|---|---|---|---|---|
| N13 | 21 | Email | Educational value | FHB: "Deposit basics explained" / New Purchase: "Borrowing power snapshot" / Refinance: "Rate health check guide" / Investor: "Portfolio strategy check" / Commercial: "What lenders look for" |
| N14 | 28 | SMS | Social proof | "Another QLD family settled with us. See their story: {link}" |
| N15 | 35 | Email | Value-add offer | "Free borrowing power check via our Cotality tool. No credit impact. Send me the property address and I'll run it." |

### Medium-term nurture (Months 2-3)

| N# | Day | Channel | Content theme | Purchase Type personalisation |
|---|---|---|---|---|
| N16 | 50 | Email | Market update | FHB: grants and changes / New Purchase: local market / Refinance: rate movements / Investor: rental yield / Commercial: lending update |
| N17 | 70 | SMS | Soft check-in | "Still thinking about your home loan? No rush. We're here when you're ready. {sdr_first_name}, Fox Home Loans" |
| N18 | 90 | Email | Case study | FHB success / Investor portfolio growth / Refinance savings story |
| N19 | 110 | Email | Repricing or rate update | FHB: "How much deposit do you really need?" / Refinance: "Quarterly rate check" / Investor: "Interest-only vs P&I" |

### Long-term nurture (Months 4-9)

| N# | Day | Channel | Content theme | Purchase Type personalisation |
|---|---|---|---|---|
| N20 | 150 | Email | Seasonal / timely | Property market trends, tax time tips, government scheme updates |
| N21 | 200 | SMS | Re-engagement | "Checking in. If your plans have changed, that's okay. If not, we'd love to help. Reply CALL." |
| N22 | 270 | Email | Final nurture | "Your file is still open. One click to restart: {booking_link}." |

After N22 (Day 270): no response → move to existing FHL "Cold Lead" automation (catch-all, 55.7% open rate, runs 2 years). Do not actively re-pipeline.

Any reply at any N stage moves the card back to Interacting. SDR takes over.

---

## Broker Handoff

Lead assignment and broker routing is Fox internal policy, not something this playbook defines. Rowdie to advise. The process for moving a booked lead from the pre-sale pipeline into broker ownership is not documented yet.

### Infynity Data Bridge (No API)

**The constraint:** Infynity (FHL aggregator) has no API. Per cos.yaml `2026-04-27` decision: LMG switch is off the table. Data flows via CSV.

**Workflow:**
1. Weekly CSV export from Infynity (broker or admin task).
2. CSV import workflow parses, matches to GHL contact records on email + name.
3. Settlement detection triggers downstream lifecycle.
4. Loan product details (rate, term, fixed expiry, lender) populated into GHL custom fields.

Minimum CSV fields required:

- Customer name + contact details (matching key)
- Settlement date
- Loan amount, rate, product type, term
- Lender name
- Property address
- Fixed rate expiry date if applicable

CSV format and export cadence to be confirmed during build.

---

## Cotality Integration (FHL Pre-Sale Value-Add)

Cotality property valuation tool. Subscription already paid for (cos.yaml). Generates a market appraisal in 1 minute. Used pre-sale as a trust-building free value-add.

### Pre-sale use cases

- **Refinance leads**: send a Cotality valuation as part of N15 (Day 35 value-add offer). Shows equity position. Builds trust without pressure.
- **Investor leads**: portfolio property valuations on request.
- **New Purchase / FHB**: not used pre-sale (no property to value yet).

### Workflow

1. Lead opts in to "free borrowing power check" or "free property valuation" CTA in N15 or T8.
2. SDR generates Cotality report (1 minute turnaround).
3. Auto email delivers the report with a "happy to walk you through this" CTA.
4. Any reply moves the card to Interacting. SDR takes over.

API integration TBC. Manual SDR generation works as interim per cos.yaml.

---

## Red Dot Protocol (FHL)

Stage-based SLA enforcement. Same dot logic as FFG. Different escalation chain.

### Dot legend

- 🔴 **RED dot** = high priority, fast SLA.
- 🟡 **YELLOW dot** = medium priority, longer SLA, breach is a warning.
- 🟢 **GREEN dot** = on track.

### SLAs by stage (FHL)

| Stage | SLA | Dot | Tier 1 alert | Tier 2 alert |
|---|---|---|---|---|
| Interacting (reply detected) | 1 hour business hours | 🔴 | Broker | Bill Robb at 2hr |
| FUP (waiting on lead) | 24 hours from task fire | 🟡 | Broker at 24hr | Bill Robb at 48hr |
| T3-T5 (Day 1-2 calls) | 4 hours each after the previous clears | 🔴 / 🟡 | Broker | -- |
| T7 (Day 5 call + voicemail) | 4 hours after T6 fires | 🟡 | Broker | -- |
| T9 (Day 9 final call + voicemail) | 4 hours after T8 fires | 🟡 | Broker | -- |
| Reply from N-series (lands in Interacting) | 1 hour business hours | 🔴 | Broker | Bill Robb at 2hr |
| Pre-Appointment (no-show) | 1 hour after missed appointment | 🔴 | Broker | -- |
| High-value (>$800K loan) | Immediate | 🔴 | Bill Robb notified on creation | -- |
| Tags incomplete at handoff | Immediate | 🔴 | Broker, lifecycle cannot personalise without tags | -- |
| FFG referral (cross-sell from FFG) | Same business day | 🔴 | Broker, Bill Robb notified | -- |

### Escalation chain (FHL)

Tier 1: Broker → Tier 2: **Bill Robb** (Head of Home Loans / Partnerships) → Tier 3: **Rowdie Lang** → Tier 4: **Nathan Drew** (systemic only).

### Business hours

Mon-Fri, 8:30am-5:30pm AEST. Outside hours, dots pause and resume at 8:30am next business day.

### Lost reasons (FHL)

- `Ghosting`, no reply after N22.
- `Settled elsewhere`, lead confirms competitor.
- `Not eligible`, application would not pass any FHL lender (e.g. LVR, serviceability).
- `Spam / bot`, quality-control flag.
- `Opted out`, STOP / unsubscribe.
- `Wrong product`, better fit for FFG (cross-back to FFG playbook).

---

## Automated Scripts (System-Fired Touchpoints)

All automated email and SMS that fire without a broker pressing send. Voice scripts cover call openers and voicemails. The broker handoff brief lives in the handbook.

Brand sender: **Fox Home Loans**. All emails carry the standard FHL ABN + ACL footer.

T1 and T2 are the only touches that vary based on input (Purchase Type if known at intake). Everything from T6 onwards is identical regardless of Purchase Type.

**SMS pair timing rule:** wherever an automated SMS pair fires (T2, T6, T11), the second SMS lands one minute after the first. The lead reads them as a single burst. Do not space pairs further apart.

### Compliance footers (apply to every automated send)

These are mandatory on every automated touchpoint. The script templates below show them inline, but the rule is universal — if a new template is added later, these still apply.

- **Every SMS:** must end with `Reply STOP to opt out.` Twilio's STOP keyword handling must be configured so opt-outs flow back into GHL and disable the SMS channel for that contact.
- **Every email:** must include an unsubscribe link in the footer. Australian Spam Act compliance. The standard FHL ABN + ACL footer block already includes this — confirm it renders in every template before launch.
- **First SMS in any new sequence:** the opt-out line must appear in the first send, not just later ones.

Build sign-off should verify both rules on each template before workflows go live.

### T1 auto email (Day 1, 0 min)

Generic version. Subject: `Got your enquiry, {first_name}`

```
Hey {first_name},

{sdr_first_name} from Fox Home Loans here. Got your home loan enquiry.

I'll give you a quick bell shortly.

Cheers,
{sdr_first_name}
Fox Home Loans
{phone}
```

Where Purchase Type is known at intake, swap the second line for the matching variant.

FHB:

```
Got your first home loan enquiry. We'll keep this simple.
```

Refinance:

```
Got your refinance enquiry. We'll have a quick look at what's possible for you.
```

Investor:

```
Got your investment lending enquiry. We'll talk through what each lender will do for your situation.
```

Commercial:

```
Got your commercial finance enquiry. We'll walk you through what's realistic.
```

New Purchase:

```
Got your home loan enquiry. We'll help you map out the next step.
```

### T2 auto SMS pair

T2a (Day 1, +5 min):

```
Hey {first_name}, {sdr_first_name} from Fox Home Loans. Got your enquiry. Reply STOP to opt out.
```

T2b (Day 1, +6 min):

```
I'll give you a call shortly, ok?
```

### T6 auto SMS pair (Day 2 afternoon)

T6a:

```
Hey {first_name}, tried to reach you again about your home loan enquiry.
```

T6b:

```
If it's easier, {first_name}, just reply here and we'll sort it from your phone. Reply STOP to opt out.
```

### T8 auto email (Day 5)

Subject: `Still here when you're ready, {first_name}`

```
Hi {first_name},

Mortgage decisions take time. Plenty of people we work with take a few weeks to weigh things up.

Whenever you're ready for a chat, here's the link: {booking_link}

If there's a specific question I can help with by email, just hit reply.

Cheers,
{sdr_first_name}
Fox Home Loans
```

### T10 auto email (Day 9)

Subject: `Open door, {first_name}`

```
Hi {first_name},

It's been about a week since you reached out. No follow-up needed if the timing isn't right. Things change.

If your situation has shifted or you'd like a hand, we're here. {phone} or {booking_link}.

Cheers,
{sdr_first_name}
Fox Home Loans
```

### T11 auto SMS pair (Day 9)

T11a:

```
Hi {first_name}, {sdr_first_name} from Fox Home Loans, just tried you again about your home loan.
```

T11b:

```
If you'd still like a hand, give me a quick reply and I'll sort a time.
```

### T12 auto breakup email (Day 16)

Subject: `Door's always open, {first_name}`

```
Hi {first_name},

I'll stop the follow-ups. The door's always open at Fox Home Loans.

If something changes down the track, we're on {phone}. No expiry.

Cheers,
{sdr_first_name}
Fox Home Loans
```

---

### Booking Confirmation, Reminders and No-Show Recovery

The booking confirmation SMS + email, the pre-appointment reminders, and the no-show recovery sequence now live in the Closer Booking playbook (`09d-closer-booking.md`). They fire after the SDR books the appointment and the card exits this pipeline.

---

### N-Series Nurture Scripts (N13 to N22)

**N13. Day 21 educational email (Purchase Type-specific)**

FHB. Subject: `Deposit basics, plain English`

```
Hi {first_name},

Quick rundown on deposits.

You usually need 5% to 20% of the property price. Less than 20% means you'll likely pay LMI (lender's mortgage insurance, a one-off cost that lets you borrow more without 20% saved).

Government schemes change the maths. The First Home Buyer Scheme can let you buy with 5% and skip LMI if you qualify. Worth checking.

Want to know what you could borrow with what you've got? Reply REVIEW and I'll run a quick check, no credit hit.

Cheers,
{sdr_first_name}
Fox Home Loans
```

Refinance. Subject: `Rate health check, plain English`

```
Hi {first_name},

Quick rundown on whether refinancing actually saves money.

Three things to check:
- Your current rate vs what's around now
- Fees on the new loan (and any exit fees on the old one)
- Loan features (offset, redraw, fixed vs variable)

Sometimes the savings stack up. Sometimes they don't. The only way to know is to actually look.

Want a free Cotality property valuation to see your equity position? Reply VAL and I'll send it over. No commitment.

Cheers,
{sdr_first_name}
Fox Home Loans
```

Investor. Subject: `Investor lending basics`

```
Hi {first_name},

Investor lending has its own rules. Lenders look at rental income (usually 70-80% counted), tax position, and how this property fits your portfolio cash flow.

Three structure choices most investors weigh up:
- Interest-only vs principal and interest
- Offset vs redraw
- Fixed vs variable

The right answer depends on your strategy, not a rule.

Happy to walk through what each lender will do for your situation. Reply CHAT or grab a time: {booking_link}

Cheers,
{sdr_first_name}
Fox Home Loans
```

New Purchase and Commercial: mirror the same structure with Purchase Type-specific content.

**N14. Day 28 social proof SMS**

```
Hi {first_name}, thought you'd like this. Quick story from a recent Fox Home Loans client: {story_link}. Reply STOP to opt out.
```

**N15. Day 35 value-add offer email**

Subject: `A free property check, no strings`

```
Hi {first_name},

We use a tool called Cotality that gives you a market appraisal on any property in 1 minute. We're happy to run one for you.

What you get:
- Estimated current market value
- Recent comparable sales
- Suburb trend snapshot

No credit check. No commitment. Just useful information for whatever you're weighing up.

Reply VAL with the property address and I'll send it through.

Cheers,
{sdr_first_name}
Fox Home Loans
```

**N16. Day 50 market update email (Purchase Type-specific)**

Topics by type:
- FHB: "First home buyer grants and what's changed this quarter"
- New Purchase: "What's happening in your local market"
- Refinance: "Rate movements this quarter"
- Investor: "Rental yield trends"
- Commercial: "Commercial lending update"

**N17. Day 70 soft check-in SMS**

```
Hi {first_name}, {sdr_first_name} from Fox Home Loans. Still thinking about your home loan? No rush. We're here when you're ready. Reply STOP to opt out.
```

**N18. Day 90 case study email**

Anonymised customer story by Purchase Type. Same shape as FFG N18. One client, one situation, one outcome.

**N19. Day 110 repricing or rate update email**

Topics by type:
- FHB: "How much deposit do you really need? (the answer most people get wrong)"
- Refinance: "Quarterly rate check, here's what moved"
- Investor: "Interest-only vs principal and interest, which makes sense right now?"

**N20. Day 150 seasonal / timely email**

Property market seasonal trends, tax time tips, government scheme updates. Generic across Purchase Types.

**N21. Day 200 re-engagement SMS**

```
Hi {first_name}, checking in. If your plans have changed, that's okay. If not, we'd love to help. Reply CALL and I'll reach out. Reply STOP to opt out.
```

**N22. Day 270 final nurture email**

Subject: `Your file is still open, {first_name}`

```
Hi {first_name},

It's been a while. I'll stop the regular updates from here.

Your file is still open. If your situation changes or the timing works, we're on {phone} or {booking_link}.

If you'd rather we updated your preferences, reply REMOVE and we'll take care of it.

All the best.

Cheers,
{sdr_first_name}
Fox Home Loans
```

After N22: no reply → move to long-tail "Cold Lead" automation (existing FHL sequence: 7 emails over 2 years, 55.7% open rate). Do not actively re-pipeline.

---

*End of FHL Pre-Sales Developer Guide.*
