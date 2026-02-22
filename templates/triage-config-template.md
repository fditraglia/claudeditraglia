# Triage Configuration
*Technical configuration for /triage-inbox and /morning-brief skills*

## What This Is
This file maps your Gmail label names to their internal IDs and defines the rules for automatic email classification. It's the "brain" of the triage system.

## Prerequisites
- Gmail labels created (see email-policy-template.md)
- Label IDs retrieved (see "How to Find Label IDs" below)

## How to Find Gmail Label IDs

**Method 1: Using Claude Code (recommended)**
Run this in Claude Code:
```
Ask Claude to call mcp__google_workspace__list_gmail_labels with your email address
```
This returns all labels with their IDs.

**Method 2: Gmail API Explorer**
1. Go to https://developers.google.com/gmail/api/reference/rest/v1/users.labels/list
2. Click "Try it" and authorize
3. Copy the label IDs from the response

**Method 3: Manual lookup**
Gmail label IDs for user-created labels look like `Label_1`, `Label_2`, etc. System labels use names like `INBOX`, `UNREAD`, `SPAM`.

---

## Label IDs

| Label Name | Label ID | Notes |
|------------|----------|-------|
| @ToRead | YOUR_LABEL_ID | Replace with your actual label ID |
| @Announcements | YOUR_LABEL_ID | Replace with your actual label ID |
| @School | YOUR_LABEL_ID | Replace with your actual label ID |
| @Family | YOUR_LABEL_ID | Replace with your actual label ID |
| @FYI | YOUR_LABEL_ID | Optional — create if you want a "for your information" label |
| Expenses-Pending | YOUR_LABEL_ID | Under Expenses/ parent label |
| Expenses-Personal | YOUR_LABEL_ID | Under Expenses/ parent label |
| Expenses-Uncertain | YOUR_LABEL_ID | Under Expenses/ parent label |
| Auto-Archive | YOUR_LABEL_ID | For low-priority automated emails |

---

## Label Application Rules

| Routing Tier | Add Label | Remove From | Read Status |
|-------------|-----------|-------------|-------------|
| @ToRead | Label ID | INBOX | Leave UNREAD |
| @Announcements | Label ID | INBOX | Leave UNREAD |
| @School | Label ID | INBOX | Leave UNREAD |
| @Family | Label ID | INBOX | Leave UNREAD |
| @FYI | Label ID | INBOX | Leave UNREAD |
| Expenses-Pending | Label ID | INBOX | Mark as READ |
| Expenses-Personal | Label ID | INBOX | Mark as READ |
| Expenses-Uncertain | Label ID | INBOX | Leave UNREAD |
| Auto-Archive | Label ID | INBOX | Mark as READ |

---

## Expense Vendor Domains

Emails from these domains are flagged as potential expenses.

| Domain | Vendor Type | Notes |
|--------|------------|-------|
| uber.com | Transport | Uber rides/Eats |
| lyft.com | Transport | Lyft rides |
| amazon.com | Retail | Amazon purchases |
| paypal.com | Payment | PayPal transactions |
| square.com | Payment | Square receipts |
| stripe.com | Payment | Stripe payments |
| [add your vendors] | [type] | [notes] |

---

## Expense Subject Keywords

Subjects containing these words (from vendor-like senders) are flagged as expenses:
- receipt, invoice, payment, order confirmation, transaction, purchase, charge

## Expense Skip Patterns

NOT expenses even if from a vendor domain:
- "welcome", "verify your email", "password reset", "account update", "terms of service"

---

## Newsletter Platform Domains

Emails from these domains are routed to @ToRead:
- substack.com
- beehiiv.com
- convertkit.com
- mailchimp.com
- buttondown.email

---

## School Domains

Emails from these .edu domains are routed to @School (excluding VIP/Family addresses):
- [youruniversity].edu
- [department].youruniversity.edu

---

## @ToRead Sender Whitelist

Specific senders always routed to @ToRead (regardless of other signals):
| Sender | Notes |
|--------|-------|
| [newsletter@example.com] | [Newsletter name] |

---

## Classification Score Thresholds

| Score | Classification |
|-------|---------------|
| Newsletter platform domain | @ToRead (immediate) |
| @ToRead whitelist match | @ToRead (immediate) |
| Newsletter score >= 3 | @Announcements |
| Announcement score >= 2 + .edu | @Announcements |
| Receipt/notification from noreply | Auto-Archive |
| Score 1-2 mixed signals | SKIP (uncertain) |
| Score 0 or no match | SKIP (leave in inbox) |

---

## Classification Overrides

Manual overrides that take precedence over scoring. Add entries here when triage misclassifies a sender.

| Sender Pattern | Override To | Notes |
|---------------|-------------|-------|
| [sender@domain.com] | [@ToRead / @Announcements / Auto-Archive] | [Why] |

---

## Classification Priority (Tiebreaking)

When multiple categories match, use this priority order:
1. VIP (always wins — stays in inbox)
2. Expenses (financial takes priority)
3. @ToRead (user-subscribed content)
4. @School (institutional)
5. @Announcements (general)
6. Auto-Archive (lowest priority)

---

## Customization Points

- **Label IDs:** You MUST replace all `YOUR_LABEL_ID` values with your actual Gmail label IDs before using triage skills.
- **Vendor domains:** Add your common receipt senders (airlines, hotels, subscriptions).
- **Newsletter platforms:** Add any newsletter platforms you subscribe to.
- **School domains:** Add your institution's email domains.
- **Score thresholds:** Adjust if triage is too aggressive (lower) or too passive (raise).
- **Classification overrides:** Add entries as you correct triage mistakes — this is the feedback loop.
