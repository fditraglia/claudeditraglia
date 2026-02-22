# Revise Proposal
*v1.0 — Public release*

Apply reviewer, collaborator, or self-review comments to an existing proposal draft while maintaining voice consistency.

## Overview

This skill takes an existing proposal draft and feedback (dictated, typed, or from a file), applies the changes, and outputs an updated draft with a change summary. Designed for iterative revision.

**The key value is the collaborator handoff:** A team member reads the draft, dictates or types all their feedback in one pass, and Claude extracts the actionable items and applies them. No one has to edit markdown directly.

## Voice Pack (Optional)

If you maintain a voice pack:

```
@~/Proposal_Resources/voice/PROPOSAL_VOICE.md
@~/Proposal_Resources/voice/PROPOSAL_EXAMPLES.md
```

If not found, the skill uses general academic voice rules.

## Instructions

### Step 1: Find the Draft

Look for the draft in this order:
1. Path provided in `$ARGUMENTS`
2. Most recent `*_Draft.md` in `05_Submissions/Grants/` — confirm with user
3. If not found: "Usage: /revise-proposal <draft-path> [feedback]"

Read the full draft. Parse revision notes (if present) to understand prior inputs and remaining placeholders.

Also read `.claude/CLAUDE.md` for project config.

### Step 1.5: Donor Profile Lookup

After finding the draft, identify the funder:

1. Check for a donor profile at `~/Proposal_Resources/donors/[funder-slug].md`
2. **If found:** Display "What They Value" and "What to Avoid" — these inform revision decisions
3. **If not found:** Continue without funder-specific guidance

### Step 2: Collect Feedback

Feedback can come from any combination:

**Inline (dictated/typed).** Extract actionable feedback from conversational input.

Example:
```
/revise-proposal 05_Submissions/Grants/Draft.md
Tighten the intro. The power calc section needs updated numbers.
Cut 200 words from methodology. Add cost-per-unit breakdowns to budget.
```

**Comments file (`comments:path`).** Read and process any format.

**Formal reviewer comments (`reviewer:path`).** Categorize each comment:
- **MUST ADDRESS** — factual errors, missing content, fundamental concerns
- **SHOULD ADDRESS** — suggestions that improve the proposal
- **CONSIDER** — stylistic preferences or minor points
- **DISAGREE** — note the disagreement and reason

Show categorization and wait for confirmation before applying.

**Funder conflict flagging:** If a suggestion conflicts with the donor profile, flag it:
> "Note: This suggestion may conflict with [funder]'s preference for [X]. Applying as requested, but flagging for review."

### Step 3: Apply Revisions

For each piece of feedback:

1. **Locate** the relevant section
2. **Revise** the text to address the comment
3. **Maintain voice** — short sentences, active voice, numbers over adjectives, claims-first topic sentences
4. **Preserve structure** — don't reorganize sections unless asked
5. **Track changes** — keep a running list of what changed and why

**Rules:**
- Don't rewrite sections that aren't commented on
- If filling a PLACEHOLDER, remove the marker and replace with real content
- If a comment is ambiguous, make your best interpretation and note it

### Step 4: Backup, Save, and Report

**Backup first.** Copy the current draft to `[filename].bak`.

**Save** the updated draft. Update the revision notes:

```markdown
---
## Revision Notes

**Draft created:** [original date]
**Last revised:** [today] by `/revise-proposal`
**Revision round:** [increment]
**Changes this round:**
- [Brief list of major changes]
**Gaps / placeholders:**
- [Updated list]
```

**Report:**
```
Draft updated: [filepath]
Backup saved: [filepath].bak

Changes made:
1. Section [X]: [What changed] — Reason: [comment ref]
...

Word count: [before] -> [after] ([+/- change])

Next steps:
1. Review changes in the draft
2. [If placeholders remain] Fill in: [list]
3. Run Writing Reviewer agent for voice consistency check
```

## Arguments

`$ARGUMENTS`:
- Draft file path (first positional argument)
- `comments:path` — file with comments
- `reviewer:path` — formal reviewer comments (triggers categorization)
- `nodiff` — skip the change summary

## Examples

```
# Self-review
/revise-proposal 05_Submissions/Grants/Draft.md
Tighten the intro. Cut 200 words from methodology.

# Collaborator feedback from file
/revise-proposal Draft.md comments:~/Downloads/feedback.txt

# Formal reviewer comments
/revise-proposal Draft.md reviewer:~/Downloads/reviews.pdf
```

## Error Handling

- If draft not found: Check `05_Submissions/Grants/` for alternatives, suggest closest match
- If voice pack not found: Continue with general voice rules
- If feedback is empty: Ask user to clarify
- If draft has no revision notes: Create from scratch
