# Download Skills

*Reading time: 6 minutes*

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

-   :material-draw-pen: **[Writing Reviewer](#writing-reviewer)** — Academic prose QA (agent)
    { .card-mini }

-   :material-flask-outline: **[Methodology Reviewer](#methodology-reviewer)** — Empirical methods QA (agent)
    { .card-mini }

-   :material-file-document-outline: **[CLAUDE.md Template](#claudemd-template)** — Starter config file
    { .card-mini }

-   :material-bullseye-arrow: **[Goals Template](#goals-template)** — Project & priority tracker
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

- **Log file location:** The default is `~/Documents/session-log.md`. Change this to wherever you want your session history (e.g., a project folder, a synced Dropbox directory).
- **Project matching:** Add logic to match against a projects list in your CLAUDE.md or a goals.yaml file, so sessions auto-tag by project.
- **Archive threshold:** The default has no auto-archiving. Add pruning logic if your log exceeds 500 lines (e.g., archive entries older than 60 days).

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
