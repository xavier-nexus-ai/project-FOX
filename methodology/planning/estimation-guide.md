# Estimation Guide

How to estimate effort for Njin engagements across different project types and phases. These are heuristics, not precise formulas — use them as a starting point, adjust for context.

---

## Estimation Philosophy

**Two modes of estimation:**

| Mode | Purpose | Source |
|------|---------|--------|
| **AI self-estimate** | Scoping, early planning, directional | Coordinator agent based on framework patterns |
| **Dev team estimate** | Sprint commitment, technical work | Direct from assigned developer |

**Rule:** AI estimates for scoping. Dev estimates for committing. Never commit a sprint to a client using AI-only estimates without at least a PM sanity check.

---

## Standard Phase Durations by Project Type

### Njin Method Playbook Engagement

| Phase | Typical Duration | Client Time | Njin Time |
|-------|------------------|-------------|-----------|
| Activation — Data Collection | Week 0 (7 days) | 3-5 hours | 4-6 hours |
| Activation — Data Validation | Week 1 | 1-2 hours | 2-4 hours |
| Immersion & Tone of Voice | Weeks 1-2 | 2-3 hours | 6-10 hours |
| Methodology Creation (playbook draft) | Weeks 2-3 | 2-3 hours | 20-30 hours |
| Strategic Presentation & Revision | Week 3 | 3-4 hours | 8-12 hours |
| CRM Implementation | Weeks 4-6 | 2-4 hours | 30-50 hours (dev heavy) |
| Team Training | Weeks 7-8 | 4-8 hours | 6-10 hours |
| Live Monitoring | Weeks 9-12 | 2-3 hours/week | 4-6 hours/week |
| Handover & 30-Day Review | Day 30 | 1 hour | 3-5 hours |
| 90-Day Performance Review | Day 90 | 2 hours | 5-8 hours |

**Total Njin time for a 2-playbook engagement:** ~120-180 hours over 12 weeks.

### AI Orchestration (90-day Build)

| Phase | Weeks | Client Time | Njin Time |
|-------|-------|-------------|-----------|
| Pre-engagement (handover, kickoff) | Week 0 | 1-2 hours | 3-5 hours |
| Immersion (AI literacy, industry, stack, quick win) | Weeks 1-4 | 8-12 hours | 30-40 hours |
| Mapping (IP extraction, methodology, diagnostics, constraints, leverage) | Weeks 5-8 | 15-20 hours (peak) | 40-60 hours |
| Transformation (framework build, QA, deployment) | Weeks 9-12 | 5-8 hours | 50-80 hours |
| Post-engagement (optional retainer) | Week 13+ | varies | varies |

**Total Njin time:** ~120-185 hours over 12 weeks.
**Total client time:** ~30-45 hours over 12 weeks.

### VIBE OS (Software Build)

Estimation depends heavily on feature count and complexity. Use story-level estimation:

| Story Complexity | Hour Range |
|------------------|------------|
| Trivial (UI tweak, config change) | 0.5-2 hours |
| Simple (single component, standard pattern) | 2-6 hours |
| Moderate (multi-component, integration) | 6-16 hours |
| Complex (new architecture, research required) | 16-40 hours |
| Epic (major feature, multi-sprint) | 40-100+ hours |

**Rule for VIBE OS:** If a story is >16 hours, break it down before estimating.

### AetherFlow (Website/Funnel)

| Deliverable | Hour Range |
|-------------|------------|
| Simple landing page (single column, 3-5 sections) | 8-16 hours |
| Marketing website (5-10 pages) | 30-60 hours |
| High-conversion funnel (VSL + opt-in + book + thank you) | 40-80 hours |
| Full product site (15+ pages with blog, resources) | 80-150 hours |
| Dashboard / web app | 60-150+ hours |

Plus content: ~2-4 hours per page for copy, ~1-2 hours per page for SEO.

---

## Complexity Multipliers

Apply these to baseline estimates:

| Multiplier | When to apply |
|------------|---------------|
| **1.0x (baseline)** | Similar to prior work, clear requirements, familiar tech |
| **1.2x** | Some unknowns, moderate uncertainty |
| **1.5x** | Significant unknowns, new integration, unfamiliar CRM/platform |
| **2.0x** | High uncertainty, custom build, research required |
| **3.0x** | First time doing this, experimental approach |

**Rule:** If complexity is 2x+, flag it — consider whether to take on the work at all or scope differently.

---

## Capacity Rules

### James's capacity
- **4 hours/day maximum** of Reclaim task time
- **~20 hours/week** for task work
- Remaining ~30 hours/week: meetings, habits, buffers
- Heavy meeting days (Wednesdays) can be near zero
- Light days (Mondays/Fridays) can stretch to 4h+

### Team capacity (assume for sprint planning)
- **Full-time team member:** 30-35 hours/week of actual work (deducting meetings, admin, context switching)
- **Part-time (50%):** 15-18 hours/week
- **Contractor:** 20-30 hours/week depending on engagement

### Sprint capacity calculation
1. Start with nominal hours (100% availability)
2. Subtract known commitments (leave, existing projects, meetings)
3. Apply a **25% buffer** for unknowns
4. Final: nominal × 0.75 × availability factor

**Example:**
- Xavier, full week, no leave: 30h × 0.75 = **22.5h available**
- Xavier, 2 days leave: 30h × 0.6 × 0.75 = **13.5h available**

---

## Risk Multipliers for Unknowns

Add buffers for known risks:

| Risk | Buffer to add |
|------|---------------|
| New integration / API | +30% |
| Client access dependencies | +20% |
| First time using a tool | +40% |
| Multi-stakeholder review | +25% |
| Regulatory/compliance review | +50% |

---

## Common Estimation Mistakes

| Mistake | Fix |
|---------|-----|
| Estimating only the "happy path" | Add buffer for debugging, review cycles, revisions |
| Forgetting review and iteration time | Always include internal review + client review cycles |
| Not accounting for context switching | A 4-hour task in an interrupted day is actually 6 hours |
| Using optimistic estimates from the devs | Add 20% to anything the devs estimate — they're always optimistic |
| Ignoring meeting load in the sprint | Subtract expected meeting hours from available capacity |
| Assuming 100% availability | Never. Always apply the 25% buffer. |

---

## When to Escalate Estimates

Flag to James or the client when:
- Total estimate exceeds budgeted time by more than 20%
- Critical path has high-uncertainty items
- Dependencies on third parties can't be confirmed
- Client is expecting a deadline that the estimate can't hit

**Rule:** Flag early. Estimates that go sideways mid-sprint are worse than scope conversations at the start.

---

## Documenting Estimates

Every AI self-estimate must include:
1. **The number** (in hours or story points)
2. **The assumptions** (what you're assuming to be true)
3. **The risks** (what could blow it out)
4. **The confidence level** (high / medium / low)

**Without assumptions documented, the PM cannot review what they can't see.**

---

**Source:** Apr 6 and Apr 7 meeting transcripts, AI Orchestration SOP (timeline sections), playbook creation SOP (timeline sections), master project `CLAUDE.md` (capacity rules).
