# Fox Provider Access Audit

**Date:** 05/05/2026
**Owner at Fox:** Rowdie Lang (primary). Nathan Drew for compliance and lead market.
**Scope:** FFG and FHL only. UMI is out of scope. Not included in any access ask.
**Purpose:** Work out what we have, what we still need, and what each provider must give us before the GHL playbook build kicks off.

---

## 1. Data Feeds (High-Level Enrichment into GHL)

These feed customer and loan data into GHL. Used for cross-sell triggers, lifecycle nurture, and segmentation.

| # | Provider | Side | What we know | What we need |
|---|---|---|---|---|
| 1 | **Ambition** (aggregator) | FFG side | Has API. 3CX phone integrated. Email templates live. | API key and docs. Sample contact and loan export. Webhook check. Owner contact at Ambition. |
| 2 | **Infynity** (aggregator) | FHL side | NO API per discovery. LMG switch was being looked at (Mar 28). Blocker for FHL data flow. | Confirm: did the LMG switch happen? If no, agreed CSV or PDF export cadence (weekly?). Who owns the export? Sample file. |
| 3 | **Cotality** | FHL | Property valuation tool. Subscription paid. 1-minute valuation turnaround. | API credentials. Rate limits. Sample call. Account owner at Fox. |
| 4 | **TypeForm** | Both | 5+ forms with conditional logic. 70% completion rate. Zapier routes leads. | Account access (or service-account API key). List of all live forms and which side they feed. Map of current Zapier flows. |

---

## 2. Direct Access (We Set It Up)

Give us access. We configure inside the platform.

| # | Provider | What we know | What we need |
|---|---|---|---|
| 5 | **Zapier** | Current automation layer. Stays as Zapier. | Account access. Full Zap inventory. |
| 6 | **Google Ads** | $1,500/month FFG. UMI spend out of scope. | MCC access for Njin. Conversion tracking audit. |
| 7 | **Facebook Ads** | Minimal retargeting. | Business Manager access. Pixel audit. |
| 8 | **GA4** | Live. | View access plus property IDs for FFG and FHL sites. |
| 9 | **SendGrid** | We believe Njin already has access. | Verify access. Domain auth (SPF, DKIM, DMARC). Template list. Decision: keep as send layer, or move sends to GHL? |

---

## 3. Audit Only (No Access Needed Now)

| # | Provider | What we need |
|---|---|---|
| 10 | **Gravity Forms** | List of which forms are in use, on which sites, and what each one feeds. No admin access. |
| 11 | **3CX** | Look into GHL integration options for future scoping. Not urgent. |
| 12 | **Lead Market Platform** | Identify which platform it is. Pull API docs to see if there's an automation play. Low priority. |

---

## 4. Not Required

| Provider | Reason |
|---|---|
| UMI proprietary system | Out of scope. |
| Looker Studio | GHL reporting replaces it. |
| Calendly | GHL Calendars replaces it. |
| Microsoft 365 / Teams | Fox internal team handles this. Njin gives them the config (e.g. email sender domain), Fox sets it up. |

---

## 5. Plus, Non-Tech Access

- GHL sub-account: confirm Njin admin, Rowdie admin, Nathan admin
- Email send domain: which domain for cross-sell sends? (foxfinance.com.au? foxhomeloans.com.au? foxgroup.com.au?)
- Test phone numbers for SMS testing (Twilio)
- Compliance sign-off contact: who at Fox approves financial messaging?
- Brand assets: logos, colours, fonts for FFG and FHL in editable format
- Customer data export: one-time historical export from Ambition and Infynity to seed GHL

---

## Owner Routing

| Hand to | Items |
|---|---|
| **Rowdie Lang** | 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11. Plus all non-tech access items. |
| **Nathan Drew** | 12 (Lead Market). Compliance sign-off contact. |

---

## Next Step

Send this list to Rowdie and Nathan. Track each row to closure in `cos.yaml` `data_access`. Re-run readiness check once the first two access groups are confirmed.
