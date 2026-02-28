# Initial Audit of claudeblattman (Forked Repo)

*Generated: 2026-02-28 by Claude, at Francis DiTraglia's request.*

**Status: Fact-finding only.** This document records first impressions from an
automated review of the forked repo. It is not a plan, not a set of decisions,
and not prescriptive. Observations here may turn out to be wrong, incomplete, or
irrelevant once real customization work begins.

---

## What the repo is

**Claude Blattman** is a free, open-source educational resource + toolkit by
Chris Blattman (political economist, UChicago Harris). It targets non-developers
— academics and professionals — who want to move beyond casual chatbot use and
build real productivity systems with Claude Code.

The repo serves two purposes:

1. **Documentation website.** `docs/` builds to claudeblattman.com via MkDocs
   Material, auto-deployed through GitHub Pages on every push to `main`.
2. **Downloadable skill library.** `skills/`, `agents/`, and `templates/`
   contain markdown files users `curl` into their `~/.claude/` directory.

Blattman's own Claude Code config lives in `~/.claude/` (gitignored). He
develops skills privately, sanitizes them (4-pass checklist in CONTRIBUTING.md),
and publishes generic versions here. The repo is a distribution channel, not his
working environment.

## Repo structure

```
claudeblattman/
├── docs/                  Website source (MkDocs Material, ~12k lines of markdown)
│   ├── essentials/        Chatbot fundamentals, prompting, tool guides
│   ├── setup/             Claude Code installation, VS Code, modes, skill reference
│   ├── toolkit/           CLAUDE.md guide, MCP setup, skills guide, exec assistant
│   ├── workflows/         Prompt-Plan-Review-Revise loop, project mgmt, examples
│   ├── system/            Building skills, agents vs skills, patterns, continuous improvement
│   ├── tax-workflow/      Complete tax-season case study
│   └── downloads/         Reference library
├── skills/                23 downloadable slash commands (markdown)
├── agents/                2 reviewer agents (writing, methodology)
├── templates/             5 starter configs (CLAUDE.md, goals.yaml, policies)
├── overrides/             MkDocs theme customizations
├── .github/workflows/     GitHub Actions deploy pipeline
├── mkdocs.yml             Site config
├── CONTRIBUTING.md        Maintenance guide + sanitization checklist
├── README.md              Project overview
└── LICENSE                MIT
```

## What it actually does (functional capabilities)

### Skills (23 slash commands)

| Category | Skills | What they do |
|---|---|---|
| Daily ops | `/checkin`, `/morning-brief`, `/triage-inbox` | Scan Gmail with adaptive time windows, classify emails (VIP/newsletter/expense/archive), batch label changes, pull calendar + reminders, generate daily briefings |
| Project mgmt | `/weekly-review`, `/goals-review`, `/setup-project-management` | Synthesize progress from WhatsApp, Zoom transcripts, Granola meetings, email into Google Doc dashboards; track OKRs with evidence-based scoring |
| Prompt engineering | `/prompt`, `/prompt-only`, `/prompt-refine` | Format rough/dictated requests into structured prompts with depth calibration (light/standard/deep) |
| Todo | `/todo-add`, `/todo-queue`, `/todo-review` | Batch emails into Apple Reminders via osascript, review/consolidate tasks |
| Communication | `/schedule-query`, `/proposal-write`, `/proposal-revise` | Calendar availability replies, grant proposal drafting with context gathering |
| Session mgmt | `/done` | Capture decisions/questions/follow-ups to handoff file for next session |
| Review | `/review-plan` | Structured critique with fresh-context perspective |
| Goals | `/goals-review` | OKR tracking with evidence from Gmail, Calendar, Granola |
| Tips pipeline | `/tips-curate`, `/tips-integrate` | Capture and act on workflow discoveries |

### Agents (2 templates)

- **Writing reviewer** — Critiques academic prose (argument structure, clarity, evidence, voice). Runs as isolated subagent to avoid self-bias.
- **Methodology reviewer** — Audits causal language, identification strategy, statistical claims, robustness. Directly relevant to econometrics work.

### MCP integrations

- **Gmail MCP** (`google_workspace_mcp`) — search, fetch, label, draft, filter
- **Google Calendar MCP** — event queries, multi-calendar support
- **Granola MCP** — meeting transcript search (optional)
- **Apple Reminders** — via macOS osascript (not MCP)

### State management

- `~/.claude-assistant/config/` — user policies (email, calendar, triage, goals.yaml)
- `~/.claude-assistant/state/` — runtime state (triage timestamps, processed IDs)
- `~/.claude-assistant/logs/` — performance CSV
- `~/.claude/handoff.md` — cross-session continuity via SessionStart hook

## Observations: what's strong

- **Graceful degradation.** Every skill handles missing MCPs by skipping sections, not crashing.
- **Approval gates.** Email sends, label changes, file writes all require explicit confirmation.
- **Fresh-context agents for critique.** Isolated subagents for writing/methodology review avoid self-bias.
- **Batched execution.** Skills collect user decisions first, then execute MCP calls together.
- **Adaptive time windows.** Triage tracks last-run timestamps to prevent reprocessing.
- **VIP safety.** Important contacts never auto-triaged; family emails excluded from archiving.
- **Modular design.** Average skill ~180 lines. Shared config files referenced by multiple skills.
- **Sanitization discipline.** 4-pass checklist for PII removal before publishing.
- **Depth calibration.** Light/standard/deep prompt framework matches complexity to task.
- **The methodology reviewer agent** audits causal language, identification, clustering/multiple testing, effect sizes.

## Observations: potential gaps relative to Francis's setup

These are first impressions, not decisions. Each would need investigation before acting on.

### Email: Gmail vs Fastmail
The entire email stack is built around Gmail MCP. Francis uses Fastmail. No
Fastmail MCP exists in the current ecosystem. Possible paths include Fastmail's
JMAP API (open standard, well-documented), community JMAP MCP implementations,
or IMAP-based alternatives. Needs investigation.

### Transcription: Granola/Wispr Flow vs whisper.cpp
The repo recommends proprietary tools (Wispr Flow for dictation, Granola for
meeting transcription). Francis has whisper.cpp installed and prefers
open-source/local. The `/weekly-review` skill already handles multiple transcript
formats (Zoom VTT, markdown), which suggests extending it for whisper.cpp output
may be straightforward.

### Notes/todos: Google Docs + Apple Reminders vs Joplin
Project dashboards target Google Docs. Todo management uses Apple Reminders via
osascript. Francis has a Joplin MCP server configured, which could serve as a
local, open-source replacement for both.

### Calendar
Francis uses Google Calendar, so that integration should work directly.

### No research-workflow skills
The repo targets admin/management workflows. Missing for an econometrician:
- No R/Stata/LaTeX integration
- No literature monitoring or BibTeX management
- No simulation study or Monte Carlo orchestration
- No data wrangling skills for messy datasets
- Proposal skills target grants, not journal submissions

### Minor technical observations
- No rate-limiting guidance for parallel MCP calls
- No PII redaction before sending LLM-drafted emails
- No conflict handling if same skill runs concurrently
- Tax workflow case study is US-specific
- Session logs grow unboundedly within 60-day window

---

*End of initial audit. This document will likely become outdated as
customization work proceeds. It should be treated as a historical snapshot, not
a living reference.*
