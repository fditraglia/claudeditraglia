# Prompt Engineering

*Reading time: 5 minutes*

Prompt engineering sounds technical. It isn't. It's the skill of asking AI tools for what you actually want, in a way that gets useful results on the first try.

This page covers prompt engineering as a *structured practice* — not a collection of tips, but a repeatable method you can apply to any task.

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

## The Prompt-as-Skill Pipeline

Once you find prompts that work well for recurring tasks, you can turn them into reusable tools:

1. **Collect** — Save good prompts in a text file or note
2. **Template** — Replace specifics with `[FILL IN]` placeholders
3. **Automate** — In Claude Code, save templates as *skills* (slash commands) that run with a single command

The [Toolkit](../toolkit/index.md) path shows how to do step 3. But steps 1 and 2 are valuable on their own, even if you never touch Claude Code.

---

## Recommended Resources

- **[Anthropic's Prompt Engineering Guide](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview)** — The official reference. Thorough and practical.
- **The Quickstart on this site** — [Quickstart](../quickstart.md) demonstrates these principles in a 5-minute exercise.

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
