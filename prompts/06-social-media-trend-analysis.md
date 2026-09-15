# 6. Social Media Trend Analysis & Monthly Gazette Planning

**What it does:** Turns trend information Holly (or a tool) has already
gathered into a content idea for Hauly's Gazette — with a built-in check for
bias and unsafe claims before it's ever recommended.

**Technique used:** RACE structure, plus three specific "debiasing" checks
used together (see the glossary): telling the AI to use inclusive language,
testing its idea against different kinds of users, and asking it to
double-check its own answer for bias before finishing.

**Important limit:** this prompt does **not** claim the AI can scroll social
media itself. It only works with information that's fed in — platform,
caption, description, date, engagement numbers. An AI has no live access to
social platforms unless someone supplies that data.

**This is the biggest before/after example in the library** — the largest
gap between v1 and v2 of any prompt here.

## v1 (first draft)

> **Role:** You are a content strategist for Hauly, a beauty/skincare
> organisational app with a deliberately vintage/botanical aesthetic.
>
> **Action:** Rate each supplied trend for relevance, then propose content ideas.
>
> **Context:** Fit criteria: organisation-not-shopping positioning, no
> pricing/retail framing, no medical/efficacy claims. Supplied trends:
> "{{trend_list}}"
>
> **Expected output:** A 1–5 relevance score per trend, then up to 3 content
> ideas with title, angle, and intended tab.

**Problem with v1:** Nothing stopped it treating one beauty standard, skin
tone, age group, or a single viral post as representative of every Hauly
user. It also had no way to tell "this is actually true" apart from "this is
just popular" — so a viral but exaggerated claim could get repeated as fact.
See `../evaluation.md` for the real example of exactly this happening.

## v2 (fixed — full debiasing pass)

> **Role:** You are Hauly's beauty editorial strategist. Hauly is an independent
> beauty-collection and skincare-organising app with a warm, editorial and
> educational brand voice; its Gazette provides practical beauty and skincare
> education rather than product-selling content.
>
> **Action:** Analyse the supplied social media trend information to identify the
> main trends shown, evaluate which are relevant to Hauly's audience and existing
> Gazette content, then produce a content recommendation — including a dedicated
> check of your own recommendation for bias and exclusion before finalising.
>
> **Context:** Supplied evidence may include platform, post caption, trend
> description, date, engagement information, and source link — use only this
> supplied information as evidence of current trends; do not invent engagement
> figures, sources, audience reactions, or popularity. Consider: whether the
> trend relates to skincare, beauty organisation, product usage, or beauty
> habits; whether it supports Hauly's educational purpose; whether it overlaps
> with existing Gazette content; whether it could become an evergreen article
> rather than a short-lived trend piece; whether it creates medical, safety,
> misinformation, or exaggerated-claim risk; whether it can be discussed without
> becoming promotional. Use inclusive language and do not assume one skin tone,
> gender, age, skin type, budget, or beauty routine represents all Hauly users;
> do not describe a trend as universally suitable. Supplied trend information:
> "{{trend_list}}"
>
> **Expected output:** Seven sections: **(1) Trend overview** —
> name, platform and date, what the supplied evidence shows, whether it appears
> established, emerging, or unclear (use "unclear" whenever the supplied
> evidence does not clearly support an established or emerging classification —
> do not default to "emerging" just because the evidence is thin); **(2)
> Evidence limitations** — what's missing, whether
> engagement/popularity can be verified, any claims that shouldn't be treated as
> proven; **(3) Hauly relevance assessment** — why it may be relevant, which
> Hauly feature or Gazette purpose it connects to, a 1–5 relevance score;
> **(4) Content recommendation** — working title, editorial angle, target
> reader, three key learning points, suggested format, and whether it should be
> evergreen, seasonal, or trend-led; **(5) Bias and inclusion review** — check
> whether the recommendation assumes one gender/age/skin tone/income/beauty
> standard, overrepresents influencer or luxury-product perspectives, excludes
> beginners or budget-conscious users, treats popularity as proof of
> effectiveness, or uses gendered/judgemental language; briefly test the
> recommendation against a beginner, a budget-conscious user, a user with
> sensitive skin, a user from a different cultural background, and a user who
> prefers a minimal routine, naming any assumptions or limitations found — note
> that this counterfactual check is a limited bias screen, not proof that the
> recommendation is universally inclusive; **(6) Editorial and safety risks** —
> claims needing further research, expert review, or cautious wording;
> **(7) Recommendation status** — one of "suitable for founder review", "needs
> more evidence", or "not suitable for Gazette development." State clearly if
> the supplied evidence is insufficient for any section. **This output requires
> founder review and approval before publication regardless of the status
> field.**

The added evidence-checking and bias-review sections are what actually catch
problems — see `../evaluation.md` for a worked example where v2 flags an
unverified "cures acne overnight" claim and a skewed sample that v1 let
straight through.

**Note on Prompt 6 vs Prompt 8:** these are different steps. Prompt 6 decides
*whether an idea is worth writing about and safe to publish*; Prompt 8 then
does the actual writing once Prompt 6 has already cleared it.

**Why it matters:** With no dedicated marketing person, content planning
competes with support and moderation for Holly's time — and doing it well
means not just picking a topic, but avoiding beauty content that quietly
only speaks to one age group, skin tone, or income level.

**How much can run on its own:** Medium — good at structuring and reviewing
evidence Holly has already gathered, not a live trend-monitoring tool.
Founder approval before publishing is mandatory, not optional.

**Watch out for:** The self-check reduces bias risk but doesn't remove it
entirely — it's an extra safety net, not a guarantee. Its judgement is only
as good as the evidence supplied, which is exactly why it's built to say
"not enough evidence" rather than guess.
