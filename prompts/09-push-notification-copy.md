# Prompt 9 — Push Notification and Banner Copy

**Workflow stage:** Content drafting

## Intended task

Write a push notification and an in-app banner for one announcement.

## Problem being solved

Announcements need to go out quickly and sound like Hauly, without a copywriter.

## Prompting techniques

Role framing; character and word limits, and a ban on pushy sales language (constraints); fixed output format (structured output).

## Automation potential

**High** — the copy could be used with limited manual editing. A low-risk, frequent task — a quick tone check before sending is enough.

## Risks and limitations

- **Length limit:** 40 characters is a chosen target, not a platform rule. How much text shows depends on the device and whether images are used. CleverTap (n.d.) and Reteno (n.d.) suggest iOS titles of about 25–50 characters and Android titles of up to 65, so 40 keeps the text short enough for both.
- **Paid features:** announcements about a Hauly Plus feature must say so clearly.

## What the versions illustrate

| Version | What changed | What to notice in the response |
| --- | --- | --- |
| V1 | No Role (found by checking all ten prompts against RACE) | Push "Scan ingredients, get plain English" (35 characters); banner 17 words; met every rule |
| V2 (final) | Adds the Role | Push "Scan a label for a plain-English report" (39 characters); banner 18 words; met every rule |

**Discussion:** Both versions used the same announcement. Adding the Role made no visible difference in this test; the change keeps the prompt consistent with RACE; it did not improve the copy. **Naming note:** the sample announcement says "Ingredient Report"; on the app screen the feature is titled "Label report", so a real announcement should use that name.

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

## Prompt Lab check (GPT-4.1 mini)

To check the results weren't specific to one AI model, the first and final versions were re-run in La Trobe Prompt Lab using GPT-4.1 mini, with exactly the same prompt text. Prompt Lab's prompt review scores the prompt itself out of 100.

**What GPT-4.1 mini did:**

| Version | Push | Banner | Rules met |
| --- | --- | --- | --- |
| V1 | "Scan ingredients for a clear report" (35 characters) | 13 words; mentions Hauly Plus | All |
| V2 (final) | "Scan ingredients for easy reports" (33 characters) | 13 words; mentions Hauly Plus | All |

- **Same finding as Claude Sonnet 5:** both versions met every rule, and adding the Role made no visible difference.
- **Prompt Lab review:** V1 scored 90.25/100 and V2 scored 90.5/100 — almost the same, which agrees with the outputs. The V1 review did not mention the missing Role.

### Prompt Lab — V1

**Recorded response (GPT-4.1 mini)**

~~~text
{"push": "Scan ingredients for a clear report", "banner": "Now with Hauly Plus: scan any product’s ingredients for a simple, easy-to-understand report."}
~~~

**Prompt Lab review:** overall score 90.25/100

~~~text
Rubric Scores
* Clarity: 90/100 - The prompt is mostly clear, specifying the tone, content, and format, but could clarify the exact style of "plain, warm" voice with examples.
* Constraints: 95/100 - The prompt provides strong constraints on length, tone, and style, including specific prohibitions on urgency and punctuation.
* Structure: 90/100 - The prompt is well-structured with clear sections (Action, Context, Announcement, Expected output), but could benefit from bullet points or numbered lists for easier parsing.
* Verifiability: 85/100 - The prompt is verifiable by checking length, tone, and content, but "plain, warm" voice is subjective and may need more concrete criteria.
* Hallucination Risk: 95/100 - The prompt is low risk for hallucination as it is based on a specific announcement and clear instructions.
Overall score: 90.25/100
Top Improvements
* Provide concrete examples or definitions of "plain, warm" voice to reduce subjectivity.
* Use bullet points or numbered lists to improve prompt readability and structure.
* Clarify how to handle contractions or specific language style to better guide tone.
~~~

### Prompt Lab — V2 (final)

**Recorded response (GPT-4.1 mini)**

~~~text
{"push": "Scan ingredients for easy reports", "banner": "Scan any product’s ingredients and get a clear Ingredient Report with Hauly Plus."}
~~~

**Prompt Lab review:** overall score 90.5/100

~~~text
Rubric Scores
* Clarity: 90/100 - The prompt clearly defines the role, action, context, announcement, and output format, but could be slightly clearer on tone nuances.
* Constraints: 95/100 - The prompt provides specific length limits and style restrictions, effectively constraining the output.
* Structure: 90/100 - The prompt is well-organized with labeled sections, though the formatting could be more visually distinct for easier parsing.
* Verifiability: 85/100 - The announcement content is explicit and verifiable, but the prompt could specify how to handle ambiguous terms like "plain-English."
* Hallucination Risk: 95/100 - The prompt minimizes hallucination risk by providing exact announcement text and clear style guidelines.
Overall score: 90.5/100
Top Improvements
* Clarify the tone further by providing examples or more detailed descriptors of "plain, warm, never salesy."
* Improve structure by using bullet points or clearer separation between sections.
* Specify how to handle ambiguous terms like "plain-English" to ensure consistent interpretation.
~~~
