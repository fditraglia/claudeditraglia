# Skill Library

All downloadable skills, agents, and templates. Each entry includes installation commands, usage examples, and customization guidance.

**Workflow tags:** Skills are tagged by which workflow they belong to — `[PM]` for [Project Management](../workflows/project-management.md), `[EA]` for [Executive Assistant](../toolkit/executive-assistant.md), `[First Session]` for [First Session Skills](../workflows/first-session-skills.md).

---

## Quick Setup

These commands create the folders where Claude Code looks for skills and agents. `mkdir -p` creates a folder (and any parent folders needed). `curl -o` (used below) downloads a file from the internet and saves it to your computer.

```bash
# Create the directories (if they don't exist)
mkdir -p ~/.claude/commands
mkdir -p ~/.claude/agents
```

After saving any new skill file, **restart Claude Code** for the command to become available.

---

## Skills

### /done — Session Capture
`[First Session]`

**What it does:** Captures key decisions, open questions, and follow-ups from your current Claude Code session. Writes a structured entry to a session log file.

**MCP dependencies:** None.

**Install:**
```bash
curl -o ~/.claude/commands/done.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/done.md
```

**Usage:**
```
/done              # Full capture
/done quick        # Abbreviated (decisions + follow-ups only)
/done project:xyz  # Tag with a project name
```

**Customization:** Log file location (default `~/Documents/session-log.md`), project matching, archive pruning threshold (default 60 days).

---

### /morning-brief — Daily Briefing
`[EA]`

**What it does:** Generates a daily briefing combining calendar, reminders, inbox highlights, VIP tracking, overdue items, goal alignment, and optional auto-triage.

**MCP dependencies:** Gmail MCP (required). Google Calendar MCP (required). Apple Reminders via osascript (macOS, optional). Granola MCP (optional).

**Install:**
```bash
curl -o ~/.claude/commands/morning-brief.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/morning-brief.md

# Config templates (if not already installed)
mkdir -p ~/.claude-assistant/config
curl -o ~/.claude-assistant/config/email-policy.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/email-policy-template.md
curl -o ~/.claude-assistant/config/calendar-policy.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/calendar-policy-template.md
curl -o ~/.claude-assistant/config/triage-config.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/triage-config-template.md
```

**Usage:**
```
/morning-brief                # Full briefing
/morning-brief no-triage      # Skip auto-triage
/morning-brief email          # Also email the briefing to yourself
/morning-brief no-reminders   # Skip Apple Reminders (non-macOS)
```

**Customization:** Weather city, timezone, email delivery, triage integration, goal alignment via `goals.yaml`, deep work nudges, reminder platform.

---

### /prompt — Format and Execute
`[First Session]`

**What it does:** Takes an informal, conversational request and reformats it into a structured prompt, then executes it. Especially powerful with dictation (Wispr Flow).

**MCP dependencies:** None for formatting. Uses whatever MCP tools the *executed* prompt requires.

**Install (full bundle — 4 files):**
```bash
mkdir -p ~/.claude/commands/prompt-references

curl -o ~/.claude/commands/prompt.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/prompt.md
curl -o ~/.claude/commands/prompt-only.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/prompt-only.md
curl -o ~/.claude/commands/prompt-refine.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/prompt-refine.md
curl -o ~/.claude/commands/prompt-references/formatting-core.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/prompt-references/formatting-core.md
```

**Usage:**
```
/prompt Draft an email to the team about the schedule change
/prompt depth:deep Write a methodology section for the grant proposal
```

**Variants:**

- **`/prompt-only`** — Same formatting, outputs without executing. Use when building reusable prompts or running in another tool.
- **`/prompt-refine`** — Audits an existing prompt against a quality checklist and outputs an improved version.

**Customization:** Personal style preferences file, tool routing table, depth defaults.

---

### /review-plan — Plan Review
`[First Session]`

**What it does:** Stress-tests a plan with structured expert critique. Auto-detects domain, assigns an expert persona, researches best practices, provides red/yellow/green assessment.

**MCP dependencies:** Web search (optional, for best-practice research).

**Install:**
```bash
curl -o ~/.claude/commands/review-plan.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/review-plan.md
```

**Usage:**
```
/review-plan                                    # Review the most recent plan
/review-plan file:~/Documents/plan.md           # Review a specific file
/review-plan quick                              # Skip web research
/review-plan depth:deep focus:feasibility       # Deep review on feasibility
```

**Customization:** Expert role mapping, local reference files, focus weight defaults.

---

### /revise-proposal — Proposal Revision
`[PM]`

**What it does:** Applies reviewer, collaborator, or self-review feedback to an existing proposal draft while maintaining voice consistency. Handles dictated feedback, comment files, and formal reviewer comments (with categorization).

**MCP dependencies:** None required. Google Docs MCP optional for project context.

**Install:**
```bash
curl -o ~/.claude/commands/revise-proposal.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/revise-proposal.md
```

**Usage:**
```
# Self-review — dictate feedback directly
/revise-proposal 05_Submissions/Grants/Draft.md
Tighten the intro. Cut 200 words from methodology.

# Collaborator feedback from file
/revise-proposal Draft.md comments:~/Downloads/feedback.txt

# Formal reviewer comments (shows categorization before applying)
/revise-proposal Draft.md reviewer:~/Downloads/reviews.pdf
```

**Customization:** Voice pack path, donor profile directory, backup behavior.

---

### /schedule-query — Calendar Availability
`[EA]`

**What it does:** Checks calendar availability across all Google calendars and drafts a scheduling reply with specific time proposals.

**MCP dependencies:** Google Calendar MCP (required). Gmail MCP (optional, for sending reply).

**Install:**
```bash
curl -o ~/.claude/commands/schedule-query.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/schedule-query.md

mkdir -p ~/.claude-assistant/config
curl -o ~/.claude-assistant/config/calendar-policy.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/calendar-policy-template.md
```

**Usage:**
```
/schedule-query with:Jane duration:60
/schedule-query range:7               # Look 7 days ahead
/schedule-query email:msg_id          # Reply to a scheduling email
```

**Customization:** Calendar IDs, working hours, deep work protection, reply tone templates.

---

### /setup-project-management — Project Setup
`[PM]`

**What it does:** Initializes a project management system for a research project. Interactive discovery, gap analysis, and design discussion before creating any files.

**MCP dependencies:** None required. Google Docs MCP useful for document hub setup.

**Install:**
```bash
curl -o ~/.claude/commands/setup-project-management.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/setup-project-management.md
```

**Usage:**
```
/setup-project-management              # Full interactive setup
/setup-project-management discover     # Assessment only
/setup-project-management plan         # Propose plan, stop before implementing
/setup-project-management minimal      # Quick setup: just .claude/CLAUDE.md
```

**Customization:** Project types (quantitative, qualitative, theory/writing), folder naming conventions, external storage integration.

---

### /todo-add — Add To-Do Item
`[EA]`

**What it does:** Adds a to-do item to the correct list with duplicate checking. Routes items based on keywords.

**MCP dependencies:** None.

**Install:**
```bash
curl -o ~/.claude/commands/todo-add.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/todo-add.md
```

**Usage:**
```
/todo-add Fix the authentication bug
/todo-add list:work Set up CI pipeline
```

!!! note "Session-scoped tasks"
    `/todo-add`, `/todo-review`, and `/todo-queue` manage Claude Code's *session-level* task tracking. They do **not** replace Apple Reminders, Google Tasks, or Todoist for persistent action items. Use your real reminder system for durable tasks; use these for within-session work management.

---

### /todo-queue — Todo Queue
`[EA]`

**What it does:** Batch-processes emails in a designated Gmail label, converting them to Apple Reminders with timing extracted from email body.

**MCP dependencies:** Gmail MCP. Apple Reminders via osascript (macOS only).

**Install:**
```bash
curl -o ~/.claude/commands/todo-queue.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/todo-queue.md
```

**Usage:**
```
/todo-queue              # Process all pending
/todo-queue dryrun       # Preview only
/todo-queue limit:5      # Process first 5 only
```

---

### /todo-review — To-Do Review
`[EA]`

**What it does:** Reviews and consolidates to-do items across all configured files. Duplicate detection and batch actions.

**MCP dependencies:** None.

**Install:**
```bash
curl -o ~/.claude/commands/todo-review.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/todo-review.md
```

**Usage:**
```
/todo-review           # Quick summary (high priority only)
/todo-review full      # All priority levels
```

---

### /triage-inbox — Smart Inbox Triage
`[EA]`

**What it does:** Scans inbox for emails to auto-label and archive — newsletters, announcements, receipts, low-priority notifications. Uses heuristics that Gmail filters can't (List-Unsubscribe detection, body analysis, multi-signal scoring).

**MCP dependencies:** Gmail MCP (required).

**Install:**
```bash
curl -o ~/.claude/commands/triage-inbox.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/triage-inbox.md

mkdir -p ~/.claude-assistant/config ~/.claude-assistant/state ~/.claude-assistant/logs
curl -o ~/.claude-assistant/config/email-policy.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/email-policy-template.md
curl -o ~/.claude-assistant/config/triage-config.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/triage-config-template.md
```

**Usage:**
```
/triage-inbox                    # Scan, report, and apply labels
/triage-inbox noapply            # Preview only
/triage-inbox days:14            # Scan last 14 days
```

**Customization:** VIP list, label IDs, vendor domains, score thresholds, manual overrides.

---

### /weekly-review — Weekly Project Review
`[PM]`

**What it does:** Generates a comprehensive weekly summary for a research project, pulling from WhatsApp, meeting transcripts, Gmail, and working documents. Produces a project dashboard and detailed weekly log, writing directly to Google Docs.

**MCP dependencies:** Google Docs MCP (required). Gmail MCP (recommended). WhatsApp MCP (optional). Granola (optional, for transcripts).

**Install:**
```bash
curl -o ~/.claude/commands/weekly-review.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/weekly-review.md
```

**Usage:**
```
/weekly-review                    # Full review, default date range
/weekly-review days:14            # Last 14 days
/weekly-review tab1only           # Quick dashboard update
/weekly-review skipwhatsapp       # Skip WhatsApp if unavailable
```

**Customization:** Data sources, date range logic, dashboard template (quantitative vs. qualitative projects), synthesis detail level, email filtering keywords.

---

### /write-proposal — Proposal Drafting
`[PM]`

**What it does:** Drafts a funding proposal from structured inputs — application template, research design, project context, and donor intelligence. Auto-gathers context from the project record and enforces voice consistency.

**MCP dependencies:** None required. Google Docs MCP recommended for project context. Gmail MCP optional for related correspondence.

**Install:**
```bash
curl -o ~/.claude/commands/write-proposal.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/write-proposal.md
```

**Usage:**
```
/write-proposal "Example Foundation" deadline:2026-06-01
/write-proposal "Impact Funder" template:~/Downloads/template.pdf budget:150000
/write-proposal "Foundation X" resubmission
/write-proposal "Foundation Y" dryrun
```

**Customization:** Voice pack path and style, donor profile directory, context gathering sources, word budgets, default proposal structure.

---

## Agents

Agents are subprocesses that Claude Code launches for specialized tasks. They run in fresh context (avoiding blind spots of the main session) and return structured results.

### Writing Reviewer
`[PM]`

**What it does:** Reviews academic prose for clarity, argument structure, evidence integration, and voice consistency.

**Install:**
```bash
curl -o ~/.claude/agents/writing-reviewer.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/agents/writing-reviewer.md
```

**Usage:** "Launch the writing reviewer agent on my draft at ~/Documents/paper-draft.md"

---

### Methodology Reviewer
`[PM]`

**What it does:** Reviews empirical social science papers for causal language accuracy, identification strategy soundness, statistical practice, and robustness discussion.

**Install:**
```bash
curl -o ~/.claude/agents/methodology-reviewer.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/agents/methodology-reviewer.md
```

**Usage:** "Launch the methodology reviewer on sections 3-5 of the paper draft"

---

## Templates

### CLAUDE.md Template

A starter CLAUDE.md file with all common sections. See [Your CLAUDE.md](../toolkit/claude-md.md) for the full setup guide.

```bash
curl -o ~/.claude/CLAUDE.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/claude-md-template.md
```

### Goals Template

YAML file for tracking goals, projects, and priorities. Referenced by skills that need to know what you're working on.

```bash
curl -o ~/.claude/goals.yaml \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/goals-yaml-template.yaml
```

### Email Policy Template

Email handling rules: VIP contacts, auto-archive patterns, label routing. Required by `/triage-inbox` and `/morning-brief`.

```bash
mkdir -p ~/.claude-assistant/config
curl -o ~/.claude-assistant/config/email-policy.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/email-policy-template.md
```

### Triage Config Template

Gmail label-to-ID mapping and classification rules. Required by `/triage-inbox` and `/morning-brief`.

```bash
mkdir -p ~/.claude-assistant/config
curl -o ~/.claude-assistant/config/triage-config.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/triage-config-template.md
```

### Calendar Policy Template

Calendar IDs, scheduling preferences, timezone, deep work protection. Required by `/schedule-query` and `/morning-brief`.

```bash
mkdir -p ~/.claude-assistant/config
curl -o ~/.claude-assistant/config/calendar-policy.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/calendar-policy-template.md
```
