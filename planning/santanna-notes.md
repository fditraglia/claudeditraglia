# Notes on Sant'Anna's claude-code-my-workflow

*Generated: 2026-02-28 by Claude, at Francis DiTraglia's request.*

**Status: Fact-finding only.** These are observations from reviewing Pedro
Sant'Anna's repo (github.com/pedrohcgs/claude-code-my-workflow). Nothing here
is prescriptive.

**Current intent:** Fork Sant'Anna's repo separately, since it serves a
different architectural role from this repo (per-project template vs global
config staging). This may change.

---

## What it is

A self-contained Claude Code project template for academic work (slides, papers,
R analysis, replication packages). Created by Pedro H.C. Sant'Anna
(econometrician, Emory). MIT licensed.

Unlike Blattman's repo (global skills installed to `~/.claude/commands/`),
Sant'Anna's setup lives *inside* each project repo as a `.claude/` directory.
You'd clone/fork it when starting a new paper or course.

## Architecture at a glance

- **22 skills** — `/compile-latex`, `/deploy`, `/slide-excellence`, `/qa-quarto`,
  `/create-lecture`, `/lit-review`, `/data-analysis`, `/research-ideation`,
  `/review-paper`, `/review-r`, `/learn`, etc.
- **10 agents** — proofreader, pedagogy-reviewer, r-reviewer, domain-reviewer,
  slide-auditor, quarto-critic, tikz-reviewer, beamer-translator, verifier,
  quarto-fixer
- **7 hooks** — file protection, desktop notifications, pre/post-compact state
  preservation, context monitoring, verify-after-edit reminders, session log
  enforcement
- **No MCP servers** — everything via native Claude Code tools + Bash (xelatex,
  quarto, Rscript, git, gh)
- **Quality scoring** — Python script (0-100), gates at 80 (commit), 90 (PR),
  95 (excellence)

## How it differs from Blattman

| Dimension | Blattman | Sant'Anna |
|---|---|---|
| Scope | Global admin workflows | Per-project academic template |
| Install location | `~/.claude/commands/` | `.claude/` inside the repo |
| Integrations | MCP (Gmail, Calendar, Granola) | Bash (LaTeX, Quarto, R) |
| Quality control | Approval gates | Scoring system + adversarial agents |
| Agents | 2 reviewers | 10 specialized |
| Hooks | None in repo | 7 |
| Audience | Non-developers | Academics who compile LaTeX |

## Design patterns worth studying

These are ideas observed in the repo, not recommendations. Each would need
evaluation before adopting.

### 1. Hook system
Seven hooks covering the full session lifecycle:
- **protect-files.sh** (PreToolUse) — prevents edits to protected files
- **notify.sh** (Notification) — desktop notifications via osascript
- **pre-compact.py** (PreCompact) — captures plan status, tasks, decisions to
  JSON before context compression
- **post-compact-restore.py** (SessionStart) — displays saved state on resume
- **context-monitor.py** (PostToolUse) — warns at 40/55/65/80/90% context usage
- **verify-reminder.py** (PostToolUse) — reminds to compile after file edits
- **log-reminder.py** (Stop) — blocks if 15+ responses without session log

All hooks "fail open" — never block Claude on errors. 5-10 second timeouts.

### 2. Adversarial agent pairs
Critics (read-only) identify issues; fixers (read-write) apply solutions.
Critics re-audit after fixes. Up to 5 rounds. Prevents self-bias more
aggressively than Blattman's fresh-context approach.

### 3. Quality scoring
`scripts/quality_score.py` scores files 0-100. Detects compilation failures,
equation overflow, citation breaks, path issues, reproducibility markers. Exit
codes: 0 (commit-ready), 1 (blocked), 2 (auto-fail). Integrated into hooks.

### 4. Two-tier memory
- **MEMORY.md** (committed) — generic cross-session patterns, tagged
  `[LEARN:category]`, max ~200 lines
- **personal-memory.md** (gitignored) — machine-specific: tool paths, local
  quirks, personal preferences

### 5. Context compression survival
Pre-compact hook saves active plan, first unchecked task, recent decisions to
JSON in `~/.claude/sessions/`. Post-compact hook restores this on resume.
Addresses the "lost my place" problem.

### 6. Session logging discipline
Timestamped logs in `quality_reports/session_logs/`. Three triggers: post-plan,
incremental (on decisions/corrections), end-of-session. Enforced by hook that
blocks after 15+ responses without a log update.

### 7. Plan-first workflow
Non-trivial work requires entering plan mode. Plans saved to
`quality_reports/plans/` as timestamped markdown. Survive context compression
because they're on disk.

## Tools integrated

LaTeX (XeLaTeX only), Quarto RevealJS, TikZ (with SVG conversion), BibTeX, R
(Rscript, ggplot2, RDS caching), Python (scoring, hooks), Git/GitHub CLI,
GitHub Pages, pdf2svg, pdftk, ghostscript.

## Relevance to Francis (speculative)

Potentially relevant:
- R integration patterns (code review agent, data analysis skill)
- LaTeX compilation workflows
- The methodology/domain reviewer agent concept
- Quality scoring for academic outputs
- Literature review and research ideation skills

Less obviously relevant:
- Beamer-to-Quarto translation pipeline
- TikZ-specific tooling
- Emory-specific styling/colors

---

*End of notes. To be revisited when setting up the forked Sant'Anna repo.*
