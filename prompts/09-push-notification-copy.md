# Prompt 9 — Push Notification and Banner Copy

**Workflow stage:** Content drafting

| | |
| --- | --- |
| **Task** | Write a push notification and an in-app banner for one announcement. |
| **Problem it solves** | Announcements need to go out quickly and sound like Hauly, without a copywriter. |
| **Prompting techniques** | Role framing; character and word limits, and a ban on pushy sales language (constraints); fixed output format (structured output). |

## Final prompt (v2)

> Role: You are Hauly's in-house copywriter, writing announcement copy for users.
> Action: Write a push notification and an in-app banner for the announcement below.
> Context: Hauly's voice: plain, warm, never salesy. Announcement: "{{announcement}}"
> Expected output: Push notification of no more than 40 characters. Banner no more than 25 words. No stacked exclamation marks, no urgency or fear-of-missing-out language ("don't miss out", "limited time"). Output as: {"push": "...", "banner": "..."}

Words in `{{double brackets}}` are filled in each time the prompt is used.

## How the prompt was improved

All versions were tested on the same sample message (written for testing, based on real Hauly features): *"New in Hauly: scan the ingredients list on any product and get a plain-English Ingredient Report (a Hauly Plus feature)."*

**v1** — had no Role. The gap was found by checking all ten prompts against the RACE structure.

**v2 (final)** — added the Role.

**Test results:**
- **v1:** push *"Scan ingredients, get plain English"* (35 characters); banner 17 words.
- **v2:** push *"Scan a label for a plain-English report"* (39 characters); banner 18 words.
- Both met every rule. **Adding the Role made no visible difference in this test.** The change keeps the prompt consistent with the RACE structure; it is not evidence of better copy.

Full test outputs: [Appendix — Prompt 9](../appendix-test-outputs.md#prompt-9).

## Automation potential

**High.** A low-risk, frequent task — a quick tone check before sending is enough.

## Risks and limitations

- **Length limit:** 40 characters is a chosen target, not a platform rule. How much text shows depends on the device and whether images are used. CleverTap (n.d.) and Reteno (n.d.) suggest iOS titles of about 25–50 characters and Android titles of up to 65, so 40 keeps the text short enough for both.
- **Paid features:** announcements about a Hauly Plus feature must say so clearly, so free users aren't misled.
