# Hauly Prompt Library

**BUS4005 — Assessment 1: Individual Prompt Library, Oral Presentation and Report**
La Trobe University, Term 5 2026

## 1. Business context

Hauly is an iPhone app for organising a personal makeup and skincare collection. Users track the products they own and their expiry dates, keep a restock list, find lookalike products, read the Gazette (Hauly's in-app editorial section), and share with friends in Circle, a private social feed. Hauly is deliberately **for organising, not shopping**: it shows no prices or shopping features, and social features use @usernames rather than real names. Free accounts can save up to 35 products; Hauly Plus is the paid upgrade.

Hauly is run by one person. As solo founder, Holly handles every operational job — support, bug triage, feature planning, community moderation, content and reporting — jobs a larger company would split across several roles.

## 2. The workflow

The ten prompts follow Hauly's operations from a message arriving to a weekly decision:

| Stage | Prompt | What it does |
| --- | --- | --- |
| Intake | [1. Support Ticket Triage](prompts/01-support-ticket-triage.md) | Sorts each support message by category, urgency and app tab |
| Intake | [4. Bug Report Summary](prompts/04-bug-report-summarisation.md) | Turns a messy bug report into a clear ticket |
| Response | [2. Customer Support Reply Drafting](prompts/02-customer-support-reply-drafting.md) | Drafts a reply for Holly to check and send |
| Response | [3. Collection Ingredient Report](prompts/03-collection-ingredient-report.md) | Flags ingredient pairing cautions across a user's whole collection |
| Planning | [5. Feature Request Scoring](prompts/05-feature-request-evaluation.md) | Scores requests against Hauly's product principles |
| Moderation | [7. Circle Community Moderation](prompts/07-circle-community-moderation.md) | Recommends an action on a Circle post; a human decides |
| Content planning | [6. Trend Analysis and Gazette Planning](prompts/06-social-media-trend-analysis.md) | Checks trends for evidence, bias and safety before recommending an article |
| Content drafting | [8. FAQ and Gazette Drafting](prompts/08-faq-gazette-article-drafting.md) | Drafts help answers and approved articles |
| Content drafting | [9. Push Notification and Banner Copy](prompts/09-push-notification-copy.md) | Writes short announcement copy |
| Reporting | [10. Weekly Operations Report](prompts/10-weekly-trends-report.md) | Combines the week's data into one summary and recommendation |

## 3. Approved Hauly facts used in the prompts

The prompts give the AI checked facts about Hauly instead of letting it guess. These come from the Hauly app itself:

| Fact | Used in |
| --- | --- |
| **App tabs:** Haul, Restock, Match, Studio (which contains Learn and the Gazette), Circle | Prompts 1, 6 |
| **Organising, not shopping:** no prices or shopping features; the only exception is free-text prices on Rehome posts, shown only to the author | Prompts 5, 7 |
| **Privacy:** Circle uses @usernames only, never real names | Prompts 5, 7 |
| **Wording:** "lookalike", never "dupe" | Prompts 2, 5 |
| **Plans:** free accounts can save up to 35 products; Hauly Plus removes the limit | Prompt 5 |
| **Ingredient pairing list:** retinoids with AHAs, BHAs or vitamin C, and benzoyl peroxide with retinoids, AHAs, BHAs or vitamin C, should be introduced carefully — "can be harsh together — introduce them gradually or on alternate days" | Prompt 3 |
| **Circle rules:** no real names or personal details, no medical claims about what a product treats or cures, no harassment, no prices except on Rehome posts | Prompt 7 |
| **Team:** Hauly is run by one founder, with no wider team | Prompt 2 |

When a prompt is used, facts about a specific case (for example, whether a fix has been released) are added as "approved facts". If a fact isn't supplied, the prompt tells the AI not to invent it.

## 4. How every prompt is built

Every prompt uses the **RACE** structure from Module 1, Topic 3, Figure 1.9 (La Trobe University, 2026):

- **Role** — who the AI acts as
- **Action** — what it must do
- **Context** — the information it needs, including Hauly's real rules
- **Expected output** — exactly what the answer should look like

Giving the AI a role and describing the task precisely are among the core techniques identified in a review of prompting research (Hewing & Leinhos, 2024). The library also uses approved facts, fixed answer options, word and character limits, structured outputs with set data types, breaking tasks into sections, self-checks, and few-shot examples (sample inputs and outputs shown inside the prompt, used in Prompt 2).

**Prompts connect into a workflow.** Prompt 1 returns a structured triage record, which is passed straight into Prompt 2 as its input; Prompt 6's approved ideas feed Prompt 8; and Prompt 10 brings together results from Prompts 1, 4, 5, 6 and 7. Structured outputs are what make this chaining — and therefore automation — possible.

## 5. How the prompts were tested and improved

Module 1, Topic 3 recommends treating each prompt "as a hypothesis to be validated" through A/B testing. Each version of every prompt was run once on the same sample input and the outputs were compared. Where the improved version still fell short, further versions were written and tested: Prompts 1 and 2 have four versions, and Prompts 6 and 7 have three.

| Prompt | What went wrong in the first version | What the final version did |
| --- | --- | --- |
| 1 | Made up its own labels | Split a three-issue message into three correctly labelled issues, with a review flag and fixed data types |
| 2 | 231 words, several apologies, promised to tell "our team" | Used Prompt 1's triage record and few-shot examples; invented nothing and added a separate internal review note (but the reply was less specific than V3) |
| 3 | Gave its own pairing list and reassured users that some pairings had "No concern here" | Flagged only pairings on Hauly's list, marked unknown ingredients, added the disclaimer |
| 4 | Invented a technical cause for the bug | Gave no cause and marked guessed steps as "(inferred)" |
| 5 | Scored a price-comparison request 4/5 for value | Scored it 1/5 for fit and flagged a direct conflict with Hauly's no-prices principle |
| 6 | Invented Gazette sections and ignored how weak the evidence was | Rated evidence as thin, turned outside facts into research questions (a few general statements remained) |
| 7 | Output "remove", implying automatic deletion | Output "recommend_remove" with a human-review flag; the self-check didn't change the decision on this post |
| 8 | Silently guessed what kind of content to write | Asked for clarification instead of guessing |
| 9 | Missing a Role | Role added; both versions met every rule, so no visible difference |
| 10 | Presented guesses as facts | Separated given numbers from guesses and marked missing data |

Each prompt's page shows every version's full prompt text and recorded response. The [Evaluation](evaluation.md) compares the two most detailed examples.

## 6. Report contents

| Document | Purpose |
| --- | --- |
| [prompts/](prompts/) | One page per prompt: task, problem, techniques, automation potential, risks, what the versions illustrate, final prompt, and every version's prompt text and recorded response |
| [evaluation.md](evaluation.md) | Testing method and the two most detailed before-and-after comparisons |
| [business-case-and-governance.md](business-case-and-governance.md) | Business value, risks, safeguards and limitations |
| [references.md](references.md) | Reference list (APA 7th) |
