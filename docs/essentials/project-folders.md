# AI Project Folders: Turn Any Recurring Task into a System

*Reading time: 14 minutes* · *Ready to build? [Skip to the setup](#build-your-first-file).*

A single file stores your stable preferences, hard constraints, and behavioral rules for a recurring domain. Every new conversation starts from that file instead of from scratch. I use this for vacation planning (the detailed example below), but the same structure works for shopping decisions, health management, professional writing, finances — any domain where you have stable preferences and learn from experience.

This works in both ChatGPT Projects and Claude.ai Projects, with minor setup differences noted below.

---

## What This Actually Looks Like

Before you invest 14 minutes reading, here's the payoff in 30 seconds.

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

??? note "The full story: how a messy dump became a system"

    It started as a brain dump. My wife and I were planning a summer trip and I pasted a wall of text into ChatGPT — where we'd been, what the kids liked, what we couldn't stand. The AI gave decent suggestions but kept recommending beach resorts, which isn't us.

    So I refined the dump. Added explicit "avoids" for each family member. Added temperature thresholds instead of "we prefer mild weather." Added past trip patterns — not just where we went, but *which conditions made them work*: high altitude, desert-like, culturally rich small towns.

    By the third or fourth trip planned this way, the file had stabilized. I wasn't rewriting it anymore — just adding a line or two after each trip. "This destination worked when we had a car but would fail without one." "That region is too hot in July despite being great in October."

    After about six conversations, the file was reliable enough to trust. New trip planning conversations started producing useful, specific suggestions on the first exchange. No warm-up. No re-explaining who we are. The AI already knew we're a family of four with a teen who rides horses, a tween who lives for adventure sports, a parent who rock climbs, and another who wants natural beauty and water activities — and that all of us hate crowded tourist traps.

    That's when I realized: this isn't a vacation hack. It's a *pattern*. Any recurring task where you have stable preferences and learn from past experience can work this way. Shopping. Health decisions. Professional writing. Finances. The domain changes. The structure doesn't.

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

## Anatomy of a Real Project: Vacation Planning

Here's the structure of my actual vacation planning file, with annotations explaining *why* each section exists.

### System instructions

```text
I want you to be an unusually investigative advisor for travel. # (1)
Instead of focusing on being highly agreeable, be analytical and
offer critical opinions where appropriate. # (2)

When starting a new discussion, analyze the prompt and come back with:
* What kind of vacation we want (outdoorsy, urban, cultural, etc.)
* Who is going (if not clear)
* Major red flags based on my preferences # (3)
* Potential travel restrictions (visa, vaccination, safety warnings)

Please do not hallucinate details but investigate and confirm
wherever possible. # (4)

Provide 1.5 to 2 times more activity options than we have time
available so that we can pick and choose.
```

1. **Why "unusually investigative":** Without this, the AI defaults to agreeable mode — it recommends whatever you seem excited about. You want it to push back and surface problems early.
2. **Why "not agreeable":** Left to its own devices, the AI will cheerfully recommend a destination that violates three of your constraints. This instruction makes it flag conflicts instead of burying them.
3. **Why "major red flags":** This is the constraint-checking instruction. It forces the AI to cross-reference your preferences *before* generating suggestions, not after.
4. **Why "do not hallucinate":** AI chatbots will confidently invent hotel prices, restaurant hours, and activity availability. This instruction doesn't eliminate hallucination, but it reduces confident fabrication and encourages the AI to flag uncertainty.

### Persona preferences

Each family member gets their own section with preferences AND avoids. Here's one:

```text
### Teen Daughter
- Passions: Animals (especially horses — horseback riding is her top priority),
  water sports, reading, bookstores, shopping
- Adventure: Thrill rides, water parks, river rafting, swimming
- Avoids: Steady uphill hikes (unless scrambly or leading to water),
  heavy insect areas, long drives without stops
- Shopping: Loves used bookstores with good YA/fantasy sections,
  boutique clothing stores
```

The design pattern: preferences tell the AI what to suggest. Avoids tell it what to *filter out*. Without the avoids, you'll get recommendations that technically match the preferences but fail in practice.

### Logistics constraints

```text
## Climate & Weather Requirements
- Temperature: Prefer daytime highs 65-80°F; flag anything over 85°F
- Humidity: Low humidity preferred, especially if over 80°F
- Rain: Highlight wet seasons or inclement periods

## Travel Logistics
- Base strategy: Prefer one home base for 5-7 days with activities
  within 75-minute drives, rather than constant destination changes
- Driving limits: Maximum 8 hours/day, preferably 4
- Accommodation: Heavy users of home exchange; destination choice
  often driven by available exchanges
- Crowds: Avoid extremely touristy places; favor off-season or
  weekdays when possible
```

Every constraint has a number. Not "we don't like long drives" but "maximum 8 hours, preferably 4." Not "mild weather" but "65-80°F, flag over 85°F."

### Evidence bank

```text
## Successful Past Patterns
- Mountain/high altitude — Pacific Northwest in summer (worked: climate,
  outdoor sports, uncrowded)
- Cultural/authentic — Southern Mexico (worked: food scene, local flavor,
  affordable, kids engaged)
- Desert/semi-arid — Desert Southwest in winter (worked: climbing, mild
  temps, unique landscape)

## Good but Imperfect
- Coastal Mexico resort town (too muggy; inland towns were better)
- Pacific Northwest river town (fewer activities than expected;
  worked when we had water sports gear)
- Major European cities in summer (too crowded; rural areas
  in the same countries were excellent)
```

Tag each entry with its conditions. "Worked when we had a car." "Failed in summer heat." This is the most powerful section of the file — it gives the AI pattern-matching data instead of just preference lists.

---

## How This Actually Develops

Don't expect your file to be good on day one. It follows a predictable arc:

**Stage 1: Messy dump → first usable file** (conversations 1-2). Your file is rough. You update it substantially after every use. The AI's output is better than no-context conversations but still occasionally generic.

**Stage 2: Failure modes teach you the rules** (conversations 3-5). You discover what's missing — avoids, thresholds, evidence patterns — usually because the AI recommended something that violated an unstated constraint. These failures are the most productive part of the process. Each one adds a specific rule to your file.

**Stage 3: Maintenance, not building** (conversation 6+). The file is reliable enough to trust. Updates are 1-2 lines after each use, not rewrites. Your job shifts from building the file to pruning it — removing anything situation-specific that crept in, keeping it under 500 words.

---

## How a Trip Actually Works

### Step 1: Start a new conversation

Open a new thread in the project. Paste a short trip brief alongside the canonical file (or let the project instructions load automatically). The brief is situation-specific: dates, who's going, any special constraints for this particular trip.

### Step 2: Review the AI's initial response

The AI may ask clarifying questions first, or it may dive straight into suggestions. Both are normal. Before engaging with the suggestions, check: did it reference your constraints? Did it flag anything from your avoids? If it's giving generic output, reprompt: "Reference my project file. Which of my stated constraints does each option satisfy or violate?"

!!! note "Field note"
    My first version got Top 10 tourist lists. Adding explicit "avoids" per person changed everything. The AI went from suggesting beach resorts (which we rarely enjoy) to suggesting mountain towns and cultural small cities — exactly our pattern.

### Step 3: Compare options with explicit trade-offs

Ask the AI to generate 1.5-2x the options you need, with explicit trade-offs for each. A good response looks like: "Option A is best for the climber and worst for the teen. Option B satisfies everyone at a 7/10 but nobody at a 10/10. Option C is ideal weather but a 9-hour drive."

!!! note "Field note"
    The biggest upgrade: past trip patterns as evidence. Instead of "we like mild weather," I wrote "trips that worked: high altitude, desert, culturally rich small cities." It immediately stopped suggesting beach resorts.

### Step 4: Narrow and build the itinerary

Pick 1-2 top options. Ask for a realistic itinerary with pacing discipline — not a packed schedule that ignores your stated preference for late mornings or your kids' energy limits.

### Step 5: After the trip, update the file

Add 1-2 stable learnings. Not an essay — one new rule, one updated threshold.

**The decision rule:** "Would this change my recommendation for the *next* trip, even to a different destination? If yes, add it to the file. If it's specific to this trip's conditions, skip it."

!!! note "Field note"
    We planned a trip to a region known for climbing and rafting. Turned out it was one of the hotter times of year — limited our climbing days significantly. That's when I added explicit temperature thresholds: "flag anything over 85°F." Two words of specificity prevented the same mistake from recurring.

### Example trip brief

Here's an actual brief I've used (sanitized), showing how little context you need when the canonical file is doing its job:

```text
Planning: 10 days, late July. Full family (4 people).

Region: Pacific Northwest — interested in a mountain town near
major climbing areas.

Must-haves:
- Multi-pitch rock climbing accessible within 45 min of base
- Horseback riding options for the teen
- River or lake activities (SUP, kayak, rafting)
- Good restaurant/brewery scene in the town itself

Watch for:
- Heat management — check historical highs for late July
- Wildfire smoke risk in this region/season
- Book popular activities 2+ weeks ahead (horse riding, guided rafting)

Open question: Is it worth splitting the trip — 6 days mountain town
+ 4 days at the coast? Or better to commit to one base?
```

Notice what's *not* in the brief: family preferences, budget philosophy, accommodation style, driving limits, crowd preferences. All of that lives in the canonical file. The brief is just the situation-specific layer.

**Other brief styles I use:**

- **Comparison / decision problem:** "We're choosing between two coastal cities. Please compare them across our criteria and recommend one. Include a comparison table." — useful when you're stuck between options.
- **Exploratory / feasibility check:** "My son and I want a father-son trip focused on soccer and Spanish immersion in Latin America. Is this realistic for a 10-day window? What are the best options?" — useful when you're not sure the idea even works.

### Copy-ready brief templates

Use these as starting points for different planning modes:

**Two-destination routing:**

```text
Planning: [DURATION], [DATES]. [WHO IS GOING].

Route: [DESTINATION A] → [DESTINATION B]
Split: [X] days at A, [Y] days at B, [Z] day transit

Destination A priorities:
- [Activity/goal 1]
- [Activity/goal 2]

Destination B priorities:
- [Activity/goal 1]
- [Activity/goal 2]

Transit day: Recommend a worthwhile stop between A and B?
Open question: [Your actual uncertainty about this trip]
```

**Single base + day trips:**

```text
Planning: [DURATION], [DATES]. [WHO IS GOING].

Base: [TOWN/REGION]
Radius: Day trips within [X] minutes drive

Must-do activities:
- [Activity 1]
- [Activity 2]

Day trip ideas (rank by priority for our family):
- [Potential day trip 1]
- [Potential day trip 2]

Rain plan: If weather turns, what's the best swap from the day
trip list to an indoor/covered alternative?
```

**Skills/activities with daily constraint:**

```text
Planning: [DURATION], [DATES]. [WHO IS GOING].

Focus: [PRIMARY ACTIVITY — e.g., climbing, diving, language school]
Daily constraint: [PERSON] needs [X] — build this into every day

Structure each day as modular 60-90 minute blocks:
- Morning block: [primary activity]
- Midday block: [flexible — could be rest, food, or secondary activity]
- Afternoon block: [secondary activity or family time]

Flag any days where the primary activity isn't available
(weather, closures, rest days) and suggest alternatives.
```

---

## This Pattern Works Beyond Travel

The domain changes. The structure doesn't. A few examples:

**Shopping.** Stable preferences per family member, size/brand preferences, budget thresholds, retailer avoids, past purchases that worked or didn't. Detailed example coming soon.

**Health & fitness.** Exercise constraints, dietary preferences, medical considerations, what's worked and what hasn't, provider preferences. Detailed example coming soon.

**Rock climbing trip planning.** Grade ranges per climber, gear availability, approach difficulty limits, seasonal access windows, guide service preferences, which areas have worked for the group's mixed skill levels.

**Professional: referee reports, recommendation letters.** Recurring structure with personalized content. Your stable preferences for how you approach referee reports (what you focus on, your standards, your voice) don't change — only the paper does. Same for recommendation letters: your template, your voice, your emphasis patterns are stable. The student's details are the situation-specific brief.

**Finances & taxes.** Recurring annual processes with stable rules. Account structures, tax categories, deduction patterns, filing preferences, advisor contacts.

I'll add detailed walkthroughs for these over time. The pattern is identical — what changes is the domain.

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

## Optional Add-Ons

You probably don't need these. Add them only when you feel recurring pain in one of these areas:

- **Decision matrix** — When you're stuck between 3+ options and need a structured comparison. Ask the AI to build a weighted scoring table against your criteria.
- **Research log** — When source quality matters. Track which recommendations were AI-generated vs. independently verified.
- **Post-trip/post-project reflection** — Five bullet points: what worked, what didn't, what to add to the file, what to remove, what surprised you.
- **Packing module** — Families with kids tend to adopt this first. Stable packing lists per person, per trip type, with "don't forget" flags from past experience.
- **Booking/logistics checklist** — Time-sensitive tasks: what to book early, what to book late, what requires advance reservations in your typical destinations.

---

## Next Steps

<div class="grid cards" markdown>

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
