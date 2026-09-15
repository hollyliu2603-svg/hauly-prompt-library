# 5. Feature Request Evaluation & Prioritisation Scoring

**What it does:** Scores one feature request so it can feed into a
prioritisation backlog, instead of Holly judging each one purely on gut feel
or how loudly it was asked for.

**Technique used:** RACE structure, with fixed scoring categories so every
request is judged the same way.

> **Role:** You are a product analyst helping an indie founder prioritise feature
> requests.
>
> **Action:** Score the feature request below.
>
> **Context:** Confirmed current product principles: {{product_principles}}
> (e.g., as of this draft: no pricing shown in-app, usernames only — no real
> names — for social features, freemium model capped at 30 products free tier,
> no retail/shopping framing; confirm these are still current before each use).
> Confirmed technology stack, if relevant: {{tech_stack}}. Feature request:
> "{{request}}". Frequency mentioned (if known): {{frequency}}
>
> **Expected output:** A 1–5 score on each of: user demand signal, alignment with
> product principles, and estimated build complexity (low/med/high). Flag
> explicitly if the request conflicts with a stated product principle, with
> one-sentence reasoning per score.

**v1 → v2 note:** The first version of this prompt didn't ask the AI to
check requests against Hauly's actual product principles (no pricing shown
in-app, usernames only, etc.) — it just scored "how good is this idea?" in
the abstract. That meant a request that quietly broke a product principle
(e.g. someone asking for price comparisons) could score well anyway. Adding
an explicit "flag if it conflicts with a stated principle" step fixed that.

**Why it matters:** As a solo founder, it's easy to get pulled toward
whoever asks the loudest rather than what's actually best for the app;
principle conflicts need to be caught before something gets built.

**How much can run on its own:** Medium — useful as a first-pass, consistent
scorecard, not a replacement for Holly's own judgement on bigger bets.

**Watch out for:** Complexity scores are only a rough guess based on the
stack named in the prompt, not a real engineering estimate — the AI can't
see the actual codebase. Scores should be treated as a starting point, not
the final word, so they don't quietly override the founder's own judgement.
