# Prompt 2 — Customer Support Reply Drafting

**Workflow stage:** Response

| | |
| --- | --- |
| **Task** | Draft a reply to a support message for Holly to check and send. |
| **Problem it solves** | Writing every reply from scratch is slow, and tone slips when busy. |
| **Prompting techniques** | Role framing (Holly as founder); brand-voice rules and banned words (constraints); a three-part reply structure and word limit (structured output); an "only use facts given" rule to stop made-up details. |

## Final prompt (v3)

> **Role:** You are Holly, the solo founder of Hauly, replying directly to a user. There is no wider team.
>
> **Action:** Write a reply to the user message below.
>
> **Context:** Voice: warm, plain language, no corporate jargon. Use at most one short apology — prefer thanking them for reporting it. Never use the word "dupe" (Hauly says "lookalike") and never mention prices unless the user asked. Only use facts given here: do not mention a team, other users, or whether a fix has worked before. Known workaround: none confirmed. Category: {{category}}. User message: "{{message}}"
>
> **Expected output:** Under 80 words, in three parts: (1) one sentence acknowledging their specific issue; (2) what you're doing about it — if no workaround is confirmed, say you're looking into it and ask for one detail that would help (such as phone model and app version) instead of inventing a fix; (3) one warm sign-off line.

Words in `{{double brackets}}` are filled in each time the prompt is used.

## How the prompt was improved

All versions were tested on the same sample message (written for testing, based on real Hauly features): *"The app keeps crashing when I try to add a new product to my Haul. This is so annoying, I've lost half my collection I already typed in!"*

**v1** — one line: *"Reply to this user complaint about a bug in a friendly way."*

- **Result:** 231 words. It apologised several times and gave generic tips (update the app, restart the phone, look for an autosaved draft). It also promised to "flag this to our team", but Hauly has no team.

**v2** — added Holly as the Role, voice rules, and an under-80-word, three-part structure.

- **Result:** 71 words and specific to the crash. But it opened with "I'm so sorry", said "our team is digging into" it, and offered a workaround it claimed "seems to help", with nothing to back that up.

**v3 (final)** — said Holly is a solo founder, allowed at most one apology, banned mentioning a team, other users or unconfirmed fixes, and told it to ask for a useful detail instead of inventing a workaround.

- **Result:** 66 words, no apology (it thanked the user instead), no invented team or fix, and it asked for the phone model and app version.

Full test outputs: [Appendix — Prompt 2](../appendix-test-outputs.md#prompt-2).

## Automation potential

**Medium.** Good for routine bugs and how-to questions. Replies are always checked by Holly before sending; complaints, refunds and anything about payment stay fully manual.

## Risks and limitations

- The AI only knows what is in the prompt, so it can't confirm whether a fix exists — Holly must add known workarounds.
- If sent unedited at high volume, replies may start to sound repetitive.
