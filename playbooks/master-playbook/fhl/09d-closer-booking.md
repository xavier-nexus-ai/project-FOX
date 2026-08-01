# FHL Closer Booking

**Brand:** Fox Home Loans (mortgages, refinance, investment property, commercial property)
**Playbook:** Closer Booking (suffix d)
**Version:** 1.0
**Created:** 2026-05-19
**Owner:** James
**Status:** Draft

---

## Purpose

This is the booking-call layer. It fires once the SDR books the broker appointment and the card exits the pre-sale pipeline. It is NOT the full closing process. Fox owns that. Scope here is the booking confirmation, the pre-appointment reminders, and no-show recovery only.

For FHL a broker appointment is a closing appointment. Everything in this doc sits with that appointment.

---

## Closer Booking Pipeline (FHL)

A small pipeline. It picks up the card the moment the SDR books the broker appointment and ends when the lead either attends or is closed off.

### Stage type legend

| Symbol | Meaning |
|---|---|
| ➡️ | Opportunities are automatically added (the card arrives here when the SDR books) |
| ⚡️ | Moving a card here triggers an automation (email, SMS, task) |
| 👤 | Manual stage. SDR must action the task to move the card. |

### Stages

| # | Stage | Type | Description |
|---|---|---|---|
| 1 | Booked | ➡️ ⚡️ | Card arrives when the SDR books the broker appointment. Booking confirmation SMS + email fire on entry. |
| 2 | Confirmed | ⚡️ | 24hr reminder SMS fires. |
| 3 | Reminded | ⚡️ | 2hr reminder SMS + 1hr-before email fire. |
| 4 | Attended | 👤 | Lead showed for the appointment. SDR marks attended. Card exits to Fox's own closing process. |
| 5 | No-Show | ⚡️ | Appointment missed. No-show recovery sequence fires. |
| 6 | No-Show Recovery | 👤 | SDR owns the recovery thread, not the broker. SDR works the recovery, then either re-books (card returns to Booked) or marks Lost. |

The SDR owns the no-show recovery thread, not the broker. After recovery with no result, mark **Lost** (reason `Ghosting`). Never recycle a card back into the pre-sale cadence.

---

## Pre-Appointment Sequence (Show-Up Rate)

Pre-call SMS + email sequence highlights:

- **Confirmation** (instant after booking): SMS + email confirming time, broker, what to bring.
- **24hr reminder** SMS.
- **2hr reminder** SMS with "call {broker_direct} if anything changes."

Optional identity-framing email between confirmation and 24hr reminder. Topics:

- FHB: "What first home buyers wish they knew before their broker meeting"
- Refinance: "3 questions to ask your broker about refinancing"
- Investor: "How smart investors structure their lending"

---

## Pre-Appointment Automated Sequences

**Booking confirmation SMS (instant)**

```
You're booked, {first_name}. {broker_first_name} from Fox Home Loans on {calendar_date_time}. Save {phone}. Reply STOP to opt out.
```

**Booking confirmation email (instant)**

Subject: `You're booked in, {first_name}`

```
Hi {first_name},

You're locked in with {broker_first_name} on {calendar_date_time}.

What to expect:
- A 30-minute appointment. We'll talk through your situation, run the numbers, and answer everything.
- No pressure to decide on the call.
- {broker_first_name} will already have your details.

What to bring (or have handy):
- Photo ID
- 2 recent payslips (or 2 years tax returns + financials if self-employed)
- 3 months bank statements (all accounts)

If something comes up and you need to reschedule, reply to this email or grab a new time: {booking_link}

Cheers,
{sdr_first_name}
Fox Home Loans
```

**24hr reminder SMS**

```
Hi {first_name}, quick reminder: chat with {broker_first_name} from Fox Home Loans on {calendar_date_time}. All good to go ahead? Reply STOP to opt out.
```

**2hr reminder SMS**

```
Hey {first_name}, {broker_first_name} from Fox Home Loans giving you a buzz in about 2 hours at {calendar_date_time}. Talk soon. Reply STOP to opt out.
```

**1hr-before email**

Subject: `Quick read before our chat, {first_name}`

```
Hi {first_name},

Looking forward to our chat at {calendar_date_time}.

You don't need to prepare anything. Just be ready to chat about where you're at, what you're trying to sort, and what's on your mind.

Cheers,
{sdr_first_name}
Fox Home Loans
```

---

## No-Show Recovery

A missed appointment is not lost. Recovery starts immediately and mirrors FFG.

Tone: no guilt, no pressure, "things come up."

---

## Automated No-Show Recovery

Fires when the booked appointment is missed.

**2min after missed appointment SMS**

```
Hey {first_name}, {sdr_first_name} from Fox Home Loans, I'm here ready when you are. Want me to send the link through again? Reply STOP to opt out.
```

**1hr after missed email**

Subject: `Still on for our chat, {first_name}?`

```
Hi {first_name},

We had a chat locked in but didn't get to connect. No worries, easy to sort.

Two options if you want to pick it up:
- Tomorrow morning, 9am
- Tomorrow afternoon, 2pm

Reply with whichever works, or grab a different time: {booking_link}

Cheers,
{sdr_first_name}
Fox Home Loans
```

**Same day 5pm SMS**

```
Hi {first_name}, reckon tomorrow morning works better? Got 9am free. Reply STOP to opt out.
```

**Day 3 door-open email**

Subject: `No stress, {first_name}`

```
Hi {first_name},

I'll leave it with you. Life gets busy.

If you'd still like to sort your {product}, we're on {phone} or {booking_link}. The door's always open.

Cheers,
{sdr_first_name}
Fox Home Loans
```

---

## No-Show Recovery Voicemail (Day 2)

```script
Hey {first_name}, {your_first_name} from Fox Home Loans. Sorry we didn't connect yesterday. Give me a ring on {phone} when it suits and we'll find a time that works. No rush. Cheers.
```

---

## Compliance Footers

These apply to every automated send in this layer, same rule as the pre-sale playbook.

- **Every SMS:** must end with `Reply STOP to opt out.` Twilio's STOP keyword handling must be configured so opt-outs flow back into GHL and disable the SMS channel for that contact.
- **Every email:** must include an unsubscribe link in the footer. Australian Spam Act compliance. The standard FHL ABN + ACL footer block already includes this. Confirm it renders in every template before launch.

Build sign-off should verify both rules on each template before workflows go live.

---

*End of FHL Closer Booking.*
