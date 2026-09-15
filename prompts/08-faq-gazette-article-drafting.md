# Prompt 8 — FAQ and Gazette Drafting

**Workflow stage:** Content drafting

## Intended task

Draft either a help FAQ answer from a resolved support thread, or a Gazette article from an idea Prompt 6 has approved.

## Problem being solved

Answering the same question again and again, and writing articles from a blank page, both take up Holly's time.

## Prompting techniques

Role framing; a mode switch so one prompt handles two jobs; a "stop and ask" rule when the mode is missing (constraint); word limits (structured output).

## Automation potential

**High** for drafting. Every FAQ and article is checked and approved by Holly before publishing.

## Risks and limitations

- An FAQ can lock in an answer that goes out of date when the app changes.
- A Gazette draft only inherits the checks Prompt 6 already did, so it should never be used on an idea Prompt 6 hasn't approved.

## What the versions illustrate

| Version | What changed | What to notice in the response |
| --- | --- | --- |
| V1 | No rule for a missing mode | Silently chooses FAQ mode and writes a full draft without saying it guessed |
| V2 (final) | Adds: reply only `needs_clarification` if the mode is missing | Replies only `needs_clarification` |

**Discussion:** Both versions used the same thread with the mode deliberately left blank, testing what happens when an input is missing.

## Final prompt — reusable template (V2)

> **Role:** You are Hauly's support and editorial writer.  
>
> **Action:** Draft content in the mode given (FAQ or GAZETTE). If the mode is missing or is not one of these, reply only with `needs_clarification` and do not draft anything.  
>
> **Context:** Hauly's voice: plain language, no jargon, no shopping language. Mode: {{mode}}. Source material: "{{source_material}}" — FAQ mode uses a resolved support thread; GAZETTE mode uses an approved Prompt 6 recommendation with title, angle, target reader and learning points.  
>
> **Expected output:** FAQ mode — a question written the way a user would search it, a short answer (under 100 words), and one related tip only if it comes from the source material. GAZETTE mode — an article draft under 300 words following the supplied title, angle and three learning points, ending with one practical takeaway. Either way, this is a draft only and is not published until the founder has checked and approved it.  

Words in `{{double brackets}}` are filled in each time the prompt is used.

## Versions and recorded responses

Every version below was run once on the same sample input, written for testing and based on real Hauly features (not a real user message). Tests used Claude Sonnet 5 in September 2026. Responses are copied exactly as returned.

**Sample input** (mode left blank): *"Resolved support thread: A user asked how to move a finished product from their Haul to Restock. Answer given: in Haul, select the product, then tap 'Move to restock'."*

### V1

**Prompt text (as tested)**

~~~text
Role: You are Hauly's support and editorial writer.
Action: Draft content as either an FAQ or a GAZETTE article.
Context: Hauly's voice: plain language, no jargon, no shopping language. Mode: . Source material: "Resolved support thread: A user asked how to move a finished product from their Haul to Restock. Answer given: in Haul, select the product, then tap 'Move to restock'." — FAQ mode uses a resolved support thread; GAZETTE mode uses an approved Prompt 6 recommendation with title, angle, target reader and learning points.
Expected output: FAQ mode — a question written the way a user would search it, a short answer (under 100 words), and one related tip only if it comes from the source material. GAZETTE mode — an article draft under 300 words following the supplied title, angle and three learning points, ending with one practical takeaway. Either way, this is a draft only and is not published until the founder has checked and approved it.
~~~

**Recorded response**

~~~text
# FAQ Draft

**Question:** How do I move a finished product from my Haul to Restock?

**Answer:** Open your Haul, select the product you've finished, then tap "Move to restock." That's it — the item will now appear in your Restock list.

**Related tip:** Make sure you select the product first before looking for the "Move to restock" option — it only appears once an item is selected.

---

*Draft only — pending founder review and approval before publishing.*
~~~

### V2 (final)

**Prompt text (as tested)**

~~~text
Role: You are Hauly's support and editorial writer.
Action: Draft content in the mode given (FAQ or GAZETTE). If the mode is missing or is not one of these, reply only with `needs_clarification` and do not draft anything.
Context: Hauly's voice: plain language, no jargon, no shopping language. Mode: . Source material: "Resolved support thread: A user asked how to move a finished product from their Haul to Restock. Answer given: in Haul, select the product, then tap 'Move to restock'." — FAQ mode uses a resolved support thread; GAZETTE mode uses an approved Prompt 6 recommendation with title, angle, target reader and learning points.
Expected output: FAQ mode — a question written the way a user would search it, a short answer (under 100 words), and one related tip only if it comes from the source material. GAZETTE mode — an article draft under 300 words following the supplied title, angle and three learning points, ending with one practical takeaway. Either way, this is a draft only and is not published until the founder has checked and approved it.
~~~

**Recorded response**

~~~text
needs_clarification
~~~

## Prompt Lab check (GPT-4.1 mini)

To check the results weren't specific to one AI model, the first and final versions were re-run in La Trobe Prompt Lab using GPT-4.1 mini, with exactly the same prompt text. Prompt Lab's prompt review scores the prompt itself out of 100.

**What GPT-4.1 mini did — the final version failed on this model:**

| Version | Result | Compared with Claude Sonnet 5 |
| --- | --- | --- |
| V1 | Silently chose FAQ mode and wrote a draft; its tip mentioned "items still in transit", which is not in the source material | Same problem, plus an invented tip |
| V2 (final) | **Ignored the rule:** with the mode blank, it still wrote an FAQ draft instead of replying only `needs_clarification`; its tip ("Make sure you select the correct product…") was also not from the source | **Different** — Claude Sonnet 5 replied only `needs_clarification` |

- **Prompt Lab review:** V1 scored 82.25/100 and did not point out that the mode was missing. V2 scored 83.5/100 and suggested making the handling of a missing mode more explicit — which matches what went wrong.

**What this adds:** this is the clearest example in the library of a prompt that works on one model and fails on another. A possible next version would put the mode check first, as its own step, before any drafting instructions. That version was not tested, so it is not part of the final prompt. Until then, Holly's review before publishing is the safeguard.

### Prompt Lab — V1

**Recorded response (GPT-4.1 mini)**

~~~text
**FAQ**

**Q: How do I move a finished product from Haul to Restock in Hauly?**

A: In Haul, simply select the finished product you want to move. Then tap the button labeled “Move to restock.” This transfers the product from your Haul list to Restock, keeping your inventory organized.

**Tip:** Use this feature to keep a clear view of what’s ready to be restocked without mixing it with items still in transit.
~~~

**Prompt Lab review:** overall score 82.25/100

~~~text
Rubric Scores
* Clarity: 85/100 - The prompt is mostly clear but could benefit from more explicit instructions on how to handle the GAZETTE mode and clearer separation of modes.
* Constraints: 80/100 - The prompt sets good constraints on tone, length, and content but could specify formatting requirements more explicitly.
* Structure: 75/100 - The prompt is somewhat structured but mixes multiple instructions in a single paragraph, making it harder to parse quickly.
* Verifiability: 90/100 - The prompt references specific source material and expected outputs, which supports verifiability.
* Hallucination Risk: 85/100 - The prompt limits content to provided source material, reducing hallucination risk, but the GAZETTE mode instructions are vague and could lead to unsupported content.
Overall score: 82.25/100
Top Improvements
* Separate instructions for FAQ and GAZETTE modes more clearly to avoid confusion.
* Explicitly state formatting and length constraints for both modes.
* Clarify the source material and content boundaries for GAZETTE mode to reduce hallucination risk.
~~~

### Prompt Lab — V2 (final)

**Recorded response (GPT-4.1 mini)**

~~~text
**Q: How do I move a finished product from my Haul to Restock in Hauly?**

A: To move a finished product from your Haul to Restock, open your Haul, select the product you want to move, then tap the "Move to restock" button. This will transfer the item to your Restock list.

**Tip:** Make sure you select the correct product before tapping "Move to restock" to avoid any mix-ups.
~~~

**Prompt Lab review:** overall score 83.5/100

~~~text
Rubric Scores
* Clarity: 85/100 - The prompt clearly defines roles, modes, and expected outputs, but the mode input handling could be more explicit.
* Constraints: 80/100 - The prompt sets good constraints on language style, word limits, and output format, though the handling of missing or invalid modes could be more detailed.
* Structure: 75/100 - The prompt is somewhat dense and could benefit from clearer separation of instructions and examples for easier parsing.
* Verifiability: 90/100 - The prompt references specific source material and limits content to that, which supports verifiability.
* Hallucination Risk: 90/100 - The prompt restricts content to provided source material and specific modes, reducing hallucination risk.
Overall score: 83.5/100
Top Improvements
* Clarify the handling of the mode input, explicitly stating what valid modes are and how to respond if missing or invalid.
* Separate instructions, examples, and expected output formats more clearly for easier understanding.
* Add explicit instructions on how to handle the "related tip" in FAQ mode, especially if the source material does not contain one.
~~~
