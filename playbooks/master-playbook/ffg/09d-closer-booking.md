# FFG Closer Booking

**Brand:** Fox Finance Group (asset finance)
**Playbook:** Closer Booking (suffix d)
**Version:** 1.0
**Created:** 2026-05-19
**Owner:** James
**Status:** Draft

---

## Purpose

This is the booking-call layer. It fires once the SDR books the broker call and the card exits the pre-sale pipeline. It is NOT the full closing process. Fox owns that. Scope here is the booking confirmation, the pre-call reminders, and no-show recovery only.

For FFG a broker call is a closing call. Everything in this doc sits with that call.

---

## Closer Booking Pipeline (FFG)

A small pipeline. It picks up the card the moment the SDR books the broker call and ends when the lead either attends or is closed off.

### Stage type legend

| Symbol | Meaning |
|---|---|
| ➡️ | Opportunities are automatically added (the card arrives here when the SDR books) |
| ⚡️ | Moving a card here triggers an automation (email, SMS, task) |
| 👤 | Manual stage. SDR must action the task to move the card. |

### Stages

| # | Stage | Type | Description |
|---|---|---|---|
| 1 | Booked | ➡️ ⚡️ | Card arrives when the SDR books the broker call. Booking confirmation SMS + email fire on entry. |
| 2 | Confirmed | ⚡️ | 24hr reminder SMS fires. |
| 3 | Reminded | ⚡️ | 1hr-before email + 1hr-before SMS fire. |
| 4 | Attended | 👤 | Lead showed for the broker call. SDR marks attended. Card exits to Fox's own closing process. |
| 5 | No-Show | ⚡️ | Broker call missed. No-show recovery sequence fires. |
| 6 | No-Show Recovery | 👤 | SDR owns the recovery thread, not the broker. SDR works the recovery, then either re-books (card returns to Booked) or marks Lost. |

The SDR owns the no-show recovery thread, not the broker. After recovery with no result, mark **Lost** (reason `Ghosting`). Never recycle a card back into the pre-sale cadence.

---

## Pre-Call Automated Sequences

**Booking confirmation SMS (instant)**

```
You're booked, {first_name}. {broker_first_name} from Fox Finance Group will call you on {calendar_date_time}. Save the number {phone}. Reply STOP to opt out.
```

**Booking confirmation email (instant)**

Subject: `You're booked in, {first_name}`

```
Hi {first_name},

You're locked in for a chat with {broker_first_name} on {calendar_date_time}.

What to expect:
- A 15 minute call. We'll talk through your situation and your options.
- {broker_first_name} will already have your details. You won't have to repeat yourself.
- No pressure to decide on the call. We just want you to walk away knowing where you stand.

If something comes up and you need to reschedule, just reply to this email or grab a new time: {booking_link}

Cheers,
{sdr_first_name}
Fox Finance Group
```

**24hr reminder SMS**

```
Hi {first_name}, quick reminder: chat with {broker_first_name} from Fox on {calendar_date_time}. All good to go ahead?
```

**1hr-before email (identity framing)**

Subject: `Quick read before our chat, {first_name}`

```
Hi {first_name},

Looking forward to our chat at {calendar_date_time}.

Most people I speak to are sorting one of three things: getting ahead, getting unstuck, or making a smart move at the right time. Wherever you sit, our job is to help you figure out the next step.

You don't need to prepare anything. Just be ready to chat about what you're trying to sort.

Cheers,
{sdr_first_name}
Fox Finance Group
```

**1hr-before SMS**

```
Hey {first_name}, {broker_first_name} from Fox will give you a buzz in about an hour at {calendar_date_time}. Talk soon.
```

---

## Automated No-Show Recovery

Fires when the booked broker call is missed. SDR owns the recovery thread, not the broker.

**2min after missed call SMS**

```
Hey {first_name}, just so you know, I'm here waiting for you. Do you want me to re-send you the link?
```

**1hr after missed call email**

Subject: `Still on for our chat, {first_name}?`

```
Hi {first_name},

We had a chat locked in but didn't get to connect. No worries, easy to sort.

Two options if you want to pick it up:
- Tomorrow morning, 9am
- Tomorrow afternoon, 2pm

Reply with whichever works, or grab a different time here: {booking_link}

Cheers,
{sdr_first_name}
Fox Finance Group
```

**Same day 5pm SMS**

```
Hi {first_name}, reckon tomorrow morning works better for that finance chat? Got 9am free if it suits.
```

**Day 3 door-open email**

Subject: `No stress, {first_name}`

```
Hi {first_name},

I'll leave it with you. Life gets busy.

If you'd still like to sort your {product}, we're on {phone} or {booking_link}. The door's always open.

Cheers,
{sdr_first_name}
Fox Finance Group
```

---

## No-Show Recovery Voicemail (Day 2)

Leave this if no answer on the Day 2 follow-up call after a missed broker appointment.

```script
Hey {first_name}, {your_first_name} from Fox Finance Group. Sorry we didn't connect yesterday. Give me a ring on {phone} when it suits and we'll find a time that works. No rush. Cheers.
```

---

## Compliance Footers

These apply to every automated send in this layer, same rule as the pre-sale playbook.

- **Every SMS:** must end with `Reply STOP to opt out.` Twilio's STOP keyword handling must be configured so opt-outs flow back into GHL and disable the SMS channel for that contact.
- **Every email:** must include an unsubscribe link in the footer. Australian Spam Act compliance. The standard FFG ABN + ACL footer block already includes this. Confirm it renders in every template before launch.

Build sign-off should verify both rules on each template before workflows go live.

---

*End of FFG Closer Booking.*
