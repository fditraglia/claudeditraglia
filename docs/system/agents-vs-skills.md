# Agents vs Skills

Claude Code has two main building blocks: **skills** (slash commands that run in the main conversation) and **agents** (subprocesses that run in a separate context). Choosing the right one matters for reliability and quality.

---

## The Key Difference

| Dimension | Skill | Agent |
|-----------|-------|-------|
| **Context** | Runs in the main conversation with full history | Runs in a fresh context — no prior conversation |
| **User interaction** | Can ask questions, show drafts, get feedback | Returns a single result when done |
| **Memory** | Sees everything discussed so far | Sees only what you explicitly pass to it |
| **Bias** | May be influenced by prior conversation ("self-bias") | Fresh perspective — evaluates only what's written |
| **Speed** | Instant (already in context) | Slower (starts a new process) |

---

## When to Use a Skill

Skills work best when the task:

- **Needs conversation context** — The task builds on what you've already discussed
- **Requires user input** — You need to answer questions or make choices mid-workflow
- **Is a workflow** — Multi-step processes with user checkpoints
- **Modifies state** — Writing files, sending emails, updating docs

**Examples:**
- `/done` — Captures decisions from the *current session* (needs conversation history)
- `/prompt` — Formats and executes a prompt (needs to interact with the user)
- `/setup-project-management` — Multi-phase setup with user decisions at each stage

---

## When to Use an Agent

Agents work best when the task:

- **Benefits from fresh eyes** — Review, critique, or evaluation tasks where prior context creates blind spots
- **Can run in parallel** — Multiple evaluations or analyses that don't depend on each other
- **Needs isolation** — You don't want the task polluting your main conversation context
- **Has a clear input and output** — "Here's a file, give me a review" rather than "let's work through this together"

**Examples:**
- **Writing review** — A fresh context evaluates the prose without knowing "what you meant"
- **Methodology review** — Catches issues that the session that wrote the paper might miss
- **Parallel research** — Launch 3 agents to investigate different approaches simultaneously

---

## The Self-Bias Problem

This is the most important reason to use agents for review tasks.

When Claude writes something in a conversation and then you ask it to review that same thing, it has a systematic bias toward finding its own work acceptable. It "knows what it meant" even if the text is ambiguous. It may not question assumptions it made earlier.

An agent running in a fresh context doesn't have this problem. It evaluates only what's on the page — like handing your draft to a colleague who wasn't in the room when you wrote it.

**Rule of thumb:** If you're asking Claude to *critique* something it helped *create*, use an agent.

---

## Agent File Format

Agents are markdown files saved in `~/.claude/agents/`:

```markdown
---
name: Agent Name
description: What this agent does
model: sonnet
tools:
  - Read
  - Glob
  - Grep
---

# Agent Name

[Instructions for the agent]

## Review Dimensions
[What to evaluate]

## Output Format
[How to structure the response]
```

The YAML frontmatter specifies:
- **model** — Which Claude model to use (sonnet is cost-effective for most review tasks)
- **tools** — Which tools the agent can access (limit to what it needs)

---

## Launching Agents

From within Claude Code:

> "Launch the writing reviewer agent on ~/Documents/paper-draft.md"

Claude Code reads the agent file, starts a subprocess, passes the specified files, and returns the result to your main conversation.

You can launch multiple agents simultaneously:

> "Launch both the writing reviewer and methodology reviewer on this paper draft"

They run in parallel and return independent assessments.

---

## Design Guidance

| Scenario | Use | Why |
|----------|-----|-----|
| Reviewing your own draft | Agent | Avoids self-bias |
| Multi-step workflow with decisions | Skill | Needs user interaction |
| Parallel evaluations | Multiple agents | Independent fresh contexts |
| Task needs conversation history | Skill | Agent doesn't see prior context |
| Heavy task that would bloat context | Agent | Keeps main conversation lean |
| One-time setup or configuration | Skill | Needs to read/write files and ask questions |

For a more detailed decision framework with additional examples, see the [Agents vs Skills Decision Guide](../downloads/agents-vs-skills-guide.md) (February 2026).
