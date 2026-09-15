# Prompt 7 — Circle Community Moderation

**Workflow stage:** Moderation

## Intended task

Check one post in Circle (Hauly's private social feed) against the community rules and recommend an action.

## Problem being solved

Checking every post by hand won't scale as Circle grows, but removing posts automatically could wrongly silence users.

## Prompting techniques

Role framing with a "recommendation only" limit; Hauly's real Circle rules as context; a consistency self-check (self-critique); structured JSON output with fixed actions, data types and a human-review flag.

## Automation potential

**Medium to high** for flagging. The structured output can feed a moderation queue, but removal is never automatic — every recommendation other than "allow" goes to Holly.

## Risks and limitations

- Telling a medical claim apart from an honest personal review is a hard call the AI can get wrong either way.
- Over-flagging could discourage genuine posts, so decisions should be reviewed regularly.
- Posts contain other users' content, so they should only be processed in tools approved for that data.

## What the versions illustrate

| Version | What changed | What to notice in the response |
| --- | --- | --- |
| V1 | Actions: allow / flag for review / remove | Chooses `"remove"`, which reads as an instruction to delete automatically |
| V2 | Renames to `recommend_remove`, human decides, adds self-check | `"recommend_remove"` for the same two rules; the reason notes it applies "regardless of the poster's tone or product type" |
| V3 | Adds exact data types, rules broken as a list, and a `human_review_required` flag | Same decision, with `rules_broken` as a list and `human_review_required: true` |
| V4 (final) | Updates the names rule to “no real names or personal details of other people”, because users choose whether to add a first name | Same decision on the test post (`recommend_remove`, same two rules); on an extra post where a user uses their chosen first name, it allows the post and cites the updated rule |

**Discussion:** All versions used the same post. The self-check did not change the decision on this post, so this test doesn't show that the self-check changes outcomes — a borderline post would be needed. V3 makes the output consistent enough to feed a review queue. V4 was a maintenance re-test: the old wording ("@usernames only") didn't match the app, where each user decides whether to add a first name, which may not be their real one. On the test post the decision didn't change. An extra post was also tried, where the poster uses their own chosen first name: both V3 and V4 allowed it, but V3 had to reinterpret the name as a "profile username", while V4 applied the rule as written. This was one run on one extra post, so it shows clearer reasoning, not a proven change in decisions.

## Final prompt — reusable template (V4)

> **Role:** You are a content moderation assistant for Circle, Hauly's private social feed.  
>
> **Action:** First, draft your decision against the rules below. Then re-check it by asking: "Would this decision be the same if the poster's tone, wording, product type, or cultural background were different?" Change it if not. This is a recommendation only — you never remove content; a human moderator makes the final decision.  
>
> **Context:** Rules: no real names or personal details of other people (Circle shows each user's @username, or a first name they chose to add), no medical claims about what a product treats or cures, no harassment, no prices except on Rehome posts. Post: "{{post}}"  
>
> **Expected output:** Return pretty-printed JSON only, no text outside it, with exactly these fields and types:  
> - "action": text, exactly one of "allow", "flag_for_review", "recommend_remove"  
> - "rules_broken": a list of the rules broken, written exactly as above, or an empty list [] if none  
> - "reason": text, one sentence  
> - "human_review_required": true or false (not text) — true for any action other than "allow"  

Words in `{{double brackets}}` are filled in each time the prompt is used.

## Versions and recorded responses

Every version below was run once on the same sample input, written for testing and based on real Hauly features (not a real user message). Tests used Claude Sonnet 5 in September 2026. Responses are copied exactly as returned.

**Sample input:** *"Honestly this Calm Barrier cream cleared up my eczema in a week, better than anything my doctor gave me. Jess Kim from my work put me onto it 💚"*

### V1

**Prompt text (as tested)**

~~~text
Role: You are a content moderation assistant for Circle, Hauly's private social feed.
Action: Check the post below against the community rules.
Context: Rules: no real names or personal details (Circle uses @usernames only), no medical claims about what a product treats or cures, no harassment, no prices except on Rehome posts. Post: "Honestly this Calm Barrier cream cleared up my eczema in a week, better than anything my doctor gave me. Jess Kim from my work put me onto it 💚"
Expected output: {"action": "allow | flag_for_review | remove", "rule_broken": "text or null", "reason": "one sentence"}
~~~

**Recorded response**

~~~text
{"action": "remove", "rule_broken": "no real names or personal details; no medical claims about what a product treats or cures", "reason": "The post names a real person (Jess Kim) and claims the product cleared/cured eczema better than a doctor's treatment, violating both the personal details and medical claims rules."}
~~~

### V2

**Prompt text (as tested)**

~~~text
Role: You are a content moderation assistant for Circle, Hauly's private social feed.
Action: First, draft your decision against the rules below. Then re-check it by asking: "Would this decision be the same if the poster's tone, wording, product type, or cultural background were different?" Change it if not. This is a recommendation only — you never remove content; a human moderator makes the final decision.
Context: Rules: no real names or personal details (Circle uses @usernames only), no medical claims about what a product treats or cures, no harassment, no prices except on Rehome posts. Post: "Honestly this Calm Barrier cream cleared up my eczema in a week, better than anything my doctor gave me. Jess Kim from my work put me onto it 💚"
Expected output: Return only: {"action": "allow | flag_for_review | recommend_remove", "rule_broken": "text or null", "reason": "one sentence"}
~~~

**Recorded response**

~~~text
{"action": "recommend_remove", "rule_broken": "no medical claims about what a product treats or cures; no real names or personal details", "reason": "The post claims the product cleared eczema (a medical claim) and names a real person (Jess Kim) along with their workplace context, violating two rules regardless of the poster's tone or product type."}
~~~

### V3

**Prompt text (as tested)**

~~~text
Role: You are a content moderation assistant for Circle, Hauly's private social feed.
Action: First, draft your decision against the rules below. Then re-check it by asking: "Would this decision be the same if the poster's tone, wording, product type, or cultural background were different?" Change it if not. This is a recommendation only — you never remove content; a human moderator makes the final decision.
Context: Rules: no real names or personal details (Circle uses @usernames only), no medical claims about what a product treats or cures, no harassment, no prices except on Rehome posts. Post: "Honestly this Calm Barrier cream cleared up my eczema in a week, better than anything my doctor gave me. Jess Kim from my work put me onto it 💚"
Expected output: Return pretty-printed JSON only, no text outside it, with exactly these fields and types:
- "action": text, exactly one of "allow", "flag_for_review", "recommend_remove"
- "rules_broken": a list of the rules broken, written exactly as above, or an empty list [] if none
- "reason": text, one sentence
- "human_review_required": true or false (not text) — true for any action other than "allow"
~~~

**Recorded response**

~~~text
```json
{
  "action": "recommend_remove",
  "rules_broken": [
    "no real names or personal details (Circle uses @usernames only)",
    "no medical claims about what a product treats or cures"
  ],
  "reason": "The post names a real person (Jess Kim) and makes a medical claim that the product cleared up eczema better than a doctor's treatment.",
  "human_review_required": true
}
```
~~~

### V4 (final)

Run once on 16 September 2026 with Claude Sonnet 5 through the Claude Code command line, with no tools and a one-character system prompt. The tool still adds a short identity line, the date and the account email; none of these relate to the task. As a check, V3 was re-run in the same setup on the same post and gave the same decision (`recommend_remove`, same two rules).

**Prompt text (as tested)**

~~~text
Role: You are a content moderation assistant for Circle, Hauly's private social feed.
Action: First, draft your decision against the rules below. Then re-check it by asking: "Would this decision be the same if the poster's tone, wording, product type, or cultural background were different?" Change it if not. This is a recommendation only — you never remove content; a human moderator makes the final decision.
Context: Rules: no real names or personal details of other people (Circle shows each user's @username, or a first name they chose to add), no medical claims about what a product treats or cures, no harassment, no prices except on Rehome posts. Post: "Honestly this Calm Barrier cream cleared up my eczema in a week, better than anything my doctor gave me. Jess Kim from my work put me onto it 💚"
Expected output: Return pretty-printed JSON only, no text outside it, with exactly these fields and types:
- "action": text, exactly one of "allow", "flag_for_review", "recommend_remove"
- "rules_broken": a list of the rules broken, written exactly as above, or an empty list [] if none
- "reason": text, one sentence
- "human_review_required": true or false (not text) — true for any action other than "allow"
~~~

**Recorded response**

~~~text
```json
{
  "action": "recommend_remove",
  "rules_broken": [
    "no real names or personal details of other people (Circle shows each user's @username, or a first name they chose to add)",
    "no medical claims about what a product treats or cures"
  ],
  "reason": "The post names a coworker with identifying context and claims the product cleared eczema, violating both the personal-details and medical-claims rules.",
  "human_review_required": true
}
```
~~~

### Extra check — a user's own chosen first name

Both V3 and V4 were run once, in the same setup, on a second sample post (written for testing): *"Mia here (that's the name I picked for my profile!) — finally finished my first lip oil, restocking it next week 💚"*

**V3 recorded response**

~~~text
```json
{
  "action": "allow",
  "rules_broken": [],
  "reason": "The poster explicitly clarifies 'Mia' is a chosen profile username rather than a real name, and the post contains no medical claims, harassment, or pricing.",
  "human_review_required": false
}
```
~~~

**V4 recorded response**

~~~text
```json
{
  "action": "allow",
  "rules_broken": [],
  "reason": "The post only uses a self-chosen first name as permitted, makes no medical claims, includes no price, and contains no harassment or personal details about others.",
  "human_review_required": false
}
```
~~~

## Prompt Lab check (GPT-4.1 mini)

To check the results weren't specific to one AI model, the first and final versions were re-run in La Trobe Prompt Lab using GPT-4.1 mini, with exactly the same prompt text. Prompt Lab's prompt review scores the prompt itself out of 100.

**What GPT-4.1 mini did:**

| Version | Result | Compared with Claude Sonnet 5 |
| --- | --- | --- |
| V1 | `"remove"`; named only the medical-claim rule and **missed the real name** ("Jess Kim from my work") | Worse — Claude Sonnet 5 caught both rules. V1 only allows one `rule_broken` as text, which may have pushed it to pick one |
| V4 (final) | `"flag_for_review"`; caught **both** rules as a list; `human_review_required` was `true` (not text); no text outside the JSON | Both rules caught, as with Claude; but it chose `flag_for_review` where Claude chose `recommend_remove`, and it shortened the first rule's wording instead of writing it "exactly as above" |

- **Prompt Lab review:** V1 scored 88.25/100 and did not point out that `"remove"` implies automatic deletion. V4 scored 87.25/100; one suggestion was to "explicitly limit output to JSON only", although the prompt already says "Return pretty-printed JSON only, no text outside it", so this suggestion was not applied.

**What this adds:** both final-version outputs send the post to Holly (`human_review_required: true`), so the safeguard held on both models, but the action label differed. That difference is acceptable because a person makes the final decision either way.

### Prompt Lab — V1

**Recorded response (GPT-4.1 mini)**

~~~text
{"action": "remove", "rule_broken": "no medical claims about what a product treats or cures", "reason": "The post makes a medical claim that the product cleared up eczema, which is prohibited."}
~~~

**Prompt Lab review:** overall score 88.25/100

~~~text
Rubric Scores
* Clarity: 90/100 - The prompt clearly defines the role, action, context, rules, and expected output format, though the phrasing could be slightly more concise.
* Constraints: 85/100 - The prompt specifies clear rules and output format but could better emphasize strict adherence to the JSON structure and possible values.
* Structure: 90/100 - The prompt is well-organized with distinct sections for role, action, context, rules, post, and expected output.
* Verifiability: 80/100 - The rules are explicit, but the prompt could include examples or clarify how to handle borderline cases to improve verifiability.
* Hallucination Risk: 95/100 - The prompt minimizes hallucination risk by providing explicit rules and a concrete post to evaluate.
Overall score: 88.25/100
Top Improvements
* Emphasize strict adherence to the JSON output format and allowed values for "action."
* Include examples or clarifications for ambiguous cases to improve verifiability.
* Simplify and tighten the language for better clarity and conciseness.
~~~

### Prompt Lab — V4 (final)

**Recorded response (GPT-4.1 mini)**

~~~text
{
  "action": "flag_for_review",
  "rules_broken": [
    "no real names or personal details of other people",
    "no medical claims about what a product treats or cures"
  ],
  "reason": "The post includes a real name and makes a medical claim about the product treating eczema.",
  "human_review_required": true
}
~~~

**Prompt Lab review:** overall score 87.25/100

~~~text
Rubric Scores
* Clarity: 85/100 - The prompt is mostly clear but could better specify the format and expectations for the re-check step.
* Constraints: 90/100 - The prompt clearly defines rules and expected output format, though it could explicitly limit output to JSON only.
* Structure: 80/100 - The prompt has a logical flow but mixing the initial decision and re-check instructions in one paragraph reduces readability.
* Verifiability: 90/100 - The rules and expected output fields are well-defined, enabling straightforward verification.
* Hallucination Risk: 95/100 - The prompt restricts the assistant to a defined set of rules and output format, minimizing hallucination risk.
Overall score: 87.25/100
Top Improvements
* Separate the initial decision and re-check instructions into distinct steps for better clarity.
* Explicitly state that the output must be JSON only, with no additional text or explanation.
* Clarify how to handle the re-check step and what to do if the decision changes after re-checking.
~~~
