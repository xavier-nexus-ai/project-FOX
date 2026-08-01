# FFG Current-State Process Map
# T-System Pipeline Architecture

> **Purpose:** Map every existing FFG manual touchpoint chronologically with T-numbers, identify gaps, and design the automation layer that fills them.
> **Source Data:** Activation Meeting Transcript, COS.yaml, Extracted Sales Scripts (Docs 1-9, 11, 13), SendGrid Automation Inventory
> **Last Updated:** 2026-03-23

---

## How to Read This Document

- **T prefix** = Direct touchpoints (calls, SMS, emails to the lead)
- **N prefix** = Nurture sequence (automated, after manual exhaustion)
- **D prefix** = Declined lead re-nurture sequence
- **OF prefix** = Online Form completion path
- **RC prefix** = Reactivation/Customer Care sequence
- Manual touchpoints marked with **[BROKER]**
- Automated touchpoints marked with **[SYSTEM]**
- Semi-automated (template exists, manually triggered) marked with **[TEMPLATE]**

---

## Pipeline Entry Points

FFG receives approximately 375 leads/month:
- 254 organic website inquiries
- 98 phone calls (hottest leads, 22% settlement rate)
- 23 other (referrals, walk-ins, etc.)

All leads enter via TypeForm (conditional logic, 70% completion rate) or phone call, then route through Zapier into Ambition.

**ICA Detection at Intake:**
Capture these CRM tags on every new contact:
- Primary ICA (1 of 5 profiles)
- Age band
- Residential status
- Credit strength indicator
- Likely next finance type

**ICA Routing Priority:**
1. Business Asset Borrower (highest value, commercial)
2. Prime Vehicle Borrower (prime consumer, high certainty)
3. Young Practical Motor Borrower (volume, affordability-focused)
4. Prime Convenience-Led Repeat Borrower (fast-track, loyalty)
5. Established Personal Finance Borrower (broad capability)

---

## Primary Pipeline: Inbound Lead to Settlement

### STAGE: Interacting (24hr RED dot)

**Purpose:** Lead has replied to any touchpoint. Broker must pick up within 24 hours.
**Entry:** Lead replies to SMS, email, voicemail, or calls in.
**Exit:** Broker makes contact and moves to next stage.
**Red Dot:** 24-hour escalation if no broker action.

---

### STAGE: FUP - Follow Up (24hr task)

**Purpose:** Broker has had an interaction that needs follow-up within 24 hours.
**Entry:** Broker logs an interaction that requires a callback or follow-up action.
**Exit:** Follow-up completed, lead moves to appropriate next stage.

---

### Pre-Contact Auto-Response

| T# | Day | Channel | Type | Action | Script Reference | Current State |
|----|-----|---------|------|--------|-----------------|---------------|
| T1 | 0 | SMS | [TEMPLATE] | "Inquiry received, lending specialist will be in touch" | No named script - template in Ambition | Exists - manually triggered |
| T2 | 0 | Email | [TEMPLATE] | "Inquiry received, here's next steps + landing page" | No named script - template in Ambition | Exists - manually triggered |

**Gap identified:** T1 and T2 are currently template-triggered, not automated. Should fire within 60 seconds of form submission.

**Proposed change:** Automate T1 + T2 via N8N webhook from TypeForm/Zapier. Fire instantly, 24/7.

---

### Day 1 - First Contact Push (3 attempts)

| T# | Day | Time | Channel | Type | Action | Voicemail Script | Current State |
|----|-----|------|---------|------|--------|-----------------|---------------|
| T3 | 1 | Morning (within 5 min) | Phone | [BROKER] | Call Attempt 1. Priority call. Do not delay. | No voicemail on first attempt | Exists - manual |
| T4 | 1 | Lunchtime | Phone | [BROKER] | Call Attempt 2. If no answer, leave voicemail. | Doc 8: "Day One Voice Message" | Exists - manual |
| T5 | 1 | ~5pm | Phone | [BROKER] | Call Attempt 3. If no answer, leave voicemail. Also send SMS + email with online form link. | Doc 8: "Second Follow Up For The Day" | Exists - manual. SMS/email are template-triggered. |

**After T5 (if no contact):** Lead has received 3 call attempts, up to 2 voicemails, 1 SMS, 1 email, plus the auto-response SMS/email. Options given: call back, tell us a time, complete application online.

---

### Day 2 - Follow-Up (2 attempts)

| T# | Day | Time | Channel | Type | Action | Voicemail Script | Current State |
|----|-----|------|---------|------|--------|-----------------|---------------|
| T6 | 2 | Morning | Phone | [BROKER] | Call Attempt 4. If no answer, leave voicemail. | Doc 8: "Day Two Voice Message" | Exists - manual |
| T7 | 2 | Afternoon | Phone | [BROKER] | Call Attempt 5. | No voicemail (already left one today) | Exists - manual |

---

### Day 3 - Continued Follow-Up (2 attempts)

| T# | Day | Time | Channel | Type | Action | Voicemail Script | Current State |
|----|-----|------|---------|------|--------|-----------------|---------------|
| T8 | 3 | Morning | Phone | [BROKER] | Call Attempt 6. | No voicemail | Exists - manual |
| T9 | 3 | Afternoon | Phone | [BROKER] | Call Attempt 7. | No voicemail | Exists - manual |

---

### Day 4 - Breakup (1 attempt)

| T# | Day | Time | Channel | Type | Action | Voicemail Script | Current State |
|----|-----|------|---------|------|--------|-----------------|---------------|
| T10 | 4 | Any | Phone | [BROKER] | Final call attempt. Breakup voicemail. "I'm here when you're ready." | Doc 8: "Day Three Voice Message" | Exists - manual |

---

### MANUAL PROCESS ENDS AT T10

**Current state after T10:** Lead enters "No Contact Hopper" with basic email nurture (40-50% open rate). Content: reviews, top 5 tips, bank statements, overcoming concerns. All template-triggered, not properly automated.

**Critical stat:** 80%+ of unreached leads complete the online application form anyway. This path needs its own sequence (see Online Form Path below).

---

### "Not Responding Yet" - Automated Bridge (NEW)

These touchpoints do not exist today. They fill the gap between the broker's manual exhaustion (T10) and long-term nurture.

| T# | Day | Channel | Type | Action | ICA Personalisation |
|----|-----|---------|------|--------|-------------------|
| T11 | 5 | SMS | [SYSTEM] | "We're still here if you need us. Complete your application online: [LINK]" | Tone varies by ICA |
| T12 | 6 | Email | [SYSTEM] | Value content. Trust-building. ICA-targeted. | See ICA Content Matrix below |
| T13 | 8 | SMS | [SYSTEM] | Social proof. Google review link or testimonial. | Same for all ICAs |

---

### Automated Nurture Sequence (NEW)

Long-term nurture for leads who have not responded to T1-T13. Currently this is the weak "No Contact Hopper" with manually-triggered template emails.

| N# | Day | Channel | Type | Content Theme | ICA Personalisation |
|----|-----|---------|------|--------------|-------------------|
| N14 | 10 | Email | [SYSTEM] | Educational: "5 things that help you get approved faster" | Young Practical Motor: "First car loan? Here's what to know" / Business Asset: "Equipment finance basics for business owners" |
| N15 | 14 | SMS | [SYSTEM] | Social proof: customer review or testimonial | Same for all ICAs |
| N16 | 20 | Email | [SYSTEM] | Overcoming concerns: "Why we ask for bank statements" / "What happens if you've been declined before" | Young Practical Motor: reassurance focus / Prime Vehicle: efficiency focus |
| N17 | 28 | SMS | [SYSTEM] | Soft check-in: "Still thinking about finance? We're here when you're ready." | Same for all ICAs |
| N18 | 35 | Email | [SYSTEM] | Value content: "How brokers save you money vs going direct" | Business Asset: tax timing, working capital / Established Personal: flexibility, broad options |
| N19 | 45 | Email | [SYSTEM] | Final nurture: "Your file is still open. One click to restart." + online form link | Same for all ICAs |

**After N19:** If no response, mark as Lost ("Ghosting"). Do NOT recycle into active pipeline. Lead can re-enter via lead market reactivation (see RC sequence) or if they self-initiate contact.

---

## Branching Paths

### Online Form Completion Path

**Trigger:** Lead completes online application form at any point during T1-N19.
**Critical stat:** 80%+ of unreached leads complete the form online.

| OF# | Timing | Channel | Type | Action |
|-----|--------|---------|------|--------|
| OF1 | Instant | Email | [SYSTEM] | Application received confirmation + what happens next |
| OF2 | Instant | SMS | [SYSTEM] | "We've got your application. A broker will be in touch within 1 business day." |
| OF3 | Next business day | Phone | [BROKER] | Broker reviews application and calls. Not a cold call - they have context. |

**On OF3 success:** Lead moves into active application pipeline. Broker manages through to settlement using existing scripts:
- Doc 5: Lender Options Call (assessment complete, presenting options)
- Doc 3: Approval Call (approval notification + conditions)
- Doc 4: Insurance Introduction Call (post-docs, pre-packaging)
- Doc 1: Loan Packaging Call (presenting loan packages + insurance)
- Doc 7: Contract Sign-Up Call (loan docs walkthrough)
- Doc 9: Private Seller Call (if applicable)
- Doc 6: Settlement Calls (content still needed from Fox)

---

### Post-Application: Document Collection

**Trigger:** Lead has completed application but has not returned documents.
**Current state:** "No Docs Returned" SendGrid automation exists (4 emails, 63.4% open rate).

| T# | Timing | Channel | Type | Action | Voicemail Script |
|----|--------|---------|------|--------|-----------------|
| TD1 | Day 1 post-app | Phone | [BROKER] | Call to check on docs | Doc 8: "Doc Follow Up" |
| TD2 | Day 1 post-app | Email | [TEMPLATE] | Reminder of what docs are needed | Existing SendGrid template |
| TD3 | Day 2 post-app | Phone | [BROKER] | Second call if docs still pending | Doc 8: "Second Doc Follow Up For The Day" |
| TD4 | Day 3 post-app | Email | [SYSTEM] | Automated reminder | Existing SendGrid automation |
| TD5 | Day 5 post-app | Email | [SYSTEM] | Final docs reminder | Existing SendGrid automation |

**Current performance:** 80%+ return docs. The existing SendGrid "No Docs Returned" automation works well (63.4% open rate, 4.4% click rate).

---

### 90-Day Declined Lead Re-Nurture

**Trigger:** Application declined (~70% of submitted applications).
**Critical stat:** 20% convert on the 90-day follow-up. 9 settlements last month from this path alone.
**Current state:** SendGrid "90-Day Plan" automation exists. BEST PERFORMER: 90.2% open rate, 18.6% click rate, 0% unsubscribe.

| D# | Day | Channel | Type | Action |
|----|-----|---------|------|--------|
| D1 | 0 | Email | [SYSTEM] | 90-Day Plan email: "It's not a no, it's a not yet." Credit improvement steps. What to do over next 90 days. |
| D2 | 0 | Phone | [BROKER] | Broker explains the plan. Sets expectations. Plants the seed. |
| D3 | 30 | Email | [SYSTEM] | Check-in: "How's the 90-day plan going?" Progress tips. |
| D4 | 60 | Email | [SYSTEM] | Encouragement: "You're two-thirds of the way there." |
| D5 | 90 | Email + SMS | [SYSTEM] | Re-application invitation: "Ready to try again? Your file is here." |
| D6 | 90 | Phone | [BROKER] | Broker calls to discuss re-application. |

**This path is gold.** 20% conversion rate. 90.2% open rate. Zero unsubscribes. Do not change the approach, just automate the timing and add ICA personalisation.

---

### Customer Care Reactivation (Existing Clients)

**Trigger:** Post-settlement customer, typically 6-12+ months since last loan.
**Critical stat:** 41 new inquiries last month from outbound calls alone, no automation.
**Script:** Doc 2/13: Consumer Customer Care Script

| RC# | Channel | Type | Action |
|-----|---------|------|--------|
| RC1 | Phone | [BROKER] | Outbound customer care call using Consumer Customer Care Script. Mention rate drops, new lenders, cross-sell opportunities. |
| RC2 | Email | [SYSTEM] | If no answer, automated email with same messaging. |
| RC3 | SMS | [SYSTEM] | If no answer after email, SMS with callback option. |

**ICA personalisation for RC1:**
- Young Practical Motor: "How's the car going? With recent rate drops, refinancing could save you money."
- Business Asset: "Any equipment needs coming up? EOFY is a good time to look at tax-effective financing."
- Prime Vehicle: "Time for an upgrade? We can make it smooth and easy."
- Prime Convenience Repeat: "Quick check-in. Need anything? We can fast-track for you."
- Established Personal: "Just touching base. Any big plans coming up we can help with?"

**Cross-sell flag:** During RC1, if customer expresses interest in home loans, property, or investment, flag for FHL cross-sell. ICA-to-FHL Purchase Type mapping:
- Young Practical Motor >> First Home Buyer
- Established Personal Finance >> New Purchase / Refinance
- Prime Convenience Repeat >> New Purchase / Refinance / Investor
- Business Asset >> Commercial
- Prime Vehicle >> New Purchase / Refinance / Investor

---

### Lead Market Reactivation (49K leads/year)

**Context:** Fox generates 49K leads/year (34K UMI, 15K Fox) that are sold to the lead market at $24-26/lead ($48K-$144K/year). These leads are never re-engaged after sale. Legal to reactivate after 3-month cooling period. Estimated $1M/year potential if properly recycled.

| LR# | Timing | Channel | Type | Action |
|-----|--------|---------|------|--------|
| LR1 | 3 months post-sale | SMS | [SYSTEM] | "Hi [Name], it's Fox Finance. We helped with your inquiry a while back. Still looking for finance? We'd love to help. Reply YES or call 07 3505 3099." |
| LR2 | 3 months + 3 days | Email | [SYSTEM] | Value content: "Things have changed since we last spoke. New lenders, better rates." |
| LR3 | 3 months + 7 days | SMS | [SYSTEM] | Social proof + soft CTA |
| LR4 | 4 months | Email | [SYSTEM] | Final attempt: "Your file is still here. One click to restart." |

**If reply received:** Route to Interacting stage. Broker picks up within 24 hours. Treat as warm lead (40-45% conversion rate for repeat/known contacts).

**Reactivation note:** Re-engage ethically. Include opt-out on every message. Do not contact broker-referred UMI clients (referral integrity).

---

## Post-Contact Application Pipeline

Once a broker makes live contact and takes an application, the lead moves through Fox's existing deal pipeline. These scripts are already well-established and work at 95%+ on-phone conversion.

### Application Pipeline Touchpoints

| Stage | Script | Doc Reference | Owner | Notes |
|-------|--------|--------------|-------|-------|
| Lender Options Presented | Lender Options Call Process | Doc 5 | Broker | Assessment complete, presenting options. Education on credit file, bank statements, profile. |
| Approval Notification | Approval Call Process | Doc 3 | Broker | Approval + conditions + next steps. Includes dealership prevention messaging. |
| Insurance Introduction | Insurance Introduction Call | Doc 4 | Broker | Post-docs received. Getting insurance quotes. Quick details grab. |
| Loan Packaging | Loan Packaging Call Process | Doc 1 | Broker | Presenting packages with insurance options. The main "sell the sizzle" moment. |
| Contract Sign-Up | Contract Sign-Up Call | Doc 7 | Broker | Walking through loan docs. Key points, T&Cs, completion. |
| Private Seller (if applicable) | Private Seller Call Process | Doc 9 | Broker | Confirming seller details, docs needed, settlement process. |
| Settlement | Settlement Calls | Doc 6 | Broker | CONTENT STILL NEEDED FROM FOX |
| Application Update | (voicemail) | Doc 8: "Update On Application" | Broker | When broker has an update and customer doesn't answer. |

---

## ICA Content Matrix for Automated Touchpoints

| ICA Profile | T12 (Day 6 Email) | N14 (Day 10 Email) | N16 (Day 20 Email) | N18 (Day 35 Email) |
|------------|-------------------|-------------------|-------------------|-------------------|
| Young Practical Motor | "Your first car loan: what to expect" | "5 things first-car buyers wish they knew" | "Why bank statements aren't scary" | "How a broker saves you vs going direct to a lender" |
| Established Personal Finance | "Finance options that fit your life" | "Consolidation, personal loans, and what's right for you" | "What we look at (and what we don't)" | "Why 50+ lenders means better options for you" |
| Prime Convenience Repeat | "Fast-track your finance" | "Repeat customers get priority" | "Your history makes approval easier" | "One call. Better deal. Done." |
| Business Asset | "Equipment finance that works for your business" | "EOFY finance planning for business owners" | "Lite-doc options for self-employed borrowers" | "Preserve working capital with smart asset finance" |
| Prime Vehicle | "Upgrade your vehicle the easy way" | "Prime borrowers get the best rates" | "What we handle so you don't have to" | "Smooth, certain, efficient. That's how we do vehicle finance." |

**Messaging priorities per ICA (from ICA definitions):**
- Young Practical Motor: Reassurance, affordability, simplicity, speed, confidence
- Established Personal Finance: Flexibility, practicality, trust, broad capability, "we can help again"
- Prime Convenience Repeat: Fast-track, loyalty, ease, tailored support, reduced friction
- Business Asset: Commercial outcomes, tax timing, asset upgrade, growth support, preserve working capital
- Prime Vehicle: Ease, certainty, quality of experience, efficient process, trusted relationship

---

## Existing SendGrid Automations (Reference)

These automations already exist and perform well. The T-System wraps around them, not replaces them.

| Automation | Emails | Open Rate | Click Rate | Unsub Rate | T-System Mapping |
|-----------|--------|-----------|------------|------------|-----------------|
| FFG New Customer Database Entry | 6 | 58.1% | 3.5% | 0.87% | Post-settlement nurture (outside pre-sales scope) |
| FFG No Customer Contact | 5 | 58.0% | 3.1% | 0.43% | Maps to No Contact Hopper (T11-N19 replaces this) |
| FFG No Docs Returned | 4 | 63.4% | 4.4% | 0.88% | Maps to TD1-TD5 doc collection path |
| FFG 90-Day Plan | 2 | 90.2% | 18.6% | 0% | Maps to D1-D6 declined re-nurture (KEEP - best performer) |
| FFG Introducers/Referrals | 1 | 66.7% | 11.1% | 0% | Referral partner path (outside pre-sales scope) |

---

## Gap Analysis Summary

| Gap | Current State | Proposed Solution | Priority |
|-----|--------------|-------------------|----------|
| T1/T2 not automated | Template-triggered manually | Automate via N8N webhook, fire within 60 seconds | High |
| No structured post-Day 4 sequence | Weak "No Contact Hopper" with basic emails | T11-T13 bridge + N14-N19 ICA-targeted nurture | High |
| Online form completion has no dedicated path | 80%+ complete form but no structured follow-up | OF1-OF3 confirmation + broker callback path | High |
| No ICA personalisation | Generic messaging for all leads | ICA detection at intake + personalised content per profile | Medium |
| 90-Day Plan not fully automated | 2 emails exist (90.2% open rate) | Expand to D1-D6 with phone touchpoints + ICA targeting | Medium |
| Customer Care calls not systematised | 41 inquiries/month from ad-hoc outbound | RC1-RC3 with ICA targeting + cross-sell flags | Medium |
| Lead market leads never reactivated | 49K/year sold and forgotten | LR1-LR4 reactivation after 3-month cooling | Medium |
| Settlement call script missing | Doc 6 is empty | Request content from Fox | Low (not blocking) |
| No cross-sell trigger at application | ICA data captured but not acted on | Flag FHL cross-sell potential based on ICA-to-Purchase Type mapping | Medium |

---

## Cross-Sell Integration Points

The unified value journey has cross-sell triggers embedded at these touchpoints:

| T# | Trigger | Action |
|----|---------|--------|
| OF3 / T3-T10 (on contact) | Broker captures ICA tags during qualification | System maps ICA to FHL Purchase Type |
| Application stage | ICA confirmed from application data | Cross-sell flag set if ICA maps to FHL opportunity |
| Post-settlement (RC1) | Customer Care call reveals property/investment interest | Route to FHL for cross-sell conversation |
| D5-D6 (90-day re-app) | Declined customer re-engages | Check if FHL product might suit instead |

**Note:** Cross-sell is a trigger point within the unified value journey, not a separate pipeline. See unified journey strategy for full details.

---

## Key Metrics to Track

| Metric | Current | Target | Source |
|--------|---------|--------|--------|
| Speed to first call | Unknown (same day) | Under 5 minutes during business hours | POLR MVP task creation timestamp |
| Contact rate | 65% | 75% | Ambition / POLR |
| On-phone application rate | 95%+ | Maintain | Ambition |
| Document return rate | 80%+ | Maintain | Ambition |
| Approval rate | ~30% | Maintain (lender-dependent) | Ambition |
| 90-day plan conversion | 20% | 25% | POLR |
| No Contact Hopper to online form | 80%+ | 85% | POLR |
| Customer Care inquiries/month | 41 | 60+ (with automation support) | POLR |
| Lead market reactivation rate | 0% | 5-10% | POLR |

---

*This process map is the foundation for the developer guide and SDR handbook. Every T-number referenced in those documents traces back to this document.*
