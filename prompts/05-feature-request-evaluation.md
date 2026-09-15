# Prompt 5 — Feature Request Scoring

**Workflow stage:** Planning

## Intended task

Score one feature request so it can be compared with others.

## Problem being solved

Without a consistent method, it is easy to build whatever is asked for most loudly, even when it goes against what Hauly stands for.

## Prompting techniques

Role framing; Hauly's real product principles as approved context; fixed scores (structured output); a required conflict flag (constraint).

## Automation potential

**Medium.** Useful as a consistent first-pass score. Final decisions on what to build stay with Holly.

## Risks and limitations

- Build-effort scores are rough guesses — the AI can't see the app's code.
- The product principles in the prompt must be kept up to date.
- Request counts are only as good as the way requests are logged.

## What the versions illustrate

| Version | What changed | What to notice in the response |
| --- | --- | --- |
| V1 | Scores "overall value" without Hauly's principles | Gives the price-comparison request 4/5 for value ("could meaningfully increase engagement"), never noticing Hauly has no prices or shopping features |
| V2 (final) | Adds Hauly's product principles, a "fit with principles" score, and a conflict flag | Scores fit 1/5, flags a "Direct conflict" with "no prices or shopping features", recommends declining or reworking it |

**Discussion:** Both versions used the same request (with a sample count of 14 requests). The model could only judge fit with Hauly once Hauly's principles were given to it as approved facts.

## Final prompt — reusable template (V2)

> **Role:** You are a product analyst helping an indie founder prioritise feature requests.  
>
> **Action:** Score the feature request below.  
>
> **Context:** Hauly is an iPhone app for organising a makeup and skincare collection. Hauly's product principles: Hauly is for organising, not shopping — no prices or shopping features (the only exception is free-text prices on Rehome posts, shown only to the author); @usernames only, never real names, in social features; the word "lookalike", never "dupe"; free accounts can save up to 35 products, and Hauly Plus removes the limit. Feature request: "{{request}}". Number of requests: {{request_count}}.  
>
> **Expected output:** A 1–5 score for user demand, a 1–5 score for fit with the product principles, and build effort (low/medium/high), each with one sentence of reasoning. Clearly flag any conflict with a product principle.  

Words in `{{double brackets}}` are filled in each time the prompt is used.

## Versions and recorded responses

Every version below was run once on the same sample input, written for testing and based on real Hauly features (not a real user message). Tests used Claude Sonnet 5 in September 2026. Responses are copied exactly as returned.

**Sample input:** *"Can you show the price of each product and tell me where it's cheapest to restock? That would make Restock so much more useful."* (requested 14 times — a sample number)

### V1

**Prompt text (as tested)**

~~~text
Role: You are a product analyst helping an indie founder prioritise feature requests.
Action: Score the feature request below.
Context: Hauly is an iPhone app for organising a makeup and skincare collection. Feature request: "Can you show the price of each product and tell me where it's cheapest to restock? That would make Restock so much more useful.". Requested by 14 users this month.
Expected output: A 1–5 score for user demand, a 1–5 score for overall value, and build effort (low/medium/high), each with one sentence of reasoning.
~~~

**Recorded response**

~~~text
**User Demand: 4/5**
14 requests in a single month for a niche organization app is a strong, concentrated signal that this isn't a fringe want — it's a recurring pain point tied to your most-used feature (Restock).

**Overall Value: 4/5**
It directly deepens the core Restock use case (turning "what do I need" into "what should I buy and where"), which could meaningfully increase engagement and justify premium pricing, though it's an enhancement rather than a new core capability.

**Build Effort: High**
Delivering accurate, up-to-date pricing and "cheapest retailer" comparisons requires either manual data entry (poor UX, high maintenance) or integrating/maintaining multiple retailer APIs or scrapers — a significant and ongoing engineering and data-maintenance burden for an indie team.
~~~

### V2 (final)

**Prompt text (as tested)**

~~~text
Role: You are a product analyst helping an indie founder prioritise feature requests.
Action: Score the feature request below.
Context: Hauly is an iPhone app for organising a makeup and skincare collection. Hauly's product principles: Hauly is for organising, not shopping — no prices or shopping features (the only exception is free-text prices on Rehome posts, shown only to the author); @usernames only, never real names, in social features; the word "lookalike", never "dupe"; free accounts can save up to 35 products, and Hauly Plus removes the limit. Feature request: "Can you show the price of each product and tell me where it's cheapest to restock? That would make Restock so much more useful.". Requested by 14 users this month.
Expected output: A 1–5 score for user demand, a 1–5 score for fit with the product principles, and build effort (low/medium/high), each with one sentence of reasoning. Clearly flag any conflict with a product principle.
~~~

**Recorded response**

~~~text
# Feature Request Scoring: Price Display + Cheapest Restock Location

**User Demand: 3/5**
14 requests in one month is a meaningful signal for a specific feature, but it's not (yet) an overwhelming groundswell — worth tracking for trend velocity next month.

**Product Principle Fit: 1/5**
🚩 **Direct conflict**: Hauly's core principle is explicitly "organising, not shopping — no prices or shopping features," with the *only* sanctioned exception being free-text prices on Rehome posts visible solely to the author. Showing product prices and price-comparison-for-purchase (cheapest restock location) is essentially a shopping/price-comparison feature — the exact thing the product has deliberately excluded.

**Build Effort: High**
Even setting the principle conflict aside, "cheapest place to restock" would require live retailer price feeds/integrations, ongoing price maintenance, and likely affiliate or scraping infrastructure — a significant scope and maintenance burden for a small team.

---

**Recommendation:** Decline or heavily reframe. This isn't a "not now" — it's a "not this," since it contradicts a stated product principle rather than just being low priority. If the underlying user need is "I want to know when I'm running low and remember where I usually buy this," consider a lighter-touch alternative that stays in "organising" territory — e.g., a free-text "usual restock notes" field per product (similar in spirit to the Rehome price exception) rather than live price comparison. That would address some of the intent without turning Hauly into a shopping/price tool.
~~~
