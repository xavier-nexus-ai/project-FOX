# Workflow: Meeting Review (Transcript > COS Updates)

**Purpose:** Process a meeting transcript to extract PM-relevant decisions, action items, blockers, and updates — then sync them into the COS and njin-vibe.

**Duration:** 15-30 minutes per meeting.

**Owner:** PM (driving), Orchestrator (executing via meeting-review skill)

---

## Prerequisites

- [ ] Meeting has happened
- [ ] Transcript is available (Fathom, Otter, manual notes, etc.)
- [ ] Transcript is in `docs/background/meetings/` or provided inline
- [ ] Project has an initialised `cos.yaml`

---

## Workflow Steps

### Step 1: PM Provides Transcript

PM places transcript in `docs/background/meetings/` or pastes inline:

```
/meeting
```

or

```
Review this meeting: docs/background/meetings/2026-04-09-client-call.md
```

---

### Step 2: Orchestrator Invokes Meeting Review Skill

Orchestrator runs `meeting-review` skill. This is a built-in skill — no specialist agent spawned.

The skill follows 6 stages:

### Stage 2.1: Transcript Analysis
- Read the transcript in full
- Identify the client/project being discussed
- Extract PM-relevant items:
  - **Completed items** (work that was done or confirmed complete)
  - **New tasks** (work identified that needs doing)
  - **Blockers** (things preventing progress)
  - **Timeline changes** (deadlines shifted, new dates)
  - **Decisions** (choices made during the meeting)
  - **Context / intel** (useful info that's not a task but matters)
- Ignore: greetings, off-topic chat, technical troubleshooting irrelevant to PM work

### Stage 2.2: Cross-Reference COS
- Read current `cos.yaml`
- Compare extracted items against existing state
- Identify:
  - Which items confirm existing COS state (no action)
  - Which items change existing state (need update)
  - Which items are entirely new (need to be added)
  - Any contradictions between transcript and COS

### Stage 2.3: Clarify Gaps
- Ask the PM about ambiguities using AskUserQuestion:
  - Who owns this new task?
  - What priority should it have?
  - Is this deadline realistic?
  - Is this a blocker or just a concern?
- One question at a time, never a wall of questions
- Skip questions where the answer is clear from context

### Stage 2.4: Cross-Reference Notion/njin-vibe
- Check if new tasks already exist in njin-vibe
- Check if blockers are already logged
- Avoid creating duplicates

### Stage 2.5: Propose Update Plan
- Present to PM the full set of proposed changes:
  - COS updates (specific fields)
  - New tasks for njin-vibe (with priority, owner, deadline)
  - Blockers to log
  - Change log entry
- **Wait for PM approval** before executing any changes

### Stage 2.6: Execute Updates
- After PM approves:
  - Update `cos.yaml` field by field
  - Use `vibe-sync` skill to push new tasks to njin-vibe
  - Add change log entry
  - Confirm each update with the PM as it's made

---

### Step 3: Summary to PM

Orchestrator ends with:

```
Meeting review complete.

What I did:
- Reviewed transcript: [meeting date, attendees]
- Extracted: X completed, Y new tasks, Z blockers, N decisions
- Updated COS: [specific fields]
- Pushed to njin-vibe: X tasks

What you have now:
- Updated cos.yaml
- X new tasks in njin-vibe linked to Project Dashboard
- Change log entry dated [date]

What's next:
- [Recommended next action based on findings]
```

---

## COS Fields Updated

The meeting-review skill can update these COS fields:
- `phase.<current_phase>.deliverables.*` — when completion is confirmed
- `blockers` — new blockers added
- `risks` — new risks identified
- `communications.last_client_touchpoint` — if client meeting
- `communications.next_client_meeting` — if scheduled
- `change_log` — always add an entry

**Rule:** The skill never invents or infers — if the transcript doesn't explicitly mention something, don't add it.

---

## njin-vibe Task Creation Rules

When creating new tasks from meeting extraction:
- [ ] Every task has a Project Dashboard link (critical)
- [ ] Use format: `Task Name | Brand < > Client` (Reclaim) or title with project prefix (Notion)
- [ ] Title does NOT include client name (linked via relation)
- [ ] Priority assigned (Critical / High / Medium / Low)
- [ ] Owner assigned (never leave blank)
- [ ] Due date assigned
- [ ] Est Effort (Hours) populated
- [ ] Body contains: Overview, Scope, Dependencies, Context, Acceptance Criteria
- [ ] Max 2-3 Critical/High per client

---

## Failure Modes

| Failure | Recovery |
|---------|----------|
| Transcript is incomplete or unclear | Ask PM for clarification, or flag items as "to verify" |
| Extracted items contradict COS | Present contradiction to PM, let them decide which is correct |
| New task owner unclear | Ask PM before creating |
| Blocker already exists in COS | Update existing blocker, don't duplicate |
| njin-vibe Project Dashboard not linked | Cannot push tasks — fix link first |

---

## Anti-Patterns

- **Silent updates** — every change must be proposed to PM before executing
- **Inferring tasks not explicitly mentioned** — stick to what the transcript says
- **Creating duplicate tasks** — always check njin-vibe first
- **Missing Project Dashboard link** — breaks tracking, do not skip
- **Walls of questions** — one question at a time via AskUserQuestion

---

*Reference: Portfolio-level meeting-review skill methodology. `methodology/ways-of-working/notion-task-guidelines.md`.*
