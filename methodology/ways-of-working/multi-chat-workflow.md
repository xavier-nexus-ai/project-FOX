# Multi-Chat Workflow Model

The Njin PM Framework uses a multi-chat workflow model. This document explains how it works, why it exists, and the rules that govern agent coordination.

---

## The Core Pattern

```
Persistent Orchestrator (your main session)
        |
        v
Creates handoff document
        |
        v
Spawns Specialist Agent (new chat)
        |
        v
Specialist returns completion report
        |
        v
Orchestrator reviews, writes files, updates COS
        |
        v
Next handoff
```

The **Orchestrator** is the PM's persistent working session. Specialist agents are spawned in **new chats** when specific work needs to happen, then return their output.

---

## Why Multi-Chat?

### Context isolation
Specialist agents don't need the full project history — they need the specific task context. Spawning a fresh chat:
- Keeps the specialist's context window clean and focused
- Prevents context pollution across different types of work
- Makes debugging easier (one chat = one piece of work)

### Token economy
A long session accumulates context. Every new interaction re-sends all prior context. Specialist agents in fresh chats start clean — cheaper to run, faster to respond.

### Task specialisation
Different agents need different instructions and tool permissions. The multi-chat model enforces clean separation.

---

## The Spawned Agent Sandbox Rule

**CRITICAL TECHNICAL CONSTRAINT:**

Spawned agents (subagents) operate in a sandboxed filesystem. **File writes from subagents do not persist** back to the parent session. Not `Write`, not `Edit`, not `Bash` file operations — nothing.

This means:
- Specialist agents must output deliverables as **text in their task output**
- The **parent session (Orchestrator)** must extract the content and write the files itself
- Read-only operations are unaffected — agents can read anything

### What this looks like in practice:

**Wrong:**
```
Orchestrator: "Scoping Agent, create the scope document and save it to docs/scope.md"
Scoping Agent: [writes file internally, which disappears]
Orchestrator: "Done?"
Scoping Agent: "Yes, file saved."
Orchestrator: [opens docs/scope.md — file doesn't exist]
```

**Right:**
```
Orchestrator: "Scoping Agent, produce the full scope document content in your response. I'll write the file."
Scoping Agent: [outputs full markdown content]
Orchestrator: [extracts content, runs Write tool, saves to docs/scope.md]
Orchestrator: [verifies file exists, updates COS]
```

---

## Handoff Documents

Every agent boundary requires a handoff document. The handoff is the transfer mechanism.

### What a handoff document contains:

1. **Context the specialist needs** — relevant COS sections, prior work, client background
2. **The task** — exactly what the specialist is being asked to produce
3. **The inputs** — paths to files the specialist should read, data to use
4. **The expected output** — format, structure, length, success criteria
5. **Constraints** — what NOT to do, edge cases, boundaries

### Handoff document format:

```markdown
# Handoff: [Agent Name] — [Task]

## From
Orchestrator (session: [session-id])

## Task
[One-sentence description of what needs to happen]

## Context
[Relevant COS state, prior decisions, why this work is needed]

## Inputs
- [File paths to read]
- [Data to use]
- [Prior work to reference]

## Expected Output
- [Format]
- [Structure]
- [Length]
- [Success criteria]

## Constraints
- [What NOT to do]
- [Known edge cases]
- [Boundaries]

## Quality Check
[What the Orchestrator will verify on return]
```

---

## PM Review at Every Handoff

**The PM reviews every handoff document before passing it to the next agent.**

This is a mandatory human checkpoint. Not optional. The purpose:
1. Catch misunderstandings early — before an agent spends 15 minutes producing the wrong thing
2. Confirm the PM understands what's about to happen
3. Prevent runaway automation where agents chain without oversight

**Rule:** If the PM is uncertain about a handoff, the specialist does not start. Clarify first.

---

## Agent Roles in the Framework

In the Njin PM Framework specifically:

| Agent | Where it runs | What it does |
|-------|---------------|--------------|
| **Orchestrator** | Persistent session (the PM's main chat) | Central coordinator, COS owner, handoff creator, file writer |
| **Initialization Agent** | Spawned once at project start | Ingests contract/transcripts/docs, bootstraps COS |
| **Business Analyst** | Spawned when Discovery or Scoping runs | Discovery skill first, then Scoping skill |
| **Coordinator** | Spawned for sprint planning, estimation | Sprint plans, velocity, resource allocation |
| **Communication Agent** | Spawned for client comms | Emails, presentations, status updates |
| **Specialist agents** (Onboarding, AI Coach, Product Owner, QA Tester, Tone of Voice) | Spawned as needed | Role-specific work |

---

## Cross-Session Continuity

Because the Orchestrator is persistent and the COS is the state file, work continues cleanly across sessions:

1. **Session ends** — COS is up to date, change log captures what happened
2. **New session starts** — Orchestrator reads COS, picks up where previous session left off
3. **No context loss** — the state is external to the session, not internal

**Rule:** Always update the COS before ending a session. Next you, or future you, depends on it.

---

## Session Management Rules

- **Multi-session agents** (like IP Extraction in AI Orchestration) checkpoint after every major batch
- **Progress files** live in `docs/progress/` and enable clean session resumption
- **Each session ends with:** what was completed, what's next, any blockers
- **COS updates happen** after every meaningful change, not batched at session end
- **Never run multiple Orchestrator sessions in parallel** on the same client — they'll fight for state ownership

---

## Common Failure Modes

| Failure | Cause | Prevention |
|---------|-------|------------|
| Specialist "saves" a file that doesn't exist | Ignored the sandbox rule | Always have specialists output content as text, Orchestrator writes |
| Handoff too vague, specialist produces wrong output | Incomplete handoff document | Use the full handoff template, don't shortcut |
| PM rubber-stamps handoffs without reviewing | Skipped the review checkpoint | Mandatory human review at every agent boundary |
| Session loses context | COS not updated before ending | Update COS and change log at every meaningful change |
| Parallel sessions fight over COS | Multiple Orchestrator sessions running | One active Orchestrator per client, ever |

---

**Source:** Project `CLAUDE.md` (Multi-Chat Workflow Model), global `CLAUDE.md` (Spawned Agent Sandbox), Apr 7 meeting transcript (handoff document pattern).
