# Download Skills

*Reading time: 12 minutes*

Downloadable skills (slash commands) and agents for Claude Code. Each one is a markdown file you save to your commands folder.

---

## Start With These 3

New to skills? Install these first — they're the most universally useful and have no external dependencies.

<div class="grid cards" markdown>

-   **:material-check-circle-outline: /done — Session Capture**

    ---

    Captures decisions, questions, and follow-ups from your work session. Run it every time you finish working. Builds searchable history across sessions.

    *No MCP needed*

    [:octicons-arrow-right-24: Install & details](#done-session-capture)

-   **:material-format-text: /prompt — Format & Execute**

    ---

    Takes your rough, conversational request and turns it into a structured prompt — then executes it. Essential for dictation users. Comes with 3 variants.

    *No MCP needed*

    [:octicons-arrow-right-24: Install & details](#prompt-format-and-execute)

-   **:material-clipboard-check-outline: /review-plan — Plan Review**

    ---

    Stress-tests any plan with expert critique. Auto-detects the domain, assigns a reviewer persona, flags red/yellow/green issues. Catches blind spots.

    *Web search optional*

    [:octicons-arrow-right-24: Install & details](#review-plan-plan-review)

</div>

---

## Browse All Skills & Agents

<div class="grid cards" markdown>

-   :material-check-circle-outline: **[/done](#done-session-capture)** — Session capture
    { .card-mini }

-   :material-format-text: **[/prompt](#prompt-format-and-execute)** — Format & execute prompts
    { .card-mini }

-   :material-format-text: **[/prompt-only](#prompt-only-format-without-executing)** — Format without executing
    { .card-mini }

-   :material-format-text: **[/prompt-refine](#prompt-refine-review-and-improve-a-prompt)** — Improve existing prompts
    { .card-mini }

-   :material-clipboard-check-outline: **[/review-plan](#review-plan-plan-review)** — Stress-test plans
    { .card-mini }

-   :material-folder-cog-outline: **[/setup-project-management](#setup-project-management-project-setup)** — Initialize project tracking
    { .card-mini }

-   :material-plus-circle-outline: **[/todoa](#todoa-add-to-do-item)** — Add a to-do item
    { .card-mini }

-   :material-format-list-checks: **[/todor](#todor-to-do-review)** — Review all to-do items
    { .card-mini }

-   :material-email-fast-outline: **[/todoq](#todoq-todo-queue)** — Email-to-reminder queue
    { .card-mini }

-   :material-inbox-arrow-down: **[/triage-inbox](#triage-inbox-smart-inbox-triage)** — Smart email triage
    { .card-mini }

-   :material-calendar-search: **[/schedule-query](#schedule-query-calendar-availability)** — Calendar availability
    { .card-mini }

-   :material-weather-sunny: **[/morning-brief](#morning-brief-daily-briefing)** — Daily morning briefing
    { .card-mini }

-   :material-draw-pen: **[Writing Reviewer](#writing-reviewer)** — Academic prose QA (agent)
    { .card-mini }

-   :material-flask-outline: **[Methodology Reviewer](#methodology-reviewer)** — Empirical methods QA (agent)
    { .card-mini }

-   :material-file-document-outline: **[CLAUDE.md Template](#claudemd-template)** — Starter config file
    { .card-mini }

-   :material-bullseye-arrow: **[Goals Template](#goals-template)** — Project & priority tracker
    { .card-mini }

-   :material-email-edit-outline: **[Email Policy Template](#email-policy-template)** — Email handling rules
    { .card-mini }

-   :material-tag-multiple-outline: **[Triage Config Template](#triage-config-template)** — Gmail label & classification config
    { .card-mini }

-   :material-calendar-edit: **[Calendar Policy Template](#calendar-policy-template)** — Scheduling preferences
    { .card-mini }

</div>

---

## Quick Setup

```bash
# Create the directories (if they don't exist)
mkdir -p ~/.claude/commands
mkdir -p ~/.claude/agents
```

After saving any new skill file, **restart Claude Code** for the command to become available.

---

## Skills

### /done — Session Capture

**What it does:** Captures key decisions, open questions, and follow-ups from your current Claude Code session. Writes a structured entry to a session log file. Run at the end of any substantive work session.

**MCP dependencies:** None — pure filesystem operation.

**When to use:** End of any work session where you made decisions, raised questions, or committed to next steps. Builds a searchable history of what you've done across sessions.

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

??? note "View full skill file"
    ```markdown
    --8<-- "https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/done.md"
    ```
    [Download from GitHub](https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/done.md)

**Customization points:**

- **Log file location:** The default is `~/Documents/session-log.md`. Change this to wherever you want your session history (e.g., a project folder, a synced directory).
- **Project matching:** Add logic to match against a projects list in your CLAUDE.md or a goals.yaml file, so sessions auto-tag by project.
- **Handoff file location:** The default handoff note goes to `~/.claude/handoff.md`. This is read by SessionStart hooks for next-session context.
- **Archive pruning:** v1.1 auto-prunes entries older than 60 days. Adjust the threshold in the Maintenance step.

---

### /prompt — Format and Execute

**What it does:** Takes an informal, conversational request (often dictated) and reformats it into a structured prompt, then executes it. Bridges the gap between how you naturally speak and what gets the best AI output.

**MCP dependencies:** None for formatting. Uses whatever MCP tools the *executed* prompt requires.

**When to use:** Anytime you want to give Claude a rough instruction and have it formalized before execution. Especially powerful with dictation (Wispr Flow) — dictate a rambling request, get a crisp prompt, get a crisp answer.

**Install (full bundle — all 4 files):**
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

!!! info "About `@` references"
    The prompt skills use `@path/to/file` syntax to load the shared `formatting-core.md` at runtime. This is a Claude Code feature — it injects the referenced file's contents into the skill's context. The skills reference `@~/.claude/commands/prompt-references/formatting-core.md`, which is where the bundle install puts it. If the file is missing, the skills still work but lose the shared formatting rules and depth calibration logic.

**Usage:**
```
/prompt Draft an email to the team about the schedule change
/prompt depth:deep Write a methodology section for the grant proposal
/prompt hold Just format this, don't execute yet
```

**Customization points:**

- **Personal style preferences:** The generic version has no `@` reference to a personal preferences file. To add one, create `~/.claude/commands/prompt-references/my-preferences.md` with your writing style, tone, and formatting preferences, then add `@~/.claude/commands/prompt-references/my-preferences.md` to the Reference Files section of each prompt skill.
- **Tool routing:** The formatting-core.md file includes a tool-routing table (when to suggest ChatGPT, Perplexity, etc.). Customize this based on which tools you actually use.
- **Depth defaults:** If you find yourself always overriding to `depth:standard`, change the default in formatting-core.md.

---

### /prompt-only — Format Without Executing

**What it does:** Same formatting as `/prompt`, but outputs the structured prompt without executing it. Use when you want to run the prompt in a different tool (Claude.ai, ChatGPT) or save it for later.

**Included in the prompt bundle above.** See `/prompt` for installation.

**Usage:**
```
/prompt-only Write a literature review on cash transfers and crime
```

---

### /prompt-refine — Review and Improve a Prompt

**What it does:** Takes an existing prompt and audits it against a quality checklist — depth calibration, clarity, constraints, format specification, anti-patterns. Outputs an improved version with a changelog.

**Included in the prompt bundle above.** See `/prompt` for installation.

**Usage:**
```
/prompt-refine [paste your existing prompt here]
```

---

### /review-plan — Plan Review

**What it does:** Stress-tests a plan with structured expert critique. Auto-detects the domain, assigns an appropriate expert persona, researches best practices, and provides a red/yellow/green assessment with specific recommendations.

**MCP dependencies:** Web search (optional, for best-practice research). Works without it but the review is less grounded.

**When to use:** After developing any plan — project plans, research designs, implementation strategies, skill architectures. Catches blind spots, missing steps, and wishful thinking.

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
/review-plan depth:deep focus:feasibility       # Deep review, weighted toward feasibility
/review-plan role:"grant strategy specialist"   # Override expert role
```

**Customization points:**

- **Expert role mapping:** The default maps domain keywords to expert roles. Add your own mappings for domains you work in frequently.
- **Local references:** Add `@` references to your own style guides or standards documents for domain-specific reviews.
- **Focus weights:** If you always want extra focus on one dimension (e.g., feasibility), adjust the default.

---

### /setup-project-management — Project Setup

**What it does:** Initializes a project management system for a research project. Walks through discovery, gap analysis, and design discussion before creating any files. Adapts to your existing folder structure rather than forcing a template.

**MCP dependencies:** None required. Google Docs MCP useful for setting up a document hub.

**When to use:** When starting a new research project or bringing an existing project under management. Especially useful for projects with teams, external data sources, or complex folder structures.

**Install:**
```bash
curl -o ~/.claude/commands/setup-project-management.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/setup-project-management.md
```

**Usage:**
```
/setup-project-management              # Full interactive setup
/setup-project-management discover     # Assessment only, no changes
/setup-project-management plan         # Propose plan, stop before implementing
/setup-project-management minimal      # Quick setup: just .claude/CLAUDE.md
```

**Customization points:**

- **Project types:** The default supports Quantitative RCT, Qualitative/Ethnographic, and Theory/Writing. Add your own project types with custom folder structures.
- **Folder naming:** Uses numbered folders (01_Paper, 02_Presentations...) by default. Configure to match your conventions.
- **External sources:** Add sections for your institutional storage (Box, S3, shared drives) with guidance on what to sync locally vs. access on-demand.

---

### /todoa — Add To-Do Item

**What it does:** Adds a new to-do item to the correct list with duplicate checking. Routes items to configurable lists based on keywords and suggests priority.

**MCP dependencies:** None — pure filesystem operation.

**When to use:** Quick task capture from within Claude Code. Supports multiple to-do lists with keyword-based routing (e.g., email tasks go to one list, documentation tasks to another).

**Install:**
```bash
curl -o ~/.claude/commands/todoa.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/todoa.md
```

**Usage:**
```
/todoa Fix the authentication bug
/todoa list:work Set up CI pipeline
```

**Customization points:**

- **File locations:** Default is `~/Documents/todo.md`. Configure one or multiple to-do files.
- **Keyword routing:** Define which keywords route to which list (e.g., "email" → work list, "docs" → training list).
- **Priority mapping:** Customize High/Medium/Low definitions or add your own levels.

---

### /todor — To-Do Review

**What it does:** Reviews and consolidates to-do items across all your configured to-do files. Shows a summary with duplicate detection and offers actions (reprioritize, mark complete, add new, remove duplicate).

**MCP dependencies:** None — pure filesystem operation.

**When to use:** Regular task review — see all your to-dos in one view, find duplicates across lists, and take batch actions.

**Install:**
```bash
curl -o ~/.claude/commands/todor.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/todor.md
```

**Usage:**
```
/todor           # Quick summary (high priority only)
/todor full      # All priority levels
```

**Customization points:**

- **File locations:** Configure which to-do files to scan.
- **Priority sections:** Map your section headers to priority levels.
- **Quick vs. full mode:** Customize which sections appear in each mode.

---

### /todoq — Todo Queue

**What it does:** Batch-processes emails in a designated Gmail label, converting them to Apple Reminders with timing extracted from the email body. Forward any email to yourself with timing syntax (e.g., `due:Friday list:Personal`) and this skill processes the queue.

**MCP dependencies:** Gmail MCP (search, read, modify labels). Apple Reminders via osascript (macOS only).

**When to use:** Processing a batch of self-sent reminder emails. Works with the Gmail `+` alias trick — emails sent to `your-email+todo@gmail.com` auto-label and queue up.

**Install:**
```bash
curl -o ~/.claude/commands/todoq.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/todoq.md
```

!!! warning "macOS only"
    This skill uses `osascript` to create Apple Reminders. It won't work on Linux or Windows without modification.

**First-time setup:**

1. Create a Gmail label called `@ToSelf`
2. Create a filter: emails to `your-email+todo@gmail.com` → apply `@ToSelf` label
3. Note the label ID (run `list_gmail_labels` via MCP to find it)
4. Update the label ID in the skill file

**Usage:**
```
/todoq              # Process all pending
/todoq dryrun       # Preview only
/todoq limit:5      # Process first 5 only
```

**Customization points:**

- **Gmail alias:** Set up your `+todo` address for email-to-task capture.
- **Reminder lists:** Configure which Apple Reminder lists to use (Work, Personal, Someday).
- **Default time:** Change the default reminder time from 9am.
- **Label ID:** Replace `YOUR_LABEL_ID` with your actual Gmail label ID.

---

### /triage-inbox — Smart Inbox Triage

**What it does:** Scans your inbox for emails that should be auto-labeled and archived — newsletters, announcements, receipts, and low-priority notifications. Uses header and content heuristics that Gmail filters can't do (List-Unsubscribe detection, body text analysis, multi-signal scoring).

**MCP dependencies:** Gmail MCP (search, read, batch modify labels, create filters).

**When to use:** Daily inbox cleanup. Catches new and unfamiliar senders that don't have permanent Gmail filters yet. Over time, you'll build permanent filters for the most common senders.

**Install (skill + config files):**
```bash
# Install the skill
curl -o ~/.claude/commands/triage-inbox.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/triage-inbox.md

# Create config directory and download templates
mkdir -p ~/.claude-assistant/config
mkdir -p ~/.claude-assistant/state
mkdir -p ~/.claude-assistant/logs

curl -o ~/.claude-assistant/config/email-policy.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/email-policy-template.md

curl -o ~/.claude-assistant/config/triage-config.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/triage-config-template.md
```

!!! info "Setup required"
    Before using this skill, you must fill in your config files: add your VIP list to `email-policy.md`, and add your Gmail label IDs to `triage-config.md`. See the template files for step-by-step instructions on finding label IDs.

**Usage:**
```
/triage-inbox                    # Scan, report, and apply labels
/triage-inbox noapply            # Preview only
/triage-inbox days:14            # Scan last 14 days
/triage-inbox limit:20           # Process first 20 emails
```

**Customization points:**

- **VIP list:** Define who should never be auto-triaged.
- **Label IDs:** Map your Gmail labels to the triage categories.
- **Vendor domains:** Add your common receipt/expense senders.
- **Score thresholds:** Tune how aggressive the classification is.
- **Override table:** Add manual sender→category overrides as you correct mistakes.

---

### /schedule-query — Calendar Availability

**What it does:** Checks calendar availability across all your Google calendars and drafts a scheduling reply with specific time proposals. Scores available slots by preference (morning deep work, meeting density, proximity).

**MCP dependencies:** Google Calendar MCP (get events). Gmail MCP (optional, for finding recipient email and sending reply).

**When to use:** When someone asks to meet and you need to propose times. Run standalone or as part of an email workflow.

**Install (skill + config):**
```bash
curl -o ~/.claude/commands/schedule-query.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/schedule-query.md

# If you haven't already:
mkdir -p ~/.claude-assistant/config

curl -o ~/.claude-assistant/config/calendar-policy.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/calendar-policy-template.md
```

!!! info "Setup required"
    Before using, fill in your calendar IDs and timezone in `calendar-policy.md`. See the template for instructions on finding Google Calendar IDs.

**Usage:**
```
/schedule-query with:Jane duration:60
/schedule-query range:7               # Look 7 days ahead
/schedule-query email:msg_id          # Reply to a scheduling email
```

**Customization points:**

- **Calendar IDs:** Add all calendars to check for conflicts.
- **Working hours:** Set your actual availability window and timezone.
- **Deep work protection:** Configure how aggressively to protect focus time.
- **Reply tone:** Customize scheduling reply templates for different formality levels.

---

### /morning-brief — Daily Briefing

**What it does:** Generates a comprehensive daily briefing combining calendar, reminders, inbox highlights, VIP tracking, overdue items, goal alignment, and optional auto-triage — all in one view. Can email the briefing to you as formatted HTML.

**MCP dependencies:** Gmail MCP (required). Google Calendar MCP (required). Apple Reminders via osascript (macOS, optional). Granola MCP (optional, for meeting context).

**When to use:** Start of your workday. Gives you a single view of everything that needs attention: today's schedule, urgent tasks, VIP emails, overdue items, and suggested priorities.

**Install (skill + all config files):**
```bash
curl -o ~/.claude/commands/morning-brief.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/morning-brief.md

# Create config directory (if not already done)
mkdir -p ~/.claude-assistant/config
mkdir -p ~/.claude-assistant/state
mkdir -p ~/.claude-assistant/logs

# Download all required config templates
curl -o ~/.claude-assistant/config/email-policy.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/email-policy-template.md

curl -o ~/.claude-assistant/config/calendar-policy.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/calendar-policy-template.md

curl -o ~/.claude-assistant/config/triage-config.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/triage-config-template.md

# Optional: goals file for goal alignment
curl -o ~/.claude-assistant/config/goals.yaml \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/goals-yaml-template.yaml
```

!!! info "Setup required"
    This skill needs all three config files filled in before first use. At minimum, set your calendar IDs and timezone in `calendar-policy.md` and your Gmail email in `email-policy.md`.

**Usage:**
```
/morning-brief                    # Full briefing
/morning-brief no-triage          # Skip auto-triage
/morning-brief email              # Also email the briefing to yourself
/morning-brief tomorrow           # Preview tomorrow's schedule
/morning-brief no-reminders       # Skip Apple Reminders (non-macOS)
```

**Customization points:**

- **Weather city:** Set your city in `calendar-policy.md` for the weather line.
- **Timezone:** All times display in your configured timezone.
- **Email delivery:** Opt-in — configure your email addresses to enable auto-emailing the briefing.
- **Triage integration:** Uses the same classification logic as `/triage-inbox`. Runs automatically unless `no-triage` is specified.
- **Goal alignment:** Reads `goals.yaml` to connect your schedule to your priorities.
- **Deep work nudges:** Configure `push_level` (gentle/moderate/assertive) for focus time protection.
- **Reminders:** macOS only (uses osascript). Skip with `no-reminders` on other platforms.

---

## Agents

Agents are subprocesses that Claude Code launches for specialized tasks. They run in a fresh context (avoiding the "blind spots" of the main session) and return results.

### Writing Reviewer

**What it does:** Reviews academic prose for clarity, argument structure, evidence integration, and voice consistency. Provides a structured assessment with specific rewrite suggestions.

**Install:**
```bash
curl -o ~/.claude/agents/writing-reviewer.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/agents/writing-reviewer.md
```

**Usage** (from within Claude Code):
> "Launch the writing reviewer agent on my draft at ~/Documents/paper-draft.md"

---

### Methodology Reviewer

**What it does:** Reviews empirical social science papers for causal language accuracy, identification strategy soundness, statistical practice, and robustness discussion. Evaluates with the rigor of a top-journal referee.

**Install:**
```bash
curl -o ~/.claude/agents/methodology-reviewer.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/agents/methodology-reviewer.md
```

**Usage:**
> "Launch the methodology reviewer on sections 3-5 of the paper draft"

---

## Templates

### CLAUDE.md Template

A starter CLAUDE.md file with all common sections. Fill in the bracketed fields and save to `~/.claude/CLAUDE.md`.

**Download:**
```bash
curl -o ~/.claude/CLAUDE.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/claude-md-template.md
```

See [Your CLAUDE.md](claude-md.md) for the full setup guide.

### Goals Template

A YAML file for tracking goals, projects, and priorities. Referenced by skills that need to know what you're working on.

**Download:**
```bash
curl -o ~/.claude/goals.yaml \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/goals-yaml-template.yaml
```

### Email Policy Template

Defines your email handling rules: VIP contacts (never auto-triaged), auto-archive patterns, and label routing. Required by `/triage-inbox` and `/morning-brief`.

**Download:**
```bash
mkdir -p ~/.claude-assistant/config
curl -o ~/.claude-assistant/config/email-policy.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/email-policy-template.md
```

### Triage Config Template

Technical configuration mapping Gmail label names to label IDs and defining classification rules (scoring thresholds, vendor domains, overrides). Required by `/triage-inbox` and `/morning-brief`.

**Download:**
```bash
mkdir -p ~/.claude-assistant/config
curl -o ~/.claude-assistant/config/triage-config.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/triage-config-template.md
```

### Calendar Policy Template

Calendar configuration with calendar IDs, scheduling preferences, timezone, deep work protection, and reply tone templates. Required by `/schedule-query` and `/morning-brief`.

**Download:**
```bash
mkdir -p ~/.claude-assistant/config
curl -o ~/.claude-assistant/config/calendar-policy.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/calendar-policy-template.md
```
