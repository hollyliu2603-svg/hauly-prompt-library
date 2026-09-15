# Prompt 5 — Feature Request Scoring

**Workflow stage:** Planning

| | |
| --- | --- |
| **Task** | Score one feature request so it can be compared with others. |
| **Problem it solves** | Without a consistent method, it is easy to build whatever is asked for most loudly, even when it goes against what Hauly stands for. |
| **Prompting techniques** | Role framing; Hauly's real product principles written into the prompt (context); fixed scores (structured output); a required conflict flag (constraint). |

## Final prompt (v2)

> Role: You are a product analyst helping an indie founder prioritise feature requests.
> Action: Score the feature request below.
> Context: Hauly is an iPhone app for organising a makeup and skincare collection. Hauly's product principles: Hauly is for organising, not shopping — no prices or shopping features (the only exception is free-text prices on Rehome posts, shown only to the author); @usernames only, never real names, in social features; the word "lookalike", never "dupe"; free accounts can save up to 35 products, and Hauly Plus removes the limit. Feature request: "{{request}}". Number of requests: {{request_count}}.
> Expected output: A 1–5 score for user demand, a 1–5 score for fit with the product principles, and build effort (low/medium/high), each with one sentence of reasoning. Clearly flag any conflict with a product principle.

Words in `{{double brackets}}` are filled in each time the prompt is used.

## How the prompt was improved

All versions were tested on the same sample message (written for testing, based on real Hauly features): *"Can you show the price of each product and tell me where it's cheapest to restock? That would make Restock so much more useful."* The prompt was also told it had been requested 14 times (a sample number).

**v1** — scored "overall value" without Hauly's product principles.
- **Result:** it gave the request 4/5 for value, saying it "could meaningfully increase engagement". It never noticed that Hauly deliberately has no prices or shopping features.

**v2 (final)** — added Hauly's actual product principles, replaced "overall value" with "fit with the product principles", and required a conflict flag.
- **Result:** it scored principle fit **1/5** and flagged a "direct conflict" with "no prices or shopping features". It recommended declining or reworking the request, and suggested an alternative that stays within the principles.

Full test outputs: [Appendix — Prompt 5](../appendix-test-outputs.md#prompt-5).

## Automation potential

**Medium.** Useful as a consistent first-pass score. Final decisions on what to build stay with Holly.

## Risks and limitations

- Build-effort scores are rough guesses — the AI can't see the app's code.
- The product principles in the prompt must be kept up to date, or requests will be judged against old rules.
- Request counts are only as good as the way requests are logged.
