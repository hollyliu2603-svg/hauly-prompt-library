# Plain-Language Glossary

Quick definitions for talking through this portfolio out loud (e.g. in the
oral presentation) without needing the textbook wording.

**Prompt** — the instruction you give the AI. This library has 10 of them,
one per Hauly task (support replies, App Store responses, moderation, etc.).

**RACE framework** — the 4-part shape every prompt follows so it's a
structured instruction, not just a vague sentence:
- **Role** — who the AI should act as
- **Action** — what to actually do
- **Context** — the details it needs to do it well
- **Expected output** — what the answer should look like

This is the structure the subject teaches (Topic 3, Figure 1.9).

**v1 / v2** — v1 is the first, rough version of a prompt. v2 is the improved
version after testing it and noticing a problem. Showing both — and *why*
v2 changed — is what proves you actually iterated, not just wrote it once.

**A/B test** — running v1 and v2 on the exact same input and comparing the
two answers side by side, instead of just assuming the new one is better.

**Automation potential** — how much of a task the AI can safely handle on
its own vs. how much still needs Holly to check before it goes out.

**Human-in-the-loop** — a required check by a person before anything is
sent, published, or removed. Nothing in this library skips that step for
anything public or permanent.

**Debiasing techniques** — three specific checks (all from Topic 3), used
together in Prompt 6, to stop the AI from favouring one type of user:
1. telling it directly to use inclusive language
2. testing its answer against a few different kinds of users
3. asking it to double-check its own answer for bias before finishing

**Hallucination** — when an AI states something confidently that isn't
actually true, or wasn't in the information it was given.

**Over-reliance** — trusting the AI's output as final without a human check,
even when it could be wrong.
