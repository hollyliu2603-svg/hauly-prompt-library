# 1. Support Ticket Triage & Categorisation

**What it does:** Reads one incoming support message and sorts it — category,
urgency, which part of the app it affects — into a format that can drop
straight into a tracker, instead of Holly reading and filing it by hand.

**Technique used:** RACE structure, with a strict "answer must be valid JSON"
rule so the output can be automatically filed.

> **Role:** You are a support operations analyst for Hauly, a consumer app for
> cataloguing beauty and skincare collections (not a shopping or retail platform).
>
> **Action:** Classify the user message below.
>
> **Context:** Category options: bug, feature_request, account, how_to, praise,
> complaint, other. Urgency options: low, medium, high. Tab options: My Haul, Match,
> Restock, Circle, Learn, Account, Unknown. User message: "{{message}}"
>
> **Expected output:** Return ONLY valid JSON with this schema, no text outside the
> JSON object: `{"category": "...", "urgency": "...", "affected_tab": "...", "one_line_summary": "string, max 15 words"}`

**v1 → v2 note:** The earliest version of this prompt didn't fix the category,
urgency, or tab options — it just said "sort this message." That let the AI
invent its own labels each time (e.g. "bug" one run, "issue" the next), which
would break any tracker trying to read them. Locking in a fixed list of
options and a strict JSON format fixed that.

**Why it matters:** As the only person doing support, Holly can't manually
read and route every message during busy periods (e.g. right after an update).

**How much can run on its own:** High for the first sort — but anything
ambiguous, safety-related, about payments, or mixing several issues still
needs a human look, whatever category the AI assigns.

**Watch out for:** Misclassifying unclear or multi-issue messages; "urgency"
is a best guess, not a guarantee — a safety- or payment-related message
should always get eyes on it regardless of the label.
