# Judgement Call 2: When to Escalate to James

**Title:** Escalation Threshold — What the PM Can Handle Alone vs What Needs James

**The Decision:** When should the PM (or the AI agent) proceed vs stop and flag to James?

**Signals that require James:**

| Situation | Why |
|-----------|-----|
| New project type with no prior example in the framework | No delivery precedent exists. Guessing creates a wrong plan (like Michael's Avanti plan). |
| Client pushes back on scope or deliverables mid-engagement | Contract-level decision. PM has no authority to change scope. |
| Technical architecture decision (e.g., which MCP servers, agent structure, database choice) | James owns technical design. |
| Pricing, contract, or commercial changes | Revenue and legal — always James. |
| A project plan was created without consulting the framework delivery procedure | The plan is likely wrong. Stop. Rework from the framework. |
| The AI agent flags a gap it cannot fill without human judgement | If the system flags it, trust the flag. |
| Client hasn't provided required access after 5 business days | Escalate to client point of contact *and* flag to James. |

**Default:** If the PM is unsure whether something falls within their authority, assume it doesn't and escalate. Being wrong about escalating costs a 10-minute conversation. Being wrong about proceeding can cost a client.

**Exceptions:**
- Routine comms (status updates, meeting scheduling, chasing access) — PM handles independently.
- Decisions clearly within the playbook SOP (e.g., which sections to include based on playbook type) — PM follows the SOP, no escalation needed.
- The framework itself provides the answer — use it before escalating. That's what it's for.

**Source:** Apr 6 and Apr 7 meeting transcripts — Michael's Avanti plan created without framework consultation flagged as a direct failure mode.
