# Fox Finance Group — POLR Compliance Annotations
**Prepared by:** Domain Expert (Dr. Evelyn Reed)
**Date:** 2026-03-23
**Version:** 1.0
**For:** Retention Specialist (lifecycle matrix build) + HTML tool compliance warning layer

---

## Important Disclaimer

This document provides domain-level compliance guidance based on Australian financial services regulation as of the knowledge cutoff (August 2025). It references specific legislation and ASIC regulatory guidance but is **not legal advice**. Fox Finance Group must have a qualified compliance lawyer or their ACL licensee compliance team review and approve all communications, data practices, and lifecycle messaging before implementation. Where UMI Loans is involved (direct lender), additional review through UMI's credit licence obligations is required.

---

## How to Use This Document

This document is structured across four tasks:

1. **Non-Client Communications** — What Fox can send to people who have never applied
2. **Unified Database Privacy** — What sharing customer data between FFG and FHL requires
3. **Reactivation Compliance** — How to re-engage 49,000 declined leads legally
4. **Lifecycle Stage Annotations** — Stage-by-stage compliance notes for the HTML tool

The Retention Specialist should use Task 4 annotations directly in the lifecycle matrix. The HTML tool should surface the relevant annotation as a tooltip or warning panel against each stage.

**Framing principle:** POLR's proactive lifecycle management — particularly repricing advocacy and cross-sell education — already exceeds what most brokers do for duty-of-care. Compliance here is a differentiator, not a constraint. Fox can and should position POLR as the responsible choice precisely because it does what most brokers won't.

---

## Task 1: Non-Client Communications Compliance

### Context

POLR wants to communicate with people who have not applied for a financial product with Fox. This includes:
- People who signed up to POLR directly for free tools or education
- Content leads (blog subscribers, social follows who gave an email)
- Referral leads before formal enquiry

This is one of the highest-compliance-risk areas in the POLR model. Getting it right unlocks 49,000+ leads per year. Getting it wrong risks ASIC enforcement and Spam Act penalties.

---

### 1.1 Can Fox Send Marketing Communications to Non-Clients?

**Answer: Yes, with consent and proper disclosure.**

There is no blanket prohibition on contacting non-clients. The key is consent and content classification. Australian law distinguishes between:

- **Commercial electronic messages** (regulated by the Spam Act 2003)
- **Financial product advice** (regulated by the Corporations Act 2001 and ASIC)
- **Credit assistance** (regulated by the National Consumer Credit Protection Act 2009, "NCCP Act")

Non-client communications from POLR are legal provided:

1. Consent has been obtained at sign-up (express or inferred)
2. Content stays within "general information" rather than personal advice
3. Messages include required identifiers and unsubscribe mechanisms
4. Fox's ACL or credit licence details are disclosed when the content relates to credit products

**Practical implication:** The POLR sign-up flow must include a clear consent tick-box (not pre-ticked) stating that the person agrees to receive educational content and updates from Fox Finance Group and its related brands. This is the single most important gate.

---

### 1.2 Spam Act 2003 Requirements

The Spam Act 2003 (Cth) applies to all commercial electronic messages sent to Australian addresses. A commercial electronic message is broadly defined — if it offers, advertises, or promotes a financial service, it is commercial.

**Three rules Fox must follow:**

**Rule 1 — Consent**
Express consent is required unless the message can rely on inferred consent. Inferred consent applies only when:
- The person has a business or other relationship with the sender, and
- The address was published (not provided privately), and
- There is no opt-out instruction

For POLR non-clients who signed up for tools/education, **express consent is safest and recommended**. Obtain it at registration. It does not need to be complex — a single checkbox with plain language works.

**Rule 2 — Accurate Sender Identification**
Every commercial electronic message must clearly identify who is sending it. For POLR communications, this means the message must state which Fox entity is responsible (e.g., "This message is sent by Fox Finance Group Pty Ltd, Australian Credit Licence [number]"). POLR as a brand can appear as the sender name, but the underlying legal entity must be disclosed.

**Rule 3 — Functional Unsubscribe**
Every commercial electronic message must include a functional unsubscribe mechanism that works for at least 30 days after the message is sent. Unsubscribe requests must be actioned within 5 business days. POLR's N8N/SendGrid stack must implement this at the platform level, not per-campaign.

**Penalties:** Up to $2.22 million per day for body corporates who breach the Spam Act. This is not a theoretical risk.

---

### 1.3 ASIC Responsible Lending — Does It Apply to POLR Education Content?

**Short answer: ASIC's responsible lending obligations under the NCCP Act do not apply to general education content. They apply when Fox provides credit assistance.**

The distinction matters:

| Content Type | Regulated? | Example |
|---|---|---|
| General information about how home loans work | No | "Here is how LVR affects your borrowing capacity" |
| General information about Fox's services | No | "FHL helps Australians find competitive home loans" |
| Recommendation to refinance to a specific product | Yes — credit assistance | "Based on your loan, you should switch to X lender" |
| Assessment that a consumer can afford a specific loan | Yes — responsible lending | Any specific serviceability assessment |

POLR's educational content — calculators, market data, Cotality valuations, general finance literacy — sits clearly in the unregulated zone provided it does not tip into making specific product recommendations for individual circumstances.

**The line Fox must not cross:** Sending a message that says "Based on what we know about your loan, you should refinance now" is credit assistance under s.8 of the NCCP Act. Sending a message that says "Interest rates have moved — now could be a good time to review your mortgage" is general information.

This distinction is the single most important editorial rule for lifecycle content across all stages.

---

### 1.4 Can Fox Use the Term "Free Property Valuation"?

**Answer: With care, and with the right disclosure.**

Cotality (formerly CoreLogic) provides Automated Valuation Model (AVM) estimates. These are algorithmic, not formal bank valuations or licensed property appraisals.

Using the phrase "free property valuation" without qualification is potentially misleading under:
- Australian Consumer Law (ACL), s.18 — misleading or deceptive conduct
- ASIC's guidance on comparisons and representations in financial services

**What Fox can say:**
- "Free property estimate"
- "Free automated property report powered by Cotality"
- "See your estimated property value — updated monthly using Cotality data"

**What Fox should avoid:**
- "Free valuation" without qualification (implies a formal licensed valuation)
- Any implication that the Cotality figure will be accepted by a lender
- Using the Cotality figure in a way that implies it replaces a bank's formal valuation

**Required disclosure on any Cotality output:**
> "This estimate is generated using automated valuation methodology (AVM) data provided by Cotality and is intended as a general guide only. It is not a formal property valuation, a licensed appraisal, or a substitute for a lender's assessment. Actual property values may differ."

Check Cotality's data licence agreement — their terms typically restrict how AVM data can be presented and may require specific attribution. Fox's CTO/Matty should review the API agreement before POLR displays Cotality outputs.

---

### 1.5 Disclaimers on POLR Content That Discusses Lending Products

Every piece of POLR content that discusses lending, mortgages, vehicle finance, or credit products must carry a footer disclaimer. The exact wording should be reviewed by Fox's compliance team, but the required elements are:

1. **Credit licence disclosure:** "Fox Finance Group Pty Ltd holds Australian Credit Licence [ACL number]. Fox Home Loans operates under [Connective aggregator ACL or own ACL — confirm]. UMI Loans Pty Ltd holds Australian Credit Licence [UMI ACL number]."
2. **General information statement:** "The information in this communication is general in nature and does not constitute financial advice, credit advice, or a credit assistance recommendation. It does not take into account your personal circumstances, financial situation, needs, or objectives."
3. **Seek professional advice note:** "Before making any financial decision, you should consider whether the information is appropriate for your needs and seek independent professional advice if required."

This footer should appear on:
- All POLR emails
- All POLR portal pages that reference financial products
- All downloadable content (guides, reports)
- Any SMS that contains a link to financial content

---

### 1.6 General Information vs Financial Product Advice — NCCP Act Distinction

Under the NCCP Act and the Corporations Act 2001 (for financial products), there are two relevant regimes:

**Credit assistance (NCCP Act):** Fox is already licensed to provide credit assistance (help people obtain credit, arrange credit, suggest credit products). This requires a credit licence. General information about credit products does not constitute credit assistance.

**Financial product advice (Corporations Act, managed under ASIC RG 244 and related):** For products like home loans (which are credit products not financial products under the Corporations Act), the relevant framework is the NCCP Act. For insurance products, investments, and superannuation, the Corporations Act applies separately.

**The practical distinction for POLR content:**

| Communication | Classification | Risk |
|---|---|---|
| "Here is how offset accounts work" | General information | Low |
| "Your loan is eligible for a rate review" | Marketing/general information | Low-medium |
| "We recommend you refinance to lender X at Y rate" | Credit assistance / specific recommendation | High — requires full NCCP process |
| "Based on your income of $X and loan of $Y, you can borrow $Z more" | Credit assistance with serviceability assessment | High — must not be automated without full NCCP compliance |

POLR content writers must be briefed on this distinction before any content goes live. A simple editorial test: "Does this message tell a specific person to do a specific thing with a specific product?" If yes, it needs compliance review. If no, it is likely general information.

---

## Task 2: Unified Customer Database — Privacy Compliance

### Context

POLR creates a single customer record visible across FFG and FHL. Personal information collected during an FFG asset finance application (income, employment, assets) may inform FHL cross-sell targeting. Data flows both ways.

---

### 2.1 Can Fox Share Personal Information Between FFG and FHL?

**Answer: Yes, within the same group, but only if the Privacy Policy discloses this at collection.**

Under the Privacy Act 1988 (Cth) and the Australian Privacy Principles (APPs), Fox can share personal information between related entities provided:

1. **The primary purpose of collection allows it** — APP 6 permits use and disclosure for the primary purpose of collection. If a person applies for asset finance with FFG, the primary purpose is assessing and arranging that finance.
2. **A secondary purpose is permitted if it is related to the primary purpose AND the person would reasonably expect it** — APP 6.2(a). Cross-selling home loans to a person who just got a car loan is arguably a related secondary purpose, but only if it is disclosed.
3. **The Privacy Collection Notice (APP 5) discloses the sharing** — This is the key gate. If Fox tells people at the point of collection that their information may be shared with related Fox entities for the purpose of providing other financial services, consent is covered under the collection notice.

**What this means in practice:** Every Fox intake form, application form, and POLR sign-up must include an APP 5-compliant collection notice that explicitly names Fox Finance Group, Fox Home Loans, and UMI Loans as related entities who may receive the information, and states the purposes for which it will be used (including cross-sell).

**What Fox cannot do:** Use personal information collected for an FFG loan application to market completely unrelated products, or share it with third parties outside the group without separate consent.

---

### 2.2 What Consent or Notification Is Required at Collection (APP 5)?

APP 5 requires that at or before the time of collection (or as soon as practicable after), Fox must take reasonable steps to notify the individual of:

1. Fox's identity and contact details
2. The fact that they are collecting the information and why
3. The main consequences if the information is not collected
4. Any other person or body, or type of person or body, to whom the information is usually disclosed
5. Whether the information is likely to be disclosed overseas (and which countries)
6. That the Privacy Policy contains further information and how to access it

**For POLR specifically:** The POLR sign-up screen must include an APP 5 collection notice. A short-form version can appear on the screen with a link to the full Privacy Policy. The short-form must at minimum cover points 1, 2, and 4 above.

**Action required:** Fox needs a group-level Privacy Policy that names all three entities and describes the unified data model. A single policy covering the Fox Group (FFG + FHL + UMI + POLR) is the cleanest approach, provided the policy clearly explains each entity's role.

---

### 2.3 Group Consent — Can One Consent Cover All Three Entities?

**Answer: Yes, if drafted correctly.**

A single group consent is valid under Australian privacy law provided:

- The consent is informed (person understands which entities are involved)
- The consent is voluntary (they can proceed without consenting to cross-entity use, even if that limits functionality)
- The consent is specific enough that the person knows what they are agreeing to
- The entities are named or clearly described

Fox should structure consent in two layers:

**Layer 1 — Functional consent (required for POLR to operate):**
"By creating a POLR account, your personal information will be held by Fox Finance Group Pty Ltd and may be accessed by Fox Home Loans and UMI Loans for the purposes of managing your customer profile and providing you with financial services."

**Layer 2 — Marketing consent (optional, separate tick-box):**
"I agree to receive information about products and services from Fox Finance Group, Fox Home Loans, and UMI Loans."

Separating functional and marketing consent is best practice and reduces regulatory exposure. Do not bundle marketing consent into the terms of service or make it a condition of accessing POLR tools.

---

### 2.4 Non-Client Data — What Can POLR Collect and Use?

For people who sign up to POLR without any loan application, Fox can collect:

- Name, email, phone (with consent)
- Self-reported financial goals and property interests (with consent)
- Behavioural engagement data within the platform (logged-in activity)
- Cotality property data where the person requests it

Fox **cannot** collect or use:

- Credit information (credit score, repayment history, defaults) from credit reporting bodies without a permissible purpose under the Privacy Act Part IIIA
- Income and employment data without a specific reason tied to a financial services purpose the person has initiated
- Data inferred from external sources (e.g., third-party data enrichment) without disclosure

**Key restriction:** Part IIIA of the Privacy Act governs credit-related personal information and is stricter than the general APPs. Credit reporting bodies can only provide credit information to credit providers and certain other specified entities. Fox (as a credit assistance provider) has limited access to Comprehensive Credit Reporting data and only in connection with a credit application the person has initiated.

**Implication for POLR:** POLR cannot run a background credit check on a non-client to determine their reactivation priority. Any credit-related data used in POLR must come from information the customer voluntarily provides or from data Fox legitimately holds from a prior application.

---

### 2.5 Comprehensive Credit Reporting (CCR) Restrictions

The Privacy Act Part IIIA and the Privacy (Credit Reporting) Code 2014 regulate credit reporting information. Key restrictions for Fox:

- Fox can access a person's credit report only in connection with a credit application that person has made
- Fox cannot use credit information from one application to market a second product without the person's knowledge
- Retention of credit report data is limited — it must be destroyed when no longer needed for the purpose it was collected

**For POLR:** If a person applied for an FFG loan and FFG accessed their credit report, that credit information cannot be used to trigger FHL cross-sell messaging without disclosure and appropriate use. The trigger should come from Fox's own data (e.g., settlement date, loan amount) not from credit bureau data.

---

### 2.6 Cotality Property Valuation Data Use Restrictions

Cotality (formerly CoreLogic) licences AVM data and has strict terms around:

- Redistribution — who can see the data and in what context
- Commercial use — whether the data can be used to generate commercial leads
- Display format — required attribution and disclaimer language

Fox's CTO must review the Cotality API licence agreement before building the POLR integration. Typical restrictions include:
- Data cannot be on-sold or provided to third parties not covered by the licence
- Valuations must include Cotality attribution
- Data cannot be used to make automated credit decisions without additional disclaimers
- Retention limits on stored AVM data may apply

**Recommended action:** Obtain written confirmation from Cotality that POLR's intended use (displaying AVM estimates to property owners who request them, within a portal accessible to Fox clients and registered users) is permitted under the licence Fox holds or intends to purchase.

---

## Task 3: Reactivation Strategy Compliance

### Context

Fox generates approximately 49,000 declined leads per year across FFG, FHL, and UMI. POLR proposes to re-engage these leads after a 3-month cooling period with education-first content and, eventually, product offers when their circumstances change.

This is a significant revenue opportunity but requires careful navigation.

---

### 3.1 ASIC Requirements Around Re-Contacting Declined Applicants

ASIC's responsible lending guidance (RG 209) and the NCCP Act impose obligations on credit licensees when they assess applications. However, there is no explicit ASIC prohibition on re-contacting a person who was previously declined.

The obligations are:

1. **NCCP Act s.133 — Unsuitable credit:** Fox must not provide credit or credit assistance if the credit contract would be "not unsuitable" for the consumer. This applies at the time of providing credit assistance, not at the time of re-marketing.

2. **ASIC's concern with predatory re-solicitation:** While not a specific rule, ASIC has expressed concern (in Report 726 and other guidance) about repeated re-solicitation of consumers who have been assessed as unable to afford credit. This is most acute for the UMI/sub-prime segment.

3. **The marketing/credit assistance distinction:** Sending educational content to a declined applicant is not credit assistance. Sending a targeted offer ("We think you can now qualify for X") is, and triggers NCCP obligations at the point of recommending credit.

**Practical guidance:** The 3-month cooling period is a sensible business rule, but it is not derived from a specific regulatory minimum. The real compliance test is not the cooling period — it is what Fox sends and whether, at the point of re-engagement, a new responsible lending assessment is completed before any credit assistance is provided.

---

### 3.2 NCCP Act Restrictions on Re-Solicitation After Decline

The NCCP Act does not explicitly prohibit re-solicitation after decline. However:

1. If Fox re-engages a declined lead and they subsequently apply and are approved, Fox must conduct a fresh responsible lending assessment at that point. The prior decline record does not carry forward as an approval barrier.

2. If Fox's re-engagement message implies that the person is now eligible (e.g., "Your application may now be successful"), this is a credit assistance representation and triggers NCCP obligations.

3. ASIC has indicated it will scrutinise practices that target financially vulnerable consumers with repeated credit offers. For UMI's sub-prime segment this is a meaningful risk.

**Safe approach:** Re-engagement content should focus on financial literacy, goal-setting, and general product education. The call-to-action should be "Talk to a broker" or "Apply when you're ready" — not "Apply now, you may qualify."

---

### 3.3 Consent Considerations for Declined Leads

This is the most operationally complex compliance issue in the reactivation strategy.

**What consent do declined leads have on file?**

When a person enquired with FFG or FHL, they typically provided:
- Contact details for the purpose of the credit application
- Agreement to be contacted in relation to that application

**What they almost certainly did NOT provide:**
- Consent to receive ongoing marketing communications after their application was declined
- Consent to be enrolled in a lifecycle program

**The gap:** Fox needs to review the original application forms and terms and conditions for all declined leads in the 49,000 pool. If those forms did not include marketing consent, Fox cannot send commercial electronic messages to these people under the Spam Act without first obtaining consent.

**How to close the gap:**
Option A — Audit existing consent: Review original intake documentation. If marketing consent was obtained, document it and proceed with Spam Act compliance.

Option B — Permission re-engagement: Send a single permission-request message to declined leads for whom explicit marketing consent is unclear. This message must itself comply with the Spam Act (which is somewhat circular but legally defensible if sent in the context of "service communication" regarding the prior application). The message asks them to opt into the POLR program.

Option C — New consent at reactivation: Do not contact declined leads until a permissible trigger exists (e.g., they return to the Fox website, they respond to a non-commercial communication, they are referred again). Then capture fresh consent.

**Recommendation:** Option B combined with Option C for the broader database. A one-time re-permission campaign, clearly explaining what POLR is and what they are consenting to receive, is the most practical approach and positions POLR positively.

---

### 3.4 Is 3 Months Sufficient as a Cooling Period?

**Regulatory minimum:** There is no statutory minimum cooling period for credit re-solicitation in Australia. The 3-month period is a Fox business rule, not a regulatory requirement.

**What makes it reasonable:**
- For most credit declines (serviceability-based), 3 months is enough time for circumstances to have changed meaningfully
- It avoids appearing predatory
- It aligns with the credit reporting cycle (some adverse information updates every 1-3 months)

**Where it may be insufficient:**
- For UMI sub-prime declines where the person is in financial difficulty, 3 months is short. ASIC's guidance on hardship and vulnerable consumers suggests a more conservative approach (see 3.5 below).
- Where a person was declined due to a recent default or bankruptcy, their circumstances are unlikely to change materially in 3 months.

**Recommendation:** Apply the 3-month standard for FFG and FHL declines. Apply a 6-12 month education-only period for UMI sub-prime declines before any product offer is introduced.

---

### 3.5 Additional Protections for UMI Sub-Prime Declined Leads

UMI's customers are by definition higher-risk borrowers who have been declined by mainstream lenders. Many will be in financial stress. ASIC's approach to financially vulnerable consumers (informed by RG 209, RG 274, and ASIC's 2021 Hardship report) requires licensees to take additional care.

**Specific risks for UMI re-engagement:**

1. **Hardship indicators:** If a person was declined because of indicators of financial hardship (arrears on other loans, recent default), marketing to them within a short window could be characterised as predatory. Note: the tone-of-voice prohibition on the phrase "financial hardship" is relevant here — never use this term in outbound communications.

2. **Unconscionable conduct:** The Australian Consumer Law (ACL) s.21 and the NCCP Act s.76 both prohibit unconscionable conduct. Repeatedly targeting a financially vulnerable consumer with credit offers could constitute unconscionable conduct, even if individual messages comply with other rules.

3. **Design and Distribution Obligations (DDO):** Under the Treasury Laws Amendment (Design and Distribution Obligations and Product Intervention Powers) Act 2019, product issuers and distributors must ensure products are distributed to consumers within the target market. UMI's sub-prime product has a defined target market. Re-marketing it to someone who was declined — and who may be outside the target market — requires careful assessment.

**Recommended approach for UMI declines:**
- 6-month minimum before any POLR outreach
- First 6 months: financial literacy only, no product mentions
- Month 7-12: general information about credit improvement and budgeting
- Month 12+: gentle invitation to speak with a broker if circumstances have changed
- Never use automated scoring to "approve" a UMI re-applicant without human review

---

### 3.6 Can Fox Re-Engage Declined Leads with Education Content?

**Answer: Yes — this is the cleanest and most compliant path.**

General educational content (financial literacy, budgeting tools, property market information, credit improvement tips) does not constitute credit assistance or financial product advice. Provided the Spam Act consent requirements are met, Fox can send this content to declined leads indefinitely.

**What counts as education:**
- "Here is how lenders assess vehicle loan applications"
- "Three steps to improve your credit profile"
- "Understanding your credit report" (with a link to the government's MoneySmart resource)
- "What affects your borrowing capacity" — general information, not a specific assessment

**What tips over into product solicitation:**
- "You may now qualify for a UMI loan"
- "Apply again — rates have changed"
- "Your situation looks different now — let us reassess you"

The POLR journey for declined leads should be exclusively educational for the first 6-12 months, then shift to a soft "circumstances check-in" (an invitation to speak with a human broker, not an automated offer).

---

## Task 4: Compliance Annotations by Lifecycle Stage

The following annotations are intended for direct use in the lifecycle matrix and HTML tool. Each annotation follows this structure:

- **What can be said:** Permitted content and framing
- **What cannot be said:** Prohibited content and framing
- **Disclaimers required:** Specific disclosure language
- **Compliance risk level:** Low / Medium / High
- **Key rules:** Legislation or guidance that applies

---

### FHL Lifecycle Stages

---

#### FHL Month 1: Welcome + Setup Verified

**What can be said:**
- Welcome to POLR, explain what the platform provides
- Confirmation of loan settlement details (already held by FHL)
- Overview of the lifecycle support FHL provides
- Introduction to POLR features (property tracker, document vault, broker contact)
- General information about the home loan journey ahead (what to expect in year 1)

**What cannot be said:**
- Any recommendation about rate changes or refinancing
- Any comparison of their loan to other products
- Any reference to equity or borrowing more (too early, no relationship basis yet)
- "Advice" in any form (forbidden word per tone-of-voice)
- "Guarantee" in any form (e.g., "we guarantee to support you")

**Disclaimers required:**
- Standard credit licence footer on all emails
- General information disclaimer
- If Cotality data is shown: AVM disclaimer (see Task 1.4)

**Compliance risk level:** Low

**Key rules:**
- Spam Act 2003 — ensure marketing consent was captured at application
- APP 5 — collection notice should have been completed at application; verify records
- NCCP Act — welcome messaging is not credit assistance, no NCCP obligations triggered

**Notes:** The consent basis for Month 1 communications should be the consent captured during the FHL loan application. Verify that FHL's application forms include marketing consent. If not, this is the first message that needs a consent capture mechanism built in.

---

#### FHL Month 3: 90-Day Confidence Pack (includes Cotality Valuation)

**What can be said:**
- "Here is your estimated property value based on Cotality AVM data" (with required AVM disclaimer)
- General information about how property values are tracked
- Educational modules appropriate to their buyer type: First Home Buyer tips, investor loan management, refinancer awareness
- Information about offset accounts, redraw facilities, and how to use them
- Tips on managing a mortgage in the first year

**What cannot be said:**
- "Your property has grown in value — you now have equity you could use" (this tips toward credit solicitation and requires full NCCP process)
- Any suggestion to draw on equity or borrow more
- "Based on current rates, you are paying too much" (this is a credit recommendation)
- Any comparison to current market rates without a disclaimer making clear it is general information

**Disclaimers required:**
- Standard credit licence footer
- General information disclaimer
- Cotality AVM disclaimer (mandatory — see Task 1.4)
- For FHB modules: "This information is general in nature. Your individual circumstances may affect your options. Speak with your broker before making any decisions."

**Compliance risk level:** Low-Medium

**Key rules:**
- NCCP Act s.8 (credit assistance definition) — the line between "here is your property estimate" and "here is equity you could use" must be maintained
- ASIC RG 244 (conflicted remuneration, general conduct) — general information framing required
- Cotality licence terms — AVM display attribution and disclaimer obligations

**Notes:** This stage has the highest content-creation compliance risk in the FHL lifecycle because the Cotality data, if framed poorly, can cross the line into a credit recommendation. Content writers must be briefed explicitly: the valuation is information for the customer's awareness, not a trigger for a product conversation. The product conversation happens when the customer initiates it.

---

#### FHL Month 6: Proactive Pricing Review (Repricing Advocacy)

**What can be said:**
- "Your fixed rate period is approaching expiry — now is a good time to speak with your broker" (if applicable and based on Fox's own records)
- "Lender rates change regularly — speaking with your broker about your current rate is worthwhile"
- "Here is how to prepare for a rate review conversation with your lender"
- "Your broker can advocate for you with your lender — this is part of what they do"
- General information about how variable rates work and what a rate review involves
- Educational content about the RBA cash rate and its effect on home loans

**What cannot be said:**
- "Your current rate is X% — you are paying too much compared to Y%" — this is a specific credit recommendation
- "Switch to lender X for a better deal" — this is credit assistance and triggers NCCP obligations
- "You should refinance" — specific credit recommendation, NCCP triggered
- "We guarantee we can get your rate reduced"
- Anything that implies Fox has reviewed the person's specific financial circumstances and is making a recommendation

**Disclaimers required:**
- Standard credit licence footer
- General information disclaimer
- "Speaking with your FHL broker does not obligate you to take any action. Any recommendation to refinance or change your loan will be subject to a full credit assessment."

**Compliance risk level:** Medium

**Key rules:**
- NCCP Act s.8 — the distinction between "speak to your broker (general prompt)" and "we recommend you refinance (credit assistance)" is critical
- ASIC RG 209 — responsible lending obligations apply when Fox moves from general prompt to specific recommendation
- ACL s.18 — comparisons to market rates must be accurate and not misleading
- Best interests duty (NCCP Act s.47AH) — FHL's obligation to act in the client's best interests when providing credit assistance; the proactive repricing advocacy actually supports this obligation

**Notes:** This stage is a compliance strength, not a risk, if framed correctly. FHL proactively prompting clients to review their rate is consistent with the best interests duty obligation. Frame it as "your broker working for you" not "here is what you should do." The compliance advantage: most brokers do nothing after settlement; FHL's proactive approach demonstrates best interests duty in action.

---

#### FHL Month 9: FFG Momentum Pack (Cross-Sell to Asset Finance)

**What can be said:**
- General information about FFG and the services it provides
- "Did you know Fox also helps with vehicle finance, equipment finance, and business lending?"
- An invitation to speak with an FFG broker if they have asset finance needs
- Educational content about the difference between asset finance and home lending
- General information about commercial chattel mortgages for business owners (if the ICA profile supports this)

**What cannot be said:**
- "Based on your home loan size, you can probably afford to finance a vehicle for $X per month" — this is a specific credit assessment
- "You have X equity in your property — use it to buy a car" — cross-entity credit recommendation, high risk
- Any implied approval or pre-qualification
- Any reference to the person's home loan equity as a funding source for an asset finance purchase

**Disclaimers required:**
- Standard credit licence footer (must include FFG's ACL details, not just FHL's)
- General information disclaimer
- "Fox Finance Group Pty Ltd (ACL [number]) provides credit assistance for asset finance products. Any credit assistance is subject to credit assessment and the terms of the relevant credit provider."

**Compliance risk level:** Medium-High

**Key rules:**
- NCCP Act — cross-sell from FHL to FFG triggers FFG's responsible lending obligations at the point of credit assistance
- Privacy Act APP 6 — using FHL customer data to market FFG products is a secondary use; must be disclosed in the Privacy Policy and Collection Notice
- Spam Act 2003 — if FFG sends the message (not FHL), separate sender identification is required
- Design and Distribution Obligations — FFG's products must be distributed to people within their target market; the ICA profiles help here

**Notes:** This is the highest-privacy-risk stage in the lifecycle. The data sharing between FHL and FFG for cross-sell purposes is legal but only if properly disclosed in the Privacy Policy. The key control is that POLR (not FFG) sends the message — POLR is the parent entity that holds consent to cross-entity communication. The message should come from POLR and be clearly described as POLR connecting the customer with Fox's broader services. This framing reduces the technical risk of FFG "receiving" FHL customer data without disclosure.

The ICA-targeted packs (5 profiles + equity release pack) must ensure the equity release pack does not imply a specific credit recommendation. "Equity release" as a concept can be discussed generally; specific advice requires an NCCP-compliant engagement.

---

#### FHL Month 12: Annual Property and Loan Strategy Review

**What can be said:**
- "12 months in — here is an updated Cotality property estimate for your records"
- "Now is a good time to review your mortgage with your FHL broker"
- General information about year 2 of home ownership
- Prompts to consider financial goals (buying a second property, paying down the loan faster, reviewing insurance)
- An invitation to book a broker review meeting

**What cannot be said:**
- Specific recommendations about what the client should do with their equity
- Comparisons to current market rates framed as a recommendation
- Any implied assessment of their current financial position
- "Based on your property growth, you are ready to invest"

**Disclaimers required:**
- Standard credit licence footer
- General information disclaimer
- Cotality AVM disclaimer
- "An annual review meeting with your broker is an opportunity to discuss your circumstances. Any recommendations will be based on your current situation assessed at the time."

**Compliance risk level:** Low-Medium

**Key rules:**
- Best interests duty (NCCP Act s.47AH) — the annual review supports compliance with this obligation
- NCCP Act s.8 — the invitation to review is not credit assistance; the review itself, if it results in a recommendation, triggers NCCP obligations
- APP 6 — client data used to prompt the review is within the primary purpose of the original FHL application

**Notes:** This stage is a compliance asset. FHL conducting an annual review is consistent with best interests duty and demonstrates ongoing client management. Document that reviews occurred — this record is valuable if ASIC ever reviews FHL's practices.

---

#### FHL Month 15: Refinance Pathway

**What can be said:**
- General information about what refinancing involves
- "Here are the three questions to ask your broker if you are considering refinancing"
- "Here is how to know if refinancing makes sense for you" (educational, not specific)
- An invitation to speak with a broker to assess their specific situation
- General information about the costs of refinancing (discharge fees, application fees)

**What cannot be said:**
- "You should refinance" without a full NCCP-compliant assessment
- "Your current rate is X — we can get you Y" without it being a formal credit assistance engagement
- Any specific comparison of their current loan to an identified alternative product
- "You have been declined before but now you may qualify" (not relevant here but relevant if this pathway is applied to reactivation)

**Disclaimers required:**
- Standard credit licence footer
- General information disclaimer
- "Whether refinancing is right for you depends on your individual circumstances. Speak with your FHL broker to understand your options. All refinance recommendations are subject to a full credit assessment."

**Compliance risk level:** Medium

**Key rules:**
- NCCP Act s.8 — the message invites a conversation; the conversation, if it leads to a credit recommendation, is credit assistance and must comply with NCCP including responsible lending and disclosure obligations
- NCCP Act s.47AH — best interests duty requires the broker to recommend refinancing only if it benefits the client net of costs
- ASIC RG 209 — the responsible lending assessment must be current and specific to the client's circumstances at the time of the refinance recommendation

**Notes:** The three-pathway structure (pay down, invest, refinance) is good from a compliance standpoint because it frames the conversation as a choice exploration rather than a recommendation. Maintain that neutrality in the content.

---

#### FHL Month 18: Action Window

**What can be said:**
- Synthesis of journey milestones
- A prompt to take the next step based on goals they have previously expressed
- An invitation to a review meeting framed around their stated objectives
- General celebration of the 18-month milestone

**What cannot be said:**
- Any assumption about their financial position without current data
- Automatic credit recommendations triggered by platform data without human review
- "You are ready to buy again" or similar without a broker-initiated assessment

**Disclaimers required:**
- Standard credit licence footer
- General information disclaimer
- If any financial figures are mentioned: "Figures are based on information provided at or before your loan settlement and may not reflect your current circumstances."

**Compliance risk level:** Low (invitation stage) to High (if automated credit triggers are used)

**Key rules:**
- NCCP Act — the action stage, if it results in credit assistance, requires full NCCP compliance from that point
- APP 6 — data from 18 months of engagement is being used to personalise the prompt; this is within original purpose if disclosed in the Privacy Policy

**Notes:** The compliance risk in this stage is almost entirely determined by whether the "action" is automated or human-initiated. An automated message that says "Based on your property growth of X% and your loan balance of Y, now is the time to invest" is likely a credit recommendation without the required NCCP assessment. A message that says "You have reached 18 months — your broker would love to catch up and hear what your goals are for the next chapter" is general and compliant. Keep the automation on the invitation side; keep the assessment on the human (broker) side.

---

### FFG Lifecycle Stages

Note: FFG deals in asset finance (vehicle, equipment, commercial). Average settlement is $2,300 commission with no trailing. Lifecycle management here is about cross-sell to FHL and UMI, retention through referral, and replacement cycle management.

---

#### FFG Month 1: Welcome + Setup

**What can be said:**
- Welcome and settlement confirmation
- What POLR provides for FFG clients
- Introduction to FHL and UMI services (general, not a product recommendation)
- Educational content about managing a vehicle or equipment loan
- Overview of the Fox Group

**What cannot be said:**
- Specific cross-sell offers at this stage
- Any implication that their asset finance information will be used to assess them for a home loan without their consent

**Disclaimers required:**
- Standard credit licence footer (FFG ACL)
- General information disclaimer
- APP 5 notice if not captured at application: explain that POLR holds their information and how it is used

**Compliance risk level:** Low

**Key rules:**
- Spam Act 2003 — verify marketing consent was captured at FFG application
- APP 5 — collection notice required if POLR enrolment was not covered at application

---

#### FFG Month 3: Financial Health Check-In

**What can be said:**
- General prompts about financial wellbeing
- MoneySmart-style general financial literacy content
- Prompts to review their budget or financial goals
- An invitation to speak with an FHL broker if they have home loan questions (general, not a targeted offer)

**What cannot be said:**
- "Based on your car loan, you may be eligible for a home loan" — this is a credit recommendation
- Any assessment of their creditworthiness based on their FFG data
- "Financial hardship" (forbidden phrase per tone-of-voice)

**Disclaimers required:**
- Standard credit licence footer
- General information disclaimer

**Compliance risk level:** Low

**Key rules:**
- NCCP Act — general financial health content does not trigger credit assistance obligations
- Privacy Act APP 6 — using FFG data to prompt a financial health check-in is within the primary purpose of the FFG relationship

---

#### FFG Month 6: Next Need Detector

**What can be said:**
- General prompts around common financial milestones (e.g., "many people at 6 months into a car loan start thinking about...")
- An invitation to speak with an FFG or FHL broker about their next financial goal
- General information about the range of products Fox can assist with

**What cannot be said:**
- Automated credit recommendations based on FFG data
- Specific product offers without a human broker involved
- Any implication that Fox has assessed their eligibility for a new product

**Disclaimers required:**
- Standard credit licence footer
- General information disclaimer
- If FHL is mentioned: FHL credit licence details

**Compliance risk level:** Low-Medium

**Key rules:**
- NCCP Act — the "detector" function (identifying signals that a person may have a new need) is fine; acting on those signals with a specific offer without NCCP compliance is not
- Privacy Act APP 6 — engagement data within POLR can be used to personalise messaging within the consented purposes

**Notes:** The "detector" language in the lifecycle name should not be reflected in external communications. Internally it describes the strategy; externally it should be framed as "checking in on your goals." Never communicate to a customer that they have been scored or assessed.

---

#### FFG Month 9: Value Delivery + Cross-Sell Moment

**What can be said:**
- Tangible value: updated vehicle value information (if available), finance tip relevant to their loan type
- General information about FHL or home loan products for those who do not own property yet
- An invitation to explore whether home ownership is on their roadmap (general)
- Information about equipment upgrade options for business borrowers (general)

**What cannot be said:**
- Specific offers: "You have paid down $X of your loan, you now qualify for Y"
- Any equity or asset-based credit recommendation
- Comparisons to current market rates without a general information disclaimer

**Disclaimers required:**
- Standard credit licence footer (both FFG and FHL details if FHL is mentioned)
- General information disclaimer
- DDO note if specific products are mentioned: "This product may not be appropriate for everyone. Consider whether it meets your needs."

**Compliance risk level:** Medium

**Key rules:**
- Privacy Act APP 6 — cross-sell from FFG to FHL uses FFG customer data for a secondary purpose; Privacy Policy must cover this
- Spam Act 2003 — if FHL sends any direct communication, FHL must be identified as sender
- DDO — products mentioned must align with the target market for that product

---

#### FFG Month 12: Annual Check-In

**What can be said:**
- 12-month milestone acknowledgement
- General prompt to review their asset finance and consider what comes next
- An invitation to speak with a broker about their goals for the next 12 months

**What cannot be said:**
- Specific credit recommendations
- Any automated assessment of their eligibility for a new or replacement loan

**Disclaimers required:**
- Standard credit licence footer
- General information disclaimer

**Compliance risk level:** Low

---

#### FFG Month 18: Replacement Cycle Prompt

**What can be said:**
- General information about vehicle replacement cycles
- "Many people start thinking about upgrading their vehicle at around 2-3 years" (general, not a personal assessment)
- An invitation to speak with an FFG broker about their next finance need
- Information about how FFG can assist with trade-ins and new finance arrangements

**What cannot be said:**
- "Based on your current finance, you are ready to upgrade"
- Any implied assessment of their creditworthiness for a new loan
- Pre-qualification language

**Disclaimers required:**
- Standard credit licence footer
- General information disclaimer
- If specific finance figures are mentioned: "Figures are indicative only and subject to credit assessment."

**Compliance risk level:** Low-Medium

**Key rules:**
- NCCP Act — the invitation to speak with a broker is not credit assistance; the broker's subsequent recommendation is
- ACL s.18 — any figures used (e.g., "a vehicle in this category typically costs $X per month") must be accurate and clearly framed as indicative

---

### Non-Client Journey Stages

These stages carry the highest compliance risk in the entire POLR model because the consent basis is the most uncertain. Apply extra caution.

---

#### Non-Client: POLR Onboarding

**What can be said:**
- What POLR is and what it provides
- What data will be collected and why (APP 5 notice — mandatory)
- What communications they will receive and how to opt out
- General financial literacy content available through the platform
- Overview of Fox Finance Group and related entities

**What cannot be said:**
- Anything that implies they are being assessed for a financial product they have not applied for
- Any product-specific content before they have actively engaged with the platform

**Disclaimers required:**
- Full APP 5 collection notice on the sign-up screen (not just a link to the Privacy Policy)
- Spam Act consent tick-box (not pre-ticked)
- Credit licence footer on all screens that mention financial products
- General information disclaimer

**Compliance risk level:** High (setup stage — if consent is captured incorrectly here, everything downstream is non-compliant)

**Key rules:**
- Spam Act 2003 — express consent required before sending commercial electronic messages
- Privacy Act APP 5 — collection notice mandatory at the point of data collection
- Privacy Act APP 1 — Privacy Policy must be publicly available and up to date before POLR goes live
- NCCP Act — POLR must not imply that completing the sign-up constitutes a credit application

**Notes:** Invest the most compliance review effort here. A legally sound sign-up flow protects all downstream communications. If the sign-up flow is right, the rest of the journey is significantly de-risked.

---

#### Non-Client: Ongoing Value Delivery

**What can be said:**
- General financial literacy content
- Property market information and Cotality estimates (with AVM disclaimer)
- Tools: calculators, budget planners, goal trackers
- Content about Fox's services in general terms
- MoneySmart-style content

**What cannot be said:**
- Specific product recommendations
- Any content that implies Fox has assessed their creditworthiness or financial position
- "Apply now" calls to action in the early stage of the relationship
- "Based on your profile, you may be eligible for..."

**Disclaimers required:**
- Standard credit licence footer on all emails
- General information disclaimer
- Cotality AVM disclaimer where applicable

**Compliance risk level:** Low (if education-only content is maintained)

**Key rules:**
- Spam Act 2003 — all commercial electronic messages must carry sender identification and unsubscribe mechanism
- NCCP Act — general education content does not constitute credit assistance; the line must be maintained
- ACL s.18 — all content must be accurate

---

#### Non-Client: Conversion Signal Detection

**What can be said:**
- Nothing proactive based solely on behavioural data. Conversion signal detection is an internal POLR process, not a communication type.
- When a conversion signal is detected, the appropriate response is a human outreach (broker contact), not an automated credit offer.
- An invitation to speak with a broker (general, not linked to the detected signal in external communications) is appropriate.

**What cannot be said:**
- "We noticed you looked at our home loan calculator — here is an offer" — this is both creepy from a privacy perspective and potentially a credit recommendation
- Any external communication that reveals Fox has been monitoring their platform behaviour
- Any automated pre-qualification based on self-reported or behavioural data

**Disclaimers required:**
- The fact that Fox monitors engagement data within POLR must be disclosed in the Privacy Policy
- Any outreach following a conversion signal must include standard disclaimers as above

**Compliance risk level:** Medium-High

**Key rules:**
- Privacy Act APP 3 — data collected through the platform (engagement data) must be collected in a way that is reasonable in the circumstances and disclosed in the Privacy Policy
- Privacy Act APP 6 — using engagement data to inform outreach is a secondary use; must be covered in the Privacy Policy
- ACL s.18 — any outreach must not be misleading about why Fox is contacting them

**Notes:** The safest operational model is: POLR detects the signal, flags it to a human broker, the broker makes natural contact ("Just checking in — how are you going with your goals?"). Do not reference the specific trigger in the outreach. This approach preserves the compliance position while still allowing conversion signal detection to drive broker activity.

---

## Summary: Compliance Priority Actions

The following actions should be completed before POLR goes live. They are ordered by risk priority.

| Priority | Action | Owner | Rule |
|---|---|---|---|
| 1 | Audit all intake forms (FFG, FHL, UMI) for marketing consent language. Update if missing. | Legal / Compliance | Spam Act 2003 |
| 2 | Draft and have a lawyer approve a group-level Privacy Policy covering FFG, FHL, UMI, and POLR with cross-entity data sharing disclosed. | Legal | Privacy Act APP 1, APP 5, APP 6 |
| 3 | Build an APP 5-compliant collection notice into the POLR sign-up flow. Separate marketing consent tick-box (not pre-ticked). | CTO / Dev | Privacy Act APP 5, Spam Act |
| 4 | Review Cotality API licence for display and use restrictions. Confirm POLR's intended use is permitted. Get written confirmation. | CTO / Legal | Cotality licence |
| 5 | Brief all content writers on the general information vs credit assistance distinction. Create a one-page content compliance checklist. | Njin / Marketing | NCCP Act s.8 |
| 6 | Confirm ACL numbers for FFG, FHL, and UMI. Ensure all three appear correctly in POLR footer templates. | Compliance | NCCP Act, Spam Act |
| 7 | For declined lead reactivation: audit existing consent records, determine which leads have marketing consent on file, and design a re-permission campaign for those who do not. | Marketing / CRM | Spam Act, Privacy Act |
| 8 | Apply 6-month minimum education-only period for UMI declined leads before any product content is introduced. | CRM / N8N | ASIC RG 209, NCCP Act |
| 9 | Implement platform-level unsubscribe mechanism in N8N/SendGrid (5-business-day processing, 30-day link validity). | CTO / Dev | Spam Act 2003 |
| 10 | Document all broker review meetings and rate review prompts as part of FHL's best interests duty records. | FHL Operations | NCCP Act s.47AH |

---

## Competitive Advantage Framing

POLR's proactive lifecycle management already exceeds what the industry standard requires. Most mortgage brokers send a settlement email and nothing more. The FHL lifecycle — with its repricing advocacy, annual reviews, and 18-month action window — is a demonstration of best interests duty in practice, not just in theory.

When Fox presents POLR to prospects and clients, the compliance framework is a selling point:

- "We are required to act in your best interests. POLR is how we prove we do."
- "Most brokers go dark after settlement. We built a system that means we are still working for you 18 months later."
- "Every communication we send is reviewed against Australian financial services regulations so you can trust what you read."

This framing positions compliance as evidence of trust, which is the core of Fox's brand positioning. The guardrails do not limit the strategy — they validate it.

---

*End of Compliance Annotations v1.0*
*Prepared by Dr. Evelyn Reed, Domain Expert — Njin Method Framework*
*Review required by qualified Australian financial services compliance lawyer before implementation*
