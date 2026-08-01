# HANDOFF TO ORCHESTRATOR — POLR UNIFIED VALUE JOURNEY: STRATEGY + INTERACTIVE HTML

## ACTIVATION REQUIRED — DO THIS FIRST

**Step 1: Activate the agent**
Read: .claude/agents/orchestrator.md

**Step 2: Follow activation instructions**

**Step 3: Announce initialization**
Initialized as Orchestrator. Ready to coordinate POLR Unified Value Journey — Strategy + Interactive HTML.

## PROJECT CONTEXT SUMMARY
**Project:** Fox Finance Group · Two in-scope businesses (FFG asset finance, FHL home loans). POLR is a custom platform (Supabase + Next.js + N8N + SendGrid + Twilio) that sits ABOVE both businesses as the continuous value journey layer. UMI is OUT OF SCOPE.
**Current Phase:** Observe → Roadmap transition
**Your Mission:** Two phases. PHASE 1: Coordinate strategic agents to define all matrices, entry points, handoff points, trigger points, and communication principles for the POLR unified value journey. PHASE 2: Route to Developer + UI/UX skill to build an interactive HTML tool that visualises the entire journey dynamically.
**Session Type:** Strategy → Build

## THE CORE ARCHITECTURE — POLR AS PARENT ENTITY

### Critical Framing
POLR is NOT a feature of FFG or FHL. POLR is the **parent layer** that sits above both businesses. Every person's relationship is with POLR first. POLR hands leads DOWN to FFG or FHL when trigger conditions are met. But the POLR journey NEVER stops — it continues before, during, and after any business transaction.

```
POLR (continuous value journey — owns the relationship, never ends)
  │
  ├── Handoff → FFG (pre-sales → application → settlement)
  │   FFG pre-sales playbook handles this (exists, stays as is)
  │   └── After settlement → person returns to POLR lifecycle
  │
  ├── Handoff → FHL (pre-sales → application → settlement)
  │   FHL pre-sales playbook handles this (exists, stays as is)
  │   └── After settlement → person returns to POLR lifecycle
  │
  └── No handoff yet (person receiving POLR value, building trust)
      Could be a Fox client or a complete non-client — doesn't matter
      POLR delivers the same value regardless
```

### What This Means
- **Entry points are into POLR**, not into FFG/FHL directly
- **Handoff points** are where POLR routes a person to a business (based on triggers)
- **FFG/FHL pre-sales playbooks** (existing, kept as is) handle what happens AFTER the handoff — the call cadence, scripts, application process, settlement
- **Post-settlement**, the person returns to POLR's lifecycle — it's not an "FFG lifecycle" or "FHL lifecycle," it's a POLR lifecycle that includes FFG and FHL value-adds at the right moments
- **Non-clients** stay in POLR indefinitely, receiving value. They might never become a Fox client. That's fine. But many will, because the value builds trust over time.
- **A person can be handed off to FFG, settle, return to POLR, then get handed off to FHL later** — all within one continuous POLR journey
- **The POLR journey runs in parallel with any business transaction** — when someone is in the FFG application process, POLR doesn't pause. It continues providing value on a separate track.

### Existing Playbooks — Left As Is
The FFG and FHL pre-sales developer guides and handbooks exist and handle business-level execution:
- FFG: 4-day manual call cadence, broker scripts, application process
- FHL: 10-day call cadence, journey classification, Purchase Type-specific docs, broker routing

These are NOT being redesigned. They handle what happens AFTER POLR hands off a lead. This mapping exercise defines the POLR layer that wraps around and above them.

### The Three Layers

| Layer | What It Does | Owned By | Automation Level |
|-------|-------------|----------|------------------|
| **POLR** | Continuous value journey. Entry, lifecycle, triggers, education, trust-building. Runs forever. | POLR platform (N8N + Supabase) | Mostly automated + AI-assisted |
| **Business Transaction** | Pre-sales → application → settlement. Time-bound. | FFG or FHL team (brokers, SDR) | Mostly manual (existing playbooks) |
| **Handoff Logic** | When/why POLR routes a person to FFG or FHL. And when they return. | Rules engine (N8N) | Fully algorithmic |

## THE TWO LIFECYCLES — DIFFERENT DEPTH

### FHL Lifecycle (Comprehensive — Rowdy's Design, Confirmed)
FHL has trailing revenue (0.65% trail commission on ~$600K avg loan). Every lifecycle touchpoint protects that trail. Rowdy has documented a full 18-month plan with proactive value at each stage:

- **Month 1:** Welcome + Setup Verified (phone + email)
- **Month 3:** 90-Day Confidence Pack (Cotality valuation, segmented: FHB/Investor/Refinancer)
- **Month 6:** Proactive Pricing Review (repricing advocacy — "we did the work without you asking")
- **Month 9:** FFG Momentum Pack (cross-sell handoff trigger — 5 ICA-targeted packs)
- **Month 12:** Annual Property & Loan Strategy Review (updated valuation + strategy)
- **Month 15:** Refinance Pathway (3 options: pay down, invest, refinance)
- **Month 18:** Action Window (trigger-based: fixed expiry, market movement, goal change)

This is confirmed, detailed, and ready to operationalise.

### FFG Lifecycle (Light — HYPOTHETICAL, Needs Client Validation)
FFG has NO trailing revenue — commission is one-time ($2,300 avg). There's no financial incentive to maintain intensive post-settlement engagement. The current FFG post-settlement is just basic time-based emails with no real value:
- Day 3: Thank you + review reminder
- Month 1: Reminder
- Month 6: Refer a friend
- Month 12: Home lending message
- Month 18+: Generic

**We have asked Rowdy whether a documented FFG lifecycle exists (message sent 2026-03-23). Until confirmed, use these HYPOTHETICAL FFG lifecycle touchpoints based on the business logic:**

The value of keeping an FFG client engaged is:
1. **Repeat business** — another vehicle/personal loan (replacement cycle ~3-5 years for vehicles, variable for personal loans)
2. **Cross-sell to FHL** — detect homeowner status or home-buying intent
3. **Referrals** — already 60-65% of settlements are repeat/referral

**Hypothetical FFG POLR Lifecycle:**

- **Month 1:** Welcome + Setup Verified
  - Confirm loan details, first repayment, direct debit set up
  - Introduce POLR value ("your financial wellness hub")
  - Tone: warm, reassuring ("everything's sorted, we're here if you need us")
  - Light cross-sell seed: one-line FHL mention ("when you're ready to think about property, we've got you covered")

- **Month 3:** Financial Health Check-In
  - "How's everything going with the loan? Any questions?"
  - ICA-targeted content:
    - Young Practical Motor: "5 tips to build your credit score while repaying"
    - Established Personal Finance: "Are your debts getting simpler? Here's how consolidation tracks over time"
    - Prime Convenience Repeat: "Quick check — are you getting the best rate?"
    - Business Asset: "EOFY approaching — is your asset structure working for you?"
    - Prime Vehicle: "Your vehicle value tracker — how depreciation affects your position"
  - Format: Email (light touch, not a phone call — FFG doesn't warrant the same manual investment as FHL)
  - Referral nudge: "Know someone who needs finance? We'd love to help them too"

- **Month 6:** Next Need Detector
  - Purpose: Surface the next lending opportunity or cross-sell trigger
  - ICA-targeted probing:
    - Young Practical Motor: "Thinking about upgrading? Or is it time to look at your first home?"
    - Established Personal Finance: "Planning anything big in the next 6 months? Home renos, travel, consolidation?"
    - Prime Convenience Repeat: "Need anything? Fast-track approval for existing clients"
    - Business Asset: "Equipment replacement coming up? New vehicle? Growth plans?"
    - Prime Vehicle: "Vehicle upgrade on the horizon? We can pre-approve before you start looking"
  - Cross-sell detection: If homeowner → flag for FHL handoff
  - Format: Email + optional SMS ("Quick question — got 2 minutes?")

- **Month 9:** Value Delivery + Cross-Sell Moment
  - Purpose: Deliver genuine value AND surface cross-sell naturally
  - Content: "Your Loan Health Summary" — 1-page showing: repayment progress, remaining term, early payout status (reference Early Payout Guide — Doc 11), what you've saved vs going direct
  - Cross-sell: If homeowner AND not already FHL client → "Did you know we also do home loans? We could check if you're getting the best rate on your mortgage — no cost, no obligation" → FHL handoff trigger
  - If not homeowner: "Thinking about buying your first home? Here's what you need to know" → educational content, soft FHL seed
  - Format: Email with 1-page PDF attachment

- **Month 12:** Annual Check-In + Renewal Detector
  - Purpose: Annual review, detect renewal/repeat opportunity
  - Content: "It's been a year — here's where you stand"
  - Loan status: remaining balance, early payout position
  - Prompt: "Is your car still meeting your needs? Any finance needs coming up?"
  - Referral program: "Happy with your experience? Refer a friend and we'll [incentive TBD]"
  - If loan is nearing end of term: proactive replacement conversation
  - Format: Email, escalate to broker call if engagement detected

- **Month 18:** Replacement Cycle Prompt
  - Purpose: Vehicle/equipment replacement cycle prompt
  - ICA-targeted:
    - Vehicle ICAs: "Most people start thinking about their next car around now. Want us to run the numbers?"
    - Business Asset: "Equipment replacement or fleet expansion? Let's plan ahead for next financial year"
    - Personal Finance: "Any big plans? We can pre-approve so you're ready when you need it"
  - Format: Email + SMS
  - If engaged → handoff back to FFG pre-sales (repeat business)

- **Year 2-3+:** Low-Frequency Nurture
  - Quarterly: market update, rate change notification, seasonal content
  - Annual: "Still here if you need us" + referral prompt
  - Trigger-based: if engagement detected on any touchpoint → escalate to broker outreach

**Key differences from FHL lifecycle:**

| Aspect | FHL Lifecycle | FFG Lifecycle (Hypothetical) |
|--------|--------------|------------------------------|
| **Depth** | Comprehensive — 7 proactive value touchpoints | Light — check-ins and prompts |
| **Manual involvement** | Broker calls at key moments (Month 1, 6, 12) | Mostly automated, broker only if engagement detected |
| **Value delivery** | Cotality valuations, repricing, refinance reviews | Loan health summaries, early payout info, rate checks |
| **Cross-sell** | Month 9 FFG Momentum Pack (5 ICA packs) | Ongoing homeowner detection → FHL handoff |
| **Revenue protection** | Trail commission (ongoing, must protect) | None (one-time commission, already earned) |
| **Repeat trigger** | Refinance cycle (2-3 years) | Vehicle/equipment replacement (3-5 years), personal loan needs |
| **Primary intent** | Retain + protect trail + cross-sell to FFG | Stay top of mind + detect next need + cross-sell to FHL + referrals |
| **Frequency** | Monthly-ish (7 structured touchpoints in 18 months) | Quarterly-ish (lighter, 6 touchpoints in 18 months then low-frequency) |

**IMPORTANT:** The FFG lifecycle above is HYPOTHETICAL. It's based on business logic and mirrors the FHL structure at lower intensity. It needs validation from Rowdy/Nathan. The matrix and HTML tool should flag these as "proposed" and visually distinguish them from confirmed FHL touchpoints.

## THE FIVE CORE ICAs

1. **Young Practical Motor Borrower** — Under 40, renting/parents, car loans. → FHL: First Home Buyer
2. **Established Personal Finance Borrower** — 30-59, personal loans. → FHL: New Purchase, Refinance
3. **Prime Convenience-Led Repeat Borrower** — 30-59, prime, repeat. → FHL: New Purchase, Refinance, Investor
4. **Business Asset Borrower** — 30-59, self-employed, commercial. → FHL: Commercial
5. **Prime Vehicle Borrower** — 40-59, prime, vehicle upgrade. → FHL: New Purchase, Refinance, Investor

### FHL Purchase Type Writing Guidance (Rowdy-confirmed)
- **First Home Buyer:** Fundamentals, deposit/LVR basics, up-front costs, pre-approval, confidence
- **New Purchase:** Readiness, borrowing power, offer/contract timing, reducing friction
- **Refinance:** Triggers, rate/fee comparison, equity/LVR, 'health check' decision path
- **Investor:** Cash flow, long-term strategy, structure/features, risk management (NO advice)
- **Commercial:** Documentation, timelines, deal structure, 'what to prepare' checklists

### Key Metrics
- FFG: 375 leads/month, 90-108 settlements/month, $2,300 avg commission
- FHL: 55 leads/month, 16-17 settlements/month, ~$4,987/deal + 0.65% trail on ~$600K avg loan
- 49K leads/year sold to lead market with ZERO reactivation ($1M/year potential)
- Repeat customers convert at 40-45% vs 5-10% cold
- Revenue per lead: FFG ~$433, FHL ~$1,050

## CONTEXT FILES TO READ FIRST

### Required Reading
1. `cos.yaml` — FULL file. The `icas` data has the complete 5-profile framework with FHL Purchase Type mapping, writing guidance, routing priority, and CRM tags.
2. `docs/updated-docs/extracted-content.md` — All 14 docs. Especially Doc 10 (FHL lifecycle), Docs 16-17 (ICA matrix + definitions), Doc 11 (Early Payout Guide — useful for FFG Month 9 touchpoint)
3. `docs/Background/Activation Meeting - Full Transcript.md` — Deep-dive for Nathan's "Beacon on the Hill" vision. This IS the POLR-as-parent-entity concept.
4. `playbooks/master-playbook/tone-of-voice.md` — Brand voice (5 pillars)
5. `playbooks/master-playbook/04-business-model.md` — Revenue model context
6. `docs/branding/` — Fox Finance Group Branding Guide (colours, fonts for the HTML build)
7. `deliverables/polr-mvp-scope-of-work-2026-02-13.md` — Current POLR platform capabilities

## PHASE 1: STRATEGY — DEFINE THE MATRICES

### Objective
Produce the complete strategic framework as structured data (JSON objects) that Phase 2 will render as interactive HTML. Each matrix must be fully defined before any code is written.

### Route to These Agents/Skills (in order)

**1. Hormozi Coach** — Strategic framing:
- POLR as "Grand Slam Offer" (free platform → trust → conversion)
- Customer Financed Acquisition model
- Crazy Eight LTV levers within the POLR journey
- Value equation per entry point

**2. Pre-Sales Specialist** — Entry + handoff points:
- All entry points into POLR and data captured at each
- What qualifies as a handoff trigger to FFG or FHL?
- When does a POLR non-client become a lead?
- How do existing pre-sales playbooks receive the handoff?

**3. Cross-Sell Specialist** — Trigger point mapping:
- Every cross-sell moment in the POLR journey
- ICA → FHL Purchase Type trigger logic
- Month 9 triggers in BOTH directions (FFG Momentum Pack for FHL clients, FHL cross-sell detection for FFG clients)
- How homeowner detection works as a trigger

**4. Retention Specialist** — Lifecycle backbone:
- How POLR lifecycle differs for FFG-settled vs FHL-settled vs both vs neither
- Trail commission protection (FHL) vs repeat business generation (FFG)
- Churn risk signals
- Reactivation strategy for 49K lead market leads

**5. Domain Expert** — Compliance:
- Non-client communications boundaries
- POLR as lead magnet in financial services
- Data collection obligations

### The 6 Matrices to Define

**MATRIX 1: POLR Entry Points**

```json
// For each entry point:
{
  "id": "slug",
  "name": "Human-readable name",
  "source": "organic | ads | referral | partner | polr_direct | reactivation | internal_crosssell",
  "person_type": "new_prospect | existing_ffg_client | existing_fhl_client | both_client | non_client | reactivation",
  "data_captured_at_entry": ["field1", "field2"],
  "ica_assignment_method": "algorithmic | self_declared | manual | inferred",
  "initial_polr_position": "Where they start in the POLR journey",
  "immediate_handoff_eligible": true/false,
  "handoff_target": "ffg | fhl | none",
  "example_scenario": "..."
}
```

Entry points to map:
1. FFG website/phone enquiry → POLR → immediate FFG handoff
2. FHL website/phone enquiry → POLR → immediate FHL handoff
3. POLR direct signup (has mortgage elsewhere)
4. POLR direct signup (renting, no loans)
5. Referral partner lead (FFG-aligned)
6. Referral partner lead (FHL-aligned)
7. Reactivation lead (49K lead market — FFG declined)
8. Reactivation lead (FHL declined)
9. FFG settled client returning to POLR lifecycle
10. FHL settled client returning to POLR lifecycle
11. Content/education lead (blog, social, search)
12. Google Ads lead

**MATRIX 2: Handoff Points (POLR ↔ Business)**

```json
{
  "id": "slug",
  "name": "Human-readable name",
  "direction": "polr_to_ffg | polr_to_fhl | ffg_return_to_polr | fhl_return_to_polr",
  "trigger_condition": "The IF statement that fires this handoff",
  "required_data": ["fields that must be known"],
  "handoff_method": "warm_broker_intro | automated_task | self_service_booking | internal_referral",
  "receiving_playbook": "Which existing playbook document picks this up",
  "polr_during_handoff": "What POLR does while business transaction is active",
  "return_trigger": "When the person returns to POLR lifecycle",
  "example_scenario": "..."
}
```

Handoffs to map:
1. New FFG lead → FFG pre-sales (immediate)
2. New FHL lead → FHL pre-sales (immediate)
3. POLR non-client signals FFG intent → FFG pre-sales
4. POLR non-client signals FHL intent → FHL pre-sales
5. FHL lifecycle Month 9 → FFG Momentum Pack → FFG handoff
6. FFG lifecycle Month 6/9 → homeowner detected → FHL handoff
7. FFG client business growth → FHL commercial handoff
8. FHL client needs vehicle/equipment → FFG handoff
9. FFG settlement complete → return to POLR
10. FHL settlement complete → return to POLR
11. Declined lead (3-month cooling) → re-enters POLR value journey
12. POLR non-client converts (books call / requests quote) → handoff

Critical rule: POLR reduces frequency but doesn't stop during business transactions. The parallel track continues.

**MATRIX 3: POLR Lifecycle Stages**

This is the core matrix. It maps the CONTINUOUS POLR journey, with BOTH the confirmed FHL touchpoints and the hypothetical FFG touchpoints:

```json
{
  "id": "slug",
  "name": "Touchpoint name",
  "timing": "When in the journey",
  "applies_to": "all | ffg_settled | fhl_settled | both_settled | non_client",
  "status": "confirmed | hypothetical",  // CRITICAL: flag unconfirmed FFG touchpoints
  "intent": "educate | nurture | trigger_handoff | deliver_value | cross_sell | retain | reactivate",
  "touchpoint_type": "email | sms | polr_notification | call | valuation | content",
  "manual_or_automated": "automated | manual_broker | hybrid",
  "ica_variation": {
    "young_practical_motor": "specific messaging",
    "established_personal_finance": "specific messaging",
    "prime_convenience_repeat": "specific messaging",
    "business_asset": "specific messaging",
    "prime_vehicle": "specific messaging"
  },
  "purchase_type_variation": {  // FHL only
    "first_home_buyer": "...",
    "new_purchase": "...",
    "refinance": "...",
    "investor": "...",
    "commercial": "..."
  },
  "client_vs_nonclient": "How this differs for non-clients",
  "handoff_trigger": "Does this trigger a handoff? Under what conditions?",
  "data_required": ["fields needed"],
  "compliance_notes": "...",
  "example_content": "..."
}
```

**FHL Lifecycle Stages (CONFIRMED — Rowdy's design):**
- Month 1: Welcome + Setup Verified
- Month 3: 90-Day Confidence Pack (Cotality valuation, segmented)
- Month 6: Proactive Pricing Review (repricing advocacy)
- Month 9: FFG Momentum Pack (cross-sell handoff — 5 ICA-targeted packs)
- Month 12: Annual Property & Loan Strategy Review
- Month 15: Refinance Pathway
- Month 18: Action Window

**FFG Lifecycle Stages (HYPOTHETICAL — needs Rowdy/Nathan validation):**
- Month 1: Welcome + Setup Verified (light — confirm loan, introduce POLR, soft FHL seed)
- Month 3: Financial Health Check-In (ICA-targeted content, referral nudge)
- Month 6: Next Need Detector (surface next opportunity, homeowner cross-sell detection)
- Month 9: Value Delivery + Cross-Sell Moment (loan health summary, FHL handoff if homeowner)
- Month 12: Annual Check-In + Renewal Detector (replacement cycle, referral program)
- Month 18: Replacement Cycle Prompt (vehicle/equipment, repeat FFG handoff)
- Year 2-3+: Low-frequency nurture (quarterly, trigger-based)

**Non-Client Stages (PROPOSED):**
- POLR Onboarding (first 7 days)
- Value Delivery (ongoing — tools, calculators, education)
- Conversion Signal Detection (behaviour → handoff trigger)

**MATRIX 4: Cross-Business State Resolution**

```json
{
  "ffg_state": "none | lead | applicant | settled | lifecycle_month_X | declined | lost",
  "fhl_state": "none | lead | applicant | settled | lifecycle_month_X | declined | lost",
  "is_meaningful": true/false,
  "priority": 1-5,
  "polr_action": "What POLR does",
  "handoff_eligible": "ffg | fhl | both | none",
  "communication_principle": "...",
  "example_scenario": "..."
}
```

~20-30 meaningful combinations. Top 10 highlighted.

**MATRIX 5: Communication Principles**

```json
{
  "stage_id": "slug",
  "intent": "...",
  "tone_pillar": "Which of the 5 voice pillars dominates",
  "format_primary": "...",
  "frequency": "...",
  "ica_messaging_variation": { ... },
  "purchase_type_variation": { ... },
  "client_vs_nonclient": "...",
  "compliance_boundaries": "...",
  "example_message": "..."
}
```

**MATRIX 6: Signal Detection & Data Requirements**

```json
{
  "variable_name": "...",
  "source_system": "ambition_api | finshaws_csv | polr_form | self_declared | inferred | behaviour",
  "detection_method": "...",
  "reliability": "high | medium | low",
  "when_captured": "entry | qualification | settlement | lifecycle | ongoing",
  "required_for": ["matrix1", "matrix3"],
  "fallback_if_unknown": "..."
}
```

Variables to map:
- ICA profile, homeowner status, existing Fox relationship, employment type, Purchase Type, household, loan product details, key dates, likely next finance needs, intent signals, cross-sell eligibility, churn risk, life events

### Phase 1 Output
`deliverables/unified-journey-data.json` — All 6 matrices as structured JSON.

## PHASE 2: BUILD — INTERACTIVE HTML

### Objective
Build a single-file dynamic HTML tool that visualises the POLR unified value journey.

### Route To
1. **Developer agent** — Code architecture and data binding
2. **UI/UX skill** (`/ui-ux-pro-max`) — Visual design, interactions, polish

### Tech Stack
- Single HTML file (self-contained, CDN only)
- Tailwind CSS via CDN
- Vanilla JS or Alpine.js
- Data embedded as JSON
- Branding: POLR gets its own visual identity layer above Fox. Fox branding #ED9B33 (orange), #63666A (gray), #101820 (black), Muli font. FHL accent: complementary blue. POLR accent: a colour that sits above both (teal, or a neutral that reads as "platform").

### Views

**View 1: POLR Journey Map (Default)**
The centrepiece. POLR as horizontal continuous layer. FFG and FHL branch downward at handoff points, return upward after settlement.
- Entry points on the left (filterable)
- Handoff points highlighted with directional arrows
- Lifecycle touchpoints along the POLR line
- **FHL touchpoints styled as "confirmed"** (solid)
- **FFG touchpoints styled as "hypothetical"** (dashed/hatched)
- Click any element → detail panel
- Toggle: show/hide non-client track
- Toggle: show/hide FFG lifecycle / FHL lifecycle / both
- Toggle: show/hide handoff branches

**View 2: Entry Point Explorer**
Card-based. Click → highlights path through journey map.
- Filter by person type, source, handoff eligibility

**View 3: Handoff Point Explorer**
Every POLR ↔ Business handoff.
- Timeline view
- Shows trigger condition, receiving playbook, POLR parallel behaviour
- Directional: down-arrows (POLR → business), up-arrows (return to POLR)

**View 4: State Matrix Explorer**
FFG × FHL interactive grid.
- Click cell → POLR action, handoff eligibility, communication principle
- Colour by priority
- Filter by ICA
- Top 10 highlighted

**View 5: Lifecycle Comparison**
Side-by-side: FFG lifecycle vs FHL lifecycle within POLR.
- Timeline running vertically (Month 0-18+)
- Left column: FFG touchpoints (dashed = hypothetical)
- Right column: FHL touchpoints (solid = confirmed)
- Centre: shared POLR elements
- Click any touchpoint → ICA variation detail
- Shows depth difference visually (FHL is richer, FFG is lighter)

**View 6: Communication Rules Engine**
Select: ICA + Purchase Type + Stage + Client/Non-client → see exact communication.
- Side-by-side comparison of two profiles
- Compliance warnings in red

**View 7: Signal Detection Dashboard**
Data requirements overview.
- Colour by reliability
- Filter by source system
- Highlight unknowns/blockers

### Interaction Patterns
- Tabs for views
- Persistent filters across views
- Detail panels slide from right
- Hover tooltips
- Search
- **Legend distinguishing: confirmed (FHL) vs hypothetical (FFG) vs proposed (non-client)**
- Export as text/markdown
- Print-friendly view

### Phase 2 Output
`deliverables/fox-unified-journey-explorer.html`

## CONSTRAINTS & REQUIREMENTS

### Must Follow
- POLR is the parent entity — FFG and FHL are children
- POLR journey never stops — parallel track during business transactions
- Existing FFG/FHL pre-sales playbooks stay as is
- UMI is OUT OF SCOPE
- 5-profile ICA framework is canon
- FHL lifecycle is CONFIRMED (Rowdy's design)
- FFG lifecycle is HYPOTHETICAL (needs validation — flag visually)
- Australian English, compliance-safe

### Cannot Change
- ICA profiles or Purchase Type mapping
- FHL lifecycle touchpoint timing
- Tone of voice
- Existing pre-sales playbook content

### Need Approval For
- POLR as lead magnet (PROPOSED — needs Nathan/Rowdy buy-in)
- FFG lifecycle touchpoints (HYPOTHETICAL — needs Rowdy/Nathan validation)
- Non-client value delivery (compliance check pending)
- POLR branding/positioning as parent entity

## GETTING STARTED

### Phase 1 Steps
1. Read `cos.yaml`, activation meeting transcript, extracted-content.md
2. Route to **Hormozi Coach** — POLR as Grand Slam Offer
3. Route to **Pre-Sales Specialist** — Entry points, handoff triggers
4. Route to **Cross-Sell Specialist** — Trigger points, cross-sell moments
5. Route to **Retention Specialist** — Lifecycle backbone, churn signals
6. Synthesise into 6 matrices as JSON
7. Output to `deliverables/unified-journey-data.json`

### Phase 2 Steps
8. Route to **Developer** — HTML scaffold, data binding, all 7 views
9. Invoke **/ui-ux-pro-max** — Visual design, interactions, polish
10. Output to `deliverables/fox-unified-journey-explorer.html`

### When to Escalate
**To James:** When Phase 1 matrices drafted (before HTML build)
**To Domain Expert:** If compliance boundaries unclear

## QUALITY GATES

### Phase 1 Complete When:
- [ ] All 6 matrices defined with structured JSON
- [ ] FHL touchpoints marked as confirmed
- [ ] FFG touchpoints marked as hypothetical
- [ ] Non-client journey marked as proposed
- [ ] POLR-as-parent architecture reflected in every matrix
- [ ] Handoff points defined (both directions + return)
- [ ] POLR parallel behaviour during transactions defined
- [ ] Signal detection gaps flagged
- [ ] Compliance boundaries noted

### Phase 2 Complete When:
- [ ] All 7 views functional
- [ ] Confirmed vs hypothetical vs proposed visually distinct
- [ ] POLR as parent visually clear
- [ ] Lifecycle comparison view shows depth difference (FFG light vs FHL comprehensive)
- [ ] Filters persist, detail panels work
- [ ] Fox branding with POLR layer
- [ ] Self-contained single HTML file
- [ ] Responsive (laptop + iPad)

---
Start with Phase 1. Read the activation meeting transcript first — Nathan's "Beacon on the Hill" IS the POLR-as-parent concept. Then route to Hormozi Coach for the strategic framework.
