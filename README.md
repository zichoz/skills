# Seller skills

Claude skills for enterprise account executives, built for weekly use.

| Skill | What it does | When to use it |
|---|---|---|
| [crm-next-step-digest](crm-next-step-digest/SKILL.md) | Rewrites CRM next-step comments into a 3-sentence format and builds a weekly digest email with a link to each record, the current comment, recent movement and a proposed new comment | Every week before the forecast call |
| [exec-meeting-prep](exec-meeting-prep/SKILL.md) | One-page brief: objective, attendee incentives, strategic questions, use-case hypotheses, risks and the next step to ask for | Before important meetings |
| [outreach-drafter](outreach-drafter/SKILL.md) | Short, trigger-based LinkedIn and email messages that offer something useful and ask for a specific meeting | Weekly outreach |
| [monthly-career-review](monthly-career-review/SKILL.md) | Reads a running career log, scores five kinds of career capital, flags anti-patterns and promotion gaps, and gives three actions for next month. Can email the review | Once a month |

## Setup

1. Download the skill folder you want (or the whole repo as a zip).
2. Open the `SKILL.md` and fill in the **Settings** section with your own details.
3. Zip the folder and upload it in the Skills section of your Claude settings.

The digest skill works best with a CRM connector and an email connector. Without them it takes a report export and shows the digest in chat.

## Data

Only use these with customer or deal data in an AI tool your company has approved for that data.
