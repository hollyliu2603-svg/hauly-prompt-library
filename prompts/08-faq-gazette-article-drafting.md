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
