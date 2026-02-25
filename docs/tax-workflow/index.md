# Using Claude Code for Tax Season

This year I decided to use Claude Code for as much of my tax preparation as I could. I used it to assemble my charitable contributions from a sprawling Google Sheet, compile my itemized deductions from scattered receipts across email and credit card statements, and build a Schedule C for my consulting income. Some of it was still manual. I had to eyeball credit card statements to flag which charges were medical and which were childcare. But Claude Code is surprisingly good at the grunt work: sorting transactions, filtering by category, downloading and parsing CSV exports, and assembling it all into spreadsheets ready for tax software.

It also helped me think through some tax planning decisions — weighing different filing software, running a rough cost-benefit on whether hiring an accountant was worth it given how I value my time. (For what it's worth, I think it overestimated how long the DIY route would take. I assembled and filed everything in a few hours.)

Since I'm not going to post my actual tax details on the internet, I had Claude Code invent a few fictional profiles and walk through how they'd use the skills I built. The case study below is the result. Claude Code wrote nearly all of it with minimal input from me — I mostly iterated a few times and let review agents argue with each other about what to fix.

One honest caveat: I expect this entire section to be obsolete by next tax season. The AI tools available a year from now will probably blow this out of the water. But for right now, this is what worked for me, and I think it can help you too.

---

!!! warning "This is not tax advice"
    Everything on these pages is educational content about AI workflow design. All dollar amounts are fictional. All examples use fictional personas. Nothing here constitutes tax, legal, or financial advice. Consult a qualified professional for your specific situation.

---

## Start Here

Install `/tax-guide` and answer 8 questions. You'll get a personalized plan: what documents to collect, whether to self-file or hire a professional, and which parts of this case study apply to you.

[:material-rocket-launch-outline: Install /tax-guide](tax-guide.md){ .md-button .md-button--primary }
[:octicons-arrow-right-24: Or browse the case study](case-study/the-workflow-overview.md){ .md-button }

---

## Is This for You?

This case study is useful if **any** of these apply:

- You file your own taxes (or want to understand what your preparer does)
- You have a complicated return — consulting income, multiple 1099s, itemized deductions, investment accounts
- You want to learn how to build Claude Code skills for document-heavy workflows
- You're curious about where AI actually helps with sensitive personal tasks — and where it fails

You do **not** need to:

- Use Claude Code for your own taxes (many shouldn't — see [When to Get Help](reference/when-to-get-help.md))
- Know anything about tax law
- Have any prior Claude Code experience (though the [Build Your Own](build-your-own/architecture-patterns.md) section assumes familiarity with [skills](../toolkit/skills-guide.md))

---

## What You'll Find Here

<div class="grid cards" markdown>

-   **:material-shield-check-outline: Before You Start**

    ---

    Privacy decisions, data handling, and the fictional personas used throughout. Read this first.

    [:octicons-arrow-right-24: Privacy & Setup](before-you-start/privacy-and-setup.md)
    [:octicons-arrow-right-24: Meet the Personas](before-you-start/meet-the-personas.md)

-   **:material-file-document-check-outline: The Case Study**

    ---

    The full workflow: how documents were collected, compiled, validated, and entered. What AI got wrong. Where human judgment was non-negotiable.

    [:octicons-arrow-right-24: Workflow Overview](case-study/the-workflow-overview.md)
    [:octicons-arrow-right-24: Document Collection](case-study/document-collection.md)
    [:octicons-arrow-right-24: Compilation & Review](case-study/compilation-and-review.md)
    [:octicons-arrow-right-24: What AI Got Wrong](case-study/what-ai-got-wrong.md)

-   **:material-wrench-outline: Build Your Own**

    ---

    Transferable patterns for building document-collection and compilation workflows. Starter templates you can adapt for non-tax use cases.

    [:octicons-arrow-right-24: Architecture Patterns](build-your-own/architecture-patterns.md)
    [:octicons-arrow-right-24: Validation Techniques](build-your-own/validation-techniques.md)
    [:octicons-arrow-right-24: Starter Templates](build-your-own/starter-templates.md)

-   **:material-book-open-variant: Reference**

    ---

    Tax basics for academics, escalation criteria for when to hire a professional, and downloadable checklists.

    [:octicons-arrow-right-24: Academic Tax Basics](reference/academic-tax-basics.md)
    [:octicons-arrow-right-24: When to Get Help](reference/when-to-get-help.md)
    [:octicons-arrow-right-24: Downloads](../downloads/index.md#tax-workflow-resources)

</div>

---

## The Three-Sentence Version

I built two Claude Code skills: one that searches Gmail for tax documents, downloads attachments, extracts key figures, and tracks what's still missing; and another that compiles deductions from multiple sources into spreadsheets ready for data entry. A third-year review skill compares the current return against two prior years to catch anomalies. The skills saved real time — but the biggest value was catching errors I would have missed, and the biggest lesson was learning exactly where AI needs a human checking every output.

---

## How to Read This

**Fastest path:** Run [`/tax-guide`](tax-guide.md) — it will tell you exactly which pages to read.

**If you just want the story:** Read the [Workflow Overview](case-study/the-workflow-overview.md) and [What AI Got Wrong](case-study/what-ai-got-wrong.md). Skip the technical sections.

**If you want to build something similar:** Start with [Privacy & Setup](before-you-start/privacy-and-setup.md), then read the case study pages in order, then move to [Build Your Own](build-your-own/architecture-patterns.md).

**If you're an academic wondering about your own taxes:** Start with [Academic Tax Basics](reference/academic-tax-basics.md) and [When to Get Help](reference/when-to-get-help.md).
