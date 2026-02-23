# Write Proposal
*v1.0 — Public release*

Draft a funding proposal from structured inputs, using project context and donor intelligence. Use when drafting funding proposals, LOIs, or project summaries for grant applications.

## Overview

This skill produces a first draft of a funding proposal in markdown. The flow: **Input Checklist → Auto-Gather Context → Donor Profile → Context Brief → Analyze & Plan → Draft → Save.**

## Voice Pack (Optional)

If you maintain a voice pack with your writing style:

```
@~/Proposal_Resources/voice/PROPOSAL_VOICE.md
@~/Proposal_Resources/voice/PROPOSAL_EXAMPLES.md
```

Create these files with your own writing style preferences: sentence length, active vs. passive voice, hedging rules, formatting conventions. If not found, the skill uses general academic voice.

## Instructions

### Step 1: Input Checklist

**Present this checklist immediately and collect all inputs before proceeding.**

```
PROPOSAL INPUT CHECKLIST

REQUIRED:
1. [ ] Funder name and program: ___
2. [ ] Application template / form fields / guidelines
      (Defines the structure. Without it, the draft may need restructuring.)
3. [ ] Research design document or project overview
4. [ ] Budget ceiling or range: ___
5. [ ] Deadline: ___

IF RESUBMISSION:
6. [ ] Previous submission file
7. [ ] Reviewer comments

RECOMMENDED:
8. [ ] Strategic framing notes (what to emphasize/downplay for this funder)

AUTO-LOADED (skill finds these automatically):
9.  [x] Team roster and roles (from project config)
10. [x] Project status and progress (from project config)
11. [x] Related proposals to other funders (auto-scanned for consistency)
12. [x] Donor profile (if available)
```

For each missing REQUIRED item, ask once. If they say "skip," note the gap and proceed.

### Step 2: Auto-Gather Context

After collecting checklist inputs, automatically gather project context. Each source has a word budget to prevent context bloat. **Total cap: ~8,000 words.**

| Source | What to read | Word budget |
|--------|-------------|-------------|
| `.claude/CLAUDE.md` | Team, status, priorities | ~800 (full) |
| Most recent weekly review | `10_AI_Collaboration/Weekly_Reviews/weekly-review-*.md` | ~1,500 |
| Prior submissions to this funder | `05_Submissions/Grants/*[funder]*` | ~2,000 per file (max 2) |
| Consistency reference | 2 most recent `*_Draft.md` to OTHER funders | ~500 total |
| Project Google Doc | Status section via Google Docs MCP | ~1,000 |
| Donor profile | See Step 3 | ~500 (full) |

**Do NOT read raw transcripts.** The weekly review already synthesizes them. If the most recent weekly review is >14 days old, prompt the user to run `/weekly-review` first.

**Graceful degradation:** If any source is unavailable, note it and continue.

### Step 3: Donor Profile Lookup

1. Check for a donor profile at `~/Proposal_Resources/donors/[funder-slug].md`
2. **If found:** Display "What They Value" and "What to Avoid"
3. **If not found:** Note the gap in the context brief and continue

### Step 4: Context Brief

Present a summary of what was gathered:

```
CONTEXT BRIEF

Sources gathered:
- Project config: [loaded/not found]
- Weekly review: [date] ([current/stale])
- Prior [funder] submission: [filename(s) or "none found"]
- Donor profile: [loaded / not found]
- Consistency ref: [filenames scanned / "none found"]
- Google Doc: [loaded / unavailable]

Gaps that would improve the proposal:
1. [List anything missing]
```

**TEMPLATE GATE (HARD STOP):** If no application template or RFP was provided:

> "No application template provided. Without it, the draft structure may not match funder expectations. Provide the template now, or type 'proceed without template' to continue."

### Step 5: Parse Arguments

Read `$ARGUMENTS` for:
- Funder name (required)
- Whether this is a resubmission
- File paths to template, previous submission, reviewer comments
- Budget ceiling, deadline
- `dryrun` — show plan without drafting
- `skipcontext` — bypass auto-gather
- `skipbrief` — bypass context brief display

### Step 6: Analyze and Plan

1. Map the application template sections to available content
2. Identify gaps (write from scratch vs. adapt existing)
3. Note word/page limits
4. Identify the 2-3 strongest arguments for this funder

**For resubmissions**, categorize reviewer comments:
- **MUST ADDRESS** — factual errors, missing content, fundamental concerns
- **SHOULD ADDRESS** — improvements
- **DISAGREE** — note reasoning, flag for user decision

Wait for user confirmation on the reviewer analysis before drafting.

### Step 7: Draft the Proposal

**Structure:** Follow the application template. If no template, use:

```
1. Introduction and Background (problem -> gap -> contribution)
2. Methodology and Research Approach
3. Progress and Preliminary Results
4. Timeline
5. Budget Justification (if requested)
6. Team and Capacity
7. References
```

**Voice rules:**
- First paragraph does real work: problem + stakes (with a number) → what's new → what this project does
- Topic sentences make claims, not background
- Numbers over adjectives ("43.6% report symptoms" not "many students")
- Active voice, short sentences
- No throat-clearing ("In this proposal...", "This section describes...")
- Hedge only with a reason or number
- Implementation details: who, what, when
- End sections with the ask or next step

**Budget section:**
- Cost-per-unit framing ("$30 per survey", "$3.50 per screening")
- Link costs to outputs, not activities

### Step 8: Save and Brief

Save to: `05_Submissions/Grants/[Funder]_[Year]_Draft.md`

File header:
```markdown
# [Full Proposal Title]
## DRAFT — [Date]

**PI:** [Name] ([Institution])
**Co-PIs:** [Names]
**Total Budget:** [Amount or PLACEHOLDER]
**Funder:** [Funder name and program]
**Deadline:** [Date]

---
```

Report after saving:
```
Draft saved to: [filepath]
Sections: [list with approximate word counts]
Total: ~[N] words
Placeholders remaining: [count]

Next steps:
1. Review and edit the draft
2. Fill in budget figures / placeholders
3. Run /proposal-revise with collaborator feedback
4. Run Writing Reviewer agent for voice/clarity check
5. Run Methodology Reviewer agent for design validation
```

## Arguments

`$ARGUMENTS` — natural language is fine. Common flags:
- Funder name (required)
- `resubmission` — revision of previous submission
- `template:path` — application template file
- `previous:path` — previous submission file
- `comments:path` — reviewer comments file
- `budget:N` — budget ceiling
- `deadline:YYYY-MM-DD`
- `dryrun` — show plan without drafting
- `skipcontext` — bypass auto-gather
- `skipbrief` — bypass context brief

## Examples

```
/proposal-write "Example Foundation" deadline:2026-06-01
/proposal-write "Impact Funder" template:~/Downloads/template.pdf budget:150000
/proposal-write "Foundation X" resubmission
/proposal-write "Foundation Y" dryrun
```

## Error Handling

- If no funder name: "Usage: /proposal-write <funder> [options]"
- If no application template: HARD STOP (template gate)
- If project config missing: "No .claude/CLAUDE.md found. Run from a configured project directory."
- If voice pack not found: Continue with general voice rules
- If weekly review stale (>14 days): Warn and offer to run `/weekly-review` first
