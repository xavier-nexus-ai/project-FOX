# Meeting Analysis - 2026-02-06
## Activation/Immersion Meeting with Nathan & Rowdie

---

## GAME-CHANGING REVELATIONS

### 1. UMI Loans - Third Business (NOT in COS)
- **Lender** (not broker) - completely different business model
- Founded by Dan Fox post-GFC, started with $300K mortgaged against his house
- Now $28M in loans out - generally secured car loans
- Sub-prime customers (vs Fox's near-prime/prime)
- Has own proprietary system built by CTO
- Best AI visibility of the three brands
- Website: umillines.com.au (just rebranded)
- ~18 staff
- Nathan is MD across UMI and Fox group
- Dan Fox still board-level contributor
- Separate lead market operation generating $12K/month revenue

### 2. Jared Has Resigned
- Was marketing person (blogs, EDMs, SEO, web content)
- Leaving for full work-from-home position (wife's schedule, young baby)
- Not continuing in marketing at all
- Creates immediate marketing capability gap
- Nathan/Rowdie want to explore AI/automation to replace marketing function
- Custom GPT or agent to help with content creation
- Don't want to go to external agency (compliance nightmare)

### 3. Business Scale is 3x What COS Shows
- **Fox end:** 15 staff (not 9)
- **UMI end:** ~18 staff
- **Total:** ~33 across the group
- Nathan is MD across everything

### 4. Lead Market = Massive Untapped Revenue
- 49,000 leads/year sent to lead market (34K UMI, 15K Fox)
- Revenue: $4K-$12K/month (variable)
- Last month: 4,197 people sent, 764 sold
- Average $24-26 per lead sold
- **Do NOTHING with these 49K leads after selling them**
- Can legally reactivate and resell after 3 months
- Nathan's math: **worth $1M/year compounding** if properly recycled
- Predatory lending concern acknowledged - must re-engage ethically

### 5. GHL Decision DEFERRED
- James questioned whether GHL is the right tool
- Proposed custom vibe-coded database solution instead
- Brokers don't need/want another system (Ambition works for sales)
- Can't control SMS through aggregator platform
- Only real CRM need: post-settlement nurture
- Using maybe 10% of GHL's functionality
- Nathan/Rowdie open to custom bespoke solution
- Custom solution could be foundation for "Polar" (long-term vision)
- **Decision pending** - James to consult team and Emma

### 6. Pre-Sales Playbook May Need to Pivot
- Their conversion process is already VERY strong
- Not really a "pre-sales" gap
- James: "I'm not sure you really need a presale playbook"
- Real gap is post-settlement nurture and lifecycle management
- James now prioritising pre-sale understanding first, then cross-sell
- May combine into end-to-end approach instead of separate playbook

---

## DETAILED COS UPDATE LIST

### company data
```
company.trading_names: ADD "UMI Loans - Sub-prime secured car lending (lender, not broker)"
company.active_customers: UPDATE to "~50,000+ contacts across Fox businesses + UMI database"
company.customer_facing_staff: UPDATE from 9 to "~33 across all businesses (15 Fox, 18 UMI)"
company.website: SET to "foxfinancegroup.com.au (FFG), foxhomeloans.com.au (FHL), umillines.com.au (UMI)"
```

### NEW data: businesses (expand structure)
```
businesses:
  fox_finance_group:
    type: "Asset finance brokerage"
    staff: 15
    focus: "Car loans, personal loans, equipment finance, debt consolidation, commercial"
    customer_type: "Near-prime to prime (B2C)"
    lms: "Ambition"
    website: "foxfinancegroup.com.au"
    annual_settled_deals: "~170/month across group"
    average_commission_aim: "$2,300 per settled loan"

  fox_home_loans:
    type: "Mortgage brokerage"
    focus: "Home loans, investment properties, refinancing, commercial property"
    customer_type: "Mums and dads, investors (B2C)"
    lms: "Finshaw's/Connective" # Called "Infinity" previously but actually uses Connective/Finshaw's
    lms_api: "Hopeless - no API capability"
    website: "foxhomeloans.com.au"

  umi_loans:
    type: "LENDER (not broker)"
    founded: "Post-GFC (~2009)"
    founder: "Dan Fox"
    loans_outstanding: "$28M"
    focus: "Secured car loans, sub-prime customers"
    staff: "~18"
    lms: "Proprietary system built by CTO"
    website: "umillines.com.au (just rebranded)"
    ai_visibility: "Best of the three brands"
    lead_market_monthly: "$8K-$12K revenue from selling leads"
```

### ownership.client_contacts
```
REMOVE: Jared (Gerard) - RESIGNED
UPDATE: Matty -> "CTO" (not CIO), focuses on UMI end, AI/tech thinker, software engineer
ADD:
  - Dan Fox: Founder, board-level contributor, still around UMI
  - Mason: Ops Manager (UMI end)
  - Bill: Head of Growth & Partnerships (new role)
  - Brad: Top performing broker (FFG), 70-80% repeat/referral
  - Jess: Lending specialist, potential promotion to home loans
  - Ben: Marketing (mentioned re: Facebook creative)
```

### engagement data
```
engagement.notes: UPDATE - "Jared resigned. Nathan and Rowdie are primary implementation team. They've cleared priorities to focus. January delays due to team setup and tech launches. GHL decision DEFERRED pending evaluation of custom solution alternative."

engagement.playbook_focus.secondary: UPDATE notes - "Pre-sales playbook may be pivoted/combined. James noted their sales process is already strong. Real gap is post-settlement nurture, not pre-sale qualification."
```

### core_services
```
GHL CRM Implementation:
  status: "under_review"
  notes: "GHL decision deferred. Evaluating custom vibe-coded database solution as alternative. Brokers use Ambition for sales process - only need post-settlement nurture automation. James consulting team and Emma on best approach."
```

### baseline_metrics (12 Core Numbers) - MAJOR UPDATES
```
# Revenue
revenue_last_12_months:
  value: UPDATE notes - "FFG: $1.95M. FHL: $693K. UMI: Not specified. Lead market revenue: $48K-$144K/year additional."

# Acquisition
leads_per_month:
  value: UPDATE to "401 valid leads last month (FFG only)"
  breakdown: "254 organic website, 98 phone, remainder other sources"
  notes: "98% organic. Minimal paid spend. UMI generates separately."

cost_per_lead:
  value: UPDATE to "Near zero for organic. Google Ads: ~$47/valid lead (but only 2.5% settle)"

# Conversion - DETAILED FUNNEL NOW KNOWN
lead_to_appointment_rate:
  value: UPDATE to "75% target contact rate (65% actual this month)"
  notes: "This is getting them ON THE PHONE, not an appointment. Once on phone, 95%+ do application."

show_rate:
  value: UPDATE to "95%+ once on phone do application. 80%+ return docs."

close_rate:
  value: UPDATE to "~30% approval rate from full applications. Settlement rate after approval: ~98%"
  notes: "20% of 90-day plan follow-ups also convert"

average_deal_size:
  value: UPDATE to 2300
  notes: "Team aim is $2,300. Secured can be $3-4K. Unsecured can be $990. Referral converts 40%+ vs organic 5-10%."

# Monetisation
ADD: lead_market_revenue:
  value: "$48K-$144K/year"
  notes: "49,000 leads/year sent to lead market. $24-26 average per sale. Currently untouched after selling. $1M/year potential if recycled."

ADD: repeat_referral_rate:
  value: "70-80% of settlements"
  notes: "60-65% repeat + refer-a-friend. Remaining: dealership/partner referral (minimal)"

ADD: customer_nurture_leads:
  value: "41 new inquiries last month from outbound customer care calls alone"
```

### Google Ads Performance (NEW AREA)
```
google_ads:
  ffg:
    monthly_spend: "$1,500"
    last_quarter_results:
      leads: 116
      valid_leads: 96
      applications: "50%"
      approved: "3%"
      settled: "2.5% (2 deals)"
      revenue: "$3,600"
      net_result: "-$900 (spent ~$4,500)"
    cost_per_click: "$12"
    daily_budget: "~$40"
    campaigns: "2 (Performance Max)"
    status: "Running unmanaged since November"

  umi:
    monthly_spend: "$1,500"
    status: "Running"

  facebook:
    status: "Minimal retargeting"
    creative: "5-year-old 'Keep Calm' banner still running"
    spend: "Very limited"
```

### Referral Partners (NEW AREA)
```
referral_partners:
  ffg:
    database_size: "800+ businesses in hopper"
    active_referring: "3-4 regularly"
    process: "Gravity form → SendGrid automation → thank you email → Bill follows up"
    status: "Very cold. Minimal nurture. Team too busy with pipeline to maintain relationships."

  fhl:
    database_size: "~250 businesses"
    active_referring: "Handful"

  desired_partner_types:
    - "Accountants"
    - "Financial planners"
    - "Real estate agents"
    - "Builders"
    - "Buyers agents"
    - "Conveyancers"
    - "Developers (e.g., Stockland)"

  referral_fee_philosophy: "No cash - just look after each other's customers"
  head_of_partnerships: "Bill"
```

### Home Loans Value-Add Services (NEW AREA)
```
home_loans_value_add:
  repricing:
    description: "Go back to current bank to negotiate better rate"
    frequency: "Can be done every 3 months"
    effort: "Log into lender system, submit repricing request, 1 day turnaround"
    commission: "None - but builds massive value and keeps client"
    current_status: "Done on longer intervals, talking about every 3 months"

  property_valuation:
    description: "Free market appraisal showing equity growth"
    tool: "Subscription service (already paid for)"
    effort: "Can send within 1 minute"
    trigger: "6-12 months post-settlement"

  refinance:
    description: "Move to different bank for better deal"
    trigger: "After 18-month clawback period"
    commission: "Full new commission opportunity"
    clawback: "12-18 months depending on lender. 100% clawback if refinanced within period."
```

### Lead Contact Process (NEW DETAIL)
```
lead_contact_process:
  inbound:
    auto_sms: "Inquiry received, lending specialist will be in touch"
    auto_email: "Inquiry received, here's next steps + landing page"

  outbound_cadence:
    day_1: "3 attempts (morning, lunch, 5pm)"
    day_2: "2 attempts"
    day_3: "2 attempts"
    day_4: "1 attempt (breakup)"
    automation: "NONE - all manual template clicks"

  if_no_contact:
    options_provided: "Call us back, tell us a time, complete application online"
    online_completion: "80%+ of unreached people complete form online"

  no_contact_hopper:
    email_open_rate: "40-50%"
    content: "Reviews, top 5 tips, why bank statements needed, overcoming concerns"
```

### Post-Settlement Nurture (CURRENT STATE - needs improvement)
```
post_settlement_nurture:
  current_sequence:
    - "3 days: thank you email + review reminder"
    - "1 month: reminder"
    - "6 months: refer a friend program"
    - "12 months: home lending/refinancing/different things"
    - "18 months: something else"
    - "2 years: something else"
    - "3 years: something else"
  assessment: "All messaging needs to be re-looked at"
  status: "Priority for improvement"
```

### constraint data
```
primary_evidence: ADD
  - "Lead market: 49K leads/year generated and sold with zero reactivation"
  - "Lead market recycling potential: $1M/year compounding"
  - "Referral partner database: 1,050+ businesses but only 3-4 actively referring"
  - "Post-settlement nurture: basic time-based triggers, no lifecycle scoring"
  - "Customer care calls generated 41 new inquiries last month without any automation"
  - "Home loans repricing/valuation services: 'best kept secret' - customers don't know"

secondary_constraint: UPDATE
  "Pre-sales process is actually strong (95%+ conversion once on phone). Real secondary constraint is post-settlement lifecycle nurture and lead reactivation, not pre-sale qualification."
```

### tech_stack
```
ADD:
  - tool: "3CX"
    purpose: "Phone system - all calls recorded. Linked to Ambition."
  - tool: "TypeForm"
    purpose: "Multiple conditional logic forms (bad credit, vehicle, commercial, home loans, personal)"
  - tool: "Gravity Forms"
    purpose: "Referral partner hopper and some website forms"
  - tool: "Looker Studio"
    purpose: "KPI dashboards from aggregator data"
  - tool: "Calendly"
    purpose: "Testing in home loans (not widely used)"
  - tool: "Lead Market Platform"
    purpose: "Selling unqualified leads. 49K/year. $4-12K/month revenue."

UPDATE:
  Infinity -> "Finshaw's/Connective" (home loans aggregator - hopeless API)
  Ambition: ADD "Has API to push out information"
  GHL: status -> "Decision deferred - evaluating custom alternative"

  industry_specific: ADD
  - tool: "Proprietary UMI System"
    purpose: "Built by CTO for UMI Loans lending operations"
```

### status data
```
health: "Yellow"
health_reason: "Jared resigned creating marketing gap. GHL decision deferred pending custom solution evaluation. Pre-sales playbook scope under review. Significant new data from activation meeting requires processing."

blockers:
  - "GHL vs custom solution decision not yet made"
  - "Jared's marketing responsibilities unassigned"
  - "Privacy policy check for cross-business data sharing still pending (from previous action items)"

risks: ADD
  - risk: "GHL may not be the right tool - only need post-settlement nurture"
    likelihood: "Medium"
    impact: "High - delays implementation if we pivot"
    mitigation: "James evaluating custom solution. Decision needed within 1 week."
  - risk: "Marketing gap from Jared's departure"
    likelihood: "High (confirmed)"
    impact: "Medium - blogs, EDMs, SEO updates will stall"
    mitigation: "AI content agent could replace. Absorb into existing team member."
  - risk: "Finshaw's/Connective (FHL LMS) has no API"
    likelihood: "Confirmed"
    impact: "Medium - home loans data integration will be manual"
    mitigation: "CSV/PDF export. Build reader to parse into database."
  - risk: "Broker resistance to automation (Adrian, Ryan)"
    likelihood: "Medium"
    impact: "Medium"
    mitigation: "Position as 'AI handles admin, you handle relationships'"
```

### immersion data
```
immersion.completed: "Yes"
immersion.completed_date: "2026-02-06"

current_state.sales_process_summary: MAJOR UPDATE
  "Highly regimented sales process. 401 leads/month. 75% contact rate target. 95%+ of contacted complete application. 80%+ return docs. ~30% approved. Average commission $2,300. Manual 4-day outbound cadence (not automated). 80%+ of unreached complete online form. 90-day plan for declined customers converts at 20%. Process is STRONG - not the primary gap."

current_state.marketing_channels: UPDATE
  "98% organic (primarily SEO-driven website traffic). Google Ads $1,500/month (net negative ROI). Facebook minimal retargeting (5-year-old creative). Radio considering 3-month push at $7.5K/month. No LinkedIn activity. No YouTube. No lead magnets."

current_state.tech_stack_observations: UPDATE
  "Ambition (FFG) has API. Finshaw's/Connective (FHL) has NO API - hopeless. 3CX phone system integrated with Ambition. TypeForm with conditional logic (70% completion). Zapier routing leads. UMI has proprietary system built by CTO. CTO is AI-capable software engineer. Considering vibe-coded NextJS websites to replace WordPress."

current_state.team_observations: UPDATE
  "Jared RESIGNED - marketing gap. Nathan/Rowdie primary implementation team. Bill = new Head of Growth/Partnerships. Mason = ops manager (UMI). CTO available for tech consultation. Brad = top broker (80% repeat/referral). Team is well-scripted, well-monitored (weekly KPI reviews, Looker Studio dashboards). Nathan eyeballs everyone - doesn't want offshore."

stakeholder_interviews: UPDATE
  REMOVE Jared entry (resigned)
  ADD:
    - name: "Nathan"
      key_insights: "MD across Fox and UMI. Bought remaining 50% ~1 year ago. Vision: scalable business not reliant on him producing. Champions AI but worried about team feeling replaced. 'AI handles admin, you handle relationships.' Anti-offshore. Lead market = $1M opportunity. Wants Polar/ecosystem vision long-term."
    - name: "Rowdie"
      key_insights: "6 years with Nathan. Swiss army knife. Runs Fox end day-to-day. Tech-comfortable (GHL experience from previous role). Excited about SMS and AI. Managing 15 people."

key_discoveries: ADD
  - finding: "UMI Loans is a third business (lender, not broker) with $28M loans out"
    implication: "Scope is broader than originally understood. Potential cross-sell across THREE businesses."
  - finding: "49,000 leads/year sent to lead market and never re-engaged"
    implication: "Reactivation + resale could generate $1M/year. Massive quick win."
  - finding: "Sales process is already very strong - 95%+ on-phone conversion"
    implication: "Pre-sales playbook may not be needed as standalone. Pivot to lifecycle/nurture."
  - finding: "Home loans has repricing (3-month), valuation (6-12 month), refinance (18+ month) value-adds"
    implication: "Quarterly touchpoint strategy with real value, not just check-ins."
  - finding: "800+ referral partners in database but only 3-4 actively referring"
    implication: "Massive referral partner activation opportunity."
  - finding: "Brokers don't need another system - Ambition handles sales"
    implication: "GHL may be over-engineered. Custom solution for post-settlement only."
  - finding: "CTO is AI-capable software engineer building proprietary systems"
    implication: "In-house tech capability exists for custom solution maintenance."

quick_wins_identified: UPDATE
  - "Lead market reactivation campaign (49K leads/year, SMS-based)"
  - "Facebook ad creative update (5-year-old 'Keep Calm' banner)"
  - "Lookalike audiences from successful applications for Meta ads"
  - "Lead market revenue to offset increased ad spend"
  - "Home loans repricing check automation (quarterly)"
  - "Property valuation trigger (6-12 months post-settlement)"
  - "Customer care call list prioritisation via data analysis"
  - "AI content agent to replace Jared's marketing function"
```

### NEW data: customer_geography
```
customer_geography:
  ffg:
    sunshine_coast: "~15%"
    southeast_qld: "~70-75%"
    nsw: "Remaining"
    other_states: "Small percentage"
  notes: "Primarily QLD-based. Fox hasn't pushed Sunshine Coast specifically."
```

### NEW data: marketing_strategy_notes
```
marketing_strategy_notes:
  radio:
    considering: "3-month push on C FM Sunshine Coast"
    cost: "$7,500/month"
    purpose: "Support Bill's local business outreach"
    show: "Brekie show, Monday-Friday + off slots"

  youtube_podcast:
    interest: "High - Nathan interested in podcast concept"
    approach: "Conversational style, cut to shorts for Instagram/YouTube"
    purpose: "Authority building for generative search (ASO)"

  linkedin:
    interest: "High - especially for B2B/commercial division"
    current: "Exists but inactive"
    opportunity: "Leadership content, referral partner outreach"

  lead_magnets:
    current: "Almost none"
    opportunity: "One for every loan purpose, every value-add, every customer journey stage"

  website_rebuild:
    needed: "All 3 websites (Fox, FHL, UMI)"
    reason: "Neil Patel outsourced to India, WordPress themes causing issues"
    approach: "Considering vibe coding with NextJS"
    umi_status: "Full rebrand complete, ready for new site"
    fox_status: "Brand refresh planned"
    priority: "After CRM/playbook work"
```

### change_log
```
ADD:
  - date: "2026-02-06"
    author: "Orchestrator"
    phase: "Transform → Observe"
    change: "Processed 3.5-hour activation meeting transcript. MAJOR revelations: UMI Loans is third business (lender, $28M). Jared resigned (marketing gap). 49K leads/year to lead market untouched ($1M opportunity). Sales process already strong (pre-sales pivot needed). GHL decision deferred (custom solution evaluation). 33+ staff across group (not 9). Home loans value-adds identified. Referral partner database: 1,050+ but only 3-4 active."
    sections_affected: ["company", "engagement", "baseline_metrics", "constraint", "tech_stack", "immersion", "status", "ownership"]
    source_documents:
      - "docs/Background/Activation Meeting - Full Transcript.md"
```

---

## COMPREHENSIVE TO-DO LIST

### CRITICAL / IMMEDIATE (This Week)

1. **DECISION: GHL vs Custom Solution**
   - James to evaluate options
   - Talk to business partner (George) and sales specialist
   - Talk to Emma
   - Compare: What do we ACTUALLY need vs what GHL provides?
   - Consider: Custom solution as Polar foundation
   - **Owner: James | Deadline: Within 1 week**

2. **Apply COS updates from this meeting**
   - Massive update required (see above)
   - **Owner: Orchestrator | Deadline: Today**

3. **Pre-sales playbook scope revision**
   - Their sales process is strong (95%+ on-phone conversion)
   - Real gap is post-settlement nurture
   - Decide: Standalone playbook or combine into end-to-end?
   - **Owner: James | Deadline: Before Week 2 strategy presentation**

4. **Jared's marketing replacement plan**
   - Explore AI content agent (custom GPT/Claude agent)
   - Could handle: monthly blogs (x2), matching EDMs, SEO content updates
   - Absorb into existing team member + AI assistance
   - **Owner: James to advise | Deadline: Week 2**

### HIGH PRIORITY (Weeks 1-2)

5. **Collect documents from Nathan/Rowdie**
   - Tone of voice document (existing internal version)
   - ICP documents (customer avatars - recently revisited)
   - Beacon on the Hill document (Polar vision)
   - All sales scripts and templates
   - SendGrid access
   - Ambition API documentation
   - **Owner: Chase Rowdie | Deadline: End of Week 1**

6. **Google Ads review**
   - Get ads specialist to review current campaigns
   - 2 campaigns (Performance Max) running unmanaged since November
   - Net negative ROI last quarter (-$900)
   - Consider: leave on for SEO benefit or turn off?
   - Also review UMI ads ($1,500/month)
   - Connect with Fox Google Ads account
   - **Owner: James (ads specialist) | Deadline: Week 2**

7. **Facebook retargeting update**
   - Remove 5-year-old "Keep Calm" creative IMMEDIATELY
   - Build lookalike audiences from successful applications
   - Set up proper conversion tracking through GHL (or custom)
   - **Owner: James + Ben | Deadline: Week 2**

8. **Lead market reactivation strategy**
   - Design SMS reactivation campaign for 49K leads
   - "Hey, are you the [name] that was looking for [loan type] last year?"
   - Address predatory lending concern ethically
   - Calculate: lead magnets for each category
   - **Owner: James | Deadline: Week 2-3**

9. **Tone of voice extraction**
   - Nathan offered to share existing ToV document
   - Collect it, then enhance with professional version
   - Need this BEFORE any content creation
   - **BLOCKING GATE**
   - **Owner: Tone of Voice Agent | Deadline: Once assets received**

### MEDIUM PRIORITY (Weeks 2-4)

10. **Investigate Ambition API**
    - What data can be pushed out?
    - How deep is the API?
    - Can we get settlement data, customer data?
    - Also: Does aggregator use Twilio for SMS? (Could share numbers)
    - **Owner: James + CTO consultation | Deadline: Week 2**

11. **Finshaw's/Connective (FHL) data solution**
    - No API (confirmed "hopeless")
    - Explore: CSV export, PDF download → AI reader
    - Manual or periodic sync approach
    - **Owner: James | Deadline: Week 3**

12. **Customer nurture redesign**
    - Current: time-based triggers (3 days, 1 month, 6 months, 12 months, 18 months, 2 years, 3 years)
    - Needed: lifecycle-based with real value triggers
    - Home loans quarterly cycle: repricing (Q1), valuation (Q2), different service (Q3), refinance eval (Q4)
    - Asset: car age tracking, consolidation opportunities
    - **Owner: Cross-sell specialist | Deadline: Weeks 3-4**

13. **Lead magnet strategy**
    - Currently: "not many" (near zero)
    - Need: one for every loan purpose and customer journey stage
    - Home lending, refi, equity out, car loans, personal loans, debt consolidation
    - For lead market reactivation, for customer nurture, for website conversion
    - **Owner: James + content strategy | Deadline: Weeks 3-4**

14. **Lead scoring / opportunity scoring model**
    - Car age → upgrade trigger
    - Credit card/personal loan data → consolidation trigger
    - Home loan LVR change → repricing trigger
    - Life stage indicators
    - **Owner: Data analyst | Deadline: Weeks 3-4**

### LOWER PRIORITY (Weeks 4+)

15. **Website rebuild planning**
    - 3 sites need rebuilding (Neil Patel WordPress mess)
    - UMI rebrand complete, ready for new site
    - Fox brand refresh planned
    - Vibe coding with NextJS as approach (discuss with CTO)
    - **Owner: James + CTO | Deadline: After CRM/playbook**

16. **Radio advertising evaluation**
    - 3-month C FM push at $7,500/month
    - Supporting Bill's local business outreach
    - Track: inquiry source attribution
    - **Owner: Nathan's decision | Deadline: Whenever ready**

17. **YouTube/Podcast exploration**
    - Authority channel for generative search (ASO)
    - Cut to shorts for Instagram/YouTube
    - AI creates blog posts from episodes
    - **Owner: Marketing strategy | Deadline: After core playbook**

18. **LinkedIn strategy**
    - B2B/commercial opportunity
    - Leadership content for Nathan
    - Referral partner outreach
    - Good for ASO/generative search
    - **Owner: Marketing strategy | Deadline: After core playbook**

19. **Referral partner activation**
    - 800+ FFG + 250 FHL in database, only 3-4 active
    - Bill (Head of Growth) leading this
    - GHL/custom solution: pipeline for referral management
    - Sequence: warm-up, value proposition, tracking
    - **Owner: Bill + James support | Deadline: Weeks 4-6**

20. **Polar/Ecosystem vision planning**
    - Long-term customer lifecycle platform
    - Headless database with multiple front-ends
    - Client portal, referral partner portal, team dashboard
    - Bank statement integration, property valuation integration
    - Affiliate partner directory
    - **Owner: James + CTO collaboration | Deadline: Phase 2+**

### OUTSTANDING DECISIONS (From Nathan)

21. Equipment replacement cycle length (for trigger campaigns) - Nathan to confirm
22. Google Ads agency: definitively keep, modify, or kill?
23. Referral fee/incentive structure for formalised program - Nathan's philosophy is no cash
24. Jess: promote to home loans or keep as nurture/SDR role?
25. Privacy policy update for cross-business data sharing - Rowdie checking
26. Radio: commit to 3-month C FM push?
27. GHL vs custom solution - James to recommend

---

## KEY STRATEGIC INSIGHTS

### What Changed from Previous Understanding

| Topic | Before | After |
|-------|--------|-------|
| Businesses | 2 (FFG + FHL) | 3 (FFG + FHL + UMI Loans) |
| Staff count | 9 | 33+ |
| Revenue streams | Commissions only | Commissions + lead market ($48-144K/yr) + trail book |
| Sales process | Assumed needed improvement | Already very strong - 95%+ conversion on phone |
| Pre-sales need | Full playbook | May not need standalone - pivot to lifecycle |
| CRM solution | GHL confirmed | GHL vs custom - decision pending |
| Marketing person | Jared doing it | Jared resigned - gap |
| Leads/year sold | Not known | 49,000 (worth potentially $1M/year if recycled) |
| Referral partners | "A few" | 1,050+ in database, only 3-4 active |
| Tech capability | External | CTO in-house, software engineers, AI-capable |
| Long-term vision | Cross-sell | Full customer ecosystem ("Polar") |
| Website status | Existing | All 3 need rebuilding |

### Biggest Opportunities (Ranked)

1. **Lead market reactivation** - 49K leads/year, $1M potential, low effort
2. **Customer lifecycle nurture redesign** - 41 inquiries last month from basic calls, imagine automated
3. **Referral partner activation** - 1,050 in database, 3-4 active
4. **Cross-sell automation** - Still primary playbook, now with better data
5. **Ad spend offset via lead market** - Scale ads indefinitely if lead market covers cost
6. **AI content agent** - Replace Jared's function at fraction of cost
7. **Home loans quarterly value-add cycle** - Repricing, valuation, refinance

### Biggest Risks

1. **GHL indecision** - Delays implementation if we keep going back and forth
2. **Scope creep** - UMI Loans, Polar vision, websites, marketing... massive scope
3. **Jared's departure** - Marketing continuity at risk
4. **Finshaw's no API** - Home loans data integration will be painful
5. **Nathan's resistance to offshore/full automation** - Limits efficiency options
