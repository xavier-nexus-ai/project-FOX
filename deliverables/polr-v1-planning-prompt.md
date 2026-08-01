# POLR V1 MVP — Planning Prompt

> Copy this into the fox-vibe project and run `/plan` to enter plan mode.

---

## Context Files to Read First

Read these files from `/Projects/Clients/Fox/fox-njin/` before planning:

1. `cos.yaml` — Full client context, FHL 18-month lifecycle plan (7 touchpoints, line ~1709-1849), 5 ICA profiles, tone of voice pillars, sales process scripts, blocker list, and tech stack
2. `CLAUDE.md` — Project rules, writing standards, compliance constraints
3. `playbooks/master-playbook/tone-of-voice.md` — Brand voice guide (Clear Not Clever, Calm and Reassuring, Empowering Not Controlling)
4. `docs/branding/Fox Finance Group Branding Guide.pdf` — Visual brand guide (colours, typography, logo usage)
5. `deliverables/polr-mvp-scope-of-work-2026-02-13.md` — The full POLR MVP scope of work. This is the canonical feature spec. The V1 prototype implements a subset of this spec (see SCOPE BOUNDARIES below), but the data model, architecture, dashboard design, and automation patterns defined in this document are the blueprint.

---

## Step 0: Create the Design System

**This is the first task. Do this before writing any UI code.**

Extract the Fox Finance Group brand guide and tone of voice into a structured design system file that the AI can reference consistently throughout the build. This prevents brand drift and means every component is on-brand from the start.

### Design System Tokens (create as `design-system.ts` or equivalent)

**Colours:**
- Primary Orange: `#ED9B33` (Pantone 2011 C — R237 G155 B51)
- Primary Grey: `#63666A` (Cool Gray 10 C — R99 G102 B106)
- Secondary Gold: Pantone 120 U (C0 M42 Y89 K0)
- Secondary Black: `#101820` (Pantone Black 6 C — R16 G24 B32)
- White: `#FFFFFF`
- Semantic: Success green, Warning amber (use orange sparingly — it's the brand colour), Error red, Info blue

**Typography:**
- Primary font: **Muli** (Google Font) — use for all UI text
- Fallback: Helvetica Neue, Helvetica, sans-serif
- Weights: Regular (400), Italic, Bold (700), Bold Italic
- Scale: Define a type scale for headings (h1-h4), body, small, caption

**Spacing & Layout:**
- Define a consistent spacing scale (4px base: 4, 8, 12, 16, 24, 32, 48, 64)
- Border radius tokens (small, medium, large)
- Shadow tokens for cards and modals

**Brand Elements:**
- Logo: Fox logo with "Alex the Fox" mascot. Use sparingly — once per page/view max.
- Brand badges: FFG = orange, FHL = green (for multi-brand indicators on contacts)

**Component Patterns:**
- Cards: White background, subtle shadow, rounded corners
- Tables: Clean, readable, generous row padding
- Status indicators: Use colour-coded badges/chips (green = active, amber = pending, red = overdue, grey = inactive)
- Tags: Small rounded chips with brand colours
- CTAs: Orange primary buttons, grey secondary
- Forms: Clean inputs with clear labels, validation in real-time

**Voice in UI Copy:**
- All labels, tooltips, empty states, and notifications must follow tone of voice guide
- Australian English throughout (organisation, colour, analyse)
- No jargon — "Contacts" not "CRM Records", "Due for touchpoint" not "Scheduled automation trigger"
- Banned AI words: delve, tapestry, embark, realm, leverage, navigate, unlock, landscape, foster, robust, synergy, beacon
- Compliance: Never display "advice", "guarantee", or "financial hardship" in any template or UI copy

---

## Task

Vibe code a semi-operational POLR V1 prototype — a working MVP with **two major deliverables**:

### Deliverable 1: The FHL 18-Month Post-Settlement Nurture Sequence

This is the core product, not just a feature. The entire V1 exists to bring this nurture sequence to life. It's the "moneymaker" — the thing that prevents loan book drop-off, creates FFG cross-sell opportunities, and positions Fox as the guide who stays relevant throughout the customer's journey.

The 7 touchpoints (Month 1, 3, 6, 9, 12, 15, 18) must be:
- **Visible** — Where is every FHL customer in their 18-month journey right now?
- **Editable** — Rowdie can change the email/SMS content for any touchpoint without touching code
- **Segmented** — Different content for different ICA segments at each touchpoint (especially Month 3 Confidence Pack and Month 9 Momentum Pack)
- **Trackable** — What was sent, when, to whom, what happened next
- **Actionable** — When a touchpoint triggers, the team knows what to do (call, send pack, review pricing)

### Deliverable 2: The Platform (UI/UX)

The dashboard, contact management, journey visualisation, email tools, and team workflows that make Deliverable 1 operational. This demonstrates the platform's full capability and is what gets compared side-by-side with Xavier's GHL PoC.

This needs to be presentable at a **Thursday Apr 3 review meeting with Rowdie** to convince Nate that custom beats GHL. Xavier built a GHL PoC in parallel (~70% done) — this prototype needs to show what custom can do that GHL can't: dynamic personalisation, clean dashboarding, complex segmentation logic, and editable content.

---

## Scope Boundaries

### What V1 INCLUDES (build all of this)

The MVP scope doc (`polr-mvp-scope-of-work-2026-02-13.md`) defines the full platform. V1 implements the **core platform features** but tests them with FHL nurture data only. Specifically:

**Data Model — Build the full schema from the scope doc data model:**
- `contacts` table — unified customer record across both brands
- `loans` table — every loan linked to contact
- `contact_tags` table — custom and system-generated tags
- `cross_sell_opportunities` table — identified opportunities with routing
- `automation_events` table — every automated touchpoint sent
- `lead_market_contacts` table — leads sold to market, tracked for reactivation
- `activity_log` table — audit trail
- Email marketing tables: `email_templates`, `email_campaigns`, `email_campaign_stats`, `audience_segments`, `automation_content`
- Database views: `contact_brand_membership`, `cross_sell_pool`, `email_audience_segments`

> Build the FULL data model. Don't cut tables just because V1 only tests FHL nurture. The schema should support the complete vision — we just populate it with FHL test data.

**Contact Management — Full CRUD:**
- View, create, edit, delete contacts
- Contact detail view showing: loans, tags, lifecycle stage, automation history, cross-sell opportunities, brand membership badges
- Contact list with filtering (brand, stage, tags, loan type, housing status, employment type)
- Bulk tag operations (select multiple, add/remove tags)
- Tag management page (view all tags, usage counts, autocomplete)
- Multi-brand overlap indicators (coloured badges: FFG blue, FHL green)

**Journey Visualisation:**
- Visual representation of where each contact sits in the FHL 18-month lifecycle
- Stage progression view (Stage 0-4 counts with drill-down to contact list)
- Timeline view per contact showing touchpoints completed/upcoming
- Highlight contacts approaching stage transitions

**Team Dashboard:**
- Top bar: logged-in user, brand filter (FFG / FHL / All), date range
- 4 summary cards: Active Cross-Sell Opportunities, Customers Due for Touchpoint This Week, Lead Market Reactivations Ready, Care Calls Due This Week
- Tab 1: Cross-Sell Pipeline (table sorted by score, expand for detail, assign/contact/convert/decline actions)
- Tab 2: Lifecycle + Automation (stage counts, automation event log, delivery rates)
- Tab 3: Lead Market (reactivation status counts)
- Tab 4: Care Call List (prioritised weekly list, log outcomes inline)
- Tab 5: Email Marketing (campaign list, audience builder, saved segments, nurture sequence editor)

**Nurture Sequence Content Editor:**
- List all 7 FHL touchpoints as editable workflow steps
- Edit subject line, body content, SMS text for each step
- Preview with merge fields populated from sample contact
- Changes stored in `automation_content` table
- Version history / last-edited timestamp

**Email Management:**
- Template editor (edit content within pre-designed templates, merge fields, basic formatting, preview)
- Bulk email blast interface (audience builder with filters, template selector, schedule or send, confirmation step)
- Saved audience segments (dynamic, re-evaluate at send time)

**Automations — Structure all 8 from the scope doc automation list:**
- Post-Settlement Welcome (FFG) — Day 0/3/7 sequence
- Post-Settlement Welcome (FHL) — Day 0/3/7/30 sequence
- Taylor Lifecycle Stage Transitions — daily cron, stage 0-4 logic
- FFG-to-FHL Cross-Sell Detection — weekly cron, scoring
- FHL-to-FFG Cross-Sell Detection — monthly cron
- Home Loans Value-Add Cycle — the 7 FHL touchpoints (Month 1/3/6/9/12/15/18)
- Lead Market Reactivation — daily cron, SMS + email sequence
- Customer Care Call List Generator — weekly cron, scoring

> For V1 demo: automation **structures and UI** must be functional. Actual sending (SendGrid/Twilio) can be mocked — show the logic, scheduling, and content editing, not live email delivery.

**Hard Business Rules — enforce in code:**
- FHL clawback awareness (no refinance suggestions before clawback_end_date)
- Lead market cooling period (3 months from sold_date)
- Compliance language filter (no "advice", "guarantee", "financial hardship")
- SMS opt-out tracking
- Human-led cross-sell (opportunities route to broker, no automated cross-sell emails)

### What V1 EXCLUDES (Phase 2+)

- FFG cross-sell content and logic (structure exists in schema, but no FFG-specific content or journeys populated)
- UMI Loans integration
- Referral partner management/portal
- Customer-facing portal with authentication
- Drag-and-drop email builder (V1 has content-only editor within fixed templates)
- Cotality property valuation API integration (use placeholder values)
- Live SendGrid/Twilio integration (mock sending, show the UI and logic)
- Ambition API integration (use CSV import or manual entry for demo)
- AI voice calling, chatbot, conversational AI

### Test Data Strategy

- Use the dummy application from Rowdie (`docs/updated-docs/Application-5445-20260325-054307.pdf`) as the reference for realistic FHL contact data
- Generate 20-30 sample contacts across the 5 ICA segments with varied lifecycle stages
- Include at least 2-3 multi-brand contacts (FFG + FHL) to demonstrate cross-sell detection
- Include lead market contacts at various reactivation stages
- Populate automation_content with the 7 FHL touchpoint content from cos.yaml (line ~1728-1849)

---

## Technical Stack

| Component | Technology |
|-----------|-----------|
| Database + Auth + API | Supabase (PostgreSQL) |
| Front-end | Next.js 14+ (App Router) |
| Automation engine | Next.js Edge Functions (mocked for demo) |
| Email | SendGrid (mocked — UI only for V1 demo) |
| SMS | Twilio (mocked — UI only for V1 demo) |
| Hosting | Vercel |

---

## Demo Flow for Thursday

The prototype needs to tell a story. Rowdie and Nate should see:

1. **Dashboard overview** — Summary cards showing live counts. "Here's your business at a glance."
2. **Contact deep dive** — Click into a contact, see their full profile, loans, tags, lifecycle stage, timeline of touchpoints. "This is what GHL can't show you."
3. **Journey visualisation** — Where every FHL customer sits in the 18-month lifecycle. Stage progression. Who's due for Month 6 repricing review this week.
4. **Nurture content editor** — Show how Rowdie can edit the Month 3 Confidence Pack email without touching code. Preview with real merge fields.
5. **Cross-sell detection** — Show a contact flagged for FFG cross-sell at Month 9 (the Momentum Pack). Explain how the scoring works.
6. **Care call list** — Weekly prioritised list with suggested talking points. Log a call outcome.
7. **Email marketing** — Build an audience segment (e.g., "FHL customers past Month 6, variable rate"), preview count, show how a campaign would work.
8. **The closer** — Side-by-side with Xavier's GHL PoC. "GHL can send emails on a timer. POLR knows which customer needs what, when, and why — and lets your team control the content."

---

## FHL 18-Month Touchpoints (Quick Reference)

| Month | Name | Key Deliverable |
|-------|------|----------------|
| 1 | Welcome + Setup Verified | Phone call + email/SMS, loan setup snapshot |
| 3 | 90-Day Confidence Pack | 1-page PDF: Property Position and Loan Health (segmented by customer type) |
| 6 | Proactive Pricing Review | Repricing review results, one-pager |
| 9 | FFG Momentum Pack | Segmented pack by ICA (New Home / FHB / Investor / Refi / Equity Release) |
| 12 | Annual Property and Loan Strategy Review | 2-page annual review |
| 15 | Refinance Pathway | 1-page Options Map (pay down / invest / refinance) |
| 18 | Action Window | Triggered only when relevant (fixed expiry, market move, goal change) |

---

## 5 ICA Segments (for test data)

1. **Young Practical Motor Borrower** → FHL: First Home Buyer
2. **Established Personal Finance Borrower** → FHL: New Purchase, Refinance
3. **Prime Convenience-Led Repeat Borrower** → FHL: New Purchase, Refinance, Investor
4. **Business Asset Borrower** → FHL: Commercial
5. **Prime Vehicle Borrower** → FHL: New Purchase, Refinance, Investor

---

## Tone of Voice (for all UI copy and sample content)

- **Clear Not Clever** — No jargon, no acronyms, no industry-speak in customer-facing content
- **Calm and Reassuring** — "You're on track. We checked, here's what we found."
- **Empowering Not Controlling** — Customer is the hero, Fox is the guide (StoryBrand)
- **Compliance** — Never use "advice", "guarantee", or "financial hardship"
- **Australian English** — organisation, colour, analyse

---

## Time Budget

4-5 hours. Plan for a working demo, not perfection. Prioritise in this order:

1. **Design system** (must be first — every component depends on it)
2. **FHL 18-month nurture sequence** (the core product — journey visualisation, touchpoint timeline, content editor, segmentation by ICA). This is the "moneymaker" and the centrepiece of Thursday's demo.
3. **Contact management** (full CRUD, filtering, detail view with journey context)
4. **Dashboard** (summary cards, tabs, the "at a glance" view)
5. **Seed data** (realistic FHL contacts across 5 ICAs, at varied lifecycle stages, with automation history)
6. **Email marketing module** (functional but can be lighter)
7. **Remaining automations** (structure visible, actual execution mocked)

---

## Output Expected from Planning

1. Design system file (tokens, components, patterns)
2. File structure and component list
3. Supabase schema (SQL migration file)
4. Seed data script (realistic FHL contacts across 5 ICAs)
5. Component breakdown with priority order
6. Demo walkthrough script for Thursday's meeting
7. What's functional vs mocked — be explicit
