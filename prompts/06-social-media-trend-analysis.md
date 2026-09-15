# Prompt 6 — Trend Analysis and Gazette Planning

**Workflow stage:** Content planning

| | |
| --- | --- |
| **Task** | Assess social media trends that Holly has collected, and recommend whether any should become an article in the Gazette (Hauly's in-app editorial section). |
| **Problem it solves** | Beauty trends often come with exaggerated claims and one narrow beauty standard. Choosing topics without checking can spread misinformation or leave many users out. |
| **Prompting techniques** | Role framing; a seven-section structure (decomposition); a "use only supplied information" rule (constraint); the three debiasing techniques from Topic 3 (La Trobe University, 2026) — inclusive-language guidance, testing the idea against different types of users (counterfactual prompting), and a self-check (self-critique). |

## Final prompt (v3)

> Role: You are Hauly's beauty editorial strategist.
> Action: Analyse the supplied social media trends, decide which are relevant to Hauly's audience and Gazette, and produce a content recommendation — including a check of your own recommendation for bias and exclusion before finishing.
> Context: Hauly is an app for organising a makeup and skincare collection. The Gazette is Hauly's in-app editorial section (inside Learn, in the Studio tab) with practical beauty and skincare education, not product selling. Use only the supplied information as evidence; do not invent engagement figures, sources, audience reactions, or popularity. Consider whether each trend supports Hauly's educational purpose, could become a lasting (evergreen) article, and whether it creates medical, safety, misinformation or exaggerated-claim risk. Use inclusive language and do not assume one skin tone, gender, age, skin type, budget, or routine represents all Hauly users; do not describe a trend as suitable for everyone. Do not add background facts that are not in the supplied information (for example how to do a technique, which products it uses, who it suits, or its history). If background knowledge would help, write it as a question in a "Questions to research" list inside section (2) instead of stating it as fact. Supplied trends: "{{trends}}"
> Expected output: For each trend, seven sections: (1) Trend overview — what the evidence shows, and whether it looks established, emerging, or unclear (use "unclear" when the evidence is thin); (2) Evidence limitations — what's missing, and any claims that shouldn't be treated as proven; (3) Relevance to Hauly — with a 1–5 score; (4) Content recommendation — working title, angle, target reader, three key learning points, format, and evergreen / seasonal / trend-led; (5) Bias and inclusion review — test the recommendation against a beginner, a budget-conscious user, a user with sensitive skin, a user from a different cultural background, and a user with a minimal routine, and name any assumptions found; (6) Editorial and safety risks; (7) Status — one of "suitable for founder review", "needs more evidence", or "not suitable for Gazette development". This output must be reviewed and approved by the founder before anything is published.

Words in `{{double brackets}}` are filled in each time the prompt is used.

## How the prompt was improved

All versions were tested on the same two sample trends (written for testing): a slugging video (2.1M views, shown mostly on fair/light-skin creators) and an ice-rolling video claiming it *"cured my cystic acne overnight"* (4.8M views).

**v1** — asked for a relevance score and content ideas.
- **Result:** it did flag the acne claim as medical and scored it 2/5. But it still proposed three ice-roller article ideas, invented Gazette sections that don't exist ("Nighttime Routines", "Trend Watch"), and didn't examine how weak the evidence was (one video per trend).

**v2** — added the seven sections, the evidence rule, the bias checks, and three allowed status labels.
- **Result:** it listed what the evidence couldn't prove, ran all five user checks, and marked the acne trend "not suitable for Gazette development". But it added facts that weren't in the input — for example that slugging is "a widely known, long-standing skincare technique" and that cystic acne is "inflammatory/hormonal".

**v3 (final)** — added one rule: don't add outside facts; list them as "questions to research" instead.
- **Result:** most outside facts became research questions (for example "Is there guidance on which skin types or climates this may or may not suit?"). Because only one video was supplied, it rated slugging "unclear" and "needs more evidence". A few general statements remained (for example calling occlusive moisturising "a routine cosmetic practice"), so a human fact-check is still needed.

Full test outputs: [Appendix — Prompt 6](../appendix-test-outputs.md#prompt-6).

## Automation potential

**Medium.** It organises and checks evidence Holly has already gathered. It can't search social media itself, and nothing is published without Holly's approval.

## Risks and limitations

- The AI still adds some outside information despite the rule.
- The bias check tests five types of users — it lowers the risk of excluding people but doesn't prove the content is inclusive.
- The result depends on the trends Holly supplies; a narrow sample gives a narrow result.
