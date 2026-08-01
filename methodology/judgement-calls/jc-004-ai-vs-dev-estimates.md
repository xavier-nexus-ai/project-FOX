# Judgement Call 4: AI Estimate vs Developer Estimate

**Title:** Estimation Source — When Should the Coordinator Self-Estimate vs Pull Dev Hours?

**The Decision:** For sprint planning, should the Coordinator (AI) generate its own time estimates, or ask the PM to pull estimates from the development team?

**Default workflow (from Apr 7 meeting):**
1. Coordinator starts with 100% availability assumption for sprint planning.
2. Coordinator prompts the PM: *"Should I estimate hours myself, or do you want to pull hours from the dev team?"*
3. PM decides based on the signals below.
4. If no response from PM, the Coordinator falls back to AI self-estimates with a flag: *"Using AI estimates — please validate with dev team before sprint commitment."*

**Signals: use AI estimates when:**
- Early planning / scoping phase (not sprint commitment)
- Deliverable is well-defined and similar to prior work in the framework
- No custom technical build required (e.g., playbook sections, documentation, COS setup)
- Speed matters more than precision at this stage

**Signals: pull dev estimates when:**
- Sprint commitment is being locked (estimates affect delivery dates and client expectations)
- Technical uncertainty is high (new integrations, custom builds, unfamiliar CRM platform)
- Deliverable is a software build (app, automation, CRM workflow)
- There's a specific developer assigned to the work

**Rule:** AI estimates are for planning and scoping. Dev estimates are for committing. Never commit a sprint to a client using AI-only estimates without at least a PM sanity check.

**Exceptions:**
- If the developer is unavailable and a client deadline is imminent, AI estimates with a 20% buffer are acceptable — flag the risk in the COS and to the client.

**Source:** Apr 7 meeting transcript — Coordinator design discussion, open question on default fallback rule.
