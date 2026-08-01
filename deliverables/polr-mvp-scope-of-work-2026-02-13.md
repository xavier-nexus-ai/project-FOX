# POLR MVP - Scope of Work

**Prepared by:** James Killick (Njin Method)
**Date:** 12 March 2026
**Version:** 3.1 (adds Phase 2 Roadmap; replaces v3.0 dated 23 February 2026)
**Status:** Scope of work - aligned to developer product backlog
**Client:** Fox Finance Group / Fox Home Loans

---

## 1. Project Summary

Fox Finance Group (FFG) and Fox Home Loans (FHL) operate across two siloed systems (Ambition, Finshaw's/Connective) with no unified customer view. The primary revenue constraint is **Monetisation** - leads sold to lead market and never re-engaged, cross-sell between brands is manual and untracked, and post-settlement nurture is basic time-based triggers.

GoHighLevel was abandoned (only needed ~10% of functionality). POLR MVP is a vibe-coded custom headless database solution using Next.js Edge Functions, focused on post-settlement lifecycle management, cross-sell automation, and email marketing. Brokers keep Ambition for sales. POLR handles everything after settlement.

The client's CTO (Matty) is an AI-capable software engineer who will maintain and iterate on POLR after handover.

---

## 2. What POLR MVP IS and IS NOT

**IS:**
- A unified customer database across both brands
- A post-settlement lifecycle automation engine
- A cross-sell trigger and routing system
- A team dashboard showing opportunities, contacts, and campaign performance
- A lead market reactivation manager
- An email marketing management interface (template editing, bulk sends, audience segmentation)
- A contact tagging and multi-brand overlap identification system

**IS NOT (in Phase 1):**
- A replacement for Ambition (brokers keep their LMS)
- A full CRM with sales pipeline
- A drag-and-drop email builder (Phase 2+)
- A customer-facing portal with authentication (Phase 2D - see roadmap detail)
- A referral partner portal (Phase 2+)
- A financial tools platform (Phase 2+ / Beacon on the Hill vision)
- UMI Loans integration (Phase 2F - see roadmap detail)
- Referral partner warm-up automation (Phase 2+)
- FHL lifecycle automation engine (Phase 2A - see roadmap detail)
- Cross-sell pipeline handoff workflow (Phase 2B - see roadmap detail)
- Dynamic link resource management (Phase 2C - see roadmap detail)
- Cotality property valuation integration (Phase 2E - see roadmap detail)

---

## 3. Playbook Strategy

Two playbooks are being delivered alongside POLR MVP. They define the strategy, content, and customer journeys that POLR automates.

### 3.1 Cross-Sell and Monetisation Playbook (Primary)

The primary constraint is Monetisation. FFG and FHL operate as silos with no systematic way to identify, route, or track cross-sell opportunities between brands. This playbook defines:

- **Customer journey mapping** - The Taylor lifecycle (stages 0-4) from settlement through to repeat customer and cross-brand advocacy
- **Cross-sell trigger logic** - When and why an FFG customer should be introduced to FHL (and vice versa), including scoring criteria and routing rules
- **Content strategy** - What to say at each lifecycle touchpoint, in what tone, through which channel (email, SMS, broker call)
- **Lead market reactivation approach** - How to re-engage leads sold to market after the cooling period
- **Value-add cycle** - FHL quarterly touchpoints (repricing, valuation, health check, anniversary) that build trust and create natural cross-sell moments
- **Care call methodology** - Scoring and prioritisation logic for weekly outbound care calls

### 3.2 Pre-Sales SDR Playbook

Focused on speed-to-contact and lead nurture for inbound inquiries. This playbook defines:

- **Lead qualification criteria** - How to score and route incoming leads based on ICA fit (Taylor vs Alex)
- **Nurture sequence strategy** - Content and timing for post-inquiry follow-up before a broker picks up
- **Reactivation approach** - How to bring cold leads back into the pipeline

### 3.3 Strategy Unchanged, Mechanism Changed

The original plan was to deliver both playbooks via GoHighLevel (GHL). When GHL was abandoned, the playbook strategy did not change - only the delivery mechanism. Everything that was going to be built in GHL workflows and pipelines is now being vibe-coded as a custom solution in POLR MVP.

**Playbooks define the WHAT and WHEN.** What content to send, when to send it, what triggers a cross-sell opportunity, how to score a care call, what the customer journey looks like at each stage.

**POLR defines the HOW.** The database structure, Edge Function automations, dashboard interfaces, and integrations that bring the playbook strategy to life.

The 8 automations, dashboard tabs, and email module are all direct implementations of the playbook methodology.

---

## 4. Technical Architecture

```
                    +------------------+
                    |   Supabase       |
                    |   (PostgreSQL +  |
                    |    Auth + API)   |
                    +--------+---------+
                             |
              +--------------+--------------+
              |                             |
     +--------v---------+          +--------v--------+
     | Vercel            |          | Integrations    |
     |                   |          |                 |
     | - Next.js         |          | - Ambition API  |
     |   Dashboard       |          | - SendGrid      |
     | - Edge Functions  |          | - Twilio        |
     |   (Automations)   |          | - CSV import    |
     +-------------------+          +-----------------+
```

### 4.1 Stack

| Component | Technology | Hosting | Rationale |
|-----------|-----------|---------|-----------|
| Database + Auth + API | Supabase (PostgreSQL) | Supabase Cloud | Instant REST/GraphQL API, row-level security, real-time subscriptions, auth built-in. CTO can maintain via SQL. |
| Front-end | Next.js 14+ (App Router) | Vercel | Team dashboard only in MVP. SSR for fast loads. Vercel's free tier likely sufficient for internal tool. |
| Automation engine | Next.js Edge Functions | Vercel | Cron-scheduled and webhook-triggered automations. TypeScript end-to-end. No separate infrastructure to manage. CTO can modify alongside dashboard code. |
| Email | SendGrid (existing) | SaaS | Already in use. Maintain continuity. Transactional + marketing via API. Dynamic templates for editable content. |
| SMS | Twilio | SaaS | Needed for lead market reactivation and lifecycle nudges. Inbound SMS webhook for reply tracking. |
| Monitoring | Supabase Dashboard + Vercel Logs | Built-in | No additional tooling needed for MVP. |

---

## 5. Data Model (7 Core Tables + 4 Email Marketing Tables)

### 5.1 `contacts`
The unified customer record across both brands.

| Column | Type | Notes |
|--------|------|-------|
| id | uuid (PK) | |
| first_name | text | |
| last_name | text | |
| email | text (unique) | |
| phone | text | |
| date_of_birth | date | For age-based triggers |
| state | text | QLD, NSW, etc. |
| postcode | text | For geography segmentation |
| housing_status | enum | renting, mortgaged, owns_outright, with_parents |
| employment_type | enum | payg_ft, payg_pt, casual, self_employed |
| credit_score_range | enum | poor, fair, good, excellent |
| source_brand | enum | FFG, FHL | Which brand originally acquired them |
| source_type | enum | organic, paid, referral, lead_market, partner |
| lifecycle_stage | integer | 0-4 (Taylor journey stages) |
| ica_segment | enum | taylor, taylor_plus, alex |
| is_active_customer | boolean | Has current open loan |
| created_at | timestamptz | |
| updated_at | timestamptz | |

**Multi-brand membership** is derived from the `loans` table (a contact with loans across different `brand` values is a multi-brand contact). No need for a separate field - query at read time or materialise as a view.

### 5.2 `loans`
Every loan across both brands, linked to contact.

| Column | Type | Notes |
|--------|------|-------|
| id | uuid (PK) | |
| contact_id | uuid (FK) | |
| brand | enum | FFG, FHL |
| loan_type | enum | personal, consumer, car, commercial, equipment, cashflow, home, investment, refinance |
| amount | decimal | |
| commission | decimal | Brokerage commission earned |
| settlement_date | date | Key trigger date |
| estimated_end_date | date | For refinance/renewal triggers |
| repayment_percentage | decimal | 0-100, updated periodically |
| status | enum | active, completed, refinanced, defaulted |
| lender_name | text | |
| clawback_end_date | date | FHL: 12-18 months post-settlement |
| source_system | enum | ambition, connective, manual |
| external_id | text | ID in source system |
| created_at | timestamptz | |

### 5.3 `contact_tags`
Custom and system-generated tags for segmentation.

| Column | Type | Notes |
|--------|------|-------|
| id | uuid (PK) | |
| contact_id | uuid (FK) | |
| tag_name | text | e.g., "water sports", "jet ski", "referral partner segment A" |
| tag_type | enum | custom, system | custom = team-created, system = auto-generated |
| created_by | text | User who created or "system" |
| created_at | timestamptz | |

**Unique constraint:** `(contact_id, tag_name)` - prevents duplicate tags on a contact.

**System tags** are auto-generated by Edge Function workflows:
- Brand membership tags (e.g., "brand:FFG", "brand:FHL") - derived from loans
- Lifecycle stage tags (e.g., "stage:2")
- Loan type tags (e.g., "loan:car", "loan:home")

**Custom tags** are free-text, created by team members via the dashboard:
- Interest-based: "water sports", "jet ski", "camping", "4WD"
- Product preferences: "interested in home loans", "debt consolidation candidate"
- Segment labels: any grouping the team finds useful

### 5.4 `cross_sell_opportunities`
Identified cross-sell possibilities with routing.

| Column | Type | Notes |
|--------|------|-------|
| id | uuid (PK) | |
| contact_id | uuid (FK) | |
| source_brand | enum | FFG, FHL |
| target_brand | enum | FFG, FHL |
| opportunity_type | text | e.g., "renter_to_homebuyer", "car_upgrade" |
| trigger_reason | text | What triggered this opportunity |
| score | integer | 1-100 priority score |
| status | enum | identified, assigned, contacted, converted, declined, expired |
| assigned_to | text | Broker name |
| assigned_at | timestamptz | |
| outcome_notes | text | |
| created_at | timestamptz | |

### 5.5 `automation_events`
Every automated touchpoint sent to a contact.

| Column | Type | Notes |
|--------|------|-------|
| id | uuid (PK) | |
| contact_id | uuid (FK) | |
| loan_id | uuid (FK, nullable) | |
| event_type | enum | email, sms, call_scheduled, stage_transition |
| template_name | text | Which template was used |
| channel | enum | sendgrid, twilio, manual |
| status | enum | sent, delivered, opened, clicked, bounced, failed |
| sent_at | timestamptz | |
| metadata | jsonb | Open/click data, delivery receipts |

### 5.6 `lead_market_contacts`
Leads sold to lead market, tracked for reactivation.

| Column | Type | Notes |
|--------|------|-------|
| id | uuid (PK) | |
| contact_id | uuid (FK, nullable) | Linked if they become a contact |
| original_brand | enum | FFG |
| sold_date | date | When sold to lead market |
| cooling_period_end | date | sold_date + 3 months |
| reactivation_status | enum | cooling, eligible, contacted, replied, reactivated, unresponsive, opted_out |
| reactivation_attempts | integer | Max 2 (1 SMS + 1 email) |
| last_contact_date | date | |
| loan_type_requested | text | Original inquiry type |
| amount_requested | decimal | |

### 5.7 `activity_log`
Audit trail for all system and user actions.

| Column | Type | Notes |
|--------|------|-------|
| id | uuid (PK) | |
| actor | text | User or "system" |
| action | text | |
| entity_type | text | contacts, loans, opportunities, etc. |
| entity_id | uuid | |
| details | jsonb | |
| created_at | timestamptz | |

### 5.8 Email Marketing Tables (Build Option B)

**`email_templates`**

| Column | Type | Notes |
|--------|------|-------|
| id | uuid (PK) | |
| name | text | Human-readable name |
| sendgrid_template_id | text | SendGrid dynamic template ID |
| category | enum | welcome, lifecycle, cross_sell, reactivation, marketing |
| brand | enum | FFG, FHL, all |
| subject_line | text | Editable subject line with merge field support |
| content_blocks | jsonb | Editable content blocks (array of {key, label, content}) |
| status | enum | draft, active, archived |
| last_edited_by | text | |
| last_edited_at | timestamptz | |
| created_at | timestamptz | |

**`email_campaigns`**

| Column | Type | Notes |
|--------|------|-------|
| id | uuid (PK) | |
| name | text | Campaign name |
| template_id | uuid (FK) | email_templates reference |
| audience_filters | jsonb | Saved filter criteria |
| audience_segment_id | uuid (FK, nullable) | If using a saved segment |
| audience_count | integer | Count at time of send |
| status | enum | draft, scheduled, sending, sent, cancelled |
| scheduled_at | timestamptz (nullable) | |
| sent_at | timestamptz (nullable) | |
| created_by | text | |
| created_at | timestamptz | |

**`email_campaign_stats`**

| Column | Type | Notes |
|--------|------|-------|
| id | uuid (PK) | |
| campaign_id | uuid (FK) | |
| total_sent | integer | |
| total_delivered | integer | |
| total_opened | integer | |
| total_clicked | integer | |
| total_bounced | integer | |
| total_unsubscribed | integer | |
| updated_at | timestamptz | Updated by SendGrid webhook handler |

**`audience_segments`**

| Column | Type | Notes |
|--------|------|-------|
| id | uuid (PK) | |
| name | text | e.g., "FFG renters stage 1+" |
| filters | jsonb | Filter criteria (same structure as email_campaigns.audience_filters) |
| created_by | text | |
| created_at | timestamptz | |

**`automation_content`** (used by both Core MVP and Email Module)

| Column | Type | Notes |
|--------|------|-------|
| id | uuid (PK) | |
| workflow_name | text | e.g., "ffg_welcome_sequence" |
| step_number | integer | Order within workflow |
| step_name | text | e.g., "Day 0 Welcome Email" |
| channel | enum | email, sms |
| subject_line | text (nullable) | For emails only |
| content | text | Rich text for email, plain text for SMS |
| merge_fields_used | text[] | List of merge fields for UI hints |
| sendgrid_template_id | text (nullable) | If using SendGrid template |
| last_edited_by | text | |
| last_edited_at | timestamptz | |

### 5.9 Database Views

The following should be implemented as Supabase views for dashboard consumption:

- **`contact_brand_membership`**: Derives which brands a contact belongs to from the `loans` table. Returns contact_id, array of brands, brand count. Contacts with brand_count = 2 are multi-brand.
- **`cross_sell_pool`**: Contacts in both brands, with active loans in at least one.
- **`email_audience_segments`**: Pre-built view joining contacts + tags + loans for the email blast audience builder (Build Option B).

---

## 6. MVP Automations (8 Priority Workflows)

All 8 workflows are built as Next.js Edge Functions deployed on Vercel. Each workflow's **structure and timing are defined in code**, but the **email/SMS content** within each step is stored in Supabase (`automation_content` table) and editable via the dashboard. The content and trigger logic for each workflow is defined by the playbook methodology.

### 6.1 Post-Settlement Welcome Sequence (FFG)
**Trigger:** New loan record with status=active and brand=FFG
**Implementation:** Edge Function triggered by Supabase webhook on loan insert
**Actions:**
- Day 0: Welcome email (loan summary, first repayment date, tips, one-line FHL intro)
- Day 3: SMS check-in ("How's everything feeling with your new loan?")
- Day 7: Google review request email
- Set lifecycle_stage = 0

### 6.2 Post-Settlement Welcome Sequence (FHL)
**Trigger:** New loan with brand=FHL
**Implementation:** Edge Function triggered by Supabase webhook on loan insert
**Actions:**
- Day 0: Welcome email (settlement congratulations, offset/redraw tips, what happens next)
- Day 3: SMS check-in
- Day 7: Google review request
- Day 30: Property valuation teaser ("Want to see how your property value is tracking?")

### 6.3 Taylor Lifecycle Stage Transitions
**Trigger:** Time-based + data-based checks (Edge Function cron, runs daily)
**Logic:**
- Stage 0 to 1: 1 month post-settlement
- Stage 1 to 2: 6 months post-settlement OR engagement score > threshold
- Stage 2 to 3: Loan 60-80% repaid (data trigger) OR 24 months post-settlement
- Stage 3 to 4: FHL loan settled + 5 years elapsed
**Actions per transition:** Update lifecycle_stage, send stage-appropriate email, notify assigned broker if cross-sell opportunity exists

### 6.4 FFG-to-FHL Cross-Sell Detection
**Trigger:** Multiple signals checked weekly (Edge Function cron):
- Contact housing_status = "renting" AND lifecycle_stage >= 1
- Loan repayment_percentage >= 60%
- Time since settlement > 12 months AND no FHL loan exists
**Actions:**
- Create cross_sell_opportunity (source=FFG, target=FHL, type="renter_to_homebuyer")
- Score the opportunity (based on income, credit, engagement)
- IF score > 70: notify broker immediately
- IF score 40-70: add to team dashboard queue

### 6.5 FHL-to-FFG Cross-Sell Detection
**Trigger:** Checked monthly (Edge Function cron):
- FHL customer with no active FFG loan
- Property settled > 3 months (past initial financial stress)
- Any of: new car needed (age-based), debt consolidation signals, deposit GAP funding opportunity
**Actions:**
- Create cross_sell_opportunity (source=FHL, target=FFG)
- Notify FFG team via dashboard

### 6.6 Home Loans Value-Add Cycle
**Trigger:** Time-based from FHL settlement_date (Edge Function cron):
- Quarter 1 (3 months): Repricing check offer
- Quarter 2 (6 months): Free property valuation
- Quarter 3 (9 months): Financial health check invitation
- Quarter 4 (12 months): Anniversary check-in + refinance discussion if past clawback
- Repeats annually with refinance focus after 18 months
**Actions:** Email + SMS for each touchpoint. Flag repricing and refinance as broker action items on dashboard.

### 6.7 Lead Market Reactivation
**Trigger:** Edge Function cron (daily). Picks up records where `lead_market_contacts.cooling_period_end <= today AND reactivation_status = 'eligible'`
**Actions:**
- **Step 1 - SMS (primary):** Conversational message via Twilio. e.g., "Hi [name], how did you get on with your [loan_type]? Were you able to get it sorted?"
- **Step 2 - Email (secondary):** Sent 7 days after SMS if no reply detected. Plain text via SendGrid, same conversational tone.
- **Reply tracking:** Twilio inbound SMS webhook + SendGrid Inbound Parse webhook -> Edge Function -> update `reactivation_status` to "replied" -> create dashboard notification for assigned broker.
- Broker picks up and acts manually. No AI, no automated response.
- **Max:** 1 SMS + 1 email per contact. No response after both = mark `reactivation_status` as "unresponsive".

### 6.8 Customer Care Call List Generator
**Trigger:** Weekly Edge Function cron (Monday morning)
**Logic:** Score existing customers for outbound care call priority:
- Last contact > 6 months ago (+20 points)
- Multiple loans (+10 per loan)
- Approaching loan end date (+30 points)
- High engagement (email opens) (+10 points)
- Never cross-sold (+15 points)
- Known life stage signal (renting + income growth) (+20 points)
**Actions:**
- Generate prioritised call list (top 20)
- Push to team dashboard with contact details, last interaction, suggested talking points
- Track outcomes (inquiry generated, opportunity created)

---

## 7. Email Management Module (Build Option B)

This module provides SendGrid-powered email management within the POLR dashboard, giving the team (Rowdie/Nathan) the ability to manage email campaigns without leaving the platform.

### 7.1 Template Editor

**Purpose:** Allow team to edit email content within pre-designed templates without touching code.

**Requirements:**
- Edit text content within pre-designed email templates
- Insert merge fields (contact first name, loan type, brand, settlement date, etc.)
- Basic text formatting (bold, italic, links, headings)
- Preview rendered email before saving
- NOT a drag-and-drop visual builder (that is Phase 2+)
- Templates are pre-designed (HTML/CSS structure is fixed); team edits content only

**Technical approach:**
- Templates stored as SendGrid dynamic templates
- Template metadata and content stored in Supabase (`email_templates` table)
- Dashboard provides a rich text editor (e.g., TipTap or similar) for the editable content blocks
- On save, content is pushed to SendGrid via API
- Edge Functions reference SendGrid template IDs at send time

### 7.2 Bulk Email Blast Interface

**Purpose:** Allow team to create and send marketing emails to segmented audiences directly from the dashboard.

**Audience builder** with filters:
- Brand: FFG / FHL / multi-brand (contacts in both brands)
- State, postcode
- Lifecycle stage (0-4)
- Loan type (personal, consumer, car, commercial, equipment, cashflow, home, investment, refinance)
- Loan status (active, completed, refinanced)
- Housing status (renting, mortgaged, owns_outright, with_parents)
- Employment type (payg_ft, payg_pt, casual, self_employed)
- Tags (any custom or system tag - supports AND/OR logic)
- Multi-business overlap (contacts in 1 or 2 brands)
- Contact created date range
- Last email engagement (opened/clicked within X days)

**Sending:**
- Select template from template editor or create new
- Preview with sample contact data
- Schedule for a future date/time OR send immediately
- Confirmation step before send (audience count + sample preview)
- Sends via SendGrid API

**Tracking:**
- Results visible in dashboard (Email Marketing tab)
- Metrics from SendGrid webhooks: sends, opens, clicks, bounces, unsubscribes
- Per-campaign performance summary

**Save reusable audience segments:**
- Save filter combinations as named segments (e.g., "FFG renters stage 1+", "FHL past clawback")
- Segments are dynamic (re-evaluate at send time, not static lists)

### 7.3 Nurture Sequence Content Editing

**Purpose:** Allow team to update the email/SMS copy used by the 8 automation workflows without touching code.

**Requirements:**
- Each automation workflow step has a content record in Supabase (`automation_content` table)
- Dashboard provides an editing interface grouped by workflow (e.g., "FFG Welcome Sequence" > Step 1: Day 0 Email > Step 2: Day 3 SMS > Step 3: Day 7 Email)
- Edit the subject line, body content, and SMS text for each step
- Preview with merge fields populated from a sample contact
- Changes take effect immediately (Edge Functions read content from Supabase at send time)
- Version history or last-edited timestamp visible

**Edge Function integration pattern:**
1. Edge Function triggers (e.g., new settlement webhook)
2. Edge Function queries Supabase `automation_content` table for the relevant step
3. Edge Function merges contact data into content
4. Edge Function sends via SendGrid (email) or Twilio (SMS)

This means the automation structure/timing lives in Edge Function code (hardcoded), but the actual message content lives in Supabase (editable via dashboard).

---

## 8. Contact Tagging & Multi-Brand Overlap

### 8.1 Tagging System

**Data model:** See `contact_tags` table in the data model.

**Dashboard UI requirements:**
- Add/remove tags on individual contact records
- Bulk tag operations (select multiple contacts, add/remove tags)
- Tag management page: view all tags, usage counts, delete unused tags
- Tag autocomplete when adding (suggests existing tags)
- Tag type indicator (custom vs system) - system tags are read-only in UI

### 8.2 Multi-Brand Overlap Identification

**Approach:** Brand membership is derived from the `loans` table. A contact with loans across different `brand` values is a multi-brand contact. This is cleaner than maintaining a separate field on contacts.

**Dashboard UI requirements:**
- Visual indicator on contact records showing which brands they have loans with (e.g., coloured badges: FFG blue, FHL green)
- Contact list filter: "Show contacts in 2 brands" (the cross-sell pool)
- Contact list filter: "Show contacts in brand X only" (single-brand customers)
- Cross-sell pipeline should display brand badges on each opportunity
- Summary card on dashboard: "Multi-brand contacts: X" and "Single-brand contacts: Y"

---

## 9. Team Dashboard (Next.js)

### 9.1 Layout

**Top Bar:** Logged-in user, brand filter (FFG / FHL / All), date range

**4 Summary Cards:**
1. Active Cross-Sell Opportunities (count + trend)
2. Customers Due for Touchpoint This Week (count)
3. Lead Market Reactivations Ready (count)
4. Care Calls Due This Week (count)

### 9.2 Tab 1: Cross-Sell Pipeline
Table view of cross_sell_opportunities sorted by score (highest first):
- Customer name, source brand, target brand, opportunity type, score, status, assigned broker
- Multi-brand badges on customer name
- Tags displayed as chips
- Click to expand: full contact history, loans, trigger reason
- Actions: Assign, Contact, Convert, Decline

### 9.3 Tab 2: Lifecycle + Automation
Combined view of lifecycle tracking and automation activity:

**Lifecycle view:**
- Stage 0-4 counts with trend arrows
- Drill-down to contact list per stage
- Highlight: contacts approaching stage transition

**Automation activity:**
- Recent automation events log (emails sent, SMS sent, triggers fired)
- Delivery/open/click rates (rolling 7-day and 30-day)
- Failed deliveries flagged

### 9.4 Tab 3: Lead Market
Lead market reactivation status:
- Eligible for reactivation (count)
- SMS sent, awaiting reply (count)
- Email sent, awaiting reply (count)
- Replied this month (count)
- Reactivated this month (count)
- Unresponsive (count)

### 9.5 Tab 4: Care Call List
Weekly prioritised call list:
- Customer, last contact date, priority score, suggested topics
- Log call outcome inline
- Track: inquiries generated from calls

### 9.6 Tab 5: Email Marketing (Build Option B)

**Create New Campaign:**
- Template selector (from template editor library)
- Audience builder (filters from the email marketing audience model)
- Audience count preview (live count as filters are applied)
- Schedule or send immediately
- Confirmation step

**Campaigns List:**
- Draft campaigns (editable)
- Scheduled campaigns (with scheduled date, can cancel)
- Sent campaigns with performance metrics (opens, clicks, bounces, unsubscribes)
- Click to view detailed per-campaign analytics

**Saved Segments:**
- List of saved audience segments with contact counts
- Edit, duplicate, or delete segments

**Nurture Sequence Editor:**
- List of 8 automation workflows
- Expand each to see steps
- Edit content for each step (per the nurture sequence editor requirements)

---

## 10. Hard Business Rules (Must Be Enforced in Code)

1. **FHL clawback awareness**: No refinance suggestions before clawback_end_date. Display clawback status on dashboard.
2. **Lead market cooling period**: No reactivation contact before cooling_period_end (3 months from sold_date).
3. **Compliance language**: No templates may contain "advice", "guarantee", or "financial hardship".
4. **SMS opt-out**: All SMS must include opt-out mechanism. Track opt-outs and suppress future messages.
5. **Human-led cross-sell**: All cross-sell opportunities route to a human broker for contact. No automated cross-sell emails without human review in MVP.

---

## 11. Out-of-Scope Items (NOT in MVP)

The following items have been discussed but are explicitly excluded from this scope of work. They are Phase 2+ or separate projects.

1. UME Loans integration (separate business, separate data system)
2. Referral partner management (1,050 dormant partners - Phase 2)
3. Fox's own AI product / AI monetisation
4. Running ads through Njin
5. 2 vibe-coded websites (FFG, FHL)
6. Full drag-and-drop email builder (MVP has content-only editor within fixed templates)
7. Client-facing portal / customer dashboard
8. Referral partner login portal
9. Financial tools (budgeting, credit score, savings goals)
10. Property valuation integration
11. Bank statement integration
12. AI voice calling
13. AI chatbot / conversational AI
14. Google Ads management
15. Facebook Ads creative
16. YouTube/podcast content system
17. LinkedIn automation
18. Lead magnet creation
19. Milestone rewards fulfilment (Prezzie vouchers etc.)
20. Alex (commercial) customer journey automation (Taylor journey first)
21. Retargeting pixel integration

These are all valid Phase 2+ items. MVP must prove the core automation loop works before expanding.

---

## 12. Monthly Running Costs (Estimated)

| Service | Tier | Estimated Monthly Cost |
|---------|------|----------------------|
| Supabase | Pro ($25/month) | $25 |
| Vercel (Dashboard + Edge Functions) | Free/Pro | $0-20 |
| Twilio (SMS) | Pay-per-message | $50-200 (volume dependent) |
| SendGrid | Already paid | $0 (existing) |
| **Total** | | **$75-245/month** |

*Note: Twilio cost depends on SMS volume. Lead market reactivation SMS and lifecycle nudges will push toward the higher end at scale. AU SMS rates are approximately $0.05-0.08 per message.*

---

## 13. Next Steps

1. **Nathan/Rowdie**: Review this scope document and approve
2. **Nathan**: Decide on Build Option A only vs A+B
3. **Rowdie**: Provide Ambition API documentation
4. **Rowdie**: Confirm privacy policy status for cross-business data sharing
5. **James**: Finalise developer briefing with lead market reactivation additions
6. **James**: Begin build once dependencies are cleared and scope is approved

---

## 14. Phase 2 Roadmap

Phase 2 extends POLR MVP from an internal team dashboard into a lifecycle automation engine with customer-facing capabilities. Each sub-phase is independently scoped and can be built sequentially. Dependencies between phases are noted explicitly.

**Important:** Phase 2 work should not begin until Phase 1 is deployed, stable, and validated with real data. Phase 1 proves the core automation loop; Phase 2 builds on that foundation.

### Phase 2 Dependency Map

```
Phase 1 (MVP)
    └── 2A (FHL Lifecycle Engine)
         └── 2B (Cross-Sell Pipeline Handoff)
    └── 2C (Dynamic Links / Resources)
         └── 2D (Customer Portal + Auth)
              └── 2E (Cotality Integration)
    └── 2F (Additional Integrations - independent, backlog)
```

---

### 14.1 Phase 2A - FHL Lifecycle Engine

**Priority:** Critical - this is the revenue mechanism for FHL post-settlement nurture
**Source:** `fhl_customer_lifecycle` data in COS (7 touchpoints, 4 customer segments)

#### 14.1.1 Schema Additions

**New table: `lifecycle_events`**

| Column | Type | Notes |
|--------|------|-------|
| id | uuid (PK) | |
| contact_id | uuid (FK → contacts) | |
| loan_id | uuid (FK → loans) | The FHL loan that triggered this lifecycle |
| touchpoint_month | integer | 1, 3, 6, 9, 12, 15, or 18 |
| touchpoint_name | text | e.g., "Welcome + Setup Verified", "90-Day Confidence Pack" |
| status | enum | scheduled, due, in_progress, completed, skipped |
| scheduled_date | date | Calculated from settlement_date + touchpoint_month |
| completed_date | date (nullable) | When the touchpoint was actually delivered |
| completed_by | text (nullable) | Staff member who executed the touchpoint |
| outcome_notes | text (nullable) | Call notes, client response, issues identified |
| deliverable_sent | boolean | Whether the one-pager/pack was sent |
| deliverable_url | text (nullable) | Link to dynamic resource (Phase 2C integration) |
| created_at | timestamptz | |
| updated_at | timestamptz | |

**New columns on `contacts` table:**

| Column | Type | Notes |
|--------|------|-------|
| settlement_date | date | FHL loan settlement date (copied from most recent FHL loan) |
| loan_segment | enum | fhb, investor, refinancer, new_purchase |
| current_touchpoint | integer (nullable) | Most recent completed touchpoint month |
| next_touchpoint_date | date (nullable) | Calculated next scheduled touchpoint |

#### 14.1.2 Edge Functions (7 Scheduled Triggers)

A daily cron Edge Function scans `lifecycle_events` where `status = 'scheduled' AND scheduled_date <= today`. For each due event:

1. **Month 1 - Welcome + Setup Verified**
   - Trigger: 1 month post-settlement
   - Action: Create dashboard task for assigned broker (phone call). Send email/SMS if no contact made within 3 business days.
   - Content: Loan Setup Snapshot one-pager (segment-neutral)

2. **Month 3 - 90-Day Confidence Pack**
   - Trigger: 3 months post-settlement
   - Action: Generate segment-specific deliverable, send via email with dynamic link
   - Conditional content by segment:
     - FHB: First-Year Homeowner Plan (valuation benchmark + cost-to-own baseline)
     - Investor: Investor 90-Day File Check (valuation benchmark + rent/expense tracking)
     - Refinancer: Savings Proof + Equity Baseline (valuation benchmark + refinance results)
     - New Purchase: Property Position and Loan Health (standard pack)
   - Cotality integration point: pulls valuation data if Phase 2E is active

3. **Month 6 - Proactive Pricing Review**
   - Trigger: 6 months post-settlement
   - Action: Create dashboard task for broker to run repricing check. Send result email.
   - Dual CTA: "Reply if you have questions" / "Permission to proceed with repricing"
   - Internal logging: pricing request status, rate/discount notes, next eligibility date

4. **Month 9 - FFG Momentum and Opportunity Pack**
   - Trigger: 9 months post-settlement
   - Action: Send segment-specific FFG cross-sell pack + optional FHL equity release pack
   - **Cross-sell handoff integration (Phase 2B):** If customer engages with pack, create `cross_sell_referral` record and route to FFG team
   - Conditional packs by segment:
     - New Purchase: New Home Momentum Pack (car, furniture, solar, renos, consolidation)
     - FHB: First Home Momentum Pack (car, furniture, solar, travel/wedding, consolidation)
     - Investor: Investor Leverage Pack (vehicle, equipment, business, consolidation, reno)
     - Refinancer: Refi Savings Accelerator Pack (consolidate, refinance loans, fund purchases)
   - Plus optional: Equity Release/Top-Up Pack (if equity growth warrants)

5. **Month 12 - Annual Property and Loan Strategy Review**
   - Trigger: 12 months post-settlement
   - Action: Generate annual review deliverable (2 pages max), create broker task for review call
   - Content: Updated valuation + movement since month 3, strategy recommendation, next 12-month plan
   - CTA: "Reply REVIEW to book your annual strategy call"
   - Cotality integration point: updated valuation pull

6. **Month 15 - Refinance Pathway**
   - Trigger: 15 months post-settlement
   - Action: Send Your Options Map (three paths with pros/cons and recommendation)
   - Three paths: Pay down faster / Invest or upgrade / Refinance for better deal
   - **Clawback awareness:** Must check `loans.clawback_end_date` before presenting refinance option

7. **Month 18 - Action Window**
   - Trigger: Conditional - only fires if one or more triggers are met:
     - Fixed rate expiry approaching
     - Major market movement (manual flag by broker)
     - Customer goal change (logged in CRM)
     - Lender/product change creating clear advantage
   - Action: Send Action Window Plan (recommended action, timeline, checklist)
   - CTA: "Reply GO to start the action plan"
   - If no triggers are met: skip this touchpoint, schedule next annual review at month 24

#### 14.1.3 Lifecycle Dashboard View

**New dashboard tab: "FHL Lifecycle"** (visible to Bill, Paige, Angel)

**Summary cards:**
- Customers in lifecycle (total active)
- Touchpoints due this week
- Overdue touchpoints (red highlight)
- Completed this month

**Table view:**
- Customer name, settlement date, segment, current touchpoint, next touchpoint date, status, assigned broker
- Filter by: segment, touchpoint month, status (due/overdue/completed), broker
- Sort by: next touchpoint date (soonest first, overdue at top)
- Click to expand: full lifecycle timeline showing all 7 touchpoints with status

**Overdue alert:** If a touchpoint is more than 7 days past its scheduled date and not completed, flag as overdue and send internal notification.

#### 14.1.4 SendGrid Template System

Up to 21 content variants required (3 primary segments x 7 touchpoints). In practice, months 1, 6, 15, and 18 are segment-neutral, reducing to approximately 13 unique templates:

| Touchpoint | FHB | Investor | Refinancer | New Purchase |
|------------|-----|----------|------------|--------------|
| Month 1 | Shared | Shared | Shared | Shared |
| Month 3 | Unique | Unique | Unique | Unique |
| Month 6 | Shared | Shared | Shared | Shared |
| Month 9 | Unique | Unique | Unique | Unique (+equity) |
| Month 12 | Shared | Shared | Shared | Shared |
| Month 15 | Shared | Shared | Shared | Shared |
| Month 18 | Shared | Shared | Shared | Shared |

All templates use SendGrid dynamic templates with merge fields (contact name, property address, valuation data, loan details). Content is editable via the Phase 1 nurture sequence editor.

#### 14.1.5 Effort Estimate

| Component | Hours (indicative) |
|-----------|--------------------|
| Schema additions + migrations | 4-6 |
| Lifecycle event generator (on loan settlement) | 6-8 |
| Daily cron Edge Function (7 touchpoint handlers) | 20-30 |
| Lifecycle dashboard tab | 12-16 |
| SendGrid template creation (13 templates) | 8-12 |
| Segment routing logic | 4-6 |
| Testing + edge cases | 8-12 |
| **Total Phase 2A** | **62-90 hours** |

#### 14.1.6 Prerequisites and Decisions

- **Prerequisite:** Phase 1 deployed with contacts and loans tables populated
- **Prerequisite:** Tone of voice guide applied to all lifecycle content (gate passed)
- **Decision required:** Who executes each touchpoint? Broker or dedicated client services role? (COS outstanding decision - Nathan)
- **Decision required:** Backfill strategy - do existing FHL customers get enrolled in lifecycle from their original settlement date, or start fresh?
- **Dependency:** Phase 2C (Dynamic Links) enhances deliverable delivery but is not blocking - PDFs can be used as interim

---

### 14.2 Phase 2B - Cross-Sell Pipeline Handoff Workflow

**Priority:** Critical - this is the core monetisation mechanic connecting FFG and FHL
**Resolves:** COS outstanding decision on cross-sell pipeline ownership

#### 14.2.1 Schema

**New table: `cross_sell_referrals`**

| Column | Type | Notes |
|--------|------|-------|
| id | uuid (PK) | |
| source_entity | enum | FFG, FHL | Brand that originated the referral |
| source_contact_id | uuid (FK → contacts) | The customer being referred |
| source_broker | text | Broker who identified the opportunity |
| target_entity | enum | FFG, FHL | Brand receiving the referral |
| target_broker | text (nullable) | Broker assigned on receiving end |
| referral_stage | enum | identified, routed, accepted, contacted, in_progress, converted, declined, expired |
| trigger_source | text | What created this referral (e.g., "lifecycle_month_9", "care_call", "manual") |
| opportunity_type | text | e.g., "car_loan", "home_loan", "debt_consolidation" |
| outcome | enum (nullable) | settled, lost_to_competitor, not_qualified, not_interested, timing_wrong |
| outcome_notes | text (nullable) | |
| revenue_attributed | decimal (nullable) | Commission earned from converted referral |
| loan_id | uuid (FK → loans, nullable) | Linked loan if referral converts |
| created_at | timestamptz | |
| updated_at | timestamptz | |
| accepted_at | timestamptz (nullable) | When target broker accepted the referral |
| contacted_at | timestamptz (nullable) | When target broker first contacted customer |
| converted_at | timestamptz (nullable) | When loan settled |
| expired_at | timestamptz (nullable) | Auto-expire after 90 days with no progress |

**New column on `cross_sell_referrals`:**

| Column | Type | Notes |
|--------|------|-------|
| pipeline_owner | text | The person responsible for progressing this referral |

This resolves the COS outstanding decision: pipeline ownership is explicitly assigned per referral, not per brand.

#### 14.2.2 Handoff Workflows

**FHL → FFG Handoff (Month 9 Lifecycle Trigger):**
1. Lifecycle engine fires month 9 touchpoint
2. Customer engages with FFG Momentum Pack (click tracked via SendGrid webhook)
3. Edge Function creates `cross_sell_referral` (source=FHL, target=FFG)
4. Assign `pipeline_owner` based on routing rules:
   - Consumer loans → round-robin across FFG consumer brokers
   - Commercial loans → Sam Drew (Head of Asset & SME)
5. Send internal notification to target broker (dashboard + email)
6. Log activity in `activity_log`
7. Dashboard shows referral in cross-sell pipeline with countdown timer (90-day expiry)

**FFG → FHL Handoff (Existing Cross-Sell Detection):**
1. Phase 1 cross-sell detection identifies opportunity
2. Edge Function creates `cross_sell_referral` (source=FFG, target=FHL)
3. Assign `pipeline_owner`:
   - Residential → round-robin across Bill, Paige, Angel
   - Commercial → Bill Robb
4. Send internal notification to target broker
5. Target broker accepts referral (updates stage to "accepted")
6. Target broker contacts customer, logs outcome

**Manual Referral Creation:**
- Any broker can create a referral manually from the contact record
- Supports ad-hoc cross-sell that does not come from automated triggers
- Same tracking and pipeline visibility as automated referrals

#### 14.2.3 Cross-Sell Pipeline Dashboard

**Enhanced Tab 1 (Cross-Sell Pipeline) with referral tracking:**

**Summary cards:**
- Active referrals (by direction: FHL→FFG, FFG→FHL)
- Conversion rate (rolling 90-day)
- Revenue attributed this month/quarter
- Average time from referral to conversion

**Table view:**
- Customer, source brand, target brand, opportunity type, referral stage, pipeline owner, days open, revenue
- Filter by: direction, stage, owner, date range
- Click to expand: full referral timeline (created → routed → accepted → contacted → outcome)

**Revenue attribution report:**
- Monthly/quarterly view of cross-sell revenue by direction
- Broker leaderboard (who generates and converts the most referrals)
- Conversion funnel (identified → contacted → converted, with drop-off rates)

#### 14.2.4 Effort Estimate

| Component | Hours (indicative) |
|-----------|--------------------|
| Schema + migrations | 4-6 |
| FHL→FFG handoff Edge Function | 8-10 |
| FFG→FHL handoff Edge Function | 6-8 |
| Manual referral creation UI | 4-6 |
| Pipeline dashboard enhancements | 10-14 |
| Revenue attribution reporting | 6-8 |
| Broker routing logic | 4-6 |
| Notification system (internal) | 4-6 |
| Testing + edge cases | 6-8 |
| **Total Phase 2B** | **52-72 hours** |

#### 14.2.5 Prerequisites and Decisions

- **Prerequisite:** Phase 1 cross-sell detection deployed and generating opportunities
- **Prerequisite:** Phase 2A lifecycle engine deployed (for month 9 trigger)
- **Decision required:** Pipeline ownership model - per-referral assignment (recommended) or fixed brand-level ownership?
- **Decision required:** Broker routing rules for each direction (confirm with Nathan/Rowdie)
- **Decision required:** Referral expiry policy (recommended: 90 days, then auto-expire with notification)
- **Decision required:** Privacy policy for cross-business data sharing (COS blocker)

---

### 14.3 Phase 2C - Dynamic Links / Resource Management System

**Priority:** High - replaces static PDF delivery for all lifecycle touchpoints
**Enables:** Phase 2D (Customer Portal)

#### 14.3.1 Schema

**New table: `resources`**

| Column | Type | Notes |
|--------|------|-------|
| id | uuid (PK) | |
| slug | text (unique) | URL-friendly identifier, e.g., "90-day-confidence-pack-fhb" |
| title | text | Display title |
| content | text | Rich text content (HTML) |
| segment | enum (nullable) | fhb, investor, refinancer, new_purchase, all |
| touchpoint_month | integer (nullable) | 1, 3, 6, 9, 12, 15, 18 (nullable for non-lifecycle resources) |
| brand | enum | FFG, FHL, all |
| resource_type | enum | lifecycle_deliverable, momentum_pack, guide, general |
| published | boolean | Only published resources are publicly accessible |
| last_updated | timestamptz | |
| updated_by | text | |
| created_at | timestamptz | |

#### 14.3.2 Next.js Dynamic Route

**Route:** `/resources/[slug]`

- Publicly accessible (no authentication required)
- Server-side rendered for fast load and SEO
- Clean, branded layout matching Fox Finance Group design system (orange #ED9B33, grey #63666A, black #101820)
- Mobile-responsive (most customers will open on phone from email/SMS link)
- No navigation to other resources (each link is standalone)
- Optional: branded header with Fox logo, footer with contact details

**Lifecycle deliverables mapped to resources:**

| Deliverable | Slug Pattern | Segments |
|-------------|-------------|----------|
| Loan Setup Snapshot | `loan-setup-snapshot` | Shared |
| 90-Day Confidence Pack | `90-day-confidence-pack-{segment}` | 4 variants |
| Repricing Review | `repricing-review` | Shared |
| FFG Momentum Packs | `momentum-pack-{segment}` | 4 variants |
| Equity Release Pack | `equity-release-pack` | Shared |
| Annual Review | `annual-review` | Shared |
| Options Map | `options-map` | Shared |
| Action Window Plan | `action-window-plan` | Shared |

Approximately 12 resource pages to create at launch.

#### 14.3.3 Admin Interface

**New dashboard area: "Resources"**

- List all resources with title, segment, touchpoint, published status, last updated
- Create new resource: title, slug (auto-generated from title, editable), segment, touchpoint month, brand
- Edit resource: basic rich text editor (TipTap or similar - bold, italic, headings, links, images, lists)
- Preview: render resource as it will appear on public URL
- Publish/unpublish toggle
- NOT a drag-and-drop page builder (keep it simple - rich text only)

#### 14.3.4 Integration with Lifecycle Engine

When Phase 2A lifecycle touchpoints fire, the deliverable URL is populated from the `resources` table:
1. Edge Function looks up resource by `touchpoint_month` + `segment`
2. Constructs URL: `{base_url}/resources/{slug}`
3. Includes URL in email template as the deliverable link
4. Stores URL in `lifecycle_events.deliverable_url`

This replaces static PDF attachments with living, updatable content.

#### 14.3.5 Effort Estimate

| Component | Hours (indicative) |
|-----------|--------------------|
| Schema + migrations | 2-4 |
| Dynamic route (`/resources/[slug]`) | 6-8 |
| Branded layout + responsive design | 8-12 |
| Admin interface (list, create, edit) | 10-14 |
| Rich text editor integration | 4-6 |
| Lifecycle engine integration | 2-4 |
| Initial content creation (12 resources) | 8-12 |
| Testing (public access, mobile, edge cases) | 4-6 |
| **Total Phase 2C** | **44-66 hours** |

#### 14.3.6 Prerequisites and Decisions

- **Prerequisite:** Phase 1 deployed (dashboard framework exists)
- **Prerequisite:** Tone of voice guide applied to all resource content
- **Decision required:** Domain/subdomain for public resources (e.g., `polr.foxfinancegroup.com.au/resources/` or dedicated subdomain)
- **Decision required:** Branding - unified Fox brand or separate FFG/FHL branded resources?
- **No dependency on Phase 2A** - resources can be created and published independently, then linked to lifecycle engine later

---

### 14.4 Phase 2D - Customer Portal with Authentication

**Priority:** Medium-high - customer-facing capability confirmed by Nathan (2026-03-06)
**Gates:** Phase 2C (Dynamic Links) must be deployed first
**Risk mitigation:** Staged rollout to address Nathan's IT security concerns

#### 14.4.1 Authentication

**Supabase Auth with magic links (passwordless):**
- Customer enters email on login page
- Supabase sends magic link email
- Customer clicks link, authenticated for session duration
- No passwords to manage, reset, or breach
- Session duration: 7 days (configurable)
- Rate limiting on magic link requests (prevent abuse)

**Why magic links:**
- Lowest friction for customers (no password to remember)
- Lowest risk for Fox (no password database to protect)
- Supabase Auth handles token management, session refresh, and security
- Aligns with Nathan's staged security approach

#### 14.4.2 Customer Dashboard (Read-Only)

**Route:** `/portal` (authenticated)

**Loan summary:**
- Active loans across both brands (if multi-brand customer)
- Loan amount, repayment amount, frequency, estimated end date
- Brand indicator (FFG blue / FHL green)
- NO sensitive financial data (no bank details, no credit scores, no income)

**Lifecycle progress:**
- Next scheduled touchpoint and date
- Previous touchpoints completed (timeline view)
- "Your broker" contact card with photo, phone, email

**Resource library:**
- All resources relevant to this customer's segment and completed touchpoints
- Links to Phase 2C dynamic resources
- Organised by date received

**Affiliate partner directory:**
- "Trusted by Fox" partner listing
- Partner name, field, contact details
- Curated list (not all partners - only those relevant to customer's segment/stage)

#### 14.4.3 Staged Security Implementation

| Stage | Scope | Duration | Exit Criteria |
|-------|-------|----------|---------------|
| Stage 1 | Internal testing only (staff accounts) | 2-4 weeks | No critical bugs, performance acceptable |
| Stage 2 | Beta with 10-20 selected clients | 4-6 weeks | Positive feedback, no data concerns, smooth auth flow |
| Stage 3 | Full rollout to all active FHL/FFG customers | Ongoing | Stage 2 sign-off from Nathan |

**Stage 1 actions:**
- Deploy portal to staging environment
- Create staff test accounts
- Security review (Supabase RLS policies, API exposure, data leakage)
- CTO (Matty) code review of auth implementation

**Stage 2 actions:**
- Select 10-20 engaged customers (recent touchpoint completed, high engagement score)
- Personal invitation from their broker
- Feedback collection (simple form or follow-up call)
- Monitor auth logs for issues

**Stage 3 actions:**
- Update all lifecycle email templates to include portal login link
- Announce portal via email campaign to all active customers
- FAQ page for common questions

#### 14.4.4 Privacy and Data Considerations

- **Row-Level Security (RLS):** Supabase RLS policies ensure customers can only see their own data
- **Data display policy:** NO bank details, credit scores, income, or employment data shown in portal
- **Cross-brand visibility:** Multi-brand customers see loans from both brands (FFG + FHL). This requires the cross-business data sharing privacy policy to be in place (COS blocker)
- **Audit logging:** All portal logins and page views logged in `activity_log`
- **Data retention:** Customer portal sessions expire after 7 days of inactivity

#### 14.4.5 Email Template Updates

All lifecycle email templates (Phase 2A) updated to include:
- "View in your portal" button linking to authenticated portal
- Portal login link in email footer
- Welcome email updated to include portal introduction and first login prompt

#### 14.4.6 Effort Estimate

| Component | Hours (indicative) |
|-----------|--------------------|
| Supabase Auth setup (magic links) | 4-6 |
| Login page + auth flow UI | 6-8 |
| Customer dashboard (loan summary) | 8-12 |
| Lifecycle progress view | 6-8 |
| Resource library (authenticated) | 4-6 |
| Affiliate partner directory | 4-6 |
| Row-Level Security policies | 6-8 |
| Staged rollout infrastructure | 4-6 |
| Email template updates | 2-4 |
| Security review + testing | 8-12 |
| **Total Phase 2D** | **52-76 hours** |

#### 14.4.7 Prerequisites and Decisions

- **Prerequisite:** Phase 2C (Dynamic Links) deployed - resources must exist before portal can display them
- **Prerequisite:** Privacy policy for cross-business data sharing approved (COS blocker)
- **Prerequisite:** CTO security review of auth implementation
- **Decision required:** Data display scope - exactly which fields are shown to customers? (Nathan sign-off)
- **Decision required:** Multi-brand visibility - should customers see loans from both brands in one view? (Privacy policy dependent)
- **Decision required:** Session duration and re-authentication policy

---

### 14.5 Phase 2E - Cotality Integration

**Priority:** Medium - enriches lifecycle deliverables with property valuation data
**Phased approach:** Manual first (2E-1), then API (2E-2)

#### 14.5.1 Schema

**New table: `property_valuations`**

| Column | Type | Notes |
|--------|------|-------|
| id | uuid (PK) | |
| contact_id | uuid (FK → contacts) | |
| loan_id | uuid (FK → loans, nullable) | Linked FHL loan |
| property_address | text | Full property address |
| purchase_price | decimal | Original purchase price |
| purchase_date | date | Settlement/purchase date |
| current_value | decimal | Most recent estimated value |
| valuation_date | date | Date of most recent valuation |
| equity_position | decimal | current_value - loan_balance (calculated or stored) |
| growth_rate | decimal | Percentage growth since purchase |
| growth_rate_annualised | decimal | Annualised growth rate |
| local_growth_forecast | text (nullable) | Local area growth rate/forecast narrative |
| source | enum | manual, cotality_api |
| raw_data | jsonb (nullable) | Full Cotality API response (Phase 2E-2) |
| created_at | timestamptz | |
| updated_at | timestamptz | |

#### 14.5.2 Phase 2E-1: Manual Entry

**Purpose:** Get valuation data into POLR immediately without waiting for API integration.

**Dashboard interface:**
- New contact record area: "Property Valuations"
- Add/edit valuation: property address, purchase price, purchase date, current value, valuation date
- Equity position and growth rate auto-calculated on save
- Staff manually copy-paste Cotality data from their existing subscription tool
- History view: all valuations for this contact with trend line

**Workflow:**
1. Broker runs Cotality lookup in existing subscription tool (takes ~1 minute per Rowdie)
2. Broker enters key figures into POLR dashboard
3. POLR calculates equity position and growth
4. Data feeds into lifecycle deliverables (90-Day Confidence Pack, Annual Review)

#### 14.5.3 Phase 2E-2: API Integration

**Purpose:** Automate valuation pulls at lifecycle touchpoints.

**Requirements (pending Cotality API documentation):**
- API endpoint for property valuation by address
- Authentication method and rate limits
- Data fields available (estimated value, confidence interval, comparable sales, growth rate)
- Commercial agreement and per-lookup pricing

**Automated triggers:**
- Month 3 lifecycle touchpoint: auto-pull valuation for 90-Day Confidence Pack
- Month 12 lifecycle touchpoint: auto-pull updated valuation for Annual Review
- Manual trigger: broker can request fresh valuation from dashboard

**Repricing trigger logic:**
- If equity growth exceeds threshold (configurable, default 10% annual growth), flag contact for proactive repricing conversation
- Create dashboard notification for assigned broker
- Optional: auto-trigger month 6 repricing review if equity growth is significant

#### 14.5.4 Effort Estimate

| Component | Hours (indicative) |
|-----------|--------------------|
| **Phase 2E-1 (Manual):** | |
| Schema + migrations | 2-4 |
| Manual entry UI on contact record | 6-8 |
| Equity/growth calculation logic | 2-4 |
| Integration with lifecycle deliverables | 4-6 |
| **Subtotal 2E-1** | **14-22 hours** |
| | |
| **Phase 2E-2 (API):** | |
| Cotality API integration | 8-14 |
| Automated trigger logic | 6-8 |
| Repricing threshold detection | 4-6 |
| Error handling + fallback to manual | 4-6 |
| **Subtotal 2E-2** | **22-34 hours** |
| | |
| **Total Phase 2E** | **36-56 hours** |

#### 14.5.5 Prerequisites and Decisions

- **Prerequisite (2E-1):** Phase 1 deployed with contacts table
- **Prerequisite (2E-2):** Cotality API documentation received (COS still_needed item)
- **Prerequisite (2E-2):** Commercial agreement with Cotality for API access
- **Decision required:** Cotality API pricing model - per-lookup cost affects how aggressively we auto-pull
- **Decision required:** Repricing threshold value (default 10% - confirm with Bill/Paige)
- **Note:** Phase 2E-1 can be built independently and used immediately. Phase 2E-2 is blocked until Cotality API docs are received.

---

### 14.6 Phase 2F - Additional Integrations (Backlog)

**Priority:** Low - these are future items that require external dependencies to be resolved before scoping.

#### 14.6.1 Nick/Quantum Equity Tracking App

**Status:** COS outstanding decision. Referenced in FHL lifecycle plan as affiliate partner. Integration details unknown.

**Before scoping:**
- Confirm what Quantum provides (equity tracking? property alerts? portfolio view?)
- Assess API availability and documentation
- Define integration scope (data push, data pull, or link-only?)
- Confirm commercial arrangement between Fox and Quantum

**Potential integration:**
- Push property valuation data from POLR to Quantum (or vice versa)
- Deep link from POLR customer portal to Quantum app
- Shared customer identifier for cross-platform tracking

**Do not commit development hours until API is confirmed.**

#### 14.6.2 Rowdie's Custom GPT

**Status:** Standalone tool used by Rowdie for content generation. Not core POLR functionality.

**Integration options (if desired):**
- API bridge: POLR sends customer context to GPT, receives personalised content suggestions
- Content generation: Use GPT to draft lifecycle email content, then human review in POLR
- This is an optimisation, not a core feature

**Recommendation:** Keep as standalone tool. Revisit if content generation becomes a bottleneck.

#### 14.6.3 UMI Loans System Integration

**Status:** Separate business with proprietary CTO-built system. Separate commercial discussion required.

**Considerations:**
- UMI broker-referred clients cannot be cross-sold to FFG/FHL (compliance restriction)
- Direct UMI clients can be cross-sold (when ready, via FFG/FHL)
- Integration requires CTO collaboration (Matty built the UMI system)
- Data model differences may require transformation layer

**Before scoping:**
- Nathan to confirm commercial terms for UMI integration
- CTO to provide UMI system API documentation
- Define which UMI data flows into POLR (direct clients only, or all?)
- Confirm compliance rules for broker-referred vs direct client segmentation

**Effort estimate:** Cannot estimate until API documentation and scope are defined. Likely 40-80 hours depending on system complexity.

---

### Phase 2 Summary

| Phase | Description | Hours (indicative) | Dependencies | Priority |
|-------|-------------|-------------------|--------------|----------|
| 2A | FHL Lifecycle Engine | 62-90 | Phase 1 deployed | Critical |
| 2B | Cross-Sell Pipeline Handoff | 52-72 | Phase 1 + 2A | Critical |
| 2C | Dynamic Links / Resources | 44-66 | Phase 1 | High |
| 2D | Customer Portal + Auth | 52-76 | Phase 2C + privacy policy | Medium-High |
| 2E | Cotality Integration | 36-56 | Phase 1 (2E-1) / Cotality API (2E-2) | Medium |
| 2F | Additional Integrations | TBD | External dependencies | Low |
| **Total Phase 2 (excl. 2F)** | | **246-360 hours** | | |

**Recommended build order:** 2A → 2B → 2C → 2D → 2E (with 2E-1 manual entry deployable alongside 2A)

**Key blockers to resolve before Phase 2 begins:**
1. Privacy policy for cross-business data sharing (gates 2B, 2D)
2. Cross-sell pipeline ownership model (gates 2B)
3. Client services role decision (gates 2A execution)
4. Cotality API documentation (gates 2E-2)
5. Domain/subdomain decision for public resources (gates 2C)
