# Prompt 10 — Weekly Operations Report

**Workflow stage:** Reporting (uses the other prompts' outputs)

## Intended task

Combine the week's support, bug, feature request, moderation and content data into one summary with a recommended action.

## Problem being solved

Looking at each source separately makes it easy to miss a pattern that shows up across several of them.

## Prompting techniques

Role framing; a "not provided this week" rule for missing data; only calculating a percentage when both numbers are given (constraints); separating given numbers from observations and guesses (structured output).

## Automation potential

**High** as a decision-support tool. It brings together outputs from Prompts 1, 4, 5, 6 and 7; decisions stay with Holly.

## Risks and limitations

- A report can sound confident even when the week's data is incomplete.
- It depends on the other prompts' results being logged consistently.
- It is a starting point for decisions, not a final answer.

## What the versions illustrate

| Version | What changed | What to notice in the response |
| --- | --- | --- |
| V1 | Asks for percentage change vs last week for every section | Its one percentage (+40%) is correct, but it presents guesses as facts — the bug was "likely inflating the "how_to" support volume" and "the single largest driver of this week's support spike" |
| V2 (final) | Adds "not provided" rule, percentage rule, and separating facts from guesses | Marks "No comparison available" and "Not provided this week", labels the bug link as an inference, and flags a mismatch in the data "rather than guessing the cause" |

**Discussion:** Both versions used the same data. The main risk was not invented numbers but confident interpretation; asking the model to label guesses made that visible.

## Final prompt — reusable template (V2)

> **Role:** You are writing a weekly operations summary for Hauly's founder.  
>
> **Action:** Summarise the data below. If a section has no data, write "not provided this week" — do not guess or fill the gap.  
>
> **Context:** Possible sections: support, bugs, feature requests, Circle moderation, content performance, social media trends. This week's data: "{{weekly_data}}"  
>
> **Expected output:** For each section with data: volume vs last week (up / down / flat, or "no comparison available") — only calculate a percentage change if both this week's and last week's numbers are given; the top issue, with how often it was reported and how severe it is kept as separate facts. Clearly separate numbers that were given, observations, and guesses. Then any theme that appears in more than one section, and one recommended action for next week, with reasoning linked to the data given.  

Words in `{{double brackets}}` are filled in each time the prompt is used.

## Versions and recorded responses

Every version below was run once on the same sample input, written for testing and based on real Hauly features (not a real user message). Tests used Claude Sonnet 5 in September 2026. Responses are copied exactly as returned.

**Sample input:** *"Support: 42 messages this week (bug 18, how_to 12, feature_request 8, account 4). Last week: 30 messages. Bugs: 18 this week; top bug is 'Scan ingredients' spinning then returning to Haul, reported 11 times, severity blocking. Feature requests: price tracking asked for 14 times; more Circle friends on the free plan asked for 6 times."*

### V1

**Prompt text (as tested)**

~~~text
Role: You are writing a weekly operations summary for Hauly's founder.
Action: Summarise the data below.
Context: Possible sections: support, bugs, feature requests, Circle moderation, content performance, social media trends. This week's data: "Support: 42 messages this week (bug 18, how_to 12, feature_request 8, account 4). Last week: 30 messages. Bugs: 18 this week; top bug is 'Scan ingredients' spinning then returning to Haul, reported 11 times, severity blocking. Feature requests: price tracking asked for 14 times; more Circle friends on the free plan asked for 6 times."
Expected output: For each section: volume and percentage change vs last week, and the top issue. Then any theme that appears across sections, and one recommended action for next week with reasoning.
~~~

**Recorded response**

~~~text
# Weekly Ops Summary — Week of Sept 15, 2026

## Support
- **Volume:** 42 messages (vs. 30 last week) → **+40%**
- **Breakdown:** Bugs 18, How-to 12, Feature requests 8, Account 4
- **Top issue:** Bug reports are the largest category (43% of all support volume this week)

## Bugs
- **Volume:** 18 reports this week
- **% change vs. last week:** Not calculable — last week's total (30) wasn't broken down by category, so we don't have a bug-only baseline. *(Flag: worth tracking category-level volumes going forward.)*
- **Top issue:** "Scan ingredients" spinning and returning to the Haul screen — reported **11 times**, severity **blocking**. This single bug accounts for ~61% of all bug reports this week.

## Feature Requests
- **Volume (support inbox):** 8 requests logged in support
- **Top asks:** Price tracking (14 mentions), more Circle friends on the free plan (6 mentions)
- **Note:** These two counts (14 + 6 = 20) exceed the support category total (8), suggesting they're aggregated across multiple channels (e.g., Circle, social, support) rather than support tickets alone. Worth confirming the source so requests are compared consistently week over week.

## Circle Moderation, Content Performance, Social Media Trends
- No data provided this week — recommend including these in next week's report for full coverage.

---

## Cross-Section Theme
The **"Scan ingredients" bug** is the clear throughline: it's the top bug (11 reports, blocking severity), it's likely inflating the "how_to" support volume (users trying to figure out if it's them or the app), and it's plausibly connected to the overall 40% jump in support contacts this week.

## Recommended Action for Next Week
**Prioritize an emergency fix for the "Scan ingredients" spinning bug.**

**Reasoning:** It's the single largest driver of this week's support spike, it's rated blocking (core functionality broken), and it likely has downstream effects on how-to questions and user trust. Fixing it should reduce both bug and how_to volume next week, giving a cleaner read on organic demand for feature requests like price tracking and expanded free-plan Circle limits.

*Secondary note: Standardize how feature request mentions are counted (single source vs. aggregated) so week-over-week comparisons are accurate.*
~~~

### V2 (final)

**Prompt text (as tested)**

~~~text
Role: You are writing a weekly operations summary for Hauly's founder.
Action: Summarise the data below. If a section has no data, write "not provided this week" — do not guess or fill the gap.
Context: Possible sections: support, bugs, feature requests, Circle moderation, content performance, social media trends. This week's data: "Support: 42 messages this week (bug 18, how_to 12, feature_request 8, account 4). Last week: 30 messages. Bugs: 18 this week; top bug is 'Scan ingredients' spinning then returning to Haul, reported 11 times, severity blocking. Feature requests: price tracking asked for 14 times; more Circle friends on the free plan asked for 6 times."
Expected output: For each section with data: volume vs last week (up / down / flat, or "no comparison available") — only calculate a percentage change if both this week's and last week's numbers are given; the top issue, with how often it was reported and how severe it is kept as separate facts. Clearly separate numbers that were given, observations, and guesses. Then any theme that appears in more than one section, and one recommended action for next week, with reasoning linked to the data given.
~~~

**Recorded response**

~~~text
# Hauly – Weekly Operations Summary
**Week of Sept 8–14, 2026** (prepared Sept 15, 2026)

---

## Support
- **Volume:** 42 messages this week vs. 30 last week → **up 40%** (calculated from the two given totals: +12 messages).
- **Breakdown given:** bug 18, how_to 12, feature_request 8, account 4.
- *Observation:* Bug-related messages are the largest category this week (18 of 42, ~43% of all support volume).

## Bugs
- **Volume:** 18 bug reports this week. **No comparison available** — no last week bug-specific total was given (only the overall support total had a prior-week figure).
- **Top issue:** "Scan ingredients" feature spins and returns to Haul.
  - Reported: 11 times
  - Severity: blocking
- *Observation:* This single bug accounts for 11 of the 18 bug reports this week (~61%), making it the dominant driver of bug volume.

## Feature Requests
- **Top requests given:**
  - Price tracking — 14 requests
  - More Circle friends on free plan — 6 requests
- **Volume comparison:** No comparison available — no last week figures were given for feature requests.
- *Observation:* These two requests total 20 mentions, which is higher than the "8" feature_request count logged in the Support breakdown. This is a discrepancy in the raw data (possibly different counting methods or sources) — flagging it rather than guessing the cause.

## Circle Moderation
Not provided this week.

## Content Performance
Not provided this week.

## Social Media Trends
Not provided this week.

---

## Cross-Section Theme
- **"Scan ingredients" / scanning reliability** and **overall support load** are linked: the bug category (18) is the single largest slice of total support volume (42), and one bug ("Scan ingredients") makes up the majority of bug volume. This suggests the support volume spike (+40%) is substantially tied to this one blocking bug — this is an **inference**, not a confirmed causal link, since no root-cause data was given.

---

## Recommended Action for Next Week
**Prioritize a fix for the "Scan ingredients" spinning bug.**

**Reasoning (data-linked):**
- It's the single most-reported bug (11 reports) and carries **blocking** severity — the highest urgency level given.
- Bugs are the top category driving this week's 40% jump in total support volume, and this one issue represents roughly 61% of all bug reports.
- Resolving it is likely to reduce both bug-report volume and overall support load next week — though this expected impact is an assumption, not a guaranteed outcome, since no data confirms causation.
~~~
