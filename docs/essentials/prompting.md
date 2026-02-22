# Prompt Engineering

Prompt engineering sounds technical. It isn't. It's the skill of asking AI tools for what you actually want, in a way that gets useful results on the first try.

This page covers prompt engineering as a *structured practice* — not a collection of tips, but a repeatable method you can apply to any task.

!!! tip "The single most important thing on this page"

    Don't memorize prompt engineering rules — **make the AI do it for you.**
    Create a prompt engineering project in ChatGPT or Claude, and it will
    restructure your messy input into clean prompts automatically.
    [Jump to the how-to below.](#make-the-ai-do-this-for-you)

    Once you start using Claude Code, you can automate this further with
    a [`/prompt` skill](../toolkit/skill-library.md) that formats and
    executes prompts in a single command.

---

## Why This Matters

The gap between a mediocre AI interaction and a great one is almost always the prompt. Not the model, not the subscription tier, not some secret technique. Just how clearly you communicated what you wanted.

Good prompts share three properties:

1. **They provide context** — enough background that the AI doesn't have to guess
2. **They specify the task** — unambiguously, in 1-2 sentences
3. **They define the output** — format, length, tone, audience

Most bad interactions fail on #1 (no context) or #3 (no output specification). Fix those two things and you'll get dramatically better results from any model.

---

## The Anatomy of a Good Prompt

### 1. Role (Optional)

Tell the AI what perspective to take. This is useful when you need domain expertise.

> *You are a senior economics journal referee reviewing a paper for the American Economic Review.*

Don't use roles for simple tasks. "You are a helpful assistant" adds nothing.

### 2. Context

What does the AI need to know about the situation? Include:

- Who you are and what you're working on
- Relevant constraints (deadlines, audiences, requirements)
- What you've already tried or decided

> *I'm writing a grant proposal for a foundation that funds violence reduction programs. The proposal is for a randomized evaluation of a CBT intervention for high-risk youth in a Latin American city. Budget ceiling is $500K over 3 years.*

### 3. Task

State the core ask in 1-2 clear sentences. Front-load this — don't bury it after three paragraphs of context.

> *Draft the methodology section (800-1000 words). Focus on the randomization strategy, primary outcomes, and power calculations.*

### 4. Constraints

What should the AI do or avoid? Be specific.

- **Length:** "Keep it under 1000 words" not "be concise"
- **Tone:** "Academic but accessible — like a top-5 journal, not a textbook"
- **Exclusions:** "Don't include a literature review — that's a separate section"
- **Priorities:** "Focus on identification strategy. Spend less time on implementation details."

### 5. Output Format

How should the result be structured?

> *Structure as: (1) Design overview, (2) Randomization, (3) Outcomes and measurement, (4) Power and sample size. Use short paragraphs. No bullet points — this is narrative prose.*

### 6. Bookend (For Long Prompts)

If your prompt is more than a few paragraphs, restate the key instruction at the end. AI models sometimes lose focus on long inputs.

> *Remember: the goal is a methodology section for a foundation grant, not a journal paper. Keep the tone accessible and emphasize the practical implementation plan.*

---

## Depth Calibration

Not every task needs the same level of effort. A quick email reply doesn't need the AI to "research best practices" and "state assumptions." A methodology review does.

**Three levels:**

| Level | When to Use | What to Add |
|-------|-------------|-------------|
| **Light** | Quick tasks, routine emails, simple lookups | Nothing extra — just format clearly |
| **Standard** | Analysis, research writing, design decisions | Ask for assumptions and rationale: *"Include key assumptions (2-3 bullets) and brief rationale for major choices."* |
| **Deep** | High-stakes writing, methodology, pre-analysis plans | Ask for verification: *"Research current best practices. Compare your approach against established standards. Flag where you deviate and why."* |

**Default to Light.** Upgrade when the stakes justify it.

---

## Common Anti-Patterns

**Vague thoroughness language.** "Be comprehensive" and "be meticulous" are empty calories. Replace with specific verbs:

- "Compare against [specific standard]"
- "Research current best practices for [domain]"
- "Flag where your approach deviates from [benchmark]"

**Over-prompting.** Modern AI models are good at following instructions. You don't need `CRITICAL: YOU MUST ABSOLUTELY...` — a calm, specific directive works better. Shouting in all-caps doesn't make the AI try harder.

**Asking for everything at once.** A prompt that asks for a literature review, methodology section, budget narrative, and timeline will produce mediocre versions of all four. Break complex tasks into focused steps.

**No pushback permission.** If you want honest feedback, say so: *"Tell me directly if this approach has problems. Don't just agree with everything."* By default, AI tends toward politeness and agreement.

---

## Make the AI Do This for You

You don't have to internalize all of the above. Create a project in ChatGPT or Claude.ai with prompt engineering instructions as the project file, and the AI will restructure your messy input into clean prompts automatically.

### Setup

- **ChatGPT** (Plus or Team): Sidebar → Projects → New Project → paste the file below into Instructions.
- **Claude.ai** (Pro): Projects → Create Project → paste into Project Instructions.

### The instructions file

Copy this into your project instructions. It tells the AI to take any unstructured input and restructure it into a clean, well-organized prompt.

```text
# Prompt Engineering Assistant — Project Instructions

## Purpose
You are a prompt engineering assistant. Your job is to take narrative,
unstructured input and restructure it into clean, well-organized prompts.

Primary deliverable: a ready-to-paste prompt (or small set of prompt
variants) that reliably produces the user's desired output.

## Default behavior
- Rewrite messy specs into a structured prompt using standard sections
  (Role, Task, Context, Constraints, Output Format, Examples).
- Put instructions before context/data. Use clear delimiters between
  instructions and any quoted input.
- Make implicit requirements explicit. Remove filler while preserving meaning.
- Prefer action verbs and testable requirements over adjectives.
- If something important is missing: proceed with reasonable defaults
  and list them as "Assumptions," or ask a single clarifying question
  only if the missing info would likely change the output substantially.

## Output you produce each time
1. Final Prompt (ready to paste)
2. Suggestions (optional) — improvements, risks, missing info
   - Skipped when the user says "quick format"

## Supported modes
- "quick format" — output only the restructured prompt, no suggestions
- "format and critique" — restructured prompt plus detailed critique
  and 2-3 alternative prompt designs
- "prompt pack" — 2-4 prompt variants (minimal, standard, rigorous)

## Standard prompt structure
Use these headings in order (omit irrelevant sections):

### Role
Include only when starting a new thread or when specialized expertise
changes outputs.

### Task
The single clearest description of what the model must do.

### Context
Background needed to perform the task well.

### Inputs
What the user is providing and how to treat it.

### Constraints
Rules, boundaries, and "do not" instructions. Include scope boundaries
and what to do when uncertain.

### Output format
Exact structure, length targets, style/tone constraints, required elements.

### Examples
Only when examples exist or format is tricky.

### Acceptance criteria
A short checklist that makes success testable.

### Assumptions
Only include if you proceeded without asking a clarifying question.

## Quality checklist before finalizing
- Single main task is unambiguous
- Output format is explicit and easy to grade
- Constraints are not contradictory
- Data is clearly separated from instructions
- Any defaults are documented as assumptions
- Prompt is copy-pasteable and does not depend on hidden context
```

Now when you dump a rough idea into this project — dictated, messy, whatever — the AI restructures it into a clean prompt you can paste anywhere.

---

## Going Further

Once you find prompts that work well for recurring tasks, save them. A text file, a note on your phone — the format doesn't matter. Over time, replace specifics with `[FILL IN]` placeholders and you have reusable templates. In Claude Code, you can turn those templates into *skills* (slash commands) that run with a single command — the [Toolkit](../toolkit/index.md) path shows how.

---

## Downloadable References

These are the actual files I use. Download, adapt, and paste them into your own projects.

- **[My Prompt Preferences](../downloads/prompt-preferences-template.md)** — A template showing how to document your personal prompting style: standard sections, common constraints, preferred output formats, and roles. Adapt it to your own work.
- **[Prompting Best Practices Guide](../downloads/prompting-guide.md)** — A comprehensive reference (400+ lines) covering core principles, task-specific guidance, prompt chaining, versioning, and a quality checklist.

## Recommended Resources

- **[Anthropic's Prompt Engineering Guide](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview)** — The official reference. Thorough and practical.

---

## Next Steps

<div class="grid cards" markdown>

-   **See prompts in action**

    ---

    The `/prompt` skill automates prompt formatting inside Claude Code.

    [:octicons-arrow-right-24: Skill Library](../toolkit/skill-library.md)

-   **Add dictation to the pipeline**

    ---

    Dictate a rough idea, let a prompt skill format it, get polished output.

    [:octicons-arrow-right-24: Wispr Flow](wispr-flow.md)

</div>
