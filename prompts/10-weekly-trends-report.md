# 10. Weekly Support, Community & Content Trends Report for the Founder

**What it does:** Pulls together whatever weekly data is actually available
(support, bugs, feature requests, moderation, content) into one summary for
Holly, with a recommended action — instead of her reviewing each source
separately.

**Technique used:** RACE structure, plus a direct rule to say "not provided"
rather than guess when data is missing — a straightforward way to stop the
AI from confidently filling gaps that aren't really there.

> **Role:** You are producing a weekly operations summary for Hauly's founder.
>
> **Action:** Synthesise the data sections provided below. If a section is empty
> or not supplied, state "not provided this week" rather than guessing or filling
> the gap.
>
> **Context:** Available input sections: support categories (Prompt 1), bug
> tickets (Prompt 4), feature requests (Prompt 5), Circle moderation actions
> (Prompt 7), content performance notes, and social media trend insights
> (Prompt 6). This week's data: "{{weekly_data}}"
>
> **Expected output:** For each section that is provided: volume vs last week
> (up/down/flat, or "no baseline" if not given) — do not calculate a percentage
> change unless both a current and a previous numerical total are explicitly
> supplied; and top issue(s), reporting frequency and severity as separate
> figures rather than combining them into one score unless a weighting method is
> explicitly provided. Clearly distinguish, throughout: numerical data actually
> supplied, qualitative observations, and information that is missing. Then,
> across all sections that were provided (not the ones marked "not provided"):
> any recurring theme that cuts across more than one section, and one
> recommended action for the coming week with reasoning tied to the specific
> sections supplied.

**v1 → v2 note:** An earlier version let the AI calculate a "percentage
change vs last week" even when it only had this week's number and no
previous one to compare against — which meant an invented, made-up
percentage could show up in the report looking factual. The fix was a
direct rule: don't calculate a percentage unless both numbers are actually
given.

**Why it matters:** Without a dedicated ops role, patterns across a week of
scattered interactions are easy to miss when each source is only ever
looked at on its own.

**How much can run on its own:** High as a decision-support tool — this is
the highest-value prompt in the library because it turns five other
prompts' outputs into one strategic input, rather than five separate manual
reviews.

**Watch out for:** Quality depends entirely on how complete the input data
is — a summary can sound authoritative while quietly hiding gaps in what
was actually captured that week. Treat it as a discussion starter, not a
final decision.
