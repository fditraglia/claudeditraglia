# CLAUDE.md — claudeditraglia

## What this repo is

Fork of [chrisblattman/claudeblattman](https://github.com/chrisblattman/claudeblattman)
(MIT license). It serves two purposes:

1. **Reference** — Blattman's original MkDocs site, skills, agents, and templates
2. **Staging ground** — where Francis customizes Claude Code configs before
   deploying them globally to `~/.claude/`

## Directory layout

Blattman originals (do not modify in place):
- `docs/`, `overrides/`, `mkdocs.yml` — MkDocs site (claudeblattman.com)
- `skills/`, `agents/`, `templates/` — Blattman's downloadable library
- `README.md`, `CONTRIBUTING.md`, `LICENSE`

Francis's additions:
- `planning/` — audit notes, working docs, migration plans
- `custom/skills/` — Francis's custom skills, symlinked into `~/.claude/commands/`

## Deployment

Custom skills are symlinked from `custom/skills/` into `~/.claude/commands/`:

```bash
ln -sf ~/claudeditraglia/custom/skills/<skill>.md ~/.claude/commands/<skill>.md
```

This keeps the canonical copy version-controlled here while making skills
globally available to all Claude Code sessions.

### Deployed skills

| Skill | Command | Description |
|-------|---------|-------------|
| **Zoom Summary** | `/zoom-summary` | Transcribe Zoom recording with whisper.cpp, summarize into meeting notes |

## Conventions

- **Don't edit Blattman's files** — keep the upstream diffable. Put adapted
  versions in `custom/` when the time comes.
- **Working docs go in `planning/`** — not in the repo root.
- **MkDocs auto-deploys** — pushing to `main` triggers GitHub Pages. Be
  deliberate about what you commit.

## Related repos

- **claude-code-my-workflow** (`~/claude-code-my-workflow`) — fork of
  pedrohcgs/claude-code-my-workflow. Per-project academic template for LaTeX,
  R, Quarto workflows with agents, hooks, and quality scoring. Separate repo,
  separate purpose.

## Key context

Francis's tool stack differs from Blattman's defaults:
- **Email**: Fastmail (not Gmail) — Blattman's Gmail MCP skills won't work as-is
- **Notes**: Joplin with MCP server (not Google Docs / Apple Reminders)
- **Dictation**: whisper.cpp (not Granola / Wispr Flow)
- **Calendar**: Google Calendar
- **Video**: Zoom
- **Research tools**: R, Stata, LaTeX, Git/GitHub

Any skill that assumes Gmail, Google Docs, or Granola needs adaptation before use.
