# SOP: Njin Playbook Creation Process

## Purpose
This SOP documents the end-to-end process for creating custom playbooks for clients. It covers everything from initial data collection through to final delivery of the playbook document and implementation guides.

---

## Phase 1: Client Onboarding & Data Collection

### Step 1: Create Client Portal Entry

**What to create:**
- New client record in Notion using standard template
- Client folder structure in Google Drive
- LLM project for playbook creation

**Client Portal Initial Setup:**
- Client name
- Relationship start date
- Status health: Green
- Status phase: Activation - Data Collection
- Next milestone: Complete baseline data collection
- Next milestone date: 7 days from start

**Where:** Notion database "Client Operating Systems"

---

### Step 2: Send Client Data Collection Form

**What to collect:** Use the Client Data Collection Framework

**Critical Information (Always Collect):**
- Company basics (industry, revenue model, active customers, team headcount)
- Tech foundation (CRM platform, office suite, communication tools, automation tools, AI tools, industry platforms)
- Client owner map (CRM admin, implementation approvals, main point of contact)
- The 4 Critical Qualitative Questions:
  1. "Where do you think you're leaking the most money right now?"
  2. "What's your 12-month revenue goal?"
  3. "What's your next revenue milestone?" (+ by when)
  4. "If we could fix ONE thing in the next 90 days, what would you want it to be?"
- **The Core 12 Numbers:**
  1. Revenue (last 12 months)
  2. Revenue (prior 12 months)
  3. Leads per month
  4. Cost per lead
  5. Lead → Appointment rate (%)
  6. Show rate (%)
  7. Close rate (%)
  8. Average deal size ($)
  9. MRR or contract length (months)
  10. Churn rate (%) or customer lifespan (months)
  11. Customer LTV ($)
  12. CAC ($)

**Playbook-Specific Foundation Data:**
- Refer to Client Data Collection Framework for playbook-specific must-haves
- Only collect "Optional Deep Dive" data if client has it readily available

**Tool:** Google Form linked to Client Portal automation (auto-populates Notion)

---

### Step 3: Log The Core 12 in Client Portal

**What to log in Notion Client Portal:**

**The Core 12 Numbers:**

**Revenue & Growth:**
- 1. Revenue (last 12 months): $[amount]
- 2. Revenue (prior 12 months): $[amount]

**Acquisition:**
- 3. Leads per month: [number]
- 4. Cost per lead: $[amount]

**Conversion:**
- 5. Lead → Appointment rate: [%]
- 6. Show rate: [%]
- 7. Close rate: [%]
- 8. Average deal size: $[amount]

**Monetisation & Retention:**
- 9. MRR or contract length: $[amount] or [months]
- 10. Churn rate or customer lifespan: [%] or [months]
- 11. Customer LTV: $[amount]
- 12. CAC: $[amount]

**Constraint Diagnosis:**
- Primary constraint: [Acquisition/Conversion/Monetisation/Retention]
- Secondary constraint: [What becomes bottleneck after primary is fixed]
- Rationale: [Why this diagnosis based on Core 12]
- Ninety-day priority: [From qualitative question 4]

**Purpose:** This creates the "before" snapshot to measure impact later. The Core 12 tell us which pillar is leaking.

**Client Portal Update:**
- Status phase: Activation - Baseline Complete
- Next milestone: Documentation collection

---

### Step 4: Create Client Documentation Folder Structure

**Structure in Google Drive:**

```
Njin Playbooks > [Client Name]
├── [Client Name] <> Njin (SHARED WITH CLIENT - upload access)
│   ├── Brand Guidelines
│   ├── Current Scripts
│   ├── Case Studies
│   ├── Sales Materials
│   ├── Product Documentation
│   └── [Client adds any relevant files here]
├── Internal - Research & Notes (Njin team only)
├── Internal - Playbook Drafts (Njin team only)
└── Final Deliverables (shared with client - view only after completion)
```

**Sharing permissions:**
- `[Client Name] <> Njin`: Client has upload/edit access
- `Internal - Research & Notes`: Njin team only
- `Internal - Playbook Drafts`: Njin team only
- `Final Deliverables`: Client view only (will be shared at completion)

**Share with client:** Send link to `[Client Name] <> Njin` folder with instructions:
"Please upload all relevant documentation here: brand guidelines, current scripts, case studies, sales materials, product docs, CRM screenshots, etc."

**Client Portal Update:**
- Data access - CRM access granted: No (waiting)
- Data access - Historical data received: No (waiting)
- Data access - Team interviews scheduled: No (waiting)
- Data access notes: "Waiting for client to populate shared folder"

---

### Step 5: Prerequisite Validation

Ensure all required data has been collected before proceeding to implementation.

**Required before proceeding:**
- [ ] CRM admin access granted (login credentials received)
- [ ] Historical data received (last 6-12 months export or screenshots)
- [ ] Key team members available for interviews (scheduled)
- [ ] Shared folder populated with documentation
- [ ] The Core 12 logged in Client Portal
- [ ] Playbook-specific data collected (refer to Client Data Collection Framework)

**If access delayed beyond 5 business days:**
- Escalate to client point of contact
- Document blocker in Client Portal
- Set new deadline for access

**Client Portal Update when validated:**
- Data access - CRM access granted: Yes
- Data access - Historical data received: Yes
- Data access - Team interviews scheduled: Yes
- Data access notes: "All access provided, ready for immersion"
- Status phase: Immersion - Week 1
- Next milestone: Complete immersion activities

---

## Phase 2: Tone of Voice Creation

### Step 6: Generate Tone of Voice Document

**Critical:** This must be completed before generating any playbook content in the LLM.

**Tool:** Use "The Tone of Voice Analyst" GPT  
**URL:** https://chatgpt.com/g/g-680755d37f648191957c6d9df1421b95-tone-of-voice-analyst

**Process:**
1. Collect client's existing materials:
   - Website copy
   - Email sequences
   - Sales call recordings/transcripts
   - Social media posts
   - Marketing materials
2. Upload to Tone of Voice Analyst GPT
3. Generate tone of voice profile
4. Review output for accuracy
5. Add client-specific notes or adjustments
6. Get client approval on tone profile

**If client has existing tone of voice doc:**
- Upload to Tone of Voice Analyst to validate/enhance
- Confirm it's current and accurate
- Get client sign-off

**Output format:** 1-2 page tone of voice guide with examples

**Where to store:**
- Add to LLM project knowledge base (once created)
- Save in `[Client Name] <> Njin` folder
- Reference in Client Portal under client context

**Why this matters:** Every script, email template, and piece of copy needs to sound like the client, not like generic AI.

---

## Phase 3: LLM Project Setup

### Step 7: Create LLM Project

**Platform:** Claude Projects or ChatGPT Projects

**Project naming convention:**  
`[Client Name] - [Playbook Type] - [Month Year]`  
Example: `Acme Corp - Pre-Sales Playbook - Dec 2024`

---

### Step 8: Write System Instructions

**System Instructions Template:**

```
You are the ultimate sales and revenue operations specialist, combining decades of proven sales methodology with cutting-edge AI automation strategies. Your expertise spans the entire customer lifecycle—from cold outreach through customer success—and you leverage both human psychology and intelligent automation to scale businesses predictably.

Your core competencies include:
- Building systematic sales processes that convert at scale
- Designing AI-powered automations that enhance (not replace) human connection
- Creating conversational AI agents that qualify, nurture, and book meetings
- Implementing CRM workflows that eliminate manual work and increase speed-to-lead
- Developing customer success strategies that maximise retention and lifetime value
- Crafting messaging that resonates with buyers at every stage of awareness
- Structuring offers and pricing that maximise perceived value and profitability

You are creating the [PLAYBOOK TYPE] for [CLIENT NAME].

This playbook will focus on:
[List specific focus areas based on playbook type and constraint diagnosis from COS]

Key context about this business:
- Industry: [CLIENT INDUSTRY]
- Target customer: [ICP SUMMARY from data collection]
- Current team size: [NUMBER AND ROLES]
- Main offer: [OFFER NAME, PRICE, AND POSITIONING]
- Pricing model: [ONE-TIME / RECURRING / HYBRID]
- Primary constraint: [FROM CLIENT PORTAL - Acquisition/Conversion/Monetisation/Retention]
- Ninety-day priority: [FROM CLIENT PORTAL - Critical Qualitative Question 4]

The Core 12 Numbers (baseline metrics):
1. Revenue (last 12 months): $[amount]
2. Revenue (prior 12 months): $[amount]
3. Leads per month: [number]
4. Cost per lead: $[amount]
5. Lead → Appointment rate: [%]
6. Show rate: [%]
7. Close rate: [%]
8. Average deal size: $[amount]
9. MRR or contract length: $[amount] or [months]
10. Churn rate or lifespan: [%] or [months]
11. Customer LTV: $[amount]
12. CAC: $[amount]

Reference the following documents in your knowledge base:
1. [Document name] - [What it contains and how to use it]
2. [Document name] - [What it contains and how to use it]
3. [Continue for each document...]

When creating content:
- Always use the tone of voice documented in the knowledge base
- Reference the AI Content Generation Guide for writing standards and phrases to avoid
- Use Australian English spelling and grammar
- Write at 3rd grade reading level for maximum clarity
- Prioritise bullet points over paragraphs
- Be ruthlessly practical and actionable
- Avoid jargon, fluff, and overcomplicated language
- Reference specific client data, examples, and context from The Core 12
- Balance automation with human touch
- Design for scalability without sacrificing quality
- Include specific metrics, benchmarks, and success criteria

Your output should be:
- Copy-paste ready (no need for further editing)
- Specific to this client (not generic advice)
- Matching the approved tone of voice document (already created)
- Structured following the playbook framework (Developer Guide + Rep Handbook sections)
- Balanced between strategy and execution
- Focused on revenue outcomes, not just activity metrics
```

---

### Step 9: Upload Knowledge Base Documents

**Documents to upload from `[Client Name] <> Njin` folder:**
- Client questionnaire responses
- Brand guidelines or tone of voice doc (if exists)
- Current scripts (if they exist)
- Case studies or testimonials
- Product documentation
- Current CRM screenshots or workflow docs
- Competitor research (if available)
- Sales recordings or transcripts (if available)
- Marketing materials (ads, landing pages, email sequences)
- Pricing sheets and proposal templates
- Any other relevant documentation client provided

**Also upload:**
- Client Portal export (so LLM has The Core 12 and constraint diagnosis)
- Relevant research documents (from the project knowledge base)

**Important:** List each uploaded document in the system instructions so the LLM knows what's available and how to reference it

**Client Portal Update:**
- Status phase: Methodology Creation - Weeks 1-2
- Next milestone: Complete playbook draft

## Phase 4: Playbook Document Creation

### Step 10: Create Master Playbook Document

**Format:** Google Doc with heading hierarchy for navigation

**Document naming:**  
`[Client Name] - [Playbook Type] - DRAFT v1`

**Location:** `Internal - Playbook Drafts` folder

---

### Step 11: Document Structure - Playbook Framework

**Reference:** Njin Agent Architecture Appendix for complete section details

Every playbook follows this structure (adapt depth and sections based on playbook type):

**1. Business Overview**
- Complete snapshot of the business: what they sell, who they sell to, current state, strategic direction
- Context-setting for anyone reading the playbook
- (2-3 pages, Strategy)

**2. Ideal Client Profiles & Avatars**
- Who you sell to, why they buy, what makes them say yes
- Top 20% customer analysis, avatar definitions, negative personas, and buying triggers
- (3-4 pages, Strategy)

**3. Competitive Intelligence**
- Summary of top 5 competitors with battle cards
- Links to full research in docs/research/competitor-research.md
- Quick reference for reps before competitive calls
- (3-4 pages, Strategy)

**4. Business Model**
- Documents how the business makes money TODAY
- Value proposition, revenue streams, money model (core → upsell → downsell → continuity)
- Pricing, LTGP and CAC frameworks
- Current state only, not consulting
- (3-4 pages, Strategy)

**5. Pipeline Overview**
- High-level map of the customer journey from awareness to purchase
- Pipeline stages, key activities per stage, conversion benchmarks, and handoff points between teams
- (2-3 pages, Developer)

**6. Contact Segmentation & Scoring**
- Lead scoring criteria, routing logic, demographic and behavioural signals, re-scoring triggers
- Best leads to best closers
- (Developer)

**7. [Playbook] Pipeline Developer Guide** (playbook-specific: 7a, 7b, 7c...)
*Role varies by playbook: SDR Pipeline, Closer Pipeline, CSM Pipeline, etc.*

**Purpose:** Technical blueprint for CRM implementation

**Contents:**
- Pipeline stage configuration, automation rules, stage details with full email/SMS content
- Custom fields, integrations, business hours, red dot protocol, lost reasons, DND, testing checklist
- The "how to build it" document
- (5-8 pages, Developer)

**8. [Playbook] Rep Handbook** (playbook-specific: 8a, 8b, 8c...)
*Role varies by playbook: SDR Handbook, Closer Handbook, CSM Handbook, etc.*

**Purpose:** Operational guide for reps

**Contents:**
- Daily workflow, pipeline overview, critical rules, stage workflows
- Interacting protocol, stage movements, success metrics, pro tips, what to avoid
- Red dot alerts, lost reasons, DND protocol
- The "how to use it" document
- (8-12 pages, Rep)

**9. Funnels**
- Landing pages, opt-in forms, lead magnets, page content, and lead capture systems
- Includes high-intensity funnels (direct booking), low-intensity funnels (lead magnet → nurture → book)
- Page copy, thank you page strategy, funnel architecture, A/B test plans, and tracking
- (Content)

**10. [Playbook] Scripts** (playbook-specific: 10a, 10b, 10c...)
- All scripts and messaging templates for a specific playbook type
- VSL scripts and storyboards, call scripts (cold, follow-up, discovery, closing)
- Email sequence copy, SMS scripts (split into individual messages), voicemail scripts
- LinkedIn messages, and nurture sequences
- Must follow tone-of-voice.md
- (5-10 pages, Rep)

**11. Hot Buttons (Triggers & Resonators)**
- Psychological levers that make buyers pay attention and act
- Pain triggers, desire triggers, urgency creators, social proof positioning, and risk reversal language
- Broken down by avatar
- (Rep)

**12. Objection Handlers**
- Plug-and-play frameworks to turn "not now" into "how soon can we start?"
- Covers price, timing, decision-maker, competitor, and trust objections with scripted responses
- (Manager)

**13. Call Review Framework**
- Structured system to coach, score, and improve every sales conversation
- Scoring rubric, review cadence, and coaching focus areas
- (Strategy)

**14. Sales Map (Automation vs Human)**
- Clear visual of when to automate vs when to engage personally
- Maps every touchpoint in the journey to either automated or human-owned
- (Manager)

**15. Training SOP Library**
- Simple, repeatable guides for onboarding new team members and maintaining consistency
- Role-specific SOPs, quick reference cards, and FAQ documents
- (Manager)

**16. Performance Scorecard**
- Track and reward the numbers that drive revenue growth
- KPIs, targets, leading vs lagging indicators, and incentive structures
- (Developer)

**17. Metrics & Dashboards**
- Real-time visibility into conversion rates, pipeline health, and ROI
- Dashboard specifications, reporting cadence, and alert thresholds
- (Content)

**18. Enablement Assets**
- Decks, calculators, templates, and case studies that help reps close faster
- Everything a rep needs to support conversations beyond scripts
- (Content)

**19. Proof Package**
- Segmented testimonials, client results, before/after comparisons, and video proof
- Organised by avatar and objection type for maximum relevance
- (Developer)

**20. AI & Custom Automations**
- Beyond-playbook AI workflows added after all playbooks are sorted
- Custom AI agents, advanced automations, and integration workflows
- (Developer)

---

### Step 12: Adapt Section Depth Based on Playbook Type

**Section depth guidelines:**
- **Critical sections** (core to playbook goal): 5-15 pages with detailed processes, multiple examples, troubleshooting
- **Supporting sections** (necessary but not primary): 2-5 pages with sufficient detail and 1-2 examples
- **Reference sections** (background/context): 1-2 pages providing orientation

**Prioritise sections based on playbook type:**
- **Outreach:** Focus on ICP, Pipeline, Hot Buttons, Objections, multi-channel cadences
- **Ads:** Focus on ICP, Funnels, Content, Hot Buttons, Proof, hook library, testing protocols
- **Pre-Sales:** Focus on Pipeline, SDR Dev Guide, SDR Handbook, Objections, Scorecard, Metrics, Four Pillars of Lead Nurture
- **Sales:** Focus on Pipeline, Closer Dev Guide, Closer Handbook, Objections, Call Review, discovery frameworks, closing techniques
- **Cross-Selling:** Focus on Offers, Hot Buttons, Sales Map, Metrics, customer segmentation, trigger events
- **Referral:** Focus on Philosophy, Hot Buttons, Sales Map, Metrics, timing strategies, ask scripts
- **Retention:** Focus on Pipeline, CSM Dev Guide, CSM Handbook, Scorecard, Metrics, onboarding sequences, activation strategies

**Note:** Each playbook includes role-specific Developer Guide and Rep Handbook sections tailored to that playbook's focus (e.g., SDR for Pre-Sales, Closer for Sales, CSM for Retention). Don't include sections for roles not relevant to that specific playbook.

---

## Phase 5: Content Generation

### Step 13: Use LLM Project to Generate Content

**Process per section:**
1. Reference Client Portal for relevant baseline data
2. Reference knowledge base docs for client specifics
3. Generate first draft in LLM
4. Copy into Google Doc
5. Edit for tone, accuracy, specifics
6. Add client-specific examples from The Core 12
7. Remove any remaining AI fluff
8. Ensure copy-paste readiness (templates must work as-is)

**Quality check each section:**
- [ ] Is this specific to this client (not generic advice)
- [ ] Can someone copy-paste this template and use it immediately
- [ ] Are placeholders clearly marked [LIKE THIS]
- [ ] Does this match the client's tone of voice
- [ ] Are there concrete examples or numbers from The Core 12
- [ ] Is it simple enough for a new employee to understand
- [ ] Does it reference the constraint diagnosis from Client Portal

**Important:** Don't just copy-paste LLM output. Every section needs human review and personalisation with client data.

---

### Step 14: Internal Review
**Who:** Project Manager + Subject Matter Expert  
**When:** After first complete draft

**Review checklist:**
- [ ] Does it match client's tone of voice
- [ ] Are all 19 sections complete at appropriate depth for this playbook type
- [ ] Do scripts include placeholders clearly marked
- [ ] Are metrics/benchmarks realistic and client-specific
- [ ] Is anything too generic (needs more client specifics from The Core 12)
- [ ] Can a new employee follow this without additional training
- [ ] Are there any contradictions between sections
- [ ] Do automations make sense technically for their CRM platform
- [ ] Are handoffs between teams clearly defined
- [ ] Is the balance between automation and human touch appropriate
- [ ] Does the Developer Guide have enough technical detail to build from
- [ ] Is the Rep Handbook actionable with checklists and scripts

**Process:**
1. Create copy: `DRAFT v2 - Internal Review`
2. Use track changes for all feedback
3. Schedule 60-min review call
4. Document all changes needed
5. Implement changes
6. Update to `DRAFT v3`

**COS Update:**
- Status phase: Strategic Presentation - Week 3
- Next milestone: Client approval

---

### Step 15: Client Review Round
**Who:** Project Manager  
**When:** After internal review complete

**Process:**
1. Create clean version (accept all tracked changes)
2. Rename to `DRAFT v3 - Client Review`
3. Move to `[Client Name] <> Njin` folder temporarily
4. Add comment access for client
5. Share link with client
6. Request feedback within 5 business days
7. Schedule 90-min review call to walk through document
8. Document all requested changes
9. Implement changes with track changes on
10. Update to `DRAFT v4`
11. Share updated version
12. Repeat if needed (max 2 revision rounds)

**During review call:**
- Walk through constraint diagnosis (confirm we're fixing the right thing)
- Review The Core 12 baseline (confirm accuracy)
- Walk through each major section
- Confirm Developer Guide is technically feasible for their CRM
- Confirm Rep Handbook scripts sound like their brand
- Verify metrics and benchmarks are realistic
- Get buy-in on automation approach
- Clarify any confusion
- Note additional requests

**After client approval:**
- Rename to `FINAL v1`
- Move to `Internal - Playbook Drafts` (keep secure until handover)

**COS Update:**
- Status phase: CRM Implementation - Weeks 4-6
- Next milestone: Automations built and tested

---

## Phase 6: Finalisation & Handover


### Step 16: Create Final Deliverable Package

**Final package includes:**

**1. Master Playbook Document**
- Complete with all sections
- PDF version (locked)
- Google Doc version (view only)

**2. Developer Guide** (extracted from relevant section)
- Standalone technical blueprint
- All CRM automation specifications
- Integration requirements
- Dashboard specs

**3. Team Member Handbooks** (extracted per role)
- One per role (SDR, AE, CSM, etc.)
- Daily checklists
- Scripts and processes
- Quick reference format

**4. Quick Reference Guide**
- 1-2 page cheat sheet
- Most critical info only
- Laminated card format

**5. Template Library**
- All copy-paste templates in separate doc
- Organized by use case
- Editable for client customization

**6. Implementation Checklist**
- Step-by-step what needs to happen
- Who owns each step
- Timeline and milestones
- Success criteria

**Organize in `Final Deliverables` folder:**
```
Final Deliverables
├── [Client Name] - Master Playbook - FINAL v1.pdf
├── [Client Name] - Master Playbook - FINAL v1 (Google Doc link)
├── [Client Name] - Developer Guide - FINAL v1.pdf
├── [Client Name] - [Role] Handbook - FINAL v1.pdf (one per relevant role)
├── [Client Name] - Quick Reference Guide.pdf
├── [Client Name] - Template Library (Google Doc link)
└── [Client Name] - Implementation Checklist.pdf
```

**Set permissions:**
- All PDFs: Download only
- Google Docs: View only (except Template Library = comment access)

---

### Step 17: Developer Handoff

**Handoff includes:**
- Developer Guide (extracted section)
- Access to client's CRM (login credentials)
- Access to shared folder
- List of integrations required
- Technical specifications for custom builds
- Timeline: Weeks 4-6

**Developer deliverables:**
- All workflows built and tested
- Dashboard configured
- Documentation of what was built
- Video walkthrough of system

**Client Portal Update:**
- Njin owners - CRM specialist: [Developer Name]
- Status phase: CRM Implementation - Weeks 4-6
- Next milestone: Automations built and tested

---

### Step 18: Training Material Handoff

**Handoff to trainer:**
- Team Member Handbook (extracted section per role)
- Call Review Framework section
- Training SOP Library section
- Performance Scorecard section
- Access to client team calendar

**Trainer deliverables:**
- Training session delivered
- Recording of training
- Team certification checklist
- Q&A document from training

**Client Portal Update:**
- Status phase: Team Training - Weeks 7-8
- Next milestone: Training complete and team certified

---

### Step 19: Go-Live Preparation

**Pre-launch checklist:**
- [ ] All automations tested end-to-end
- [ ] Team trained and certified
- [ ] Handbooks distributed to team
- [ ] Manager has Call Review Framework
- [ ] Dashboard access granted to stakeholders
- [ ] Backup processes documented (what if automation fails)
- [ ] Go-live date confirmed with client

**Client Portal Update:**
- Status phase: Live Monitoring - Weeks 9-12
- Next milestone: 30-day performance review
- Status health: Green

---

### Step 20: Active Monitoring (Weeks 9-12)

**Weekly activities:**
- Review CRM activity logs
- Listen to sample calls (if recorded)
- Check dashboard metrics
- Identify execution gaps
- Document adjustments needed

**Update The Core 12 with actual results:**

For each relevant metric, show before and after:
- Example: Show rate - Before: 42% | After: 61% | +45% improvement
- Example: Close rate - Before: 18% | After: 26% | +44% improvement

**Team Performance (if applicable):**
- Show rate range - Was: 35%-58% | Now: 52%-68%
- Appointments per week range - Was: 8-15 | Now: 12-22

**Client Portal Update weekly:**
- Status health notes: [Brief summary of week's observations]
- Blockers: [Any issues preventing success]
- Change log entry: Date, what was adjusted this week

**Client Portal Update at completion:**
- Status phase: Monitoring Complete - Handover to CS
- Next milestone: 30-day CS check-in
- Status health: Green/Yellow/Red
- Health notes: [Summary of results vs targets]

---

## Phase 7: Ongoing Success

### Step 21: Handover to Customer Success

**Deliverables to CS:**
- Complete playbook (with any adjustments from monitoring)
- Before/after metrics (The Core 12 updated)
- Implementation notes
- Optimisation recommendations
- Next playbook suggestions (based on secondary constraint)

**Client Portal Update:**
- Njin owners - Customer success AM: [CS AM Name]
- Status phase: Ongoing Success
- Next milestone: 30-day CS review
- Next milestone date: [Date]

---

### Step 22: 30-Day CS Review

**Review focus:**
- Are metrics trending toward targets?
- Is team following playbook consistently?
- What's working better than expected?
- What needs adjustment?

**Client Portal Update:**

Update relevant Core 12 metrics with 30-day actuals:
- Example: Show rate - 30-day: 58% (target: 60%+)
- Example: Close rate - 30-day: 24% (target: 30%+)

Update status:
- Status health: Green/Yellow/Red
- Health notes: [30-day status summary]
- Next milestone: 90-day review

---

### Step 23: 90-Day Performance Review

**Comprehensive review:**
- Full Core 12 update (before vs after with % improvement)
- ROI calculation (investment vs revenue impact)
- Team adoption assessment
- Process sustainability check
- Next bottleneck identification

**Client Portal Update:**

Update all Core 12 with 90-day actuals (before/after format with improvement percentages)

Update status:
- Status phase: Complete - Ongoing Optimisation
- Status health: Green/Yellow/Red
- Health notes: [90-day summary]
- Next milestone: v2 planning or next playbook

---

**End of SOP**