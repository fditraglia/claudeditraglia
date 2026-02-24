# /tax-guide — Your Personalized Tax Prep Plan

Answer 8 questions. Get a personalized plan: what documents to collect, whether to self-file or hire a professional, and which parts of this case study apply to you.

!!! warning "This is not tax advice"
    This tool helps you organize your tax preparation workflow. It does not interpret tax law or provide filing guidance. Consult a qualified professional for your specific situation.

---

## What It Does

`/tax-guide` is an interactive Claude Code skill that asks about your income, deductions, filing history, and goals. Based on your answers, it generates a personalized report with four sections:

| Section | What you get |
|---------|-------------|
| **Recommendation** | Self-file, self-file with care, or hire a professional — with reasoning |
| **Document checklist** | Which tax documents to collect, based on your specific income sources |
| **Suggested workflow** | Which skills and pages from this case study are relevant to your situation |
| **Privacy notes** | What data touches which tools, based on your current setup |

The whole process takes about 5 minutes.

---

## Install

### Option 1: Copy the skill file

Download or copy [`tax-guide.md`](https://github.com/chrisblattman/claudeblattman/blob/main/skills/tax-guide.md) to your Claude Code commands directory:

```bash
# Find your commands directory
ls ~/.claude/commands/

# Copy the skill file there
cp tax-guide.md ~/.claude/commands/
```

### Option 2: Create it manually

Create `~/.claude/commands/tax-guide.md` and paste the contents from the [skill file on GitHub](https://github.com/chrisblattman/claudeblattman/blob/main/skills/tax-guide.md).

### Verify installation

In Claude Code, type `/tax-guide`. If the skill is installed correctly, it will start the Q&A.

---

## What to Expect

The Q&A asks about:

1. **Primary income type** — W-2 only, W-2 + side income, self-employed, or multiple sources
2. **Number of 1099 forms** — how many independent income sources you have
3. **Deduction approach** — standard vs. itemized
4. **Complexity flags** — foreign income, rental property, stock options, crypto, K-1s
5. **Prior filing method** — software, CPA, or first time
6. **Claude Code comfort level** — calibrates which tools to recommend
7. **Gmail MCP status** — determines whether automated document collection is available
8. **Your goal** — organize documents, self-file, prep for CPA, or just explore

No real financial data is collected — only categories and preferences.

---

## Sample Output

Here's what someone with a W-2 job plus side consulting might see:

```
══════════════════════════════════════════════════════════
YOUR TAX PREP GUIDE — 2025
══════════════════════════════════════════════════════════

1. RECOMMENDATION
─────────────────
Self-file with care

You have a straightforward W-2 plus 1-2 consulting 1099s.
This is manageable with tax software, but the Schedule C
requires careful expense categorization. The three-year
review step is especially important for your situation.

2. YOUR DOCUMENT CHECKLIST
──────────────────────────
  [ ] W-2 — from your employer's HR portal
  [ ] 1099-NEC (×2) — from consulting clients, arriving by email
  [ ] 1098 — from your mortgage lender
  [ ] 1099-DIV, 1099-B — from your brokerage portal
  [ ] Charitable donation receipts or tracking spreadsheet
  [ ] Property tax bill — from county assessor website

3. SUGGESTED WORKFLOW
─────────────────────
  Step 1: Read Privacy & Setup before handling any documents
  Step 2: Run /tax-collect to find documents in Gmail
  Step 3: Download portal documents manually (brokerage, etc.)
  Step 4: Run /tax-compile schedule-c for consulting expenses
  Step 5: Run /tax-compile charitable for donation summary
  Step 6: Run /tax-compile review for three-year comparison
  Step 7: Read What AI Got Wrong before entering data
  Step 8: Enter figures into tax software manually

4. PRIVACY NOTES
────────────────
  Gmail MCP: Active — will search email subjects and attachments
  Local files: Credit card CSVs and PDFs stay on your machine
  Claude conversation: Never paste SSNs or bank account numbers

══════════════════════════════════════════════════════════
```

---

## Requirements

- **Claude Code** — any installation
- **No MCP required** — Gmail and Google Sheets MCPs enhance the full workflow but are not needed for `/tax-guide` itself
- **No financial data needed** — the skill asks about categories, not amounts

---

## After Running /tax-guide

Your personalized report tells you where to go next. Common paths:

| If your recommendation says... | Start here |
|-------------------------------|------------|
| **Self-file** | [Document Collection](case-study/document-collection.md) |
| **Self-file with care** | [Privacy & Setup](before-you-start/privacy-and-setup.md), then [Workflow Overview](case-study/the-workflow-overview.md) |
| **Hire a professional** | [When to Get Help](reference/when-to-get-help.md) for what to look for, then use the document checklist to organize materials for your CPA |

---

**Back to:** [Tax Workflow Home](index.md)
