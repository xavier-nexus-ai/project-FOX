# ICA Field Privacy + Value Filter

**Date:** 05/05/2026
**Source:** Rowdie Lang's ICA Field Audit, sent 27/04/2026 (email "RE: Confirming Monday's Meeting And Points To Cover").
**Owner:** James + Xavier draft. Rowdie sign-off.
**Status:** Blocking GHL migration.

---

## The Rule

For each field Rowdie supplied, ask:

> Does this field drive ICA routing, segmentation, behavioural branching, or content personalisation in the playbook?

- **YES** = keep. Migrate into GHL as a custom field or tag.
- **DROP** = leave behind. No operational value, or sensitive PII that creates compliance risk without proportional payoff.
- **TRANSFORM** = keep the signal, drop the raw data. (e.g. DOB stored as age band only.)

---

## Field-by-Field Recommendation

| # | Field | Njin recommendation | Reason |
|---|---|---|---|
| 1 | Broker | **KEEP** | Routes broker handoff workflow. Personalisation token in emails. |
| 2 | App Type (Consumer / Commercial) | **KEEP** | Top-level ICA split. Drives BAB routing. |
| 3 | Loan Type | **KEEP** | Core ICA classifier (Personal vs Motor vs Chattel Mortgage). |
| 4 | Lender | **KEEP** | Needed for repricing and refinance conversations. |
| 5 | Loan Tier (A / B / C) | **KEEP** | Credit-profile proxy. Drives PCLRB vs YPMB split. |
| 6 | Loan Rate | **KEEP** | Drives rate-review trigger and repricing logic. |
| 7 | Term | **KEEP** | Lifecycle timing. End-of-term return-loan signal. |
| 8 | Amount Financed | **KEEP** | Loan size segmentation. BAB high-value tagging. |
| 9 | Gender | **DROP** | No operational use. Privacy risk. Modern CRMs avoid this field. |
| 10 | Marital Status | **KEEP** | Routes ICA (PCLRB more often married/de facto). Life-stage messaging. |
| 11 | Dependents | **TRANSFORM** | Keep as boolean ("has dependents Y/N") not the count. Useful for life-stage messaging. Drop the raw count. |
| 12 | Business Name | **KEEP** | BAB ICA personalisation. EOFY messaging. |
| 13 | Asset Type | **KEEP** | Routing (car / equipment / trailer). |
| 14 | Asset Year | **KEEP** | Replacement cycle trigger (5-7 year vehicle replacement). |
| 15 | Asset Make | **KEEP** | Personalisation token. Could be useful for replacement messaging. |
| 16 | Asset Model | **KEEP** | Personalisation token. |
| 17 | Lead Source | **KEEP** | Attribution. Reactivation segmentation. |
| 18 | Referrer | **KEEP** | Referral partner tracking + thank-you triggers. |
| 19 | Applicant Phone | **KEEP** | Operational. SMS workflow. |
| 20 | Applicant Email | **KEEP** | Operational. Email workflow. |
| 21 | Applicant DOB | **TRANSFORM** | Convert to age band on import (Under 30 / 30-39 / 40-49 / 50-59 / 60+). Drop raw DOB. Age band drives ICA routing; full DOB does not. |
| 22 | Employment Type | **KEEP** | Routes BAB (self-employed) vs consumer ICAs. |
| 23 | Residential Status | **KEEP** | ICA marker. FHL pathway gate (renter vs mortgaged). |
| 24 | Asset Backed (Y/N) | **KEEP** | BAB indicator. Cross-sell signal. |
| 25 | Investment Property (Y/N) | **KEEP** | FHL Investor pathway trigger. |
| 26 | Mortgage Balance | **TRANSFORM** | Keep as banded estimate (e.g. <$300K, $300K-$600K, $600K+) for refinance trigger logic. Drop the exact balance. |
| 27 | Credit Cards (Y/N or count) | **KEEP** if just count or boolean. **DROP** if card numbers. | Useful for credit profile. Card numbers are never needed. Confirm Rowdie's intent. |
| 28 | Credit Cards Balance | **DROP** | Sensitive. Limited operational value. Snapshot ages fast. |
| 29 | Credit Card Limits | **DROP** | Sensitive. Limited operational value. Snapshot ages fast. |
| 30 | Personal Loans (Y/N or count) | **KEEP** | EPFB ICA marker. |
| 31 | Personal Loans Balance | **DROP** | Sensitive. Limited operational value. Snapshot ages fast. |
| 32 | Remittance Date | **KEEP** | Settlement anchor. Drives every workflow timer (Day 3, 90, 180, 270, 365). |

---

## Summary

| Decision | Count |
|---|---|
| KEEP | 23 |
| TRANSFORM | 4 (Dependents, DOB, Mortgage Balance, Credit Cards if just count) |
| DROP | 5 (Gender, Credit Cards Balance, Credit Card Limits, Personal Loans Balance, plus the raw versions of the four transformed fields) |

---

## Why we're dropping the financial-snapshot fields

Credit card balances, credit card limits, and personal loan balances are **point-in-time snapshots**. By Month 3 of the journey they are stale. By Month 9 they are wrong. We do not need them for routing or messaging, and storing them in GHL creates real privacy risk for limited reward.

If Fox wants live financial-position data for a customer (e.g. to trigger a refinance offer), it should be pulled fresh from the lender or credit-bureau API at the moment of the conversation, not stored in CRM.

---

## Why we're transforming DOB and Mortgage Balance

- **DOB → age band.** ICA routing only needs the band. Storing exact DOB without need is a low-value privacy risk.
- **Mortgage balance → band.** FHL refinance trigger only needs to know "above the LMI threshold yes/no" or "high enough loan to make refinance worthwhile yes/no." A banded value answers that. Exact balance does not add anything we use.

These transformations happen at the import layer (Ambition CSV → GHL or Infynity CSV → GHL). Raw values never land in GHL.

---

## Open Questions for Rowdie

1. **Field 27 "Credit Cards"** — is this a yes/no flag, a count, or full card numbers? If full card numbers, we never store these in GHL.
2. **Sensitive raw values** — confirm Fox is comfortable with the snapshot fields being dropped. If there is a use case we missed, raise it now.
3. **Age band vs DOB** — confirm the routing decision can be made on age bands alone (it can, per the 5-ICA framework, but Rowdie owns the call).

---

## Next Step

1. James + Xavier review this draft (today).
2. Send to Rowdie for sign-off.
3. Once locked, the field list becomes the GHL custom field schema. Build can start.
