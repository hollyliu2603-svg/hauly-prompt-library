# Prompt 10 — Weekly Operations Report

**Workflow stage:** Reporting

| | |
| --- | --- |
| **Task** | Combine the week's support, bug, feature request, moderation and content data into one summary with a recommended action. |
| **Problem it solves** | Looking at each source separately makes it easy to miss a pattern that shows up across several of them. |
| **Prompting techniques** | Role framing; a "not provided this week" rule for missing data, and only calculating a percentage when both numbers are given (constraints); separating given numbers from observations and guesses (structured output). |

## Final prompt (v2)

> Role: You are writing a weekly operations summary for Hauly's founder.
> Action: Summarise the data below. If a section has no data, write "not provided this week" — do not guess or fill the gap.
> Context: Possible sections: support, bugs, feature requests, Circle moderation, content performance, social media trends. This week's data: "{{weekly_data}}"
> Expected output: For each section with data: volume vs last week (up / down / flat, or "no comparison available") — only calculate a percentage change if both this week's and last week's numbers are given; the top issue, with how often it was reported and how severe it is kept as separate facts. Clearly separate numbers that were given, observations, and guesses. Then any theme that appears in more than one section, and one recommended action for next week, with reasoning linked to the data given.

Words in `{{double brackets}}` are filled in each time the prompt is used.

## How the prompt was improved

Both versions were tested on the same sample data (written for testing). It included this week's and last week's support totals, only this week's numbers for bugs and feature requests, and no moderation, content or trend data.

**v1** — asked for "percentage change vs last week" for every section.
- **Result:** its one percentage (+40% for support) was correct, and it didn't invent others. But it presented guesses as facts — that the scan bug was "likely inflating the how_to support volume" and was "the single largest driver of this week's support spike".

**v2 (final)** — added the "not provided this week" rule, limited percentages to when both numbers are given, and asked it to separate given numbers from observations and guesses.
- **Result:** it marked bugs and feature requests "no comparison available", listed the three missing sections as "Not provided this week", and labelled the link between the bug and the support rise "an inference, not a confirmed causal link". It also spotted that the feature request counts didn't match the support total, "flagging it rather than guessing the cause".

Full test outputs: [Appendix — Prompt 10](../appendix-test-outputs.md#prompt-10).

## Automation potential

**High** as a decision-support tool. It saves Holly reviewing five sources separately; decisions stay with Holly.

## Risks and limitations

- A report can sound confident even when the week's data is incomplete.
- It depends on the other prompts' results being logged consistently.
- It is a starting point for decisions, not a final answer.
