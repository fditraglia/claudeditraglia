# Prompting Best Practices Guide

*A practical reference for writing effective prompts.*
*Based on Anthropic's best practices, customized for research and professional workflows.*

---

## Core Principles

### 1. Be Clear and Specific

State your task explicitly at the beginning. Provide context. Break complex tasks into steps.

**Weak:**
> Help me with a presentation.

**Strong:**
> I need help creating a 10-slide presentation for our quarterly sales meeting. The presentation should cover Q2 sales performance, top-selling products, and sales targets for Q3. Please provide an outline with key points for each slide.

*Why it works: Specifies deliverable (10 slides), purpose (quarterly meeting), and scope (three topics).*

---

### 2. Use Examples

Show the AI what you want rather than just describing it. If you have a specific format or style, provide a sample.

**When examples help most:**
- Niche or specialized formats
- Your personal or organizational style preferences
- Complex structured outputs (tables, reports with specific sections)
- Tasks requiring consistent voice across multiple outputs

**When examples may not be needed:**
- Common formats the AI knows well (standard emails, code patterns)
- When detailed written instructions are clearer than showing
- When you want the AI to suggest the best approach

**Try zero-shot first:** Before adding examples, try the prompt without them. If the output format or style is wrong, tighten instructions or add output schema. Only add examples if that still fails.

---

### 3. Encourage Step-by-Step Thinking

For complex tasks, ask the AI to reason through the problem systematically.

**Weak:**
> How can I improve team productivity?

**Strong:**
> I'm looking to improve my team's productivity. Think through this step-by-step:
> 1. Current productivity blockers
> 2. Potential solutions
> 3. Implementation challenges
> 4. Methods to measure improvement
>
> For each step, explain your reasoning briefly. Then summarize your recommendations.

---

### 4. Iterate and Refine

If the first response isn't right, give specific feedback rather than starting over.

**Weak:**
> Make it better.

**Strong:**
> That's a good start. Please refine it:
> 1. Make the tone more casual and friendly
> 2. Add a specific example
> 3. Shorten the second paragraph to focus on benefits rather than features

---

### 5. Assign Roles When Useful

Asking the AI to adopt a perspective can improve relevance and depth.

> You are a senior economics journal referee reviewing a paper for a top journal. Identify the three most critical methodological weaknesses.

Don't use roles for simple tasks. "You are a helpful assistant" adds nothing.

---

### 6. Place Critical Information Strategically

Position your most important instructions at the beginning and end of long prompts.

**Bookend pattern:**
> **[Top]** You must cite sources for all factual claims. Do not speculate.
>
> [... task details, context, documents ...]
>
> **[Final reminder]** Remember: Cite sources for all factual claims. Do not speculate.

---

### 7. Separate Persistent vs Task-Specific Instructions

Treat prompt content as two layers:

- **System prompt (persistent):** Role, tone, safety boundaries, citation rules, house style
- **User prompt (task-specific):** The request, context, and any pasted inputs

```
## System
You are a research assistant. Always cite sources. Never fabricate data.
Tone: professional, concise.

## User
Summarize the following paper, highlighting methodology and key findings:
[paper text here]
```

---

### 8. Request Rationale, Not Chain-of-Thought

When you need transparency, request structured output:

- Ask for **key assumptions** (2-3 bullets)
- Ask for **brief rationale** (2-5 bullets explaining the approach)
- Ask for **checks performed** (what was verified)

**Avoid:** "Show your reasoning step by step" for well-specified tasks. This inflates tokens without improving output.

---

### 9. When and How to Request Thoroughness

Vague adjectives ("be thorough", "be meticulous") don't improve output. Specific action verbs do.

**Action verbs that work:**
- "Research current best practices for [domain]"
- "Compare your approach against [named standard]"
- "Flag where your approach deviates from [standard] and explain why"
- "State your key assumptions (2-3 bullets)"

**Self-verification steps** (add when reliability matters):
- "Before answering, identify the 2-3 most likely failure modes"
- "After drafting, check whether your response addresses [specific criteria]"

**What NOT to do:**
- Don't add "CRITICAL", "YOU MUST", "ABSOLUTELY" — a calm, specific directive works better
- Don't pile on directives for simple tasks

---

## Task-Specific Guidance

### Content Creation

Specify audience, tone, and structure:
> Write a blog post about cybersecurity for small business owners. Audience is not tech-savvy. Engaging, slightly humorous tone. Outline for 1000 words covering the top 5 practices.

### Document Summary

Combine specificity with citation requests:
> Summarize this 50-page report in 2 paragraphs focusing on AI trends. Then answer these 3 questions, citing specific sections.

### Data Analysis

Specify format:
> Analyze this data and present as: (1) Executive summary, (2) Key metrics table, (3) Three notable trends, (4) Three data-driven recommendations.

### Brainstorming

Set parameters and request categorization:
> Suggest 10 team-building activities. For each, explain how it fosters teamwork. Categorize by: ice-breakers, communication, problem-solving.

---

## Prompt Chaining

For complex tasks, break the work into a sequence where each step builds on the previous one.

*Prompt 1:* Analyze and identify trends.
*[Review, then...]* *Prompt 2:* Recommend visualizations.
*[Review, then...]* *Prompt 3:* Write executive summary.

**When to use chaining:**
- Multi-step analysis where you want to validate each step
- Creative work where direction might shift
- When "getting it right" matters more than speed

---

## Prompt Versioning

When a prompt is meant to be reused:

- Assign a **version** (e.g., `v1.1`) and a one-line **change note**
- Maintain a small **eval set** (5-15 test cases, including edge cases)
- After edits, re-run against a few cases and note failures

---

## Prompt Structure Template

```
## Role
[Who the AI should be — include only when specialized expertise helps]

## Task
[What you want done — be specific and action-oriented]

## Context
[Background information needed]

## Constraints
[Rules, limitations, scope boundaries, things to avoid]

## Output Format
[How you want the response structured — format, length, style]

## Examples
[Samples of desired style, if applicable]
```

---

## Quick Reference: Quality Checklist

Before sending a complex prompt:

- [ ] Task stated clearly at the beginning
- [ ] Necessary context provided
- [ ] Constraints and scope explicit
- [ ] Desired output format specified
- [ ] Examples included if format/style matters (tried zero-shot first)
- [ ] Role assigned if specialized expertise helps
- [ ] Critical instructions repeated at end (bookend pattern for long prompts)
- [ ] Depth calibration — action-verb directives, not vague adjectives
- [ ] System vs user separation clear (for reusable prompts)

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| AI hallucinates | "If unsure, say so." Ask for citations. Break into smaller steps. |
| Too generic | Add more context. Provide examples. Assign an expert role. |
| Misses requirements | List requirements as numbered items. Use the template. |
| Too long | Specify word count. Ask for bullet points. |
| Too short | Ask to elaborate on specific points. Request reasoning. |

---

*Download, adapt, and use freely. The value is in the practice, not the rules.*
