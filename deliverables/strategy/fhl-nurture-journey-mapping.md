# FHL 18-Month Nurture Process vs COS Customer Journey Mapping

**Created:** 2026-03-27
**Purpose:** Map Rowdie's FHL 18-month nurture sequence against the COS customer journey stages to identify alignments, gaps, and conflicts before building POLR V1.

---

## Source Documents Compared

| Source | Description |
|--------|-------------|
| **COS customer_journey** (cos.yaml) | "Taylor 2.0 Post-Settlement Journey" - 5 stages (0-4) spanning Week 1 to Year 5+ |
| **FHL Lifecycle Playbook** (docx) | Rowdie's detailed 7-touchpoint playbook with per-segment deliverables |
| **FHL Nurture Process Flowchart** (PDF) | Visual summary confirming touchpoint timeline and ICA-to-purchase-type mapping |

---

## Alignment Map

### COS Stage 0: "Just Settled" (Week 1-4) → FHL Month 1

| Dimension | COS Stage 0 | FHL Month 1 | Status |
|-----------|-------------|-------------|--------|
| **Timing** | Week 1-4 | 1-month follow-up | ALIGNED |
| **Emotion** | "Relieved but nervous - did I do the right thing?" | "Prevent early friction, reduce frustration or anxiety" | ALIGNED |
| **FHL Role** | "Soft seed - getting on top of this loan is first step toward future security/home goals" | "Confirm loan functioning, introduce FFG + refer a friend + affiliates" | ALIGNED (FHL adds FFG intro + affiliate intro here) |
| **Deliverables** | Welcome email + SMS check-in | Phone call + follow-up email/SMS + "Your Loan Setup Snapshot" one-pager | FHL IS MORE DETAILED - has concrete deliverable spec |

**Assessment:** Strong alignment. FHL playbook adds operational detail the COS doesn't have (specific deliverable format, follow-up process, affiliate partner overview).

---

### COS Stage 1: "Stabilise & Enjoy Life Again" (Month 1-6) → FHL Month 3 + Month 6

| Dimension | COS Stage 1 | FHL Month 3 | FHL Month 6 | Status |
|-----------|-------------|-------------|-------------|--------|
| **Timing** | Month 1-6 | 3-month follow-up | 6-month follow-up | ALIGNED (two touchpoints within one COS stage) |
| **Emotion** | "I can manage this - would like breathing room" | "Turn uncertainty into confidence" | "Demonstrate advocacy" | ALIGNED - progressive confidence building |
| **FHL Role** | "Introduce FHL as Security Partner. Invite to explore whether home could be 2-5 year goal." | "Establish benchmark for equity tracking & wealth creation" | "Proactively run repricing review" | ALIGNED - equity benchmark at 3mo sets up repricing advocacy at 6mo |
| **FFG Role** | "Position as Lifestyle Partner" | Not explicitly FFG-focused | Not explicitly FFG-focused | GAP - COS expects FFG lifestyle messaging at this stage, playbook doesn't address it |
| **Deliverables** | Email (FFG) + Email (FHL via FFG intro) + optional call | "Your Property Position and Loan Health" PDF (segmented by purchase type) | Phone call + repricing one-pager | FHL IS MORE DETAILED |

**Assessment:** Good alignment on FHL side. **Gap: COS Stage 1 expects FFG lifestyle partner messaging and a "Home Readiness Check" invite, but the FHL playbook focuses purely on FHL value-adds (equity tracking, repricing).** The FFG cross-sell messaging doesn't appear until Month 9. This may be intentional (don't cross-sell too early) or a gap to discuss with Rowdie.

---

### COS Stage 2: "Lifestyle Under Control to Security Plan" (Month 6-24) → FHL Month 9, 12, 15, 18

| Dimension | COS Stage 2 | FHL Month 9 | FHL Month 12 | FHL Month 15 | FHL Month 18 | Status |
|-----------|-------------|-------------|--------------|--------------|--------------|--------|
| **Timing** | Month 6-24 | 9-month | 12-month | 15-month | 18-month | ALIGNED (4 touchpoints within one COS stage) |
| **Emotion** | "I'm on top of things. Could owning a place actually be possible?" | N/A (FHL customers already own) | N/A | N/A | N/A | CONFLICT - see below |
| **FHL Role** | "Turn home dream into concrete security plan" | "Anticipate next financial need, funnel to FFG, plant seed of equity release" | "Annual review, show progress, map next 12 months" | "Simple pathway to refinance" | "Commence refinance" | PARTIAL - Stage 2 is about home-buying aspiration, but FHL customers already have a home |
| **FFG Role** | "Stay go-to for lifestyle finance" | Month 9 is the FFG Momentum Pack (segmented cross-sell) | Part of annual review | N/A | N/A | ALIGNED at Month 9 |

**Assessment: This is the key structural mismatch.** The COS customer journey (Taylor 2.0) was designed for FFG-first customers who don't yet own a home. FHL customers already have a home loan. The COS stages 2-4 describe a journey from "renter to homeowner to wealth builder" which doesn't apply to someone who already settled a home loan.

**However, the FHL playbook correctly handles this** by focusing on:
- Month 9: Cross-sell to FFG (lifestyle finance) + equity release options
- Month 12: Annual review + wealth strategy
- Month 15-18: Refinance pathway (the big revenue event)

The FHL playbook is effectively its own journey that runs parallel to the COS Taylor journey, not nested within it.

---

### COS Stage 3: "Get / Upgrade the Home" (Year 2-5+) → Beyond FHL 18-Month Cycle

| Dimension | COS Stage 3 | FHL Equivalent | Status |
|-----------|-------------|----------------|--------|
| **Timing** | Year 2-5+ | Post-18-month (cycle restarts) | GAP - no explicit "what happens after 18 months" in the playbook |
| **Focus** | Pre-approval, purchase process, post-settlement optimisation | Refinance at 18 months effectively restarts the cycle | IMPLICIT but not documented |

**Assessment:** The FHL playbook ends at 18 months. The COS assumes ongoing relationship. **Gap: Need to define what happens after the 18-month refinance.** Does the cycle restart? Does the customer enter a different nurture track? This is critical for POLR V1 design.

---

### COS Stage 4: "Security Achieved to Wealth Building" (Year 5+) → Not Covered

Not addressed by the 18-month playbook. Would need a separate long-term nurture track for mature customers (annual reviews, investment property pathway, wealth strategy).

---

## ICA Routing Comparison

| FHL Purchase Type | FHL Flowchart Maps To | COS ICA Maps To | Status |
|-------------------|----------------------|-----------------|--------|
| First Home Buyer | Established Personal Borrower | Young Practical Motor Borrower | CONFLICT |
| New Purchase O/O | Prime Vehicle & Prime Convenience Borrower | Established Personal Finance + Prime Convenience + Prime Vehicle | PARTIAL MATCH |
| Refinance | Prime Vehicle, Established Personal, Prime Convenience Borrower | Established Personal Finance + Prime Convenience + Prime Vehicle | ALIGNED |
| Investor | Prime Vehicle, Prime Convenience Borrower | Prime Convenience + Prime Vehicle | ALIGNED |
| Commercial | Commercial Borrower | Business Asset Borrower | ALIGNED |

**Key conflict:** The FHL flowchart maps "First Home Buyer" to "Established Personal Borrower", but the COS ICA framework maps FHB to "Young Practical Motor Borrower". These are different ICAs with different demographics and messaging priorities.

- **Young Practical Motor:** Under 30, renting, mixed credit, reassurance/affordability messaging
- **Established Personal Finance:** 30-59, renting or mortgaged, flexibility/trust messaging

**Resolution needed:** Check with Rowdie whether FHB cross-sell should route to Young Practical Motor (younger, first-time) or Established Personal (more stable, broader needs). The COS `fhl_purchase_type_mapping` data says Young Practical Motor maps to FHB, which contradicts the flowchart.

---

## Summary of Findings

### Strong Alignments (build on these)
1. Month 1 welcome/setup maps perfectly to COS Stage 0
2. Month 3 equity benchmark + Month 6 repricing align with COS Stage 1 confidence-building
3. Month 9 FFG cross-sell is the agreed critical revenue moment
4. Month 12 annual review matches COS's "big advisor moment" positioning
5. Month 15-18 refinance pathway is the documented revenue event (clawback period exit)

### Gaps to Address
1. **Post-18-month lifecycle:** What happens after refinance? Cycle restart? Different track? POLR V1 needs a defined "next state."
2. **FFG lifestyle messaging in months 1-6:** COS expects it, playbook doesn't deliver it until month 9. Deliberate or oversight?
3. **COS Stage 2-4 mismatch:** The Taylor journey assumes FFG-first (renter to homeowner). FHL customers are already homeowners. The COS journey needs a parallel "FHL-first" track, or acknowledgement that FHL customers skip stages 2-3.

### Conflicts to Resolve
1. **FHB ICA mapping:** Flowchart says Established Personal Borrower, COS says Young Practical Motor Borrower. Need Rowdie's call.

### Implications for POLR V1
1. **V1 scope (FHL 18-month nurture) is well-defined** by the playbook - 7 touchpoints, 5 purchase types, segmented deliverables.
2. **Data model is clear** from the Ambition application export - residential status, employment type, and existing liabilities are the key routing fields.
3. **The FHL playbook IS the V1 methodology** - it just needs to be encoded into POLR's touchpoint engine with the right segmentation logic.
4. **Settlement call (dealer checklist)** feeds into the referral ecosystem but is pre-nurture, not part of the 18-month sequence. It's an FFG process, not an FHL one.
