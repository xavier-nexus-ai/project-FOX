# Scoping Guide: Njin Method Client

Use this guide when running discovery and scoping for a Njin Method (playbook-based) engagement.

---

## Required Documents (Before Scoping Starts)

- [ ] Signed contract
- [ ] Approved reverse brief / scope of work
- [ ] Sales call transcripts
- [ ] Proposal PDF

---

## The Core 12 Numbers (MUST collect all)

These form the baseline. Scoping cannot proceed without them — `status: "unknown"` is acceptable for individual values, but every field must be explicitly asked.

### Revenue & Growth
1. **Revenue (last 12 months)** — $___
2. **Revenue (prior 12 months)** — $___

### Acquisition
3. **Leads per month** — ___
4. **Cost per lead** — $___

### Conversion
5. **Lead > Appointment rate** — ___%
6. **Show rate** — ___%
7. **Close rate** — ___%
8. **Average deal size** — $___

### Monetisation & Retention
9. **MRR or contract length** — $___ / ___ months
10. **Churn rate or customer lifespan** — ___% / ___ months
11. **Customer LTV** — $___
12. **CAC** — $___

---

## The 4 Critical Qualitative Questions

Ask these verbatim — the wording is deliberate:

1. **"Where do you think you're leaking the most money right now?"**
2. **"What's your 12-month revenue goal?"**
3. **"What's your next revenue milestone?"** (and by when?)
4. **"If we could fix ONE thing in the next 90 days, what would you want it to be?"**

Log all answers in the COS under `qualitative_answers`.

---

## Constraint Diagnosis (Do This Before Picking a Playbook)

Based on the Core 12, diagnose:

- **Primary constraint:** Acquisition / Conversion / Monetisation / Retention
- **Secondary constraint:** What becomes the next bottleneck after the primary is fixed
- **Rationale:** Why this diagnosis, based on the Core 12 data
- **Ninety-day priority:** From qualitative question 4

**Playbook type should match the primary constraint:**

| Constraint | Recommended Playbook |
|------------|---------------------|
| Acquisition (low lead flow) | Outreach or Ads |
| Acquisition (lead flow OK but unqualified) | Pre-Sales |
| Conversion | Sales |
| Monetisation (low ARPU) | Cross-Sell |
| Monetisation (no referrals) | Referral |
| Retention | Retention |

---

## Tech & Access Requirements

- [ ] **CRM platform:** ___ (GHL, HubSpot, Pipedrive, Salesforce, custom?)
- [ ] **CRM admin access:** granted / pending
- [ ] **Office suite:** Google Workspace / Microsoft 365 / other
- [ ] **Communication tools:** Slack / Teams / other
- [ ] **Automation tools:** Zapier / n8n / Make / other
- [ ] **AI tools in use:** ChatGPT / Claude / Gemini / other
- [ ] **Industry-specific platforms:** ___

## Client Owner Map

- [ ] **CRM admin:** ___
- [ ] **Implementation approvals:** ___ (who signs off on playbook?)
- [ ] **Main point of contact:** ___
- [ ] **Subject matter expert for interviews:** ___

---

## Playbook-Specific Data (Collect Based on Playbook Type)

### Outreach playbook
- [ ] Current outbound channels used
- [ ] Cold email platform
- [ ] LinkedIn outreach tools
- [ ] Existing outreach copy / scripts

### Ads playbook
- [ ] Current ad platforms (Google / Meta / LinkedIn / TikTok / YouTube)
- [ ] Monthly ad spend
- [ ] Existing ad accounts access
- [ ] Current landing pages / funnels
- [ ] Analytics access

### Pre-Sales playbook
- [ ] Current SDR process (if any)
- [ ] Lead scoring criteria
- [ ] Existing nurture sequences
- [ ] Speed-to-lead metrics

### Sales playbook
- [ ] Current sales process
- [ ] Existing sales scripts
- [ ] Call recording access
- [ ] Deal stages in CRM

### Cross-Sell playbook
- [ ] Product catalogue
- [ ] Customer segmentation data
- [ ] Existing upsell/cross-sell touchpoints

### Referral playbook
- [ ] Current referral process
- [ ] Existing referral incentives
- [ ] Customer advocacy history

### Retention playbook
- [ ] Churn data by segment
- [ ] Customer success process
- [ ] Onboarding process
- [ ] Support tickets / feedback data

---

## Nice-to-Have Materials (Chase but don't block)

- [ ] Brand guidelines or style guide
- [ ] Current sales scripts (any format)
- [ ] Case studies / testimonials
- [ ] Product documentation
- [ ] Competitor research
- [ ] Sales call recordings
- [ ] Marketing materials (ads, landing pages, emails)
- [ ] Pricing sheets and proposal templates

---

## Tone of Voice Data Collection

Required for ToV gate:
- [ ] Website copy
- [ ] Email sequences
- [ ] Sales call recordings or transcripts
- [ ] Social media posts
- [ ] Marketing materials

---

## Earliest Possible Win

**Critical:** Every Njin Method engagement must identify an "Earliest Possible Win" that gets delivered at the kickoff call. Ask:

- What would be the simplest, fastest thing we could deliver in week 1 that the client could immediately use or show to someone?

Document the answer in the scope document under "Earliest Possible Win".

---

## Discovery Gaps Template

After gathering everything, produce a gap list:

```markdown
## Gaps Identified

### Hard Blockers (cannot proceed without)
- [ ] Item — requested by [date]

### Nice-to-Haves (proceed with caveat)
- [ ] Item — will chase in parallel
```

---

## 5 Business Day Escalation Rule

If any hard blocker access is delayed beyond 5 business days:
1. Escalate to client point of contact
2. Document blocker in COS
3. Set new deadline
4. Flag to James if it persists

---

**Source:** `docs/background/playbook-creation-sop.md` (Phase 1: Client Onboarding & Data Collection), `docs/ip-vault/sops/sop-003-discovery-procedure.md`.
