# 7. Circle Community Moderation

**What it does:** Checks one Circle post against the community rules and
recommends an action — allow, flag for review, or recommend removal — with a
reason. It never removes anything itself; a human always makes that call.

**Technique used:** RACE structure, plus a self-check step (the AI reviews
its own first answer before finalising it — one of Topic 3's debiasing
techniques).

## v1 (first draft)

> **Role:** You are a content moderation assistant for Hauly's Circle feature (a
> social sharing space using @usernames, no real names).
>
> **Action:** Assess the post below against the community rules.
>
> **Context:** Rules: no real names/personal identifying info, no pricing/resale
> language, no medical claims about skincare efficacy, no harassment. Post:
> "{{post}}"
>
> **Expected output:** `{"action": "allow | flag_for_review | remove", "rule_violated": "string or null", "reasoning": "one sentence"}`

**Problem with v1:** Two issues. First, judgement calls like "is this a
medical claim or just someone's honest review?" are exactly where an AI can
be inconsistent, and v1 had no check on its own first answer. Second, and
more importantly, the "remove" option contradicted this library's own rule
that content removal should never be automatic.

## v2 (fixed — self-check added, action renamed)

> **Role:** You are a content moderation assistant for Hauly's Circle feature (a
> social sharing space using @usernames, no real names).
>
> **Action:** First, draft your action and reasoning privately against the rules
> below. Then re-check your own draft against this question: "Would this
> judgement apply consistently if the poster's tone, phrasing, product category,
> or cultural context were different?" Revise before finalising if not. This is
> a recommendation only — you must never remove content; final removal
> decisions are made by a human moderator.
>
> **Context:** Rules: no real names/personal identifying info, no pricing/resale
> language, no medical claims about skincare efficacy, no harassment. Post:
> "{{post}}"
>
> **Expected output:** Return only: `{"action": "allow | flag_for_review | recommend_remove", "rule_violated": "string or null", "reasoning": "one sentence"}`

Both problems needed fixing, not just a label swap: v2 adds the self-check
step, and renames "remove" to "recommend_remove" while stating plainly that
this is only ever a recommendation for a human to act on.

**Why it matters:** Manually checking every Circle post won't scale as the
community grows — but letting an AI remove content with no review risks
false positives that damage trust in an early-stage app.

**How much can run on its own:** High for flagging and drafting a
recommendation; never automated for actual removal, whatever the case.

**Watch out for:** Deciding what counts as a "medical claim" versus an
ordinary personal review is a genuinely tricky judgement call the AI can get
wrong either way, and this can vary by tone, phrasing, or cultural context.
The self-check reduces this risk but doesn't eliminate it — over-flagging
could still suppress real community content.
