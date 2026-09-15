# Prompt 1 — Support Ticket Triage

**Workflow stage:** Intake

| | |
| --- | --- |
| **Task** | Read one incoming support message and sort it by category, urgency and app tab. |
| **Problem it solves** | Holly reads and files every support message by hand. Without consistent labels, messages can't be counted or tracked. |
| **Prompting techniques** | Role framing; fixed answer options (constraints); a fixed output format a tracker can read (structured output); splitting a message into separate issues (decomposition). |

## Final prompt (v3)

> Role: You are a support operations analyst for Hauly, an app for organising a personal makeup and skincare collection (not a shopping app).
> Action: If the user message contains more than one issue, split it into separate issues and classify each one.
> Context: Category options: bug, feature_request, account, how_to, praise, complaint, other. Payment and subscription problems are "account". Urgency options: low, medium, high. Tab options: Haul, Restock, Match, Studio, Circle, Account, Unknown. User message: "{{message}}"
> Expected output: Return ONLY valid JSON with this format, no text outside it: {"issues": [{"category": "...", "urgency": "...", "affected_tab": "...", "one_line_summary": "max 15 words"}], "needs_human_review": true or false, "review_reason": "text or null"}. Set needs_human_review to true if there is more than one issue, or if the message mentions payment, safety, or lost data.

Words in `{{double brackets}}` are filled in each time the prompt is used.

## How the prompt was improved

All versions were tested on the same sample message (written for testing, based on real Hauly features): *"Hi, I got charged twice for Hauly Plus this month and now my Restock tab won't load at all. Also, could you add a way to track how much I spend on products?"*

**v1** — one line: *"Sort this message."*
- **Result:** it made up its own labels ("Billing Issue", "Bug Report") in a long formatted list. It also guessed the Restock problem might be linked to "premium features", but Restock is free in Hauly.

**v2** — added a Role, fixed lists of categories, urgency levels and tabs, and a fixed output format.
- **Result:** the format worked and used only the allowed labels. But it filed the whole message as one `bug`, so the double payment and the feature request were lost inside a single label.

**v3 (final)** — split messages into separate issues, said payment problems count as `account`, and added a "needs human review" flag.
- **Result:** three separate issues — `account` (double charge), `bug` (Restock tab), `feature_request` (spending tracker) — with `needs_human_review: true` because of the payment problem.

Full test outputs: [Appendix — Prompt 1](../appendix-test-outputs.md#prompt-1).

## Automation potential

**High** for the first sort. The fixed format means results can go straight into a tracking sheet, and the review flag sends payment, safety and multi-issue messages to Holly.

## Risks and limitations

- Urgency is the AI's judgement, not a guarantee.
- Unclear messages can still be sorted wrongly.
- Messages contain personal details, so only the message text should be pasted in — never payment details or email addresses.
