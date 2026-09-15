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
| V2 | Adds Hauly's product principles, a "fit with principles" score, and a conflict flag | Scores fit 1/5, flags a "Direct conflict" with "no prices or shopping features", recommends declining or reworking it |
| V3 (final) | Updates the first-name principle: users choose whether to add a first name, which may not be their real one | Same result as V2 — demand 3/5, fit 1/5, “Direct conflict” with “no prices or shopping features”, recommends declining or reframing |

**Discussion:** All versions used the same request (with a sample count of 14 requests). The model could only judge fit with Hauly once Hauly's principles were given to it as approved facts. V3 was a maintenance re-test: the original wording ("@usernames only, never real names") didn't match the app, where each user decides whether to add a first name. Correcting it didn't change the result, which is expected because this request is about prices, not names.

## Final prompt — reusable template (V3)

> **Role:** You are a product analyst helping an indie founder prioritise feature requests.  
>
> **Action:** Score the feature request below.  
>
> **Context:** Hauly is an iPhone app for organising a makeup and skincare collection. Hauly's product principles: Hauly is for organising, not shopping — no prices or shopping features (the only exception is free-text prices on Rehome posts, shown only to the author); @usernames in social features, and each user decides whether to add a first name, which may not be their real one; the word "lookalike", never "dupe"; free accounts can save up to 35 products, and Hauly Plus removes the limit. Feature request: "{{request}}". Number of requests: {{request_count}}.  
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

### V2

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

### V3 (final)

Run once on 16 September 2026 with Claude Sonnet 5 through the Claude Code command line, with no tools and a one-character system prompt. The tool still adds a short identity line, the date and the account email; none of these relate to the task. As a check, V2 was re-run in the same setup and gave the same scores (demand 3/5, fit 1/5, build effort high).

**Prompt text (as tested)**

~~~text
Role: You are a product analyst helping an indie founder prioritise feature requests.
Action: Score the feature request below.
Context: Hauly is an iPhone app for organising a makeup and skincare collection. Hauly's product principles: Hauly is for organising, not shopping — no prices or shopping features (the only exception is free-text prices on Rehome posts, shown only to the author); @usernames in social features, and each user decides whether to add a first name, which may not be their real one; the word "lookalike", never "dupe"; free accounts can save up to 35 products, and Hauly Plus removes the limit. Feature request: "Can you show the price of each product and tell me where it's cheapest to restock? That would make Restock so much more useful.". Requested by 14 users this month.
Expected output: A 1–5 score for user demand, a 1–5 score for fit with the product principles, and build effort (low/medium/high), each with one sentence of reasoning. Clearly flag any conflict with a product principle.
~~~

**Recorded response**

~~~text
# Feature Request Scoring: Price Display & Cheapest Restock Location

**User Demand: 3/5**
14 requests in one month is a meaningful signal for a niche feature, but without knowing total active user count or how this compares to other requests, it reads as moderate rather than overwhelming demand.

**Product Principle Fit: 1/5**
🚩 **Direct conflict** — this request violates the core principle that "Hauly is for organising, not shopping — no prices or shopping features," with the only sanctioned exception being free-text prices on Rehome posts visible solely to the author; showing product prices and comparing restock pricing across retailers is exactly the shopping functionality the app is defined against.

**Build Effort: High**
Beyond the principle conflict, this would require integrating real-time retailer price data, mapping products to multiple sellers, and maintaining pricing accuracy — a significant technical and maintenance burden even if it were greenlit.

---

**Recommendation:** Decline or heavily reframe. This isn't a "tweak the principle" edge case — it asks Hauly to become a price-comparison/shopping tool, which is the opposite of its stated identity. If the underlying user need is "help me remember what to restock," consider a lighter-touch solution (e.g., a restock checklist or reminder feature) that addresses the *organizing* pain point without introducing prices or shopping links.
~~~

## Prompt Lab check (GPT-4.1 mini)

To check the results weren't specific to one AI model, the first and final versions were re-run in La Trobe Prompt Lab using GPT-4.1 mini, with exactly the same prompt text. Prompt Lab's prompt review scores the prompt itself out of 100.

**What GPT-4.1 mini did:**

| Version | Result | Compared with Claude Sonnet 5 |
| --- | --- | --- |
| V1 | Demand 4, **value 4**, build effort High; said prices and cheapest restock options "would significantly enhance the Restock feature's usefulness" and suggested "partnerships with retailers" — never noticed Hauly has no prices or shopping features | Same problem |
| V3 (final) | Demand 4, **fit 1**, build effort Medium; flagged that the feature "conflicts directly with Hauly's principle of avoiding prices and shopping features" | Same key result; demand and build effort scores differed (Claude: demand 3, effort High) |

- **Prompt Lab review:** V1 scored 82.25/100 and V3 scored 85.25/100. The V1 review did **not** notice the missing product principles — the reason V1 failed — and its suggested rewrite still asked for "overall value". The review judges how clearly a prompt is written, not whether it fits the business.

### Prompt Lab — V1

**Recorded response (GPT-4.1 mini)**

~~~text
User Demand: 4 – Requested by 14 users this month, indicating a strong interest though not yet a majority.  
Overall Value: 4 – Showing prices and cheapest restock options would significantly enhance the Restock feature’s usefulness and user satisfaction.  
Build Effort: High – Integrating price comparison and sourcing data likely requires complex backend work and partnerships with retailers or scraping multiple data sources.
~~~

**Prompt Lab review:** overall score 82.25/100

~~~text
Rubric Scores
* Clarity: 85/100 - The prompt is mostly clear about the role, context, and expected output, but could specify the scoring scale explicitly and clarify "overall value."
* Constraints: 80/100 - The prompt sets clear constraints on output format and content but could better define "build effort" categories and reasoning length.
* Structure: 80/100 - The prompt is logically structured but could benefit from bullet points or numbered lists for clarity and easier parsing.
* Verifiability: 75/100 - The prompt includes user request count as a data point but lacks guidance on how to verify or justify scores beyond that.
* Hallucination Risk: 90/100 - The prompt minimizes hallucination risk by focusing on scoring a given feature request with provided data, but some assumptions about build effort could lead to speculation.
Overall score: 82.25/100
Top Improvements
* Explicitly define scoring scales and criteria for each score to improve clarity and verifiability.
* Provide clearer definitions or examples for build effort categories to reduce ambiguity.
* Use bullet points or numbered lists to improve prompt structure and readability.
~~~

### Prompt Lab — V3 (final)

**Recorded response (GPT-4.1 mini)**

~~~text
User demand: 4 — Requested by 14 users this month, indicating strong interest and clear demand for enhanced Restock functionality.

Fit with product principles: 1 — This feature conflicts directly with Hauly’s principle of avoiding prices and shopping features, as it involves showing prices and suggesting purchase locations.

Build effort: Medium — Integrating price data and sourcing cheapest restock locations would require moderate backend work and possibly third-party data integrations.
~~~

**Prompt Lab review:** overall score 85.25/100

~~~text
Rubric Scores
* Clarity: 85/100 - The prompt is mostly clear about the role, context, and expected output, but could benefit from slightly more explicit instructions on formatting and reasoning detail.
* Constraints: 80/100 - The prompt includes relevant constraints (product principles) and output format, but could specify the scoring scale more explicitly and clarify the reasoning length.
* Structure: 80/100 - The prompt is logically structured with role, action, context, feature request, and expected output, but could separate instructions more distinctly for easier parsing.
* Verifiability: 90/100 - The prompt provides concrete data (14 users requesting) and clear product principles, enabling verifiable scoring and conflict detection.
* Hallucination Risk: 95/100 - The prompt minimizes hallucination risk by grounding the request in specific product principles and user data, reducing ambiguity.
Overall score: 85.25/100
Top Improvements
* Explicitly define the scoring scale (e.g., 1 = low, 5 = high) for user demand and fit with product principles.
* Clarify the expected length and detail of the reasoning sentences.
* Separate the instructions for scoring and conflict flagging more clearly to avoid confusion.
~~~

**Possible next version:** the V3 review suggested defining the scoring scale (for example, 1 = low, 5 = high). The two models gave different demand scores for the same request, so a defined scale could make scores more consistent. This was not tested, so it is not part of the final prompt.
