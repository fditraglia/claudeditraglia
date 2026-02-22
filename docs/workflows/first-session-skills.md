# First Session Skills

These skills require nothing but Claude Code. No MCP integrations, no configuration files, no external services. Install them, use them, get better results immediately.

---

## The idea

Most Claude Code skills need setup — connecting your email, configuring your calendar, defining your project structure. That's where the real power is, but it takes time.

These four skills work the moment you install them. They make every Claude Code interaction better, and they teach you how skills work before you invest in the deeper integrations.

---

## 1. Better Prompts — `/prompt`

**What it does:** Takes your rough, conversational request and reformats it into a structured prompt — then executes it. Bridges the gap between how you naturally speak and what gets the best AI output.

This is especially powerful with dictation. Dictate a rambling request, get a crisp prompt, get a crisp answer.

**Install (full bundle — 4 files):**

!!! note "What these commands do"
    `mkdir -p` creates a folder (and any parent folders needed). `curl -o` downloads a file from the internet and saves it to your computer at the path you specify. You're downloading skill files from this site's GitHub repository into Claude Code's commands folder.

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

- **`/prompt`** — Format and execute. Use this for most things.
- **`/prompt-only`** — Format without executing. Use when building reusable prompts or when you want to run the prompt in a different tool (Claude.ai, ChatGPT).
- **`/prompt-refine`** — Review and improve an existing prompt. Audits against a quality checklist and outputs an improved version with a changelog.

---

## 2. Plan Review — `/review-plan`

**What it does:** Stress-tests any plan with structured expert critique. Auto-detects the domain, assigns an appropriate expert persona, researches best practices, and provides a red/yellow/green assessment with specific recommendations.

Use it after developing any plan — project plans, research designs, implementation strategies, grant proposals. It catches blind spots, missing steps, and wishful thinking. Pairs well with Plan mode — see [How Claude Code Thinks](../setup/modes.md).

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
```

---

## 3. Session Capture — `/done`

**What it does:** Captures key decisions, open questions, and follow-ups from your current Claude Code session. Writes a structured entry to a session log file. Run it every time you finish working.

Over time, this builds a searchable history of what you've done across sessions. It also creates a handoff note so your next session starts with context.

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

---

## 4. Your CLAUDE.md

Not a skill — a configuration file. But it's the single most impactful thing you can set up.

Your CLAUDE.md tells Claude Code who you are, what you work on, and how you prefer to interact. Without it, every session starts from scratch. With it, Claude Code remembers your context, projects, preferences, and voice.

**Install:**
```bash
curl -o ~/.claude/CLAUDE.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/templates/claude-md-template.md
```

Then open `~/.claude/CLAUDE.md` in any text editor and fill in the bracketed fields.

See the [full CLAUDE.md setup guide](../toolkit/claude-md.md) for details on what to include and how to iterate on it over time.

---

## What's next

Once these are working, you have two paths:

- **[Executive Assistant](../toolkit/executive-assistant.md)** — Connect your email and calendar, build inbox triage and daily briefings
- **[Project Management](project-management.md)** — Set up project folders, meeting capture, weekly reviews, and proposal drafting

Both require MCP integrations (Gmail, Calendar, Google Docs). See the [MCP Setup guide](../toolkit/mcp-setup.md) to get started.
