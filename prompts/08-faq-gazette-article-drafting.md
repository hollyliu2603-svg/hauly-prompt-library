# Prompt 8 — FAQ and Gazette Drafting

**Workflow stage:** Content drafting

| | |
| --- | --- |
| **Task** | Draft either a help FAQ answer from a resolved support thread, or a Gazette article from an idea Prompt 6 has approved. |
| **Problem it solves** | Answering the same question again and again, and writing articles from a blank page, both take up Holly's time. |
| **Prompting techniques** | Role framing; a mode switch so one prompt handles two jobs; a "stop and ask" rule when the mode is missing (constraint); word limits (structured output). |

## Final prompt (v2)

> **Role:** You are Hauly's support and editorial writer.
>
> **Action:** Draft content in the mode given (FAQ or GAZETTE). If the mode is missing or is not one of these, reply only with `needs_clarification` and do not draft anything.
>
> **Context:** Hauly's voice: plain language, no jargon, no shopping language. Mode: {{mode}}. Source material: "{{source_material}}" — FAQ mode uses a resolved support thread; GAZETTE mode uses an approved Prompt 6 recommendation with title, angle, target reader and learning points.
>
> **Expected output:** FAQ mode — a question written the way a user would search it, a short answer (under 100 words), and one related tip only if it comes from the source material. GAZETTE mode — an article draft under 300 words following the supplied title, angle and three learning points, ending with one practical takeaway. Either way, this is a draft only and is not published until the founder has checked and approved it.

Words in `{{double brackets}}` are filled in each time the prompt is used.

## How the prompt was improved

Both versions were tested on the same sample support thread (written for testing, based on Hauly's real "Move to restock" button), with the mode deliberately left blank: *"Resolved support thread: A user asked how to move a finished product from their Haul to Restock. Answer given: in Haul, select the product, then tap 'Move to restock'."*

**v1** — no rule for a missing mode.

- **Result:** it silently chose FAQ mode and wrote a full draft, without saying it had guessed.

**v2 (final)** — told it to reply only with `needs_clarification` if the mode is missing.

- **Result:** it replied only with `needs_clarification` and wrote nothing else.

Full test outputs: [Appendix — Prompt 8](../appendix-test-outputs.md#prompt-8).

## Automation potential

**High** for drafting. Every FAQ and article is checked and approved by Holly before publishing.

## Risks and limitations

- An FAQ can lock in an answer that goes out of date when the app changes.
- A Gazette draft only inherits the checks Prompt 6 already did, so it should never be used on an idea Prompt 6 hasn't approved.
