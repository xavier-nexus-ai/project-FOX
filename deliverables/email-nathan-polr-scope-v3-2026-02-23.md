**To:** Nathan, Rowdie
**Subject:** POLR MVP - Updated Scope of Work Ready for Review

---

Nathan, Rowdie,

The developers came back with their technical review and product backlog. Good news - they've tightened the architecture and brought the estimate down. I've updated the scope of work to align with their feedback and a few decisions we've made along the way.

**What changed (all improvements):**

- **Focused on FFG + FHL only.** UME Loans is deferred to Phase 2. This keeps the MVP tight and lets us prove the system works across your two core brokerage brands before adding the lending side.
- **Cleaner architecture.** The developers recommended replacing the separate automation server with Next.js Edge Functions. This means everything runs on one platform (Vercel) instead of two, and Matty only has one codebase to maintain.
- **Referral partner management deferred to Phase 2.** The 1,050 dormant partners are a big opportunity, but they're not needed to prove the core automation loop. We'll add this once the foundation is solid.
- **Lead market reactivation stays in.** Simplified to one SMS and one follow-up email per contact, with reply tracking so your brokers get notified when someone responds. No AI, no automated responses - just a smart nudge and a human picks up the conversation.

**What hasn't changed:**

The playbook strategy is exactly the same. The cross-sell and monetisation playbook and the pre-sales SDR playbook still drive everything - the customer journeys, the content, the trigger logic, the workflows. We were originally going to deliver these through GoHighLevel. Now we're vibe-coding a custom solution instead. Same strategy, better mechanism.

**What POLR delivers in this build:**

- Unified customer database across FFG and FHL
- 8 automated workflows (welcome sequences, lifecycle tracking, cross-sell detection, value-add cycle, lead market reactivation, care call list)
- 5-tab team dashboard (cross-sell pipeline, lifecycle + automation, lead market, care calls, email marketing)
- Contact tagging and multi-brand identification
- Email marketing module with template editing, audience segmentation, and campaign management (Option B)

**Budget:**

The total estimate fits within the range we discussed. Option A (core MVP) and Option B (email marketing) are still quoted separately so you can choose one or both.

**Scope document:**

[LINK]

**Decisions needed from you:**

1. **Option A only, or A + B?** Option A gives you all the automations and dashboard. Option B adds the email marketing capability (template editor, bulk sends, audience segmentation). Both are included in the scope doc.
2. **Happy with UME and referral partners deferred?** Both are Phase 2 items. Want to confirm you're comfortable with that sequencing.

**Still needed from your end:**

- Ambition API documentation (Rowdie)
- Privacy policy status for cross-business data sharing (Rowdie)
- Tone of voice sign-off for email/SMS templates

Once you've reviewed the scope and we're aligned, I'll finalise the developer briefing and we can lock in the build schedule.

Let me know if you want to jump on a call to walk through it.

James
