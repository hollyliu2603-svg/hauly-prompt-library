# Prompt 4 — Bug Report Summary

**Workflow stage:** Intake

## Intended task

Turn a messy user bug report into a clear, structured ticket for fixing.

## Problem being solved

User bug reports are informal and incomplete. Holly has to reread them and work out the steps before any fixing can start, and a guessed cause can send the work in the wrong direction.

## Prompting techniques

Role framing; fixed ticket sections (structured output); a rule against guessing the cause; labelling any step the user didn't state as "(inferred)" (constraints).

## Automation potential

**High.** This can run on every bug report, because a person still reads the ticket before any work starts.

## Risks and limitations

- Steps marked "(inferred)" can be wrong.
- Severity is a first guess and needs checking before deciding what to fix first.
- The AI can't see the app's code, so it can't diagnose problems — which is why it is told not to try.

## What the versions illustrate

| Version | What changed | What to notice in the response |
| --- | --- | --- |
| V1 | Asks for a "likely technical cause" | Invents a cause ("the recent update introduced a breaking change to the ingredient-scan API call or response parsing") and lists steps the user never described without marking them |
| V2 (final) | Removes the cause section, bans guessing, requires "(inferred)" labels | No cause; unstated steps marked "(inferred)"; missing device details listed as "not provided"; the 200 products noted with "relevance to bug not confirmed" |

**Discussion:** Both versions used the same report. Asking for a cause invited the AI to produce a reasonable-sounding explanation with no evidence — reasonable is not the same as verified.

## Final prompt — reusable template (V2)

> **Role:** You are turning raw user bug reports into a structured ticket for a solo developer.  
>
> **Action:** Pull out the details needed to fix the bug without re-reading the original message. Do not guess the technical cause unless the message gives evidence for it.  
>
> **Context:** Hauly is an iPhone app. Message: "{{message}}"  
>
> **Expected output:** Steps to reproduce (numbered; if a step is not stated by the user, mark it "(inferred)"); expected vs actual behaviour; device details if mentioned, otherwise "not provided"; affected tab/feature; severity (cosmetic / functional / blocking) with one sentence of reasoning.  

Words in `{{double brackets}}` are filled in each time the prompt is used.

## Versions and recorded responses

Every version below was run once on the same sample input, written for testing and based on real Hauly features (not a real user message). Tests used Claude Sonnet 5 in September 2026. Responses are copied exactly as returned.

**Sample input:** *"since the last update whenever i use scan ingredients on a product it just shows a spinning wheel forever then goes back to my haul. i have like 200 products in there. iphone"*

### V1

**Prompt text (as tested)**

~~~text
Role: You are turning raw user bug reports into a structured ticket for a solo developer.
Action: Pull out the details needed to fix the bug without re-reading the original message, including the likely technical cause.
Context: Hauly is an iPhone app. Message: "since the last update whenever i use scan ingredients on a product it just shows a spinning wheel forever then goes back to my haul. i have like 200 products in there. iphone"
Expected output: Steps to reproduce (numbered); expected vs actual behaviour; device details; affected tab/feature; likely technical cause; severity (cosmetic / functional / blocking) with one sentence of reasoning.
~~~

**Recorded response**

~~~text
# Bug Ticket: Scan Ingredients — Infinite Spinner, Silent Failure

## Title
Scan Ingredients hangs on loading spinner then silently returns to Haul (post-update regression)

## Steps to Reproduce
1. Open Hauly app on iPhone
2. Navigate to Haul (user's product list, ~200 items)
3. Select a product from the Haul
4. Tap "Scan Ingredients" on that product
5. Observe loading spinner appears
6. Wait — spinner spins indefinitely
7. App automatically navigates back to the Haul screen (no result, no error shown)

## Expected vs. Actual Behavior
- **Expected:** Scan Ingredients processes the product and returns ingredient analysis/results within a reasonable time.
- **Actual:** Spinner loads indefinitely, then the app silently exits the flow back to the Haul screen with no output, no error message, and no ingredient data shown.

## Device Details
- **Platform:** iPhone (iOS)
- **App:** Hauly
- **Regression trigger:** Started after the most recent app update (pre-update behavior not specified — need to confirm if this worked before)
- **User's dataset size:** ~200 products in Haul (may be relevant — see likely cause)

## Affected Tab/Feature
- Scan Ingredients feature (likely OCR/ingredient-parsing flow), triggered from within a Haul product detail view

## Likely Technical Cause
- Most probable: the recent update introduced a breaking change to the ingredient-scan API call or response parsing (e.g., changed endpoint, schema mismatch, or auth token handling), causing the request to hang until a client-side timeout silently kicks the user back rather than surfacing an error.
- Secondary possibility: performance/memory issue tied to large Haul size (~200 products) — e.g., the scan flow may be doing a full Haul re-sync or lookup against the entire product list before/after scanning, and that operation is timing out or crashing silently on larger datasets.
- Worth checking: is failure reproducible with a smaller/fresh Haul, or only with 200+ items? This will help isolate between "API regression" vs. "scale/performance regression."

## Severity: **Blocking**
Reasoning: This disables a core feature (ingredient scanning) entirely for the user with no error feedback or workaround, directly preventing the app's primary use case.
~~~

### V2 (final)

**Prompt text (as tested)**

~~~text
Role: You are turning raw user bug reports into a structured ticket for a solo developer.
Action: Pull out the details needed to fix the bug without re-reading the original message. Do not guess the technical cause unless the message gives evidence for it.
Context: Hauly is an iPhone app. Message: "since the last update whenever i use scan ingredients on a product it just shows a spinning wheel forever then goes back to my haul. i have like 200 products in there. iphone"
Expected output: Steps to reproduce (numbered; if a step is not stated by the user, mark it "(inferred)"); expected vs actual behaviour; device details if mentioned, otherwise "not provided"; affected tab/feature; severity (cosmetic / functional / blocking) with one sentence of reasoning.
~~~

**Recorded response**

~~~text
# Bug Ticket

**Title:** Scan Ingredients hangs on spinning wheel and reverts to Haul (post-update)

## Steps to Reproduce
1. Open Hauly app (inferred)
2. Navigate to a product within the Haul (inferred)
3. Tap "Scan Ingredients" on that product
4. Observe spinning wheel
5. Wheel spins indefinitely, then app returns to the Haul screen with no result

## Expected vs Actual Behavior
- **Expected:** Scan Ingredients completes and displays ingredient results for the product.
- **Actual:** Spinning wheel loads indefinitely, then the app kicks the user back to the Haul screen without showing results or an error message.

## Device Details
- Device: iPhone
- Model: not provided
- iOS version: not provided
- App version: not provided (user references "the last update" but does not name a version)

## Affected Tab/Feature
Scan Ingredients feature (accessed from a product within the Haul tab)

## Additional Context Provided by User
- Haul contains ~200 products (user-supplied detail, relevance to bug not confirmed)
- Issue reportedly began after the most recent app update

## Severity
**Blocking** — The Scan Ingredients feature, a core function of the app, fails 100% of the time as described, with no apparent workaround mentioned by the user.
~~~
