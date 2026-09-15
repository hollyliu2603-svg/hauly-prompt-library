# Prompt 4 — Bug Report Summary

**Workflow stage:** Intake

| | |
| --- | --- |
| **Task** | Turn a messy user bug report into a clear, structured ticket for fixing. |
| **Problem it solves** | User bug reports are informal and incomplete. Holly has to reread them and work out the steps before any fixing can start. |
| **Prompting techniques** | Role framing; fixed ticket sections (structured output); a rule against guessing the cause, and labelling any step the user didn't state as "(inferred)" (constraints). |

## Final prompt (v2)

> **Role:** You are turning raw user bug reports into a structured ticket for a solo developer.
>
> **Action:** Pull out the details needed to fix the bug without re-reading the original message. Do not guess the technical cause unless the message gives evidence for it.
>
> **Context:** Hauly is an iPhone app. Message: "{{message}}"
>
> **Expected output:** Steps to reproduce (numbered; if a step is not stated by the user, mark it "(inferred)"); expected vs actual behaviour; device details if mentioned, otherwise "not provided"; affected tab/feature; severity (cosmetic / functional / blocking) with one sentence of reasoning.

Words in `{{double brackets}}` are filled in each time the prompt is used.

## How the prompt was improved

All versions were tested on the same sample message (written for testing, based on real Hauly features): *"since the last update whenever i use scan ingredients on a product it just shows a spinning wheel forever then goes back to my haul. i have like 200 products in there. iphone"*

**v1** — asked for a "likely technical cause" as one of the sections.

- **Result:** it wrote a detailed cause — "the recent update introduced a breaking change to the ingredient-scan API call or response parsing" — plus a second theory about the 200 products. None of this came from the user's message. It also listed steps the user never described, without saying they were guesses.

**v2 (final)** — removed the cause section, banned guessing the cause without evidence, and required unstated steps to be marked "(inferred)".

- **Result:** no cause was given. The first two steps were marked "(inferred)", phone model and iOS version were listed as "not provided", and the 200 products were noted with "relevance to bug not confirmed".

Full test outputs: [Appendix — Prompt 4](../appendix-test-outputs.md#prompt-4).

## Automation potential

**High.** This can run on every bug report, because a person still reads the ticket before any work starts.

## Risks and limitations

- Steps marked "(inferred)" can be wrong.
- Severity is a first guess and needs checking before deciding what to fix first.
- The AI can't see the app's code, so it can't diagnose problems — which is why it is told not to try.
