# Business Model

**Playbook:** Fox Group Master Playbook (Cross-Sell and Monetisation)
**Version:** 2.0
**Created:** 2026-03-12
**Owner:** James
**Status:** Active

---

## Purpose

How Fox Group makes money today. How the new GHL-delivered 5-ICA engine shifts that model from one-off commissions to lifetime customer value. Cross-sell trigger is locked at 9-12 months post-settlement, with an at-settlement seed.

UMI revenue is included for group completeness. UMI is **not in scope** for either playbook. Treat UMI numbers as background.

---

## Value Proposition

### Unique Selling Proposition

Fox Group is the only financial services group in Queensland that connects asset finance, home loans, and sub-prime lending under one client relationship. The 12-month, 5-ICA post-settlement system (built in GHL, content driven by Fox-MIS) is what turns that connection into compounding lifetime value rather than three businesses sharing a logo.

### Differentiators

| Differentiator | Description |
|----------------|-------------|
| Ecosystem breadth | Asset finance + home loans + sub-prime under one ownership |
| 5-ICA journeys | Five separate post-settlement journeys, one per ICA. Content, tone, FHL pathway, and cross-sell timing all change based on profile |
| Give it all away | Cotality valuations, rate intelligence, and education delivered before any sales pitch. Earn the right to sell at Month 9 |
| Behavioural branching | Click on FHL content, sequence pivots. Click on rate calculator, get a rate review. Email opens are not the trigger (iOS Mail Privacy Protection) |
| 9-12 month cross-sell window | Locked timing matches credit-recovery curve and historical second-loan data. Plus an at-settlement seed for purchase-type identification |
| UMI graduation pipeline (ecosystem context only) | Direct UMI clients can rehabilitate into mainstream Fox products as their credit recovers. Out of playbook scope but worth noting as a long-term group flywheel |

### Pillars of Value

**Expertise across the full lending spectrum.** From a $10,000 consumer car loan to a multi-million dollar commercial property deal, Fox Group has the capability, lender relationships, and specialist knowledge to support clients at every level.

**Proactive advocacy, not reactive service.** Fox does not wait for clients to ask. Rate reviews happen regardless. Valuations are sent without prompting. Cross-sell opportunities are surfaced based on life stage data.

**A lifelong relationship, not a transaction.** The settlement is not the end. It is the beginning. The 12-touchpoint nurture continues to deliver value for as long as the client is in the Fox ecosystem.

**Dignity for every client.** UMI clients are treated with the same respect as anyone in the Fox ecosystem. Second-chance is a different starting point, not a lower tier.

---

## Revenue Streams Breakdown

### FFG: Commission on Settled Asset Finance

FFG is a broker. It matches borrowers to lenders and earns a commission on settlement.

| Metric | Value |
|--------|-------|
| Leads per month | 375 |
| Settlements per month | 90-108 |
| Average commission per deal | $2,300 |
| Revenue per lead | ~$433 |
| End-to-end conversion rate | ~17% |
| Monthly revenue estimate | $207,000-$248,400 |
| Annual revenue estimate | $2.5M-$3.0M |

FFG earns once per deal. There is no trail. When the loan settles, the financial relationship with FFG is complete unless the client returns for another deal.

Repeat and referral business accounts for 70-80% of settlements. Repeat customers convert at 40-45% vs 5-10% for organic new leads.

### FHL: Upfront Commission + Trail + Fees

FHL is a mortgage broker with three revenue components.

| Component | Value |
|-----------|-------|
| Income per deal (combined) | $4,750-$5,225 |
| Trail commission | 0.65% per annum on loan balance |
| Broker fee (client-paid) | $990 |
| Commercial mandate | ~$2,000 |
| Conveyancer referral fee | $200 per deal |
| Average loan size | ~$600,000 |
| Settlements per month | 16-17 |
| Leads per month | 55 |
| Revenue per lead | ~$1,050 |
| Residential/commercial split | 70/30 |
| Clawbacks per month | 1-2 |

Trail commission is the most structurally significant element. A $600,000 loan at 0.65% trail generates $3,900 per year in recurring revenue for as long as the loan remains with the original lender. A book of 200 settled loans generates approximately $780,000 per year in trail alone, independent of new settlements.

Clawbacks (1-2 per month) reduce income when a client refinances or exits within the lender's clawback period (typically 12-24 months). This is why the FHL lifecycle plan delays the refinance conversation until Month 18.

### UMI: Interest Income on Loan Book (Ecosystem Context, Out of Scope)

UMI is a lender, not a broker. It holds its own loan book and earns through interest charged to borrowers. **UMI is not in scope for either playbook.** This block is here for group completeness, not as a workstream.

| Metric | Value |
|--------|-------|
| Loan book | ~$28 million |
| Revenue type | Interest income |
| Average loan size | Not yet validated (Mason to provide) |
| Default rate | Not yet validated (Mason to provide) |

UMI carries credit risk that FFG and FHL do not. If borrowers default, UMI wears the loss. That is a different game from a commission model. The playbooks do not touch this game.

### Lead Market Revenue

| Metric | Value |
|--------|-------|
| Leads sold per year | 49,000 (34,000 UMI + 15,000 Fox) |
| Revenue | $48,000-$144,000 per year ($4,000-$12,000/month) |
| Average lead price | $24-26 per lead sold |
| Reactivation status | Zero. Never re-engaged after selling. |
| Reactivation potential | $1 million per year (Nathan's estimate, compounding) |

Leads can legally be reactivated and re-engaged after a 3-month cooling period. Currently none are. The reactivation campaign in this playbook targets the **FFG** portion of that pool (15,000 per year). UMI leads are out of scope for the reactivation build.

### Trusted by Fox (Affiliate Ecosystem)

The referral partner ecosystem is conceptual, not yet operational. The $200 conveyancer referral fee is the only active element.

When operational, the ecosystem will include accountants, insurance brokers, property buyers agents, conveyancers, family lawyers, business coaches, and HR providers. The philosophy is "no cash, just look after each other's customers" for reciprocal referrals, with the conveyancer arrangement as the exception.

Revenue contribution from the full ecosystem is not yet defined.

---

## Money Model

### Current State

| Stage | FFG | FHL |
|-------|-----|-----|
| Core offer | Asset finance (car, personal, equipment, consolidation) | Home loan (purchase, refinance, investment) |
| Upsell | Insurance add-ons (comprehensive, warranty packages) | Commercial mandate ($2,000), broker fee ($990) |
| Continuity | None (one-time commission) | Trail commission (0.65% ongoing) |
| Cross-sell | Manual referral to FHL (underperforming) | Manual referral to FFG (underperforming) |

### How the New System Changes the Money Model

The post-settlement engine does not generate direct revenue. It creates the conditions for dramatically higher lifetime value per client by:

1. **Earning the right to sell at Month 9.** Each ICA journey delivers 2-3 pieces of value before any soft product mention. By Month 9 the customer trusts Fox. The "ready when you are" message lands instead of being filtered as spam.

2. **Surfacing cross-sell opportunities automatically.** When a customer clicks any FHL-related link, the `FHL_Interest` tag triggers the 3-email FHL Referral Workflow plus a notification to the FHL broker. The ICA workflow pauses for 21 days. No human has to remember.

3. **Reactivating dormant leads.** 49,000 leads per year currently sold to the lead market. The reactivation campaign targets 6-12 month dormant leads (12-month tested first per Rowdie), nurturing with value-first content rather than selling them.

4. **Hot-lead capture in the cross-sell window.** Click on a FFG product CTA in months 7-12 applies the `FFG_HotLead` tag, sends a broker task, pauses the email sequence for 14 days for human follow-up. The hot moment is never missed.

5. **VIP treatment for highest-value ICAs.** Prime Convenience-Led Repeat Borrowers (PCLRB) get pre-approval offers at Day 270, the most effective trigger for the highest-conversion-probability ICA.

---

## Cross-Sell Revenue Opportunity

### Cross-Sell Timing (Locked 27 April 2026)

Cross-sell triggers at two points:
- **At settlement** - identify FHL purchase type during the FFG settlement call. Tag accordingly. Seed the FHL pathway in the customer's journey from Day 3.
- **9-12 months post-settlement** - the conversion window. Aligns with credit-score recovery and historical data showing the most common second-loan timing.

This replaces the earlier "Month 18 refinance conversation" framing. The 9-12 month window is locked.

### FFG to FHL

Nathan confirmed approximately 50% of FFG clients already own a home (not necessarily with FHL).

| Scenario | Conservative (5%) | Moderate (10%) |
|----------|-------------------|----------------|
| FFG homeowner clients per month | 45-54 | 45-54 |
| Conversion to FHL refinance in 9-12 month window | 2.25-2.7 per month | 4.5-5.4 per month |
| FHL income per deal | $4,750-$5,225 | $4,750-$5,225 |
| New FHL monthly revenue | $10,688-$14,108 | $21,375-$28,215 |
| New FHL annual revenue | $128,250-$169,290 | $256,500-$338,580 |

This is new FHL revenue generated from the existing FFG client base at near-zero acquisition cost. These clients are already in the ecosystem. The only cost is the GHL delivery and the 9 months of value content that earns the right to ask.

Plus trail commission: each converted client adds approximately $3,900 per year in ongoing trail revenue on a $600,000 loan.

**FHL conversion ranking by ICA (highest to lowest probability):** PCLRB > PVB > EPFB > YPMB > BAB. PCLRB has the highest FHL conversion potential of any ICA (investment property and refinancing both realistic). YPMB is First Home Buyer pathway only - longer fuse, lower per-deal value but high lifetime value if Fox is their first home loan.

### Lead Market Recapture

267-285 FFG leads per month currently do not convert and are sold to the lead market.

If 50% of non-converting leads enter the reactivation campaign instead of being sold:
- 133-143 leads per month enter the nurture pipeline
- At 5% conversion over 12 months: 6-7 additional FFG settlements per month
- At $2,300 commission: $13,800-$16,100 per month in recovered revenue

**Trade-off note:** Retaining leads for reactivation partially offsets current lead market revenue ($48,000-$144,000 per year). The business case depends on actual reactivation conversion, which is measurable after the campaign goes live. Nathan to make the call with full data. Reactivation campaign starts with 12-month dormant leads (test before scaling to 6-month sweet spot).

### FHL to FFG

FHL clients who settle a home loan often have immediate adjacent needs: car for the new commute, furniture, renovations (non-structural), debt consolidation. The FHL 18-month lifecycle plan includes a Month 9 "FFG Momentum Pack" with segmented packs for New Purchase, FHB, Investor, and Refinancer profiles. This direction sits inside the FHL master playbook (separate from this cross-sell-from-FFG playbook). Revenue contribution to be quantified once both playbooks are live.

---

## LTGP and CAC Frameworks

### Current State

| Metric | FFG | FHL |
|--------|-----|-----|
| Customer Lifetime Value | Unknown (not tracked) | Unknown (not tracked) |
| Cost to Acquire Customer | $100-$150 (estimate) | Not specified |
| LTV:CAC Ratio | Cannot calculate | Cannot calculate |

### What Changes with the New System

The single most important metric this engine enables is **cross-entity lifetime value**. Today, LTV is measured per entity (if it is measured at all). With the 5-ICA engine, a client who enters through FFG for a car loan, refinances through FHL in the 9-12 month window, returns for a second FFG deal, and adds an investment property has a group LTV that spans both entities.

Example (Prime Convenience-Led Repeat Borrower path):
- FFG settlement (PCLRB tagged at settlement): $2,300 commission
- Pre-approval offer at Day 270 - PCLRB clicks - `FFG_HotLead` tag fires
- FHL refinance in the 9-12 month window: $4,750-$5,225 upfront + $3,900/year trail
- Second FFG deal at Month 18-24: $2,300 commission
- FHL investment property at Year 3-5: $4,750-$5,225 upfront + trail on combined book

Client group LTV over 5-7 years: $20,000+ upfront plus growing trail. Compared to $2,300 one-time without the engine.

---

## Ideas

One future consideration is packaging the 5-ICA engine + Fox-MIS content stack as a white-label offering for non-competing brokerages in other states. If Fox demonstrably lifts cross-entity LTV through this system, there may be a licensing or partnership opportunity. This is speculative and out of scope for the current implementation. The Beacon on the Hill long-term vision (custom POLR build) remains paused but not killed and may resume if GHL surfaces real gaps.

---

## Related Documents

- Business Overview
- Ideal Client Profiles and Avatars
- Pipeline Overview (pending)
- Performance Scorecard (pending)
