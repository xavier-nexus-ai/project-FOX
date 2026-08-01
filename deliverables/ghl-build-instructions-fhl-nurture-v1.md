# GHL Proof of Concept: FHL 18-Month Nurture Sequence

**Prepared by:** James Killick (Njin Method)
**For:** Fox Finance Group GHL Tech Team
**Date:** 2026-03-27

---

## Background: Who Is Fox and Why Are We Doing This?

Fox Finance Group is a QLD-based financial services group with two customer-facing businesses:

1. **Fox Finance Group (FFG)** - Asset finance brokerage. Car loans, personal loans, equipment finance, debt consolidation. ~33 staff, ~90-108 settlements per month. Commission-based ($2,300 average per deal).
2. **Fox Home Loans (FHL)** - Mortgage brokerage. Home loans, refinancing, investment property, commercial property. 3 brokers (Bill, Paige, Angel), ~16-17 settlements per month. Higher value ($4,750-$5,225 per deal).

These two businesses share customers but currently operate in silos. Someone who gets a home loan through FHL might also need a car loan or personal loan through FFG, but there's no system connecting the two. That's money being left on the table.

Fox also has a third business (UMI Loans, sub-prime car lending) but that's out of scope for this work.

**The problem we're solving:** FHL has a detailed 18-month post-settlement nurture plan that their brokers follow manually. It includes touchpoints at months 1, 3, 6, 9, 12, 15, and 18 after a home loan settles. At month 9, there's a natural cross-sell moment to FFG. At month 18, the clawback period ends and refinance becomes the revenue event. None of this is automated or tracked in a system right now.

**Why this POC matters:** The business owner (Nathan) wants to see whether GoHighLevel can handle this before committing to a platform decision. We're also building a custom prototype (POLR) as an alternative. This GHL build is one side of a head-to-head comparison so Nathan can make an informed call. We need the GHL POC to be a genuine, fair test - not a straw man. If GHL handles it well, that's a valid outcome. If it struggles with the segmentation and branching logic, that tells us something too.

---

## What We're Testing

Three things:

1. **Can we log all the customer data we need?** Custom fields on contact records that capture the loan details, customer profile, and cross-sell status.
2. **Can we identify cross-sell opportunities?** At a glance, can we see who's an FFG customer, FHL customer, or both - and who *should* be both?
3. **Can we trigger the right actions at the right time with the right segmentation?** 7 touchpoints over 18 months, with different content for 5 different customer types. Does GHL handle this cleanly or does it get messy?

We're not building the final system. No real content needed - just placeholder templates to prove the triggers and branching work. Use dummy customer data throughout.

---

## The Concept

Every FHL customer who settles a home loan enters an 18-month nurture sequence. They hit 7 touchpoints. The content at each touchpoint changes based on their **purchase type** (First Home Buyer, New Purchase, Refinance, Investor, or Commercial).

At month 9, we cross-sell to FFG based on who they are. At month 18, we drive refinance (the clawback period is over, so this is the revenue event). The system needs to know: who is this person, what type of home loan did they get, and what FFG products might suit them next.

---

## 1. Custom Fields to Set Up

These are the data points we need on each contact record. Use dummy data for the POC.

### Must-have fields (these drive the sequence)

1. **FHL Purchase Type** (Dropdown: First Home Buyer, New Purchase, Refinance, Investor, Commercial) - This is the master segmentation field. Everything branches off this.
2. **FHL Settlement Date** (Date) - Triggers the entire 18-month sequence. Every touchpoint is calculated from this date.
3. **FHL Lender** (Text) - Needed to know who to submit repricing requests to at month 6.
4. **FHL Loan Amount** (Currency) - Used in equity calculations and refinance scenarios.
5. **FHL Interest Rate** (Number, %) - Baseline for repricing comparison.
6. **FHL Loan Structure** (Dropdown: Variable, Fixed, Split, Interest Only) - Fixed rate expiry is a key refinance trigger.
7. **FHL Property Value** (Currency) - Baseline for equity tracking at months 3 and 12.
8. **FHL Broker** (Dropdown: Bill Robb, Paige Beveridge, Angel) - Assigns who owns the relationship and gets the internal tasks.
9. **Employment Type** (Dropdown: PAYG Full-Time, PAYG Part-Time, Casual, Self-Employed) - Affects which FFG products make sense at the month 9 cross-sell.
10. **Residential Status** (Dropdown: Owner Occupied, Investor, Renting) - Key signal for cross-sell routing.

### Nice-to-have fields (powers personalisation)

1. **FHL Fixed Rate Expiry** (Date) - If fixed or split. Triggers refinance conversations earlier if expiry is approaching.
2. **FHL Offset Account** (Yes/No) - Setup verification at month 1.
3. **Household Type** (Dropdown: Single, Couple, Couple + Dependants, Single + Dependants) - Content personalisation.
4. **Likely Next Needs** (Multi-select: Vehicle, Travel, Wedding, Reno/Solar, Debt Consolidation, Business Finance) - Captured from broker notes. Powers the month 9 FFG pack.

### Cross-sell tracking fields

1. **Customer Type** (Dropdown: FFG Only, FHL Only, Both, Potential Both) - This is the key field. Shows at a glance who is a cross-sell candidate. Should auto-set based on whether they have active loans with both businesses.
2. **FFG Cross-Sell Status** (Dropdown: Not Started, Pack Sent, Responded, Opportunity Created, Settled, Not Interested) - Tracks the month 9 cross-sell pipeline.

---

## 2. Cross-Sell Routing Logic

This is what we're really testing. Can GHL handle the "who should get what" logic?

When a contact's purchase type is set, the system should know which FFG products to suggest at month 9:

1. **First Home Buyer** → Car loan, personal loan. Reasoning: younger, early-stage. Just bought first home, next need is usually a car or furniture funding.
2. **New Purchase** → Car loan, personal loan, reno finance. Reasoning: established buyer moving into a new place, likely needs car for new commute, renos, appliances.
3. **Refinance** → Debt consolidation, car refinance, personal loan. Reasoning: just freed up cashflow from a better rate, good time to clean up other debts too.
4. **Investor** → Equipment finance, business finance, vehicle. Reasoning: often self-employed or business-minded, growth-oriented purchases.
5. **Commercial** → Equipment finance, fleet, working capital. Reasoning: business borrower with commercial asset needs.

**The POC question:** Can we set up workflow branching in GHL that sends different content based on this purchase type? Or does it get clunky with 5 branches?

---

## 3. Pipeline (7 Stages)

Create a pipeline called **"FHL 18-Month Nurture"** with these stages:

1. **Month 1 - Welcome** (triggers ~Day 25 after settlement) - Check loan setup is working. Introduce FFG and affiliates.
2. **Month 3 - Confidence Pack** (triggers ~Day 85) - Property valuation benchmark. Equity position baseline.
3. **Month 6 - Repricing** (triggers ~Day 175) - Run repricing with lender. Show we're actively saving them money.
4. **Month 9 - FFG Cross-Sell** (triggers ~Day 265) - Send the right FFG pack based on purchase type. This is the key revenue moment.
5. **Month 12 - Annual Review** (triggers ~Day 360) - Updated valuation. Strategy for next 12 months.
6. **Month 15 - Refi Prep** (triggers ~Day 445) - Options map: pay down faster, invest, or refinance.
7. **Month 18 - Refi Window** (triggers ~Day 535) - Clawback period is over. Commence refinance if right for the customer.

**The POC question:** Can GHL auto-move contacts between stages based on date calculations from a custom field (settlement date)? This is the core automation we need to prove.

---

## 4. Dashboard View

We want to see at a glance:

- How many contacts are in each nurture stage (pipeline view)
- Who is FFG-only, FHL-only, or both (cross-sell opportunity view)
- Repricing results (how many submitted, approved, total savings)
- Cross-sell conversion (month 9 packs sent vs responses vs settled FFG loans)
- Refinance pipeline (month 15-18, who's in progress)

**The POC question:** Can GHL's reporting and dashboard handle these views cleanly, or does it need workarounds?

---

## 5. Test Scenarios

Load 5 dummy contacts covering the key variations. Each one should be at a different stage of the nurture sequence based on their settlement date:

1. **Test FHB** - Purchase type: First Home Buyer. Settlement date: 2026-01-15. Employment: PAYG Full-Time. Structure: Variable. Should be at the Month 3 stage by now. Test: does the confidence pack segmentation trigger correctly for a first home buyer?

2. **Test NewPurchase** - Purchase type: New Purchase. Settlement date: 2025-09-15. Employment: PAYG Full-Time. Structure: Split. Should be at the Month 6 stage. Test: does the repricing workflow fire?

3. **Test Refinancer** - Purchase type: Refinance. Settlement date: 2025-06-15. Employment: Self-Employed. Structure: Variable. Should be at the Month 9 stage. Test: does the FFG cross-sell route to the right pack (debt consolidation, car refinance)?

4. **Test Investor** - Purchase type: Investor. Settlement date: 2025-03-15. Employment: Self-Employed. Structure: Fixed (expiry 2026-09-15). Should be at the Month 12 stage. Test: does the annual review trigger, and does the fixed rate expiry flag anything?

5. **Test Commercial** - Purchase type: Commercial. Settlement date: 2024-09-15. Employment: Self-Employed. Structure: Variable. Should be at the Month 18 stage. Test: does the refinance window activate?

For each one, the questions are: Does the right automation fire? Does the right content branch trigger? Does the dashboard show it correctly?

---

## 6. What We're NOT Building Yet

- Actual email/SMS content (just placeholder templates to prove the triggers work)
- LMS integration (waiting on an aggregator meeting outcome on 2026-03-28)
- FFG-side nurture sequence (that's V2, after FHL proves value)
- Pre-sales SDR pipeline (shelved, not needed unless ads are pursued)

---

## Compliance Reminders

If any placeholder content is customer-facing, even as dummy text:

- Never use "advice", "guarantee", or "financial hardship"
- Australian English (organisation, colour, analyse)
- Keep language simple and human
