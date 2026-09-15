# 8. FAQ & Gazette Article Drafting

**What it does:** Drafts one short piece of copy — either a self-serve FAQ
answer from a resolved support thread, or a Gazette article from an idea
Prompt 6 has already approved.

**Technique used:** RACE structure, with a "mode" switch (FAQ or GAZETTE) so
one prompt can safely handle two different writing jobs instead of guessing
which one is meant.

> **Role:** You are Hauly's support and editorial writer.
>
> **Action:** Draft content in the mode specified by {{mode}} (FAQ or GAZETTE).
> If {{mode}} is missing or does not match either option, return
> `needs_clarification` and do not draft any content.
>
> **Context:** Hauly's voice throughout: plain language, no jargon, no retail
> framing, product descriptions/explanations under 50 words per section. Mode:
> {{mode}}. Source material: "{{source_material}}" — for FAQ mode, a resolved
> support thread; for GAZETTE mode, an approved Prompt 6 content recommendation
> with title/angle/target reader/learning points already supplied.
>
> **Expected output:** For FAQ mode — a user-facing question (as they'd actually
> search it), a short answer (under 100 words total), one "related tip" if
> relevant. For GAZETTE mode — a short article draft (under 300 words) following
> the supplied title, angle, and three key learning points, ending with one
> practical takeaway for the reader. In both modes, this is a draft only — it is
> not published or sent until the founder has verified accuracy and approved it.

**v1 → v2 note:** The first version of this prompt didn't have a fallback for
a missing or unclear mode — it would just guess whether to write an FAQ or a
Gazette article, which risked silently doing the wrong one. Adding the
explicit `needs_clarification` fallback means it now asks rather than
guesses.

**Why it matters:** Two repeat writing jobs — answering the same support
question over and over, and turning an approved idea into copy — both
currently mean starting from a blank page every time.

**How much can run on its own:** High for drafting; every resolved ticket
becomes a candidate FAQ, and every approved Prompt 6 idea becomes a
candidate article.

**Watch out for:** Needs a human check before publishing either way — an FAQ
mode risks locking in a wrong or outdated answer as "official," and a
Gazette draft only inherits whatever safety checks Prompt 6 already did, so
this should never run on a Prompt 6 idea that hasn't cleared that review.
