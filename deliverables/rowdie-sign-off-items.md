# Playbook — Sign-Off Items

**Raised:** 2026-05-06
**Owner:** Rowdie Lang (sign-off) + Bill Robb (operational confirmation where noted)
**Source:** FFG and FHL playbooks (pre-sales, cross-sell, shared master documents) — items extracted on playbook revision

---

## A. Technical Build (Xavier + Rowdie)

| # | Item | Owner | File |
|---|---|---|---|
| A1 | **ICA derivation rules** — proposed logic in the FFG cross-sell developer guide. Rowdie to validate or correct before build starts. | Rowdie | FFG 07e |
| A2 | **Credit Cards field format** — confirm whether Ambition exports a count, a boolean, or card numbers. Card numbers must never reach GHL. | Rowdie + Xavier | FFG 07e |
| A3 | **Routing matrix nuance** — any if-then exceptions for BAB borrowers with `mortgage_balance_band = None` or other edge cases not captured in the derivation logic? | Rowdie | FFG 07e |
| A4 | **SendGrid access method** — shared login vs own login per brand. Xavier to confirm with Rowdie before Phase 2. | Xavier + Rowdie | FFG 07e |
| A5 | **Purchase Type derivation rules (FHL)** — proposed logic in the FHL cross-sell developer guide. Rowdie to validate against current Infynity field availability. | Rowdie | FHL 07e |
| A6 | **FFG broker routing queues** — does FFG run distinct queues for vehicle, commercial, and consumer brokers, or does every FFG broker handle every type? Affects Warm Handover task routing. | Rowdie + Bill | FHL 07e |
| A7 | **Infynity CSV export cadence** — weekly is proposed. Rowdie to confirm whether the export can be scheduled or stays manual. | Rowdie | FHL 07e |
| A8 | **De-dup rule (FHL contact already exists in FFG pipeline)** — when a contact appears in both pipelines, should the FFG sequence pause, exit, or run in parallel? | Rowdie | FHL 07e |

---

## B. Legal and Compliance (Rowdie)

| # | Item | Owner | File |
|---|---|---|---|
| B1 | **Privacy policy update** — must cover cross-business data sharing (FFG settlement data used to flag FHL opportunities). Rowdie to check current privacy policy and update before launch. | Rowdie | FFG 07e |
| B2 | **Compliance footer wording** — confirm exact ACL 382952 and ACR 535038 disclaimer text matches Fox legal's current standard. Apply consistently to every email. | Rowdie | FFG 07e, FHL 07e |
| B3 | **Reactive SMS frequency cap (FHL)** — proposed 1 SMS per active month. Rowdie to confirm against ACMA Telemarketing and Fax Marketing Code and Fox's broader SMS policy. | Rowdie | FHL 07e |
| B4 | **Equity Release / Top-Up handling** — confirm these stay inside the FHL lifecycle retention playbook and are not surfaced as a cross-sell. | Rowdie + Bill | FHL 07e |

---

## C. Content Sign-Off (Rowdie)

| # | Item | Owner | File |
|---|---|---|---|
| C1 | **All automated emails and SMS** — every script in both 07e Copy Libraries is DRAFT until reviewed by Rowdie for brand voice and compliance. Voice score 24/30 minimum per email before loading into GHL. | Rowdie | FFG 07e, FHL 07e |
| C2 | **Dynamic tokens** — confirm every `{{custom.*}}` and `{{dynamic.*}}` token can be populated from Ambition CSV or Fox-MIS at send time. Replace with static fallbacks where they cannot. | Rowdie + Xavier | FFG 07e |
| C3 | **PCLRB Day 30 Market Pulse (Fox-MIS dynamic email)** — confirm whether the content layer can produce monthly-fresh content by Phase 2 of build, or whether the static fallback ships for the first 90 days. | Rowdie | FFG 07e |
| C4 | **Social proof story (FHL Referral Email 3)** — Rowdie to draft from a real anonymised case. Placeholder currently in the copy library. | Rowdie | FFG 07e |
| C5 | **Commercial Pack EOFY timing** — Day 270 may not align with EOFY depending on settlement month. Two pack variants needed: EOFY push framing and New FY planning framing. | Rowdie | FHL 07e |
| C6 | **Eftpos card fulfilment timing** — confirm 7 days post-referred-settlement is operationally accurate. | Rowdie | FFG 07e |
| C7 | **Per-ICA cross-sell language (FFG 08e)** — drafted from strategy PDF tone notes. Rowdie to review and refine. | Rowdie | FFG 08e |
| C8 | **Per Purchase Type cross-sell language (FHL 08e)** — drafted from cos.yaml lifecycle plan and FHL process map. Rowdie to review and refine. | Rowdie | FHL 08e |
| C9 | **Call scripts (FFG 10e)** — drafted from strategy PDF and customer journey doc. Rowdie to review all four call types before brokers use them. | Rowdie | FFG 10e |
| C10 | **Annual review question and reactive lifecycle call language (FHL 10e)** — Rowdie to review with Bill. | Rowdie + Bill | FHL 10e |

---

## D. Operational (Rowdie + Nathan + Bill)

| # | Item | Owner | File |
|---|---|---|---|
| D1 | **Settlement Calls script (Doc 6)** — still empty in the FFG sales process scripts. The at-settlement seed depends on this being completed. Blocker for the at-settlement trigger half of the cross-sell timing. | Rowdie | FFG 07e, FFG 10e |
| D2 | **Hot Lead SLA (24h)** — proposed. Rowdie and Bill to confirm this is operationally realistic against current broker capacity. | Rowdie + Bill | FFG 08e, FFG 10e |
| D3 | **FHL broker queue ownership** — who is in the FHL referral queue? Bill alone, or Bill + Paige + Angel rotating? Affects task routing in GHL. | Rowdie + Bill | FFG 08e |
| D4 | **Proactive call cadence (30 min/week per broker)** — proposed. Rowdie and Nathan to confirm against actual broker capacity. | Rowdie + Nathan | FFG 08e |
| D5 | **Reactive trigger SLA (48h / 24h urgent)** — proposed for FHL-side handovers. Rowdie and Bill to confirm operationally realistic. | Rowdie + Bill | FHL 07e, FHL 08e, FHL 10e |
| D6 | **Red Dot Protocol thresholds** — proposed Yellow/Red timings in FHL 08e. Rowdie to confirm. | Rowdie | FHL 08e |
| D7 | **`FFG_ExistingLoan_Other` tag** — proposed for tracking FHL customers who already have FFG-equivalent loans with another lender. Rowdie to confirm whether worth the data overhead or whether to drop. | Rowdie | FHL 08e |
| D8 | **FFG broker outbound call opener** — confirm whether the FFG broker should reference the specific Momentum Pack email the customer clicked, or keep the opener generic. Currently generic. | Rowdie + Bill | FHL 10e |
| D9 | **Broker direct numbers** — confirm whether each broker has their own direct line for the follow-up email templates, or whether the central 1300 number is used. | Rowdie | FFG 08e |
| D10 | **FHL personal handover note** — confirm whether the FHL broker is expected to write a personal note on top of the auto warm handover email, or whether the auto-email alone is sufficient. | Rowdie + Bill | FHL 07e |
| D11 | **Cross-sell pipeline ownership** — who owns the FFG to FHL handoff inside Fox? Bill (Head of Home Loans)? Rowdie? Not yet settled in cos.yaml. | Rowdie + Nathan | FFG 07e |
| D12 | **Commercial Purchase Type pack content** — Bill Robb input needed on what Commercial FHL customers typically need next from FFG (likely commercial vehicle and equipment finance). | Bill | FHL 07e |

---

## E. Pre-Sales and Shared Master Items (Rowdie)

| # | Item | Owner | File |
|---|---|---|---|
| E1 | **FFG pre-sales custom-field migration** — final 31-field ICA list and privacy-filtered field set need to be locked before custom-field migration. | Rowdie + Xavier | FFG 07c |
| E2 | **FFG booking flow** — confirm GHL Calendar vs the existing booking flow now that Calendly is being replaced. | Rowdie + Xavier | FFG 07c |
| E3 | **FFG SMS sender and Booked Out handoff** — confirm Twilio sender number choice and whether Booked Out handoff to Ambition uses API push or CSV fallback. | Rowdie + Xavier | FFG 07c |
| E4 | **Pre-sales Red Dot business hours** — confirm exact business hours used by FFG and FHL SLA timers before workflow build. | Rowdie | FFG 07c, FHL 07c |
| E5 | **FHL pre-sales broker routing** — confirm Commercial, Investor, Refinance, First Home Buyer, and New Purchase routing rules plus the high-value loan threshold. | Rowdie + Bill | FHL 07c |
| E6 | **FHL Infynity and Cotality handling** — confirm Infynity CSV format/export cadence and whether Cotality stays manual or gets API treatment in V1. | Rowdie + Xavier | FHL 07c |
| E7 | **FFG pre-sales voice scripts** — final review of call openers, voicemails, BAMFAM booking, and reactivation scripts before production use. | Rowdie | FFG 10c |
| E8 | **FHL pre-sales voice scripts** — final review of broker call openers, voicemails, appointment booking, and reactivation scripts before production use. | Rowdie | FHL 10c |
| E9 | **Pre-sales customer stories** — provide anonymised story inputs for FFG ICA nurture and FHL Purchase Type nurture where placeholders remain. | Rowdie | FFG 07c, FHL 07c |
| E10 | **FHL ICA framework** — separate FHL ICA framework still required; current ICA document covers FFG ICAs only and FHL pathway notes are cross-sell routes, not FHL ICAs. | Rowdie | Master ICA doc |
| E11 | **FHL outbound cadence and call attempts** — confirm how many days FHL brokers chase leads and how many manual call attempts are expected before no-response handling. | Rowdie + Bill | FHL process map, FHL 07c |
| E12 | **FHL declined-application handling** — confirm what happens to declined FHL applications and whether a declined nurture path or equivalent 90-day plan exists. | Rowdie + Bill | FHL process map, FHL 07c |

---

*Items remain open until Rowdie or Bill marks them closed. Blocked items (D1) must be resolved before Phase 2 content load can begin.*
