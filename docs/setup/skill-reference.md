# Skill Library

All downloadable skills, agents, and templates. Each entry includes installation commands, usage examples, and customization guidance.

**Workflow tags:** Skills are tagged by which workflow they belong to — `[PM]` for [Project Management](../workflows/project-management.md), `[EA]` for [Executive Assistant](../toolkit/executive-assistant.md), `[First Session]` for [First Session Skills](../workflows/first-session-skills.md), `[Advanced]` for [system-level tools](../system/continuous-improvement.md).

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

### /checkin — Daily Check-In Session
`[EA]`

**What it does:** Interactive chief-of-staff session that combines inbox triage, reminder triage, meeting prep, email quick-fire drafting, and priority management into one 10-15 minute session. Where `/morning-brief` is a passive daily report, `/checkin` is an interactive session — it triages your inbox, triages your reminders, preps meetings, drafts emails, and surfaces priorities.

**MCP dependencies:** Gmail MCP (required). Google Calendar MCP (required). Granola MCP (optional, for meeting context). Apple Reminders via osascript (macOS, optional).

**Prerequisite skills:** `/triage-inbox` (recommended — without it, the triage phase is skipped).

**Install:**
```bash
curl -o ~/.claude/commands/checkin.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/checkin.md

# Config templates (if not already installed via /triage-inbox or /morning-brief)
mkdir -p ~/.claude-assistant/config
curl -o ~/.claude-assistant/config/email-policy.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/email-policy-template.md
curl -o ~/.claude-assistant/config/calendar-policy.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/calendar-policy-template.md
curl -o ~/.claude-assistant/config/triage-config.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/triage-config-template.md
curl -o ~/.claude-assistant/config/goals.yaml \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/goals-yaml-template.yaml
```

!!! note "If you already set up `/triage-inbox` and `/morning-brief`"
    Most config files are already in place. You only need the skill file itself and possibly `goals.yaml`.

**Usage:**
```
/checkin              # Full interactive session (10-15 min)
/checkin quick        # Status + priorities only (30 seconds)
/checkin no-email     # Skip email drafting phase
/checkin no-triage    # Skip inbox triage
/checkin tomorrow     # Preview tomorrow's schedule
```

**Customization:**

| Setting | Where to Configure | Default |
|---------|-------------------|---------|
| **Model** | Frontmatter `model:` line | `sonnet` (remove to use default) |
| **VIP list** | `email-policy.md` | No VIP highlighting |
| **Calendar IDs** | `calendar-policy.md` | Primary only |
| **Goal alignment** | `goals.yaml` | Section omitted |
| **Push level** | `goals.yaml` → `meta.push_level` | `moderate` |
| **Auto-triage** | Requires `/triage-inbox` | Skipped |
| **Reminders** | Requires macOS | Phase skipped |

---

### /goals-review — Goals Review
`[PM]`

**What it does:** Reviews quarterly objectives, updates progress scores, surfaces deadlines, and recalibrates priorities. Manages the `goals.yaml` file that `/checkin` and `/morning-brief` read for goal alignment.

**MCP dependencies:** All optional. Gmail MCP (for email evidence). Google Calendar MCP (for meeting evidence). Granola MCP (for transcript evidence). Apple Reminders (macOS, for task evidence).

**Install:**
```bash
curl -o ~/.claude/commands/goals-review.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/goals-review.md

# Goals template (if not already installed)
mkdir -p ~/.claude-assistant/config
curl -o ~/.claude-assistant/config/goals.yaml \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/goals-yaml-template.yaml
```

**Usage:**
```
/goals-review              # Full review with interactive updates
/goals-review status       # Quick dashboard only
/goals-review deadlines    # Show upcoming deadlines only
```

**Customization:**

| Setting | Where to Configure | Default |
|---------|-------------------|---------|
| **Model** | Frontmatter `model:` line | `sonnet` (remove to use default) |
| **Objectives** | `goals.yaml` → objectives | Template examples |
| **Push level** | `goals.yaml` → `meta.push_level` | `moderate` |
| **Review frequency** | Skill Step 5 | Biweekly (14 days) |

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

### /proposal-revise — Proposal Revision
`[PM]`

**What it does:** Applies reviewer, collaborator, or self-review feedback to an existing proposal draft while maintaining voice consistency. Handles dictated feedback, comment files, and formal reviewer comments (with categorization).

**MCP dependencies:** None required. Google Docs MCP optional for project context.

**Install:**
```bash
curl -o ~/.claude/commands/proposal-revise.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/proposal-revise.md
```

**Usage:**
```
# Self-review — dictate feedback directly
/proposal-revise 05_Submissions/Grants/Draft.md
Tighten the intro. Cut 200 words from methodology.

# Collaborator feedback from file
/proposal-revise Draft.md comments:~/Downloads/feedback.txt

# Formal reviewer comments (shows categorization before applying)
/proposal-revise Draft.md reviewer:~/Downloads/reviews.pdf
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

### /tips-curate — Tip Curation
`[Advanced]`

**What it does:** Processes @ToSelf emails containing tips and research. Quality-filters (High/Medium/Low), enriches via web research, presents recommendations for approval, appends to a searchable tips log.

**MCP dependencies:** Gmail MCP (required).

**Install:**
```bash
curl -o ~/.claude/commands/tips-curate.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/tips-curate.md
```

**Usage:**
```
/tips-curate              # Process first 5 unread @ToSelf emails
/tips-curate dryrun       # Preview classifications without saving or marking
/tips-curate limit:3      # Process 3 at a time
/tips-curate all          # Loop through all unread in batches of 5
```

**Customization:** Quality thresholds, tip format, log file location (default `~/.claude-assistant/tips/collected-tips-log.md`), @ToSelf label name.

**Learn more:** [Continuous Improvement](../system/continuous-improvement.md)

---

### /tips-integrate — Tip Integration
`[Advanced]`

**What it does:** Converts collected tips into concrete system improvements — direct config edits or investigation tasks. Tracks what has been processed to avoid re-proposing.

**MCP dependencies:** None (filesystem only).

**Install:**
```bash
mkdir -p ~/.claude/commands/tips-integrate-references

curl -o ~/.claude/commands/tips-integrate.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/tips-integrate.md

curl -o ~/.claude/commands/tips-integrate-references/scanning-rules.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/tips-integrate-references/scanning-rules.md
```

**Usage:**
```
/tips-integrate              # Scan all sources
/tips-integrate source:tips  # Only scan tips log (includes medium-rated items)
/tips-integrate dryrun       # Preview proposals without writing
/tips-integrate since:2026-02-01  # Only items after this date
```

**Customization:** Source selection, state file location (default `~/.claude-assistant/state/integrate-state.json`), target config files.

**Learn more:** [Continuous Improvement](../system/continuous-improvement.md)

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

### /proposal-write — Proposal Drafting
`[PM]`

**What it does:** Drafts a funding proposal from structured inputs — application template, research design, project context, and donor intelligence. Auto-gathers context from the project record and enforces voice consistency.

**MCP dependencies:** None required. Google Docs MCP recommended for project context. Gmail MCP optional for related correspondence.

**Install:**
```bash
curl -o ~/.claude/commands/proposal-write.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/proposal-write.md
```

**Usage:**
```
/proposal-write "Example Foundation" deadline:2026-06-01
/proposal-write "Impact Funder" template:~/Downloads/template.pdf budget:150000
/proposal-write "Foundation X" resubmission
/proposal-write "Foundation Y" dryrun
```

**Customization:** Voice pack path and style, donor profile directory, context gathering sources, word budgets, default proposal structure.

---

## Agents

Agents are subprocesses that Claude Code launches for specialized tasks. They run in fresh context (avoiding blind spots of the main session) and return structured results.

### Review Writing
`[PM]`

**What it does:** Reviews academic prose for clarity, argument structure, evidence integration, and voice consistency.

**Install:**
```bash
curl -o ~/.claude/agents/review-writing.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/agents/review-writing.md
```

**Usage:** "Launch the review-writing agent on my draft at ~/Documents/paper-draft.md"

---

### Review Methodology
`[PM]`

**What it does:** Reviews empirical social science papers for causal language accuracy, identification strategy soundness, statistical practice, and robustness discussion.

**Install:**
```bash
curl -o ~/.claude/agents/review-methodology.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/agents/review-methodology.md
```

**Usage:** "Launch the review-methodology agent on sections 3-5 of the paper draft"

---

## Templates

### CLAUDE.md Template

A starter CLAUDE.md file with all common sections. See [Your CLAUDE.md](../toolkit/claude-md.md) for the full setup guide.

```bash
curl -o ~/.claude/CLAUDE.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/claude-md-template.md
```

### Goals Template

YAML file for tracking quarterly objectives with weighted OKR format. Referenced by `/checkin`, `/morning-brief`, and `/goals-review` for goal alignment, stalled-goal detection, and progress tracking.

```bash
mkdir -p ~/.claude-assistant/config
curl -o ~/.claude-assistant/config/goals.yaml \
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
