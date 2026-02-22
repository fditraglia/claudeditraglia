# Calendar Policy
*Configuration for /schedule-query and /morning-brief skills*

## What This Is
This file tells scheduling skills which calendars to check, your availability preferences, and how to compose scheduling replies.

## Prerequisites
- Google Calendar with Google Workspace MCP configured
- Calendar IDs retrieved (see "How to Find Calendar IDs" below)

## How to Find Google Calendar IDs

**Method 1: Using Claude Code (recommended)**
Run this in Claude Code:
```
Ask Claude to call mcp__google_workspace__list_calendars with your email address
```
This returns all calendars with their IDs.

**Method 2: Google Calendar Settings**
1. Open Google Calendar > Settings (gear icon)
2. Click on each calendar name in the left sidebar
3. Scroll to "Integrate calendar" section
4. Copy the "Calendar ID" value

**Calendar ID formats:**
- Primary calendar: usually `your-email@gmail.com`
- Secondary calendars: `[random-string]@group.calendar.google.com`
- Subscribed calendars: varies

---

## Calendar IDs

List all Google Calendar IDs to check for availability:

| Calendar Name | Calendar ID | Notes |
|--------------|-------------|-------|
| Primary | your-email@gmail.com | Main calendar |
| Work | [calendar-id]@group.calendar.google.com | Work meetings |
| [Other calendar] | [calendar-id] | [Description] |

---

## Scheduling Preferences

### Working Hours
- **Start:** 9:00 AM [YOUR_TIMEZONE]
- **End:** 5:30 PM [YOUR_TIMEZONE]
- **Days:** Monday-Friday

### Timezone
- **Primary:** [YOUR_TIMEZONE] (e.g., America/Chicago, America/New_York, Europe/London)
- **Abbreviation:** [TZ] (e.g., CT, ET, GMT)
- **UTC offset:** [offset] (e.g., -06:00, -05:00, +00:00)

### Buffer Times
- **Between meetings:** 15 minutes minimum
- **Before deep work:** 30 minutes (if protecting deep work blocks)

### Preferences
- Prefer morning deep work: avoid scheduling 8-10am
- Prefer Friday PM free: avoid scheduling after 2pm on Fridays
- No back-to-back: don't create 3+ consecutive meetings
- Protect largest free block each day for deep work

### Deep Work Protection
- **push_level:** `gentle` | `moderate` | `assertive`
  - `gentle` -- just show schedule, no nudges
  - `moderate` -- protect largest free block, suggest deep work
  - `assertive` -- flag when <2 hours free, suggest declining meetings

---

## Scheduling Reply Tone

### Tier 2 (Most Common -- Colleagues, Collaborators)
```
Hi [Name],

I'm free at these times:
- [Day], [Month] [Date] at [time] [TZ]
- [Day], [Month] [Date] at [time] [TZ]
- [Day], [Month] [Date] at [time] [TZ]

Let me know what works and I'll send a calendar invite.

[Your name]
```

### Tier 1 (Formal -- Senior Contacts, External)
```
Hi [Name],

I'd be happy to meet. I have availability at the following times:
- [Day], [Month] [Date] at [time] [TZ]
- [Day], [Month] [Date] at [time] [TZ]
- [Day], [Month] [Date] at [time] [TZ]

Please let me know which works best for you.

Best,
[Your name]
```

---

## Slot Scoring (preference order)

1. Mid-morning (10am-12pm) or mid-afternoon (2pm-4pm)
2. Not adjacent to existing long meetings
3. Days with fewer existing meetings
4. Closer dates (sooner is better)

---

## Customization Points

- **Calendar IDs:** Add all calendars you want checked for conflicts. Missing a calendar = double-booking risk.
- **Working hours:** Adjust to your actual schedule. The skill won't propose times outside these hours.
- **Timezone:** Set to your primary timezone. All proposed times are displayed in this timezone.
- **Deep work protection:** Set `push_level` based on how aggressively you want to protect focus time.
- **Reply tone:** Add your own voice templates. The skill uses these for drafting scheduling replies.
- **Buffer times:** Increase if you need more transition time between meetings.
