# FFG Pre-Sales Scripts

**Brand:** Fox Finance Group (asset finance)
**Playbook:** Pre-Sales SDR (suffix c)
**Version:** 1.1
**Created:** 2026-05-05
**Owner:** James
**Status:** Draft

---

## Purpose

Voice scripts only. Phone call openers, voicemails, BAMFAM booking, and reactivation call scripts. Automated email and SMS touchpoints live in the developer guide. The broker handoff brief lives in the handbook.

Standards: Australian English. Third-grade reading level. Zero em dashes. No banned words. SDR not setter.

Sender phone in voicemails: `07 3505 3099` (cos.yaml `ffg_sales_process_scripts` Doc 8).

---

## SDR Call Openers

Use the opener that matches the lead magnet (or generic if no magnet). UTMs on the contact record tell you which path the lead came in through. These openers apply at T3, T4, T5, T7, T8, T10, T11, and T13.

### Commercial Vehicle

```script
Hey {first_name}, it's {your_first_name} from Fox Finance Group. You grabbed our commercial vehicle guide. Quick check, are you looking at a specific vehicle or still working out the budget side?
```

### Commercial Equipment

```script
Hey {first_name}, it's {your_first_name} from Fox Finance Group. You picked up our commercial equipment guide. Are you looking at a specific piece of gear or sizing up your options?
```

### Consumer Personal

```script
Hey {first_name}, it's {your_first_name} from Fox Finance Group. You grabbed our consumer personal loan guide. What's the loan helping you sort out?
```

### Consumer Vehicle

```script
Hey {first_name}, it's {your_first_name} from Fox Finance Group. You picked up our consumer vehicle guide. Have you got a car in mind or still shopping?
```

### Generic enquiry

```script
Hey {first_name}, it's {your_first_name} from Fox Finance Group. You filled in our enquiry form. What's the finance for?
```

---

## Voicemails

### T5 — Lead magnet voicemails (Day 1, 5pm)

Leave one of these if no answer on the T5 call attempt.

**Commercial Vehicle**

```script
Hey {first_name}, it's {your_first_name} from Fox Finance Group. Just following up on the commercial vehicle guide you grabbed. If you've got a vehicle in mind or just want to talk through what's possible, give me a ring on {phone}. No rush. Cheers.
```

**Commercial Equipment**

```script
Hey {first_name}, {your_first_name} from Fox Finance Group. Following up on the equipment finance guide. If you'd like to talk through your options, give me a ring on {phone}. No pressure. Cheers.
```

**Consumer Personal**

```script
Hey {first_name}, {your_first_name} from Fox Finance Group. Just following up on the personal loan guide. Give me a ring on {phone} when it suits and I'll walk you through your options. Cheers.
```

**Consumer Vehicle**

```script
Hey {first_name}, {your_first_name} from Fox Finance Group. Following up on the car finance guide. Five minute chat any time you're ready, give me a ring on {phone}. Cheers.
```

**Generic enquiry**

```script
Hey {first_name}, {your_first_name} from Fox Finance Group. Just following up on your finance enquiry. Give me a ring on {phone} when you get a chance. No rush. Cheers.
```

### T13 — Final call voicemail (Day 4)

```script
Hey {first_name}, {your_first_name} from Fox Finance Group. Last one from me on this. If you'd still like a hand sorting your finance, ring me on {phone}. Otherwise no worries, all the best. Cheers.
```

### No-show recovery voicemail (Day 2)

The no-show recovery voicemail now lives in the Closer Booking playbook (`09d-closer-booking.md`). It fires after a missed broker appointment, once the card has exited this pipeline.

---

## BAMFAM Booking Script

Book A Meeting From A Meeting. Never end a call without the next step locked.

### Step 1: The book

```script
Best move from here is a quick chat with one of our brokers. They'll walk you through your options. I've got a 15 minute slot today at 2pm or tomorrow at 10am. Which works?
```

### Step 2: The confirm

*(Send calendar invite while still on the call, then say:)*

```script
Just sent you the invite. Did it land?
```

### Step 3: The expectation set

```script
{broker_first_name} will call you on this number. They'll have your details so you don't repeat yourself. The call's about 15 minutes. No pressure to decide anything on it.
```

### Step 4: The close

```script
Anything you want to read before the call, the guide you grabbed has the basics. Cheers, {first_name}.
```

### Booking rules

- Lock the broker call inside 24 hours from first contact wherever possible.
- Prime Convenience Repeat → broker call same day if the slot exists.
- Commercial leads → broker call inside 48 hours unless the lead pushes back. Don't lose them to a dealer.
- Confirm the SMS booking confirmation fired in GHL within 60 seconds.

---

## Reactivation Call Script

Use when an SDR calls a reactivation lead who replied YES to the SMS. Call within 5 minutes of the reply.

### Opener

```script
Hey {first_name}, it's {your_first_name} from Fox Finance Group. Got your reply, thanks for getting back. Quick one, has your situation shifted since we last chatted?
```

### If they say yes (something changed)

```script
Fair enough. What's moved? I'll see what fits where things are at now.
```

### If they say no (just curious)

```script
All good. Worth knowing rates and lender options have shifted in the last while. Want me to send a quick rundown for your situation? Two-minute read.
```

### If there's heat (they want to act)

Move straight to BAMFAM.

### If they want to think

```script
No worries. I'll leave it with you. We're on {phone} when you're ready. The door's always open.
```

---

*End of FFG Pre-Sales Scripts.*
