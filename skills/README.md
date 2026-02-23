# Skills & Agents

Downloadable skills (slash commands) and agents for Claude Code.

## Quick Install

Skills go in `~/.claude/commands/`. Agents go in `~/.claude/agents/`.

```bash
# Create directories
mkdir -p ~/.claude/commands
mkdir -p ~/.claude/agents

# Download a skill
curl -o ~/.claude/commands/done.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/skills/done.md

# Download an agent
curl -o ~/.claude/agents/review-writing.md \
  https://raw.githubusercontent.com/chrisblattman/claudeblattman/main/agents/review-writing.md
```

Restart Claude Code after adding new commands.

## Available Skills

| Skill | Command | Dependencies | Description |
|-------|---------|-------------|-------------|
| **Check-In Session** | `/checkin` | Gmail MCP, Calendar MCP, goals.yaml | Interactive daily check-in: inbox triage, reminder triage, meeting prep, email drafting, priorities |
| **Session Capture** | `/done` | None | Captures decisions, questions, and follow-ups from the current session |
| **Goals Review** | `/goals-review` | goals.yaml | Review and update quarterly objectives, progress scores, and deadlines |
| **Morning Briefing** | `/morning-brief` | Gmail MCP, Calendar MCP | Daily briefing: calendar, reminders, inbox highlights, VIP tracking, goal alignment, optional triage |
| **Prompt Formatter** | `/prompt` | formatting-core.md | Formats informal requests into structured prompts, then executes |
| **Prompt Only** | `/prompt-only` | formatting-core.md | Formats prompts without executing (for use in other tools) |
| **Prompt Refine** | `/prompt-refine` | formatting-core.md | Reviews and improves existing prompts |
| **Proposal Revision** | `/proposal-revise` | None | Applies reviewer/collaborator feedback to proposal drafts |
| **Proposal Writing** | `/proposal-write` | None | Drafts funding proposals from structured inputs and project context |
| **Plan Review** | `/review-plan` | None (web search optional) | Structured expert critique of plans |
| **Schedule Query** | `/schedule-query` | Calendar MCP | Checks calendar availability and drafts scheduling replies |
| **Project Setup** | `/setup-project-management` | None | Initializes project management system for research projects |
| **Add To-Do** | `/todo-add` | None | Adds a to-do item to the correct list with duplicate checking |
| **Todo Queue** | `/todo-queue` | Gmail MCP, Apple Reminders | Batch-processes emails into Apple Reminders with timing extraction |
| **Todo Review** | `/todo-review` | None | Reviews and consolidates to-do items across configured files |
| **Inbox Triage** | `/triage-inbox` | Gmail MCP | Smart email classification with heuristics Gmail filters can't replicate |
| **Weekly Review** | `/weekly-review` | Google Docs MCP | Comprehensive weekly project summary from multiple data sources |

## Available Agents

| Agent | Description | Model |
|-------|-------------|-------|
| **Writing Reviewer** | Reviews academic prose for clarity, structure, and voice | Sonnet |
| **Methodology Reviewer** | Checks empirical claims, causal language, and identification strategy | Sonnet |

## The Prompt Bundle

The `/prompt`, `/prompt-only`, and `/prompt-refine` skills share a companion file: `formatting-core.md`. Install all four files together:

```bash
# Install the prompt family
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

## Templates

| Template | Description |
|----------|-------------|
| `claude-md-template.md` | Starter CLAUDE.md file with all common sections |
| `goals-yaml-template.yaml` | Goals and priorities tracking file (OKR format with weighted objectives) |

## Customization

Each skill is designed to work out of the box but can be customized. See the [Skill Library](https://claudeblattman.com/toolkit/skill-library/) on the website for customization guidance.
