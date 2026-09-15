# Evaluation

## How testing worked

Module 1, Topic 3 (La Trobe University, 2026) describes treating each prompt "as a hypothesis to be validated", measured on outcomes such as accuracy, consistency, readability and alignment with business criteria. This library followed that approach:

1. **Write a first version (v1)** of each prompt.
2. **Test it** on a sample input written to reflect real Hauly features.
3. **Find what went wrong** in the output.
4. **Fix the prompt (v2)** and test it on the *same* input, so the two outputs can be compared fairly.
5. **Repeat (v3, v4)** where the new version still fell short — Prompts 1, 2 and 7 reached v4, and Prompts 5, 6 and 8 reached v3 (the last versions of Prompts 5 and 7 were a maintenance re-test after correcting the first-name wording).

All tests were run in September 2026 using Claude Sonnet 5, with no other instructions added. The maintenance re-tests of Prompts 5 and 7 were run through the Claude Code command line, which adds a short identity line, the date and the account email; re-running the previous versions in that setup gave the same results. Each version was run once. Because AI outputs vary from run to run, one run shows what the prompt *can* produce, not what it will produce every time.

Across the ten prompts, the most common problem in first versions was the AI **adding information that wasn't given** — an invented team (Prompt 2), an invented bug cause (Prompt 4), invented app sections (Prompt 6), and guesses presented as facts (Prompt 10). This matches research showing that language models "can generate outputs that are untruthful", and that even a model trained to follow instructions "still makes simple mistakes" (Ouyang et al., 2022, p. 1). The most effective fix was a direct rule telling the AI to use only the facts given, and what to do instead when something is missing.

## Cross-model check (La Trobe Prompt Lab, GPT-4.1 mini)

To check the results weren't specific to one model, the first and/or final versions of all ten prompts were re-run in La Trobe Prompt Lab using GPT-4.1 mini, with the same prompt text. Most runs were also scored by Prompt Lab's prompt review, which rates the prompt out of 100.

| Prompt | Held on GPT-4.1 mini | Differed on GPT-4.1 mini |
| --- | --- | --- |
| 1 (V4) | Correct data types, allowed labels, review flag | Labelled lost data as a second `bug` rather than `complaint` |
| 2 (V1, V3, V4) | V1 still wrote as a team; V3 invented nothing | V4 hinted at "how to recover your data" — not an approved fact |
| 3 (V1, V2) | V1 reassured and missed Hauly pairings; V2 exactly matched Hauly's list | — |
| 4 (V1, V2) | V1 invented a technical cause; V2 gave none | V2 marked fewer assumed steps and skipped "not provided" |
| 5 (V1, V3) | V1 scored value 4/5; V3 scored fit 1/5 and flagged the conflict (same in two runs each) | Build-effort score changed between runs |
| 6 (V2, V3) | — | Used "emerging"/"established" on one-video evidence, marked ice rolling "suitable for founder review", and stated many outside facts |
| 7 (V1, V4) | V1 said "remove"; V4 flagged both rules and required human review | V1 missed the real name; V4 chose `flag_for_review` instead of `recommend_remove` |
| 8 (V1, V2, V3) | V1 guessed the mode; V3 replied only `needs_clarification` | **V2 failed:** drafted an FAQ instead of replying `needs_clarification`, which led to V3 |
| 9 (V1, V2) | Both met every rule; the Role made no visible difference | — |
| 10 (V1, V2) | V2 invented no numbers and marked missing sections | **V1 invented last week's bug count** (the problem V2 fixes); V2 recommended three actions instead of one |

**What the reviews showed:** Prompt Lab's review scored every prompt between 72 and 91.5 out of 100. It did not notice that Prompt 8 V1's mode was missing, that Prompt 5 V1 lacked Hauly's principles, or that Prompt 7 V1's "remove" implied automatic deletion, and it scored Prompt 6 at over 90 even though the outputs broke the prompt's rules. Several suggestions asked for things the prompts already contained. The review is useful for checking how clearly a prompt is written, but it cannot replace testing the output against the business's real rules.

The two comparisons below show the process in the most detail.

## Example 1 — Prompt 2: Customer Support Reply Drafting

**Sample input:** *"The app keeps crashing when I try to add a new product to my Haul. This is so annoying, I've lost half my collection I already typed in!"*

| Criterion | V1 | V2 | V3 | V4 (final) |
| --- | --- | --- | --- | --- |
| Length (limit: under 80 words) | 231 words | 71 words | 66 words | Under 80 words |
| Specific to the user's problem | Partly | Yes | Yes — mentions lost work | Less specific — "how frustrating that must be" |
| Invented details | "flag this to our team" | "Our team is digging into" it; a workaround that "seems to help" | None | None |
| Clear next step | Several generic tips | An unconfirmed workaround | Asked for phone model and app version | Asked for device and app version |
| Internal review note | No | No | No | Yes — "Review: YES" with reasons from the triage record |

**V3 output (in full):**

> Hi there,
>
> Thank you for reporting this — that sounds really frustrating, especially losing the work you'd already put into your Haul.
>
> I'm looking into what's causing the crash right now. Could you tell me your phone model and the app version you're using? That'll help me track down what's going on.
>
> Thanks for your patience with me on this — I'll get it sorted.
>
> Holly

**V4 output (in full):**

> Reply: Thanks for flagging this — I can see how frustrating that must be. I'm looking into the crashing issue with adding new products to Haul. Could you tell me what device and app version you're using? That will help me dig into what's happening. — Holly
>
> Review: YES — multiple issues reported (crash + lost data) and message mentions lost data, with no confirmed workaround or data recovery.

**What this shows:** adding a Role, voice rules and a word limit (V2) fixed the length, but the AI still made up facts to sound helpful; an explicit "use only the facts given" rule (V3) stopped that. V4 connected Prompt 2 to Prompt 1 — the triage record became the input — and added two few-shot examples. The examples produced the exact Reply/Review pattern and an accurate internal review note, which makes the output easier to route automatically. But the reply no longer mentioned the lost collection, so the examples improved the format more than the quality of the reply. V4 also added the triage record and approved facts to the input, so it is not a pure same-input comparison with V1–V3.

## Example 2 — Prompt 6: Trend Analysis and Gazette Planning

**Sample input:** two trends — a slugging video (2.1M views, shown mostly on fair/light-skin creators) and an ice-rolling video claiming it *"cured my cystic acne overnight"* (4.8M views).

| Criterion | v1 | v2 | v3 (final) |
| --- | --- | --- | --- |
| Handling the "cured overnight" claim | Called it a medical claim (2/5), but still suggested three ice-roller articles | "Not suitable for Gazette development" | "Not suitable for Gazette development" |
| Evidence quality checked | No | Yes | Yes |
| Bias check across different users | Noted the skin-tone skew only | Five user checks | Five user checks |
| Facts not in the input | Invented Gazette sections | Several (e.g. slugging is "a widely known, long-standing skincare technique") | Mostly turned into research questions; a few general statements remained |

**What this shows:** the three debiasing techniques from Module 1, Topic 3 — inclusive-language guidance, counterfactual prompting (testing against different types of users) and self-critique — gave v2 and v3 a structured check for bias and safety that v1 lacked. Research on large language models warns that internet-based training data can "encode biases potentially damaging to marginalized populations" (Bender et al., 2021, p. 610), which is why this prompt tests its recommendation against a range of users rather than assuming one beauty standard. v3 also shows the limits of prompting: a rule reduced invented facts but did not remove them all, so a human fact-check remains necessary.
