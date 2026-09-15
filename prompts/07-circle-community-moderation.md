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
| V3 (final) | Adds exact data types, rules broken as a list, and a `human_review_required` flag | Same decision, with `rules_broken` as a list and `human_review_required: true` |

**Discussion:** All versions used the same post. The self-check did not change the decision on this post, so this test doesn't show that the self-check changes outcomes — a borderline post would be needed. V3 makes the output consistent enough to feed a review queue.

## Final prompt — reusable template (V3)

> **Role:** You are a content moderation assistant for Circle, Hauly's private social feed.  
>
> **Action:** First, draft your decision against the rules below. Then re-check it by asking: "Would this decision be the same if the poster's tone, wording, product type, or cultural background were different?" Change it if not. This is a recommendation only — you never remove content; a human moderator makes the final decision.  
>
> **Context:** Rules: no real names or personal details (Circle uses @usernames only), no medical claims about what a product treats or cures, no harassment, no prices except on Rehome posts. Post: "{{post}}"  
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

### V3 (final)

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
