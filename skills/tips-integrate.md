---
model: sonnet
---
# Tips Integrate
*v1.1 — 2026-02-22*

Convert collected tips, reference pack recommendations, and session follow-ups into concrete system improvements. Use when you've accumulated new tips (`/tips-curate`), built a reference pack, or want to review session follow-ups for system changes. Run biweekly or after major collection sessions.

## CRITICAL: No Permission Prompts

**DO NOT use Task agents or ToolSearch for this skill.** All required tools are pre-approved. Call them directly:

- Read, Edit, Write, Glob, Grep (filesystem only — no MCP tools needed)

## Arguments

`$ARGUMENTS` can include:
- `source:tips` — Only scan collected-tips-log.md (includes medium-rated items)
- `source:refs` — Only scan reference packs (requires reference pack setup — see Customization)
- `source:session` — Only scan session-log.md
- `dryrun` — Show proposals without writing anything
- `since:YYYY-MM-DD` — Only items after this date
- `compact` — Prune old state entries (housekeeping mode), then stop

If no `source:` argument, scan all sources.

## Instructions

### Phase 0: Pre-Checks

0. **Tips freshness check:**
   - Read `~/.claude-assistant/logs/skill-performance.csv`
   - Search for the most recent row where the skill name is `tips-curate`
   - If file doesn't exist or can't be read: "skill-performance.csv not found — skipping freshness check." Proceed.
   - If no matching entry found: "Tips have never been curated. Run `/tips-curate` first, then rerun `/tips-integrate`. Continue without tips? (yes/skip)" — if yes, proceed without tips source; if skip, stop.
   - If most recent entry is >14 days old: "Tips last curated [N] days ago ([date]). Run `/tips-curate` first, then rerun `/tips-integrate`. Or continue with stale tips? (yes/skip)" — if yes, proceed; if skip, stop.
   - If ≤14 days old: proceed silently.

1. **Read/create state file** at `~/.claude-assistant/state/integrate-state.json`
   - If missing or corrupt: create with default structure (see State Management below), warn "Created fresh state file", continue
   - Extract `last_run` date for filtering

2. **Run automatic pruning:**
   - Remove `deferred_items` older than 90 days (they'll be re-proposed if still in source)
   - Strip `change_summary` from `integrated_items` older than 6 months
   - If `compact` argument: save pruned state, report counts, and STOP

3. **Lightweight system inventory** — Glob for file **names only** (do NOT read contents):
   - `~/.claude/commands/*.md` → list of skill names
   - `~/.claude-assistant/rules/*.md` → list of rule names

4. **Read CLAUDE.md inline triggers section only:**
   - Read `~/.claude/CLAUDE.md`
   - Extract only the section from "**Inline triggers**" through the next `---` separator
   - This provides the mapping of what directives exist — used for dedup in proposals

### Phase 1: Scan Sources

**Read `tips-integrate-references/scanning-rules.md` first** — it contains tag-to-target mappings, the direct-vs-investigation heuristic, and source-specific parsing logic.

**Context budget rules (IMPORTANT):**
- Read only entries **since `last_run` date** from tips log. On first run, read last 30 days.
- Reference packs: read only `actionable.md` or `direct_advice.md` — NOT all files.
- Session log: read only last 30 days of entries (or `since:` override).
- **NEVER read target file contents during scanning.** Full reads happen only in Phase 4 (execution).

For each enabled source, collect candidate items. Skip any item whose `item_key` appears in `integrated_items` or `deferred_items` in the state file.

**Source A: Tips log** (`~/.claude-assistant/tips/collected-tips-log.md`)
- If file missing: "No tips log found. Run /tips-curate first." Skip this source (don't stop entirely).
- Parse entries since `last_run` (or last 30 days on first run)
- Default: only `[high]` items. If `source:tips` explicit: include `[medium]` too.
- Use the `Action:` line as the pre-generated proposal seed
- Item key format: `YYYY-MM-DD::Title` (e.g., `2026-02-20::SDD Pattern`)

**Source B: Reference packs** (`~/.claude-assistant/reference-packs/*/`)
- Scan subdirectories for `actionable.md` or `direct_advice.md`
- If neither file exists in a subdirectory, skip with note: "Pack [name] has no actionable file — skipping"
- Extract each recommendation, match against system inventory file names
- Item key format: `ref-pack:dirname::recommendation-title`

**Source C: Session log** (`~/.claude-assistant/logs/session-log.md`)
- If file missing: "Session log not found — skipping"
- Parse unchecked follow-ups (`- [ ]`) from last 30 days (or `since:` override)
- Only surface items referencing system infrastructure keywords: skill, rule, CLAUDE.md, config, command, agent, policy, settings, MCP, integration
- Skip project-specific follow-ups (those under project headings without infrastructure keywords)
- Item key format: `session:YYYY-MM-DD::follow-up-text-truncated-to-60-chars`

### Phase 2: Generate Proposals

Read `tips-integrate-references/scanning-rules.md` for the direct-vs-investigation heuristic.

**Two proposal types based on specificity:**

**Type A — Direct Proposal** (action references a specific existing file AND a concrete change):
```
────────────────────
DIRECT PROPOSAL [N of M]
────────────────────
Source: [tips / ref-pack:name / session-log]
Item: [title or follow-up text]
File: [exact target file path]
Current: [3-5 relevant lines from target file — read ONLY for direct proposals]
Change: [what to add/modify — under 10 lines, shown as diff-style preview]
Rationale: [1 sentence]
```

**Type B — Investigation Proposal** (directional but not specific enough for a direct edit):
```
────────────────────
INVESTIGATION PROPOSAL [N of M]
────────────────────
Source: [tips / ref-pack:name / session-log]
Item: [title or follow-up text]
Task: [1-2 sentence description of what to research/design before making a change]
Destination: todo-items.md (as new development task)
Rationale: [1 sentence]
```

**Decision heuristic:** If the Action line names a specific existing file AND describes a concrete addition (e.g., "Add X to tool-limitations.md"), generate Type A. If it says "Consider...", "Explore...", "Compare...", or references creating something new, generate Type B. **Most tips will be Type B — be honest about this.** Vague proposals you can't evaluate are worse than honest "needs research" items.

For Type A proposals only: read the specific target file section needed (not the entire file) to populate the `Current:` field.

### Phase 3: Batch Present

If no actionable items found: "No new items to integrate. [N] previously processed." STOP.

If `dryrun`: show proposals, then STOP (don't write anything).

Otherwise, group proposals and present:

```
────────────────────
INTEGRATE REVIEW — [N] proposals from [M] sources
────────────────────

DIRECT PROPOSALS (ready to apply):

  EXISTING SKILLS ([count]):
    1. [proposal summary — file + change preview]

  RULES & POLICIES ([count]):
    2. [proposal summary]

  CLAUDE.MD ([count]):
    3. [proposal summary]

INVESTIGATION PROPOSALS (add to todo list):

  NEW SKILLS TO DESIGN ([count]):
    4. [task summary]

  RESEARCH NEEDED ([count]):
    5. [task summary]

ALREADY PROCESSED: [N] items skipped (previously integrated/deferred)
────────────────────
Apply which? (e.g., "1,3,5" / "all direct" / "all investigate" / "all" / "none" / "defer 2,4")
```

**Wait for the user's response before proceeding.**

### Phase 4: Execute Approved Changes

**For approved Direct Proposals:**
1. Read the full target file (first time reading full contents — context budget preserved)
2. Make the specific edit using Edit tool
3. Record in state file as `integrated_items` with `type: "direct"` and `change_summary`

**For approved Investigation Proposals:**
1. Append task to `~/.claude-assistant/tasks/todo-items.md`
   - Add under `## Active (Current Focus)` section, before the first `---` separator after that heading
   - Format: `- [ ] **[Task title]** — [1-2 sentence description]. *(Source: /tips-integrate, YYYY-MM-DD)*`
2. Record in state file as `integrated_items` with `type: "investigation"`

**For deferred items:** Record in state file with reason (user's words if given, else "deferred")
**For rejected items:** Record as deferred with reason "rejected"

Save updated state file.

### Phase 5: Report & Log

```
────────────────────
INTEGRATION COMPLETE
────────────────────
Direct changes applied: [N]
  [list each: file → change summary]
Investigation tasks added: [N] (to todo-items.md)
  [list each: task title]
Deferred: [N] items
Skipped (already processed): [N]
Sources scanned: [list]
Next run suggestion: [date — 2 weeks from now]
────────────────────
```

Log to skill-performance.csv:
```bash
echo "$(date +%Y-%m-%d),tips-integrate,~TOOL_CALLS,[N]-direct-[M]-investigate-[K]-deferred" >> ~/.claude-assistant/logs/skill-performance.csv
```

## State Management

**State file:** `~/.claude-assistant/state/integrate-state.json`

Default structure:
```json
{
  "schema_version": 1,
  "last_run": null,
  "integrated_items": [],
  "deferred_items": []
}
```

Each `integrated_items` entry:
```json
{
  "source": "tips",
  "item_key": "2026-02-20::SDD Pattern",
  "date_integrated": "2026-02-22",
  "target": "todo-items.md",
  "type": "investigation",
  "change_summary": "Added as dev task"
}
```

Each `deferred_items` entry:
```json
{
  "source": "tips",
  "item_key": "2026-02-20::Volt Tool",
  "date_deferred": "2026-02-22",
  "reason": "Tool not mature enough"
}
```

## Error Handling

| Scenario | Handling |
|----------|---------|
| Tips log missing | Skip source, note "No tips log found — run /tips-curate first" |
| Session log missing | Skip source, note "Session log not found — skipping" |
| Reference pack has no actionable.md | Skip that pack, note in report |
| State file missing | Create with default structure, continue |
| State file corrupt/unparseable | Warn, create fresh state (old state lost), continue |
| Target file for direct edit doesn't exist | Skip proposal, warn in report |
| No actionable items found | "No new items to integrate. [N] previously processed." |
| todo-items.md missing | Create with header, then append |

## Known Limitations

| Limitation | Note |
|-----------|------|
| Most tips produce investigation proposals, not direct edits | By design — vague edits are worse than honest "needs research" |
| Context window pressure on large tip backlogs | Mitigated by `since:` date filtering and lightweight scanning |
| Quality of proposals depends on quality of source Action lines | `/tips-curate` generates these — improve upstream if proposals are weak |
| Cannot auto-detect new reference packs | Pack must contain actionable.md or direct_advice.md to participate |

## Integration Points

| Skill | Relationship |
|-------|-------------|
| `/tips-curate` | **Upstream.** Collects and rates tips; `/tips-integrate` converts them into changes |
| `/done` | **Upstream.** Writes session log; `/tips-integrate` scans follow-ups |
| `self-improvement.md` | **Complementary.** Reactive in-session corrections; `/tips-integrate` is proactive periodic review |
| `todo-items.md` | **Downstream.** Investigation proposals land here as dev tasks |
