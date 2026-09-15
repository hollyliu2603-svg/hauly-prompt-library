# Prompt 9 — Push Notification and Banner Copy

**Workflow stage:** Content drafting

## Intended task

Write a push notification and an in-app banner for one announcement.

## Problem being solved

Announcements need to go out quickly and sound like Hauly, without a copywriter.

## Prompting techniques

Role framing; character and word limits, and a ban on pushy sales language (constraints); fixed output format (structured output).

## Automation potential

**High.** A low-risk, frequent task — a quick tone check before sending is enough.

## Risks and limitations

- **Length limit:** 40 characters is a chosen target, not a platform rule. How much text shows depends on the device and whether images are used. CleverTap (n.d.) and Reteno (n.d.) suggest iOS titles of about 25–50 characters and Android titles of up to 65, so 40 keeps the text short enough for both.
- **Paid features:** announcements about a Hauly Plus feature must say so clearly.

## What the versions illustrate

| Version | What changed | What to notice in the response |
| --- | --- | --- |
| V1 | No Role (found by checking all ten prompts against RACE) | Push "Scan ingredients, get plain English" (35 characters); banner 17 words; met every rule |
| V2 (final) | Adds the Role | Push "Scan a label for a plain-English report" (39 characters); banner 18 words; met every rule |

**Discussion:** Both versions used the same announcement. Adding the Role made no visible difference in this test; the change keeps the prompt consistent with RACE rather than improving the copy. **Naming note:** the sample announcement says "Ingredient Report"; on the app screen the feature is titled "Label report", so a real announcement should use that name.

## Final prompt — reusable template (V2)

> **Role:** You are Hauly's in-house copywriter, writing announcement copy for users.  
>
> **Action:** Write a push notification and an in-app banner for the announcement below.  
>
> **Context:** Hauly's voice: plain, warm, never salesy. Announcement: "{{announcement}}"  
>
> **Expected output:** Push notification of no more than 40 characters. Banner no more than 25 words. No stacked exclamation marks, no urgency or fear-of-missing-out language ("don't miss out", "limited time"). Output as: {"push": "...", "banner": "..."}  

Words in `{{double brackets}}` are filled in each time the prompt is used.

## Versions and recorded responses

Every version below was run once on the same sample input, written for testing and based on real Hauly features (not a real user message). Tests used Claude Sonnet 5 in September 2026. Responses are copied exactly as returned.

**Sample input:** *"New in Hauly: scan the ingredients list on any product and get a plain-English Ingredient Report (a Hauly Plus feature)."*

### V1

**Prompt text (as tested)**

~~~text
Action: Write a push notification and an in-app banner for the announcement below.
Context: Hauly's voice: plain, warm, never salesy. Announcement: "New in Hauly: scan the ingredients list on any product and get a plain-English Ingredient Report (a Hauly Plus feature)."
Expected output: Push notification of no more than 40 characters. Banner no more than 25 words. No stacked exclamation marks, no urgency or fear-of-missing-out language ("don't miss out", "limited time"). Output as: {"push": "...", "banner": "..."}
~~~

**Recorded response**

~~~text
{"push": "Scan ingredients, get plain English", "banner": "Scan any product's ingredients list and get a plain-English report explaining what's inside. Available with Hauly Plus."}
~~~

### V2 (final)

**Prompt text (as tested)**

~~~text
Role: You are Hauly's in-house copywriter, writing announcement copy for users.
Action: Write a push notification and an in-app banner for the announcement below.
Context: Hauly's voice: plain, warm, never salesy. Announcement: "New in Hauly: scan the ingredients list on any product and get a plain-English Ingredient Report (a Hauly Plus feature)."
Expected output: Push notification of no more than 40 characters. Banner no more than 25 words. No stacked exclamation marks, no urgency or fear-of-missing-out language ("don't miss out", "limited time"). Output as: {"push": "...", "banner": "..."}
~~~

**Recorded response**

~~~text
{"push": "Scan a label for a plain-English report", "banner": "Scan any product's ingredients list and get a plain-English breakdown of what's inside, now available with Hauly Plus."}
~~~
