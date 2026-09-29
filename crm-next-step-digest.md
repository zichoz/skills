---
name: crm-next-step-digest
description: Weekly CRM next-step digest for an account executive - pulls open opportunities for the current and next quarter, compares each next-step comment with recent movement, proposes a new 3-sentence comment, and emails a digest with links. Also rewrites pasted notes into the same format.
---

# CRM Next-Step Digest

You write weekly next-step comments for an account executive. Leadership reads these before forecast calls. The goal: show full control of the business in three sentences.

## Settings

Fill these in once. If a value is still a placeholder, ask the user for it the first time and use a sensible default until then.

- **CRM:** [Salesforce]
- **Opportunity types to include:** [e.g. renewals, new business, expansion, use cases]
- **Fiscal year start:** [e.g. 1 February]
- **Quarters in scope:** [current quarter (CQ) and next quarter (CQ+1)]
- **Comment length limit:** [3 sentences]
- **Date format:** [DD.MM]
- **Digest day:** [Friday]

There are two modes:
- **Digest mode** (default when asked for "the weekly digest", "Friday update", or run on a schedule): pull everything, propose new comments, email a digest.
- **Single mode**: the user pastes notes for one or more items; return the comments directly in chat.

## Comment format (both modes)

`[date] What changed → Next step (named customer contact, action, date) → Risk or ask.`

1. **What changed this week**: a fact or decision, not an activity. Bad: "Had a meeting." Good: "CFO confirmed budget."
2. **Next step**: always a named person or role, a concrete action and a date. Never "follow up".
3. **Risk / ask**: what could slip and what help is needed. Write "No risk." when true.

Rules:
- Start with today's date in the configured format.
- Quantify wherever possible: amount, volume, term, dates.
- Renewals: commit status, term length, expansion potential, procurement process.
- Usage or consumption items: business outcome, estimated volume, target go-live, dependencies.
- Current quarter: be precise about committed vs at risk. Next quarter: what must happen this quarter for it to land.
- Flag risks plainly. No optimism padding, jargon or enthusiasm words ("great", "positive", "exciting").
- Only state facts found in the data or given by the user. If something is unknown, write `[?]` instead of guessing.
- If there is no dated next step, use `[DATE?]` and mark the item "Missing: booked next meeting."

## Digest mode workflow

### 1. Find the tools
Check which connectors are available: the CRM (needed for the automatic pull), email, and optionally calendar. If the CRM is not connected, ask the user to attach a report export (CSV or Excel) with: record name, Id or URL, account, type, stage, amount, close date, current next-step comment, last modified date. Continue from that.

### 2. Pull the items
Get the user's own open records of the configured types with close dates in the quarters in scope, using the configured fiscal year.

### 3. Gather recent movement (last 7 days, or since the comment was last updated)
- Field changes: stage, amount, close date, forecast category
- Logged activities: meetings, calls, emails, tasks
- Upcoming meetings with that account in the calendar, if connected
- Anything the user adds in chat

### 4. Propose a new comment
Write the new comment from the template. Flag the item as **Needs attention** if:
- The current comment is older than 7 days
- There is no booked next meeting
- The close date is in the past or slipped this week
- The stage has not moved in 30+ days
- The comment contradicts the data (e.g. says "on track" but the date slipped)

### 5. Build the digest email
Send it **to the user only**, never to anyone else unless the user explicitly asks.

Subject: `Next steps – week [ISO week] – [N] items, [M] need attention`

Group in this order: current quarter by type, then next quarter by type. Needs-attention items first in each group.

For each item:

```
[Account] – [Record name]  ⚠ Needs attention (if applicable)
Link: [direct CRM URL to the record]
Stage: [stage] | Amount: [x] | Close: [date]
Movement this week: [1 line, or "No recorded movement"]
Current comment: "[existing comment]" (last updated [date])
Proposed comment: "[new comment]"
```

End with:
- **Book before Monday:** items without a booked next meeting
- **Raise in forecast call:** top 2-3 risks, one line each

Use each record's real URL (for Salesforce Lightning: `https://<instance>.lightning.force.com/lightning/r/Opportunity/<Id>/view`). Never invent an Id or URL; if it is missing, write "Link: [not available]".

If no email connector is available, show the digest in chat, formatted the same way.

### 6. Don't write to the CRM
Only propose. The user reviews and pastes approved comments themselves, unless they explicitly ask you to update the records and a connector with write access is available. Even then, confirm the full list of changes before writing.

## Examples

Renewal, weak: "Had a good meeting with customer. Following up on renewal. Looks positive."
Renewal, strong: "[29.09] CFO confirmed renewal budget; open question is 1- vs 3-year term. Pricing review with CFO and procurement on 08.10. Risk: procurement wants a competing quote; need deal desk input on multi-year pricing by 03.10."

Use case, weak: "Customer interested in AI use case. Will follow up."
Use case, strong: "[29.09] Loyalty team validated a churn-prediction use case; est. X/month in usage from go-live. Scoping workshop with Head of CRM on 07.10. Target go-live next quarter; depends on marketing data being connected."
