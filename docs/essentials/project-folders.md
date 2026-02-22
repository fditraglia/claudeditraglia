# AI Project Folders: Turn Any Recurring Task into a System

*Reading time: 8 minutes* · *Ready to build? [Skip to the setup](#build-your-first-file).*

A single file stores your stable preferences, hard constraints, and behavioral rules for a recurring domain. Every new conversation starts from that file instead of from scratch. I use this for vacation planning, shopping decisions, health management, professional writing, finances — any domain where you have stable preferences and learn from experience.

This works in both ChatGPT Projects and Claude.ai Projects, with minor setup differences noted below.

---

## What This Actually Looks Like

Before you invest time reading, here's the payoff in 30 seconds.

**Without a project file** — you ask ChatGPT to help plan a summer trip:

> *Here are my top 10 recommendations for a family summer vacation:*
>
> *1. Yellowstone National Park — stunning geysers and wildlife*
> *2. San Diego — beautiful beaches and the famous zoo*
> *3. Orlando — Walt Disney World and Universal Studios*
> *4. Maui — tropical paradise with snorkeling and hiking*
> *5. Washington D.C. — free museums and monuments...*

Generic. Tourist-list. Could be for any family on Earth.

**With a project file** — same question, same chatbot:

> *Given your preference for high-altitude or desert climates in summer, your teen daughter's horse-riding priority, and your budget for HomeExchange accommodations, I'd suggest looking at three options in the Mountain West. Note: I'm flagging that two of these will exceed 85°F in late July, which historically has limited your outdoor climbing days. Here's a comparison with trade-offs for each family member...*

It references your specific constraints without you repeating them. That's the difference.

If your first reaction is "I could just write a better prompt" — you're right, and that's exactly the point. The project file IS the better prompt. You write it once instead of reconstructing it every conversation.

---

<div class="narrative-block" markdown>
<p class="narrative-teaser" markdown>
The first file I built wasn't for research. It was for planning family vacations. That sounds trivial, but it taught me the pattern I now use for everything — shopping, health, finances, even rock climbing trip logistics. We once planned a trip to a great spot for climbing and rafting. Turned out it was one of the hotter times of year — we lost several outdoor days. That failure is what taught me to add explicit temperature thresholds instead of vague preferences like "we don't like heat."
</p>
</div>

---

## Build Your First File {: #build-your-first-file }

This takes about an hour for a first file — 10 minutes to update it after that. You'll end up with a reusable file that makes every future conversation in this domain dramatically better.

But before you keep reading — open ChatGPT or Claude in another tab and think of one domain where you keep repeating yourself to the AI. Vacations, shopping, meal planning, a type of professional writing. Just pick one. That's what you'll build.

### Platform setup

- **ChatGPT** (requires Plus or Team): Go to the sidebar → Projects → New Project → paste your file into the Instructions field. Every conversation in that project automatically starts with your instructions.
- **Claude.ai** (requires Pro): Go to Projects → Create Project → paste your file into Project Instructions. Claude prepends it to every conversation in the project.

Behavior differs slightly between platforms. ChatGPT persists instructions across all conversations in the project automatically. Claude prepends them to context. Both work — just be aware that if output feels different between platforms, the instruction handling may be why.

### Step 1: Narrate your situation

Open a new conversation and dump everything you know about this domain. Be messy. Be thorough. Don't organize — just talk. Even three sentences is enough to start — the interview in Step 2 will fill the gaps.

Here's the difference between a thin dump and a useful one:

**Too thin:** *"I like beaches and good food."*

**Useful:** *"We travel as a family of four — the kids need activity, not scenery. My partner is pescatarian. I'm a rock climber. We hate tourist traps, we avoid extreme heat, and our last three trips that worked were a mountain town in the Pacific Northwest, a cultural city in southern Mexico, and a desert trip in winter. The beach resort we tried was a disaster."*

More detail = better file. Include what went wrong on past attempts, not just what went right.

### Step 2: Ask the AI to interview you

After your dump, paste this prompt:

```text
Based on what I've shared, interview me to fill in the gaps. Ask me
12 questions, one at a time, covering:

1. Who is involved and what are each person's individual preferences?
2. What does each person actively dislike or avoid?
3. What are our hard constraints (budget ceilings, date windows, health limits)?
4. What specific thresholds matter (temperature ranges, drive times, flight durations)?
5. What past experiences worked well — and what specific conditions made them work?
6. What past experiences failed — and what went wrong?
7. What's our typical logistics setup (car rental, accommodation style, pace)?
8. What trade-offs are we usually willing to make?
9. What trade-offs are we NOT willing to make?
10. Are there any behavioral instructions for you — things I want you to always
    do or never do when helping with this domain?
11. What patterns have I noticed across my best experiences?
12. Is there anything I mentioned that seems contradictory or that you want
    to clarify?

Ask one question at a time. Wait for my answer before moving to the next.
```

Answer honestly. The AI is building a model of your preferences — the more specific you are, the better your file will be.

!!! tip "Add 'avoids' per person, not just 'likes'"
    Avoidances are the true constraints. A family member who "likes beaches" is flexible. A family member who "refuses to hike uphill for more than 30 minutes" is a hard constraint that changes every recommendation.

!!! tip "Use explicit threshold numbers"
    "Flag anything over 85°F" works. "We don't like heat" doesn't. "Budget under $300/night for accommodation" works. "We're not extravagant" doesn't. Numbers give the AI something to actually check against.

**Checkpoint:** You should now have 10-15 specific answers. If you have fewer than 8, go back — the thin ones are usually avoids and thresholds.

### Step 3: Ask the AI to produce a canonical file

After the interview, paste this prompt:

```text
Now synthesize everything — my initial dump and all my interview answers — into
a single canonical project file. Follow these rules:

1. SEPARATE stable preferences from situation-specific details. The file should
   contain only things that are true across all future uses of this domain.
   Anything specific to one instance (a particular trip, a specific purchase)
   should be excluded.

2. USE EXPLICIT THRESHOLD NUMBERS, not adjectives. "Prefer daytime highs
   65-80°F; flag anything over 85°F" not "we like mild weather."

3. ORGANIZE BY CATEGORY: People/preferences, Constraints, Logistics,
   Evidence from past experience, Behavioral instructions for you.

4. GIVE EACH PERSON THEIR OWN SECTION with both preferences AND explicit
   avoids.

5. FLAG anything you inferred versus what I stated directly, so I can
   correct inferences.

6. KEEP IT UNDER 500 WORDS. Shorter files produce better adherence.
   Aim for 300-500 words.

Format as clean markdown. This file will be pasted into a ChatGPT or
Claude project as standing instructions.
```

**Checkpoint:** Your file should be 300-500 words with at least one threshold number and one "avoids" entry per person or category. If it's over 600 words, ask the AI to prune situation-specific details.

### Starter template

If you'd rather start from a template and fill it in, here's a generic one that works for any recurring domain:

```text
# [DOMAIN] Planning Context

## Key Instructions
- [BEHAVIORAL RULE: e.g., "Be analytical, not agreeable. Offer critical opinions."]
- [BEHAVIORAL RULE: e.g., "Always flag potential problems before I ask."]
- [BEHAVIORAL RULE: e.g., "Provide 1.5-2x more options than needed so I can choose."]

## People & Preferences
### [Person 1]
- Priorities: [what they care about most]
- Also enjoys: [secondary interests]
- Avoids: [explicit dislikes — be specific]

### [Person 2]
- Priorities: [...]
- Avoids: [...]

## Hard Constraints
- Budget: [specific ceiling, e.g., "under $300/night accommodation, $150/day activities"]
- Time windows: [when this typically happens]
- [Other constraint]: [with threshold number]
- [Other constraint]: [with threshold number]

## Logistics & Preferences
- [How you typically handle logistics in this domain]
- [Pace/style preferences]

## Evidence: What's Worked
- [Past experience that worked] — conditions: [why it worked]
- [Past experience that worked] — conditions: [why it worked]

## Evidence: What Hasn't Worked
- [Past experience that failed] — problem: [what went wrong]
- [Past experience that failed] — problem: [what went wrong]

## Key Success Factors
- [Factor 1]
- [Factor 2]
- [Factor 3]
```

**Good fill-in:** `Budget: under $300/night for accommodation, $150/day activities`

**Bad fill-in:** `Budget: moderate`

The bad version gives the AI nothing to work with. The good version gives it a number to check against.

### How to know it's working

You're done when your file has: stable preferences for each person, at least 2-3 explicit constraints with threshold numbers, and an "avoids" section.

**Test it:** Start a *completely new* conversation in the project (this tests whether the file actually loaded, not whether it's in your current context). Ask for three suggestions in your domain. The hard test: at least one option should be explicitly eliminated or flagged because it violates a constraint in your file. If all three options look generically good, the file isn't specific enough — go back to the avoids and thresholds.

### When it doesn't work

**AI ignores the file.** This happens occasionally, especially in long conversations. Reprompt: "Reference my project file directly. Do not give generic recommendations." Starting a fresh conversation usually fixes it.

**Generic tourist-list results.** Your file lacks specificity. The fix is almost always the same: add explicit avoids, threshold numbers, and past experience patterns. The AI defaults to generic when it doesn't have enough constraints to differentiate.

**File too long or bloated.** Prune to under 500 words. Remove situation-specific details (those belong in per-instance briefs, not the canonical file). Shorter files produce noticeably better adherence, especially in ChatGPT. Aim for 300-500 words after stabilization.

---

## How This Actually Develops

Don't expect your file to be good on day one. It follows a predictable arc:

**Stage 1: Messy dump → first usable file** (conversations 1-2). Your file is rough. You update it substantially after every use. The AI's output is better than no-context conversations but still occasionally generic.

**Stage 2: Failure modes teach you the rules** (conversations 3-5). You discover what's missing — avoids, thresholds, evidence patterns — usually because the AI recommended something that violated an unstated constraint. These failures are the most productive part of the process. Each one adds a specific rule to your file.

**Stage 3: Maintenance, not building** (conversation 6+). The file is reliable enough to trust. Updates are 1-2 lines after each use, not rewrites. Your job shifts from building the file to pruning it — removing anything situation-specific that crept in, keeping it under 500 words.

---

## See It in Action

<div class="grid cards" markdown>

-   **Vacation Planning**

    ---

    The full case study: an annotated project file, trip briefs, field notes from real trips, and copy-ready templates.

    [:octicons-arrow-right-24: Read the example](folders/vacation.md)

-   **Shopping Decisions**

    ---

    Stable preferences, size/brand rules, budget thresholds, and purchase history as evidence. *Coming soon.*

-   **Health & Fitness**

    ---

    Exercise constraints, dietary preferences, medical considerations, and what's worked vs. what hasn't. *Coming soon.*

</div>

---

## Where People Use This

The domain changes. The structure doesn't:

- **Shopping.** Stable preferences per family member, size/brand preferences, budget thresholds, retailer avoids, past purchases that worked or didn't.
- **Health & fitness.** Exercise constraints, dietary preferences, medical considerations, what's worked and what hasn't, provider preferences.
- **Rock climbing trip planning.** Grade ranges per climber, gear availability, approach difficulty limits, seasonal access windows.
- **Professional: referee reports, recommendation letters.** Your stable preferences for voice, emphasis, and standards don't change — only the subject does.
- **Finances & taxes.** Recurring annual processes with stable rules. Account structures, tax categories, deduction patterns, filing preferences.

---

## Claude vs ChatGPT for This

| Dimension | ChatGPT | Claude |
|-----------|---------|--------|
| Web research | Deep Research, current prices, reviews | Limited |
| Structured analysis | Good | Better |
| Building the canonical file | Good | Better |
| Active trip/project planning | Better (browsing) | Good |
| Automating recurring processes | Limited | Claude Code excels |

**Caveat on web research:** ChatGPT's web browsing is useful for discovery but frequently hallucinates specific prices, hours, and availability — especially for travel planning. Always verify time-sensitive details independently.

**My approach:** I use ChatGPT project folders for research-heavy planning where I need current web info. I use Claude Code for professional tasks that I run repeatedly with standardized inputs. For building the canonical file itself, Claude tends to produce better-organized, more precise output.

---

!!! tip "What I Wish I'd Known"

    - **Start with a messy dump, not a template.** Your first version will be bad. That's the process. The template above is a finishing structure, not a starting point.
    - **The file becomes reliable after about 3-4 uses.** Before that, expect to update it every time. After that, your job is maintenance, not building.
    - **Post-use updates should be 1-2 lines, not essays.** One new rule. One updated threshold. One "this worked under these conditions."
    - **Guard against the AI being too agreeable.** Specific techniques: ask it to steelman the option it's *not* recommending. Ask it to identify which of your constraints a proposed option violates. Ask it to generate one "bad fit" option alongside good ones so you can see the contrast.
    - **If you edit the canonical file mid-conversation, start a new conversation afterward.** The AI has already processed the old version and may produce inconsistent results mixing old and new instructions.

---

## Next Steps

<div class="grid cards" markdown>

-   **See the full vacation example**

    ---

    Annotated project file, trip briefs, field notes, and copy-ready templates.

    [:octicons-arrow-right-24: Vacation Planning](folders/vacation.md)

-   **Level up your prompts**

    ---

    The prompting techniques that make project files (and everything else) work better.

    [:octicons-arrow-right-24: Prompt Engineering](prompting.md)

-   **Understand the landscape**

    ---

    When to use ChatGPT vs Claude — and when it matters for project folders.

    [:octicons-arrow-right-24: ChatGPT vs Claude](chatgpt-vs-claude.md)

-   **Go deeper**

    ---

    When project folders aren't enough, Claude Code turns recurring tasks into automated workflows.

    [:octicons-arrow-right-24: The Toolkit](../toolkit/index.md)

</div>
