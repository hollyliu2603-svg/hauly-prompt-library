# Prompt 1 — Support Ticket Triage

**Workflow stage:** Intake (its output feeds Prompt 2)

## Intended task

Read one incoming support message and turn it into a structured triage record: each issue's category, urgency and app tab, and whether Holly needs to review it.

## Problem being solved

Holly reads and files every support message by hand. Messages often mix several problems, and without consistent labels they can't be counted, tracked, or passed on to the next step.

## Prompting techniques

Role framing with role limits; fixed answer options (constraints); a review policy; structured JSON output with field names and data types; splitting a message into separate issues (decomposition).

## Automation potential

**High** — the first sort could be used with limited manual editing. Because the output is structured JSON with fixed fields, it can be passed straight into Prompt 2 (reply drafting) or a tracking sheet — this chaining is what raises the automation potential. The `needs_human_review` flag routes payment, safety, lost-data and multi-issue messages to Holly.

## Risks and limitations

- Urgency is the AI's judgement, not a guarantee.
- Unclear messages can still be sorted wrongly.
- The output must be checked for the right *types*, not just field names, before another step uses it.
- Messages contain personal details, so only the message text should be used — never payment details or email addresses.

## What the versions illustrate

| Version | What changed | What to notice in the response |
| --- | --- | --- |
| V1 | One line: "Sort this message" | Made up its own labels ("Billing Issue", "Bug Report") in a formatted list, and guessed the Restock problem might be linked to "premium features" — but Restock is free in Hauly |
| V2 | Adds Role, fixed options and a JSON format | Uses only allowed labels, but files a three-issue message as a single `bug` |
| V3 | Splits issues, defines payment as `account`, adds a review flag | Three correctly labelled issues and `needs_human_review: true` |
| V4 (final) | Adds role limits, a written review policy, exact data types, and `review_reasons` as a list | Same correct classification, with `needs_human_review` as true/false and reasons as a list; it still wrapped the JSON in code-formatting marks despite "no text outside it" |

**Discussion:** All four versions used the same message, so the comparison is controlled. V4 matters because a later step needs the right field *types*, not just the right names: V3 did not say whether reasons should be text or a list, so another run could change the shape. The leftover code-formatting marks around the JSON in V3 and V4 would need removing before another system reads it.

## Final prompt — reusable template (V4)

> **Role:** You are a support operations analyst for Hauly, an app for organising a personal makeup and skincare collection (not a shopping app). You classify messages; you do not reply to users, issue refunds, or promise fixes.  
>
> **Action:** If the user message contains more than one issue, split it into separate issues and classify each one. Decide whether human review is needed.  
>
> **Context:** Category options: bug, feature_request, account, how_to, praise, complaint, other. Payment and subscription problems are "account". Urgency options: low, medium, high. Tab options: Haul, Restock, Match, Studio, Circle, Account, Unknown. Review policy: human review is required if the message has more than one issue, or mentions payment, safety, or lost data. User message: "{{message}}"  
>
> **Expected output:** Return pretty-printed JSON only, no text outside it, with exactly these fields and types:  
> - "issues": a list (even if there is only one issue) of objects, each with "category" (text, one of the category options), "urgency" (text, one of the urgency options), "affected_tab" (text, one of the tab options), and "one_line_summary" (text, max 15 words)  
> - "needs_human_review": true or false (not text)  
> - "review_reasons": a list of text reasons, or an empty list [] if no review is needed  
> Do not invent details that are not in the message.  

Words in `{{double brackets}}` are filled in each time the prompt is used.

## Versions and recorded responses

Every version below was run once on the same sample input, written for testing and based on real Hauly features (not a real user message). Tests used Claude Sonnet 5 in September 2026. Responses are copied exactly as returned.

**Sample input:** *"Hi, I got charged twice for Hauly Plus this month and now my Restock tab won't load at all. Also, could you add a way to track how much I spend on products?"*

### V1

**Prompt text (as tested)**

~~~text
Sort this message.

Message: "Hi, I got charged twice for Hauly Plus this month and now my Restock tab won't load at all. Also, could you add a way to track how much I spend on products?"
~~~

**Recorded response**

~~~text
Here's the message sorted into distinct categories:

## 1. Billing Issue 💳
**Type:** Duplicate charge / Refund request
- Charged twice for "Hauly Plus" subscription this month
- **Priority:** High (financial/urgent)
- **Action needed:** Verify transaction history, process refund for duplicate charge

## 2. Bug Report 🐛
**Type:** Technical issue / App functionality
- "Restock" tab fails to load entirely
- **Priority:** High (blocking feature use)
- **Action needed:** Investigate load failure — possibly linked to account/billing issue above, or a separate technical bug

## 3. Feature Request 💡
**Type:** Product enhancement
- Requesting a spending tracker for products purchased
- **Priority:** Low/Medium (not urgent, no functionality broken)
- **Action needed:** Log for product team review; not time-sensitive

---

**Note:** Issues #1 and #2 might be related — sometimes a billing conflict (e.g., duplicate charge causing account flag) can cause premium features like "Restock" to malfunction. Worth checking if resolving the refund also fixes the tab loading issue.

Want me to draft a support response, or reformat this into a ticket/table for tracking?
~~~

### V2

**Prompt text (as tested)**

~~~text
Role: You are a support operations analyst for Hauly, an app for organising a personal makeup and skincare collection (not a shopping app).
Action: Classify the user message below.
Context: Category options: bug, feature_request, account, how_to, praise, complaint, other. Urgency options: low, medium, high. Tab options: Haul, Restock, Match, Studio, Circle, Account, Unknown. User message: "Hi, I got charged twice for Hauly Plus this month and now my Restock tab won't load at all. Also, could you add a way to track how much I spend on products?"
Expected output: Return ONLY valid JSON with this format, no text outside it: {"category": "...", "urgency": "...", "affected_tab": "...", "one_line_summary": "max 15 words"}
~~~

**Recorded response**

~~~text
{"category": "bug", "urgency": "high", "affected_tab": "Restock", "one_line_summary": "Double-charged for Hauly Plus; Restock tab not loading; also requests spending tracker feature."}
~~~

### V3

**Prompt text (as tested)**

~~~text
Role: You are a support operations analyst for Hauly, an app for organising a personal makeup and skincare collection (not a shopping app).
Action: If the user message contains more than one issue, split it into separate issues and classify each one.
Context: Category options: bug, feature_request, account, how_to, praise, complaint, other. Payment and subscription problems are "account". Urgency options: low, medium, high. Tab options: Haul, Restock, Match, Studio, Circle, Account, Unknown. User message: "Hi, I got charged twice for Hauly Plus this month and now my Restock tab won't load at all. Also, could you add a way to track how much I spend on products?"
Expected output: Return ONLY valid JSON with this format, no text outside it: {"issues": [{"category": "...", "urgency": "...", "affected_tab": "...", "one_line_summary": "max 15 words"}], "needs_human_review": true or false, "review_reason": "text or null"}. Set needs_human_review to true if there is more than one issue, or if the message mentions payment, safety, or lost data.
~~~

**Recorded response**

~~~text
```json
{"issues": [{"category": "account", "urgency": "high", "affected_tab": "Account", "one_line_summary": "User charged twice for Hauly Plus subscription this month"}, {"category": "bug", "urgency": "high", "affected_tab": "Restock", "one_line_summary": "Restock tab fails to load entirely"}, {"category": "feature_request", "urgency": "low", "affected_tab": "Unknown", "one_line_summary": "Add feature to track spending on products"}], "needs_human_review": true, "review_reason": "Multiple issues reported and message involves a payment/billing problem (double charge)"}
```
~~~

### V4 (final)

**Prompt text (as tested)**

~~~text
Role: You are a support operations analyst for Hauly, an app for organising a personal makeup and skincare collection (not a shopping app). You classify messages; you do not reply to users, issue refunds, or promise fixes.
Action: If the user message contains more than one issue, split it into separate issues and classify each one. Decide whether human review is needed.
Context: Category options: bug, feature_request, account, how_to, praise, complaint, other. Payment and subscription problems are "account". Urgency options: low, medium, high. Tab options: Haul, Restock, Match, Studio, Circle, Account, Unknown. Review policy: human review is required if the message has more than one issue, or mentions payment, safety, or lost data. User message: "Hi, I got charged twice for Hauly Plus this month and now my Restock tab won't load at all. Also, could you add a way to track how much I spend on products?"
Expected output: Return pretty-printed JSON only, no text outside it, with exactly these fields and types:
- "issues": a list (even if there is only one issue) of objects, each with "category" (text, one of the category options), "urgency" (text, one of the urgency options), "affected_tab" (text, one of the tab options), and "one_line_summary" (text, max 15 words)
- "needs_human_review": true or false (not text)
- "review_reasons": a list of text reasons, or an empty list [] if no review is needed
Do not invent details that are not in the message.
~~~

**Recorded response**

~~~text
```json
{
  "issues": [
    {
      "category": "account",
      "urgency": "high",
      "affected_tab": "Account",
      "one_line_summary": "User was charged twice for Hauly Plus subscription this month."
    },
    {
      "category": "bug",
      "urgency": "high",
      "affected_tab": "Restock",
      "one_line_summary": "Restock tab fails to load entirely."
    },
    {
      "category": "feature_request",
      "urgency": "low",
      "affected_tab": "Unknown",
      "one_line_summary": "User wants a way to track product spending."
    }
  ],
  "needs_human_review": true,
  "review_reasons": [
    "More than one issue reported",
    "Message mentions payment"
  ]
}
```
~~~

## Prompt Lab check (GPT-4.1 mini)

To check the results weren't specific to one AI model, the final version (and in some cases the first version) was re-run in La Trobe Prompt Lab using GPT-4.1 mini, with exactly the same prompt text. Prompt Lab's prompt review, where run, scores the prompt itself out of 100.

**What GPT-4.1 mini did:**

- **Same result as Claude Sonnet 5:** `issues` and `review_reasons` were lists, `needs_human_review` was `true` (not text), only allowed labels were used, and review was required because of multiple issues and lost data.
- **Difference:** it labelled the lost collection as a second `bug`; Claude Sonnet 5 labelled it `complaint`. Both are allowed options, so the category list could say more clearly which to use for data loss.
- **Same weakness:** it also wrapped the JSON in code-formatting marks despite "no text outside it".

This response was also used as the triage record for the Prompt 2 check.

### Prompt Lab — V4

**Recorded response (GPT-4.1 mini)**

~~~text
```json
{
  "issues": [
    {
      "category": "bug",
      "urgency": "high",
      "affected_tab": "Haul",
      "one_line_summary": "App crashes when adding new product to Haul"
    },
    {
      "category": "bug",
      "urgency": "high",
      "affected_tab": "Haul",
      "one_line_summary": "Lost half of collection already typed in"
    }
  ],
  "needs_human_review": true,
  "review_reasons": [
    "Multiple issues reported",
    "Lost data mentioned"
  ]
}
```
~~~
