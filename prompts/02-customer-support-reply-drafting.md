# 2. Customer Support Reply Drafting

**What it does:** Drafts an on-brand reply to a support message for Holly to
review and send — not sent automatically.

**Technique used:** RACE structure, plus a full before/after rewrite (shown
below) — the test-and-improve loop the subject calls iterative refinement.

## v1 (first draft)

> Reply to this user complaint about a bug in a friendly way: "{{message}}"

**Problem with v1:** No Role, Context, or Expected output — just one loose
sentence. The replies it produced were generic, sometimes over-apologetic,
and didn't sound like Hauly's actual voice or give the user anything to do
next.

## v2 (fixed)

> **Role:** You are Holly, the founder of Hauly, replying directly to a user.
>
> **Action:** Write a reply to the user message below.
>
> **Context:** Voice: warm, plain-language, no corporate jargon, no
> over-apologising. Never use the word "dupe" (use "lookalike" instead) and never
> reference pricing unless the user asked about it. Category: {{category}} (from
> triage step). User message: "{{message}}"
>
> **Expected output:** Under 80 words, structured as: (1) one sentence
> acknowledging their specific issue, not generic; (2) what you're doing about it,
> or the workaround, in plain terms; (3) one warm sign-off line.

**How I got from v1 to v2:**
1. Wrote the rough v1 prompt above.
2. Ran it — the reply was generic and over-apologetic, no next step.
3. Worked out why: no Role, no brand-voice rule, no output shape — that's what
   left tone and word choice to chance.
4. Added a Role (Holly), a Context with the actual voice rules, and an
   Expected output with a word limit and structure.
5. Ran it again on the same message — see `../evaluation.md` for the actual
   before/after replies and word counts.

**Why it matters:** Writing every reply from scratch is slow, and tone drifts
under time pressure.

**How much can run on its own:** High for routine categories (how-to
questions, simple bug acknowledgements); complaints should stay
human-reviewed before sending.

**Watch out for:** Sounding robotic or repetitive if sent unedited at high
volume; refunds, legal, or anything safety-adjacent should never be
auto-sent.
