# FHL Pre-Sales Scripts

**Brand:** Fox Home Loans
**Playbook:** Pre-Sales SDR (suffix c)
**Version:** 1.1
**Created:** 2026-05-05
**Owner:** James
**Status:** Draft

---

## Purpose

Voice scripts only. Phone call openers, voicemails, BAMFAM booking, and reactivation call scripts. Automated email and SMS touchpoints live in the developer guide. The broker handoff brief lives in the handbook.

Standards: Australian English. Third-grade reading level. Zero em dashes. No banned words.

Voice tone: same warmth as FFG, bigger emotional stakes. Home buying is personal. Extra reassurance and patience.

---

## SDR Call Openers

Use the opener that matches the Purchase Type. Where Purchase Type is unknown, use the generic opener. These apply at T3, T4, T5, T7, and T9.

### First Home Buyer

```script
Hey {first_name}, it's {your_first_name} from Fox Home Loans. Saw you're looking at your first home. Quick question, are you still saving the deposit or close to ready?
```

### New Purchase (not first home)

```script
Hey {first_name}, {your_first_name} from Fox Home Loans. Looks like you're moving on a new place. Have you sold your current spot, or running both?
```

### Refinance

```script
Hey {first_name}, {your_first_name} from Fox Home Loans. You were checking rates. What prompted the look?
```

### Investor

```script
Hey {first_name}, {your_first_name} from Fox Home Loans. You're looking at investment finance. Is this your first investment property?
```

### Commercial

```script
Hey {first_name}, {your_first_name} from Fox Home Loans. You're looking at commercial property finance. What type of commercial?
```

### Generic enquiry

```script
Hey {first_name}, it's {your_first_name} from Fox Home Loans. You filled in our enquiry form. What brings you to us?
```

---

## Voicemails

### T4 — Day 1 afternoon voicemail

```script
Hey {first_name}, {your_first_name} from Fox Home Loans. Just tried to give you a buzz. Quick chat about your home loan enquiry whenever you're ready. {phone}. Cheers.
```

### T5 — Day 2 morning voicemail

```script
Hey {first_name}, {your_first_name} from Fox Home Loans again. Following up on your enquiry. No rush, just letting you know I'm here when it suits. {phone}. Cheers.
```

### T7 — Day 5 voicemail

```script
Hey {first_name}, {your_first_name} from Fox Home Loans. Few attempts in. I'll back off the calls. If your situation changes or you'd like a hand, just give me a ring on {phone}. Cheers.
```

### T9 — Day 9 final voicemail

```script
Hey {first_name}, {your_first_name} from Fox Home Loans. Last one from me. Your file stays open. Whenever you're ready, the number's {phone}. All the best.
```

### No-show recovery voicemail (Day 2)

The no-show recovery voicemail now lives in the Closer Booking playbook (`09d-closer-booking.md`). It fires after a missed appointment, once the card has exited this pipeline.

---

## Appointment Booking Script (BAMFAM)

Mortgage appointments are longer than personal loan calls. Set expectations.

### Step 1: Classify and confirm

Run through Q1 (Purchase Type) and capture the mandatory tags (Q2) before offering the time. Use the handbook's full decision tree.

### Step 2: The book

```script
Best move from here is a 30-minute appointment with one of our brokers. They'll walk you through what's possible, run the numbers, and answer everything. I've got tomorrow at 10am or Friday at 2pm. Which suits?
```

### Step 3: The confirm

*(Send calendar invite while still on the call, then say:)*

```script
Just sent you the invite. Did it land?
```

### Step 4: What to bring

Tell them the Purchase Type-specific docs list:

**All Purchase Types:**
- Photo ID (driver's licence or passport)
- 2 most recent payslips (PAYG) or 2 years tax returns + financials (self-employed)
- 3 months bank statements (all accounts)

**FHB additional:** savings evidence (3-6 months), FHB grant application if eligible.
**Refinance additional:** current loan statement, fixed rate expiry dates.
**Investor additional:** rental income evidence, portfolio summary.
**Commercial additional:** 2 years business financials, ATO portal access.

### Step 5: The close

```script
We'll see you on {calendar_date_time}. Cheers, {first_name}.
```

### Booking rules

- Lock the appointment inside 48 hours of first contact wherever possible.
- High-value (>$800K) → consult Bill Robb on routing before booking.
- Cross-sell from FFG → preserve broker continuity if possible.

---

## Reactivation Call Script

Use when an SDR calls a reactivation lead who replied YES to the SMS. Call within 5 minutes of the reply.

### Opener

```script
Hey {first_name}, it's {your_first_name} from Fox Home Loans. Got your reply, thanks for getting back. Quick one, has your situation shifted since we last chatted?
```

### If they say yes (something changed)

```script
Fair enough. What's moved? I'll see where things sit for you now.
```

### If they say no (just curious)

```script
All good. Worth knowing the market's moved since we last spoke. Rates, lender options, a few things have shifted. Want me to send a quick rundown? Two-minute read.
```

### If there's heat (they want to act)

Move straight to the booking script.

### If they want to think

```script
No worries. I'll leave it with you. We're on {phone} when you're ready. The door's always open.
```

---

*End of FHL Pre-Sales Scripts.*
