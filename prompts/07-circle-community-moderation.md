# Prompt 7 — Circle Community Moderation

**Workflow stage:** Moderation

| | |
| --- | --- |
| **Task** | Check one post in Circle (Hauly's private social feed) against the community rules and recommend an action. |
| **Problem it solves** | Checking every post by hand won't scale as Circle grows, but removing posts automatically could wrongly silence users. |
| **Prompting techniques** | Role framing; Hauly's real Circle rules (context); a self-check for consistency (self-critique); fixed actions and output format (structured output); a "recommendation only" rule. |

## Final prompt (v2)

> **Role:** You are a content moderation assistant for Circle, Hauly's private social feed.
>
> **Action:** First, draft your decision against the rules below. Then re-check it by asking: "Would this decision be the same if the poster's tone, wording, product type, or cultural background were different?" Change it if not. This is a recommendation only — you never remove content; a human moderator makes the final decision.
>
> **Context:** Rules: no real names or personal details (Circle uses @usernames only), no medical claims about what a product treats or cures, no harassment, no prices except on Rehome posts. Post: "{{post}}"
>
> **Expected output:** Return only: {"action": "allow | flag_for_review | recommend_remove", "rule_broken": "text or null", "reason": "one sentence"}

Words in `{{double brackets}}` are filled in each time the prompt is used.

## How the prompt was improved

All versions were tested on the same sample message (written for testing, based on real Hauly features): *"Honestly this Calm Barrier cream cleared up my eczema in a week, better than anything my doctor gave me. Jess Kim from my work put me onto it 💚"*

**v1** — allowed actions were "allow", "flag for review" or "remove".

- **Result:** it chose `"remove"` for two broken rules (a real name and a medical claim). That label reads as an instruction to delete the post automatically.

**v2 (final)** — renamed "remove" to "recommend_remove", said a human always makes the final decision, and added a self-check: would the decision be the same if the poster's tone, wording or background were different?

- **Result:** `"recommend_remove"` for the same two rules, with a reason noting it applied "regardless of the poster's tone or product type".
- **What the test did not show:** both versions reached the same decision on this post, so this test doesn't prove the self-check changes decisions. A borderline post would be needed to show that.

Full test outputs: [Appendix — Prompt 7](../appendix-test-outputs.md#prompt-7).

## Automation potential

**Medium to high** for flagging. Removal is never automatic — every "recommend_remove" goes to Holly.

## Risks and limitations

- Telling a medical claim apart from an honest personal review is a hard call the AI can get wrong either way.
- Over-flagging could discourage genuine posts, so flagged decisions should be reviewed regularly.
- Posts contain other users' content, so they should only be processed in tools approved for that data.
