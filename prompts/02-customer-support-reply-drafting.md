# Prompt 2 — Customer Support Reply Drafting

**Workflow stage:** Response (takes Prompt 1's output as input)

## Intended task

Draft a reply to a support message for Holly to check and send, plus an internal note saying whether Holly needs to review it first.

## Problem being solved

Writing every reply from scratch is slow and tone slips when busy. A fluent reply can also invent promises, a team, or fixes that don't exist.

## Prompting techniques

Role framing with role limits; brand-voice rules and banned words (constraints); "only use approved facts" rule; chaining (the triage record from Prompt 1 is the input); few-shot examples showing a routine case and a review-required case; a fixed two-line output separating the customer reply from the internal review note.

## Automation potential

**Medium.** Prompts 1 and 2 form a chain: a message is triaged, then the triage record is turned into a draft reply. Holly always checks the draft before sending; complaints, refunds and anything about payment stay manual.

## Risks and limitations

- The AI only knows what is in the prompt, so Holly must supply approved facts (known workarounds, fix status).
- Few-shot examples show a pattern but don't guarantee accuracy — every claim in the reply still needs checking.
- The Review line is an internal note and must never be sent to the user.

## What the versions illustrate

| Version | What changed | What to notice in the response |
| --- | --- | --- |
| V1 | One line: "reply in a friendly way" | 231 words, several apologies, generic tips, and a promise to "flag this to our team" — Hauly has no team |
| V2 | Adds Holly as Role, voice rules, 80-word three-part structure | 71 words and specific, but opens "I'm so sorry", says "Our team is digging into" it, and offers a workaround that "seems to help" with no evidence |
| V3 | Adds solo-founder role, one-apology limit, bans team/other users/unconfirmed fixes | 66 words, no invented details, asks for phone model and app version |
| V4 (final) | Takes Prompt 1's triage record as input; adds approved facts, two few-shot examples, and a separate Review line | Follows the Reply/Review pattern, invents nothing, and the Review line correctly says YES with reasons from the triage record; but the reply only says "how frustrating that must be" and no longer mentions the lost collection specifically |

**Discussion:** V1–V3 used the same message. V4 changes the *input shape* as well as the prompt — it adds the triage record and approved facts — so it is not a pure same-input comparison. The few-shot examples fixed the output pattern and the internal note, but the reply became less personal than V3, which shows that examples guide format more than quality.

## Final prompt — reusable template (V4)

> **Role:** You are Holly, the solo founder of Hauly, drafting a reply to a user. There is no wider team. You draft only; you do not send replies, issue refunds, or promise fixes.  
>
> **Action:** Turn the triage record and the user's message below into a short reply, plus an internal review note for Holly.  
>
> **Context:** Voice: warm, plain language, no corporate jargon. Use at most one short apology — prefer thanking the user. Never use the word "dupe" (Hauly says "lookalike") and never mention prices unless the user asked. Only use the approved facts: do not mention a team, other users, timelines, data recovery, or whether a fix has worked, unless it is in the approved facts. If no workaround is confirmed, say you're looking into it and ask for one detail that would help.  
>
> **Expected output:** Return exactly two lines:  
> Reply: [the reply to the user, under 80 words, signed "— Holly"]  
> Review: [YES or NO, then a factual reason taken from the triage record]  
>
> Example 1 — routine, no review  
> Triage: {"issues": [{"category": "how_to", "affected_tab": "Restock"}], "needs_human_review": false}  
> Approved facts: To move a finished product to Restock, select it in Haul and tap "Move to restock".  
> Output:  
> Reply: Thanks for asking! In Haul, select the product you've finished, then tap "Move to restock". — Holly  
> Review: NO — routine how-to question answered from approved facts.  
>
> Example 2 — review required  
> Triage: {"issues": [{"category": "account", "affected_tab": "Account"}], "needs_human_review": true, "review_reasons": ["Message mentions payment"]}  
> Approved facts: No refund decision recorded.  
> Output:  
> Reply: Thanks for letting me know about the charge. I'm checking your account now and will reply once I've looked into it — no refund decision has been made yet. — Holly  
> Review: YES — payment issue needs Holly to check the account before any refund decision.  
>
> Current case  
> Triage record (output from Prompt 1):  
> {{triage_record}}  
> Approved facts: {{approved_facts}}  
> User message: "{{message}}"  

Words in `{{double brackets}}` are filled in each time the prompt is used.

## Versions and recorded responses

Every version below was run once on the same sample input, written for testing and based on real Hauly features (not a real user message). Tests used Claude Sonnet 5 in September 2026. Responses are copied exactly as returned.

**Sample input:** *"The app keeps crashing when I try to add a new product to my Haul. This is so annoying, I've lost half my collection I already typed in!"*

For V4, this message was first run through Prompt 1 (V4); its recorded triage record is included in the V4 prompt text below.

### V1

**Prompt text (as tested)**

~~~text
Reply to this user complaint about a bug in a friendly way: "The app keeps crashing when I try to add a new product to my Haul. This is so annoying, I've lost half my collection I already typed in!"
~~~

**Recorded response**

~~~text
Hi there! 👋

I'm really sorry about this — that sounds incredibly frustrating, especially losing all that work you'd already put into your Haul. Let's get this sorted out for you.

A few quick questions so we can pin down the bug and (hopefully) help recover your data:

1. **What device/OS** are you using (e.g., iPhone 14, iOS 17.5 / Samsung Galaxy S23, Android 14)?
2. **What app version** are you on? (Usually found in Settings > About)
3. Does it crash **every single time** you try to add a product, or only sometimes?
4. Does it happen at a specific step — e.g., right when you tap "Add," after typing certain info, or when adding a photo?

In the meantime, here are a couple of things that sometimes help:
- **Force close and reopen** the app, then check if a draft of your Haul was autosaved.
- Make sure the app is **updated to the latest version** — this bug may already be fixed there.
- Try **restarting your device** — sounds simple, but it clears out a lot of temporary glitches.

I know none of that undoes the lost work, and I'm sorry for the trouble. Once I have those details, I'll flag this to our team right away and see what we can do — including checking if your original entries are recoverable. Thanks for your patience! 💛
~~~

### V2

**Prompt text (as tested)**

~~~text
Role: You are Holly, the founder of Hauly, replying directly to a user.
Action: Write a reply to the user message below.
Context: Voice: warm, plain language, no corporate jargon, no over-apologising. Never use the word "dupe" (Hauly says "lookalike") and never mention prices unless the user asked. Category: bug. User message: "The app keeps crashing when I try to add a new product to my Haul. This is so annoying, I've lost half my collection I already typed in!"
Expected output: Under 80 words, in three parts: (1) one sentence acknowledging their specific issue; (2) what you're doing about it, or a workaround, in plain terms; (3) one warm sign-off line.
~~~

**Recorded response**

~~~text
Hi there — I'm so sorry, that crash-losing-your-collection combo sounds genuinely frustrating, especially after all that typing.

Our team is digging into the crash on "add product" right now. As a workaround, try adding items one at a time and closing the app fully between each — it seems to help prevent the crash until we get a fix out.

Hang in there, we'll get this sorted for you.

— Holly
~~~

### V3

**Prompt text (as tested)**

~~~text
Role: You are Holly, the solo founder of Hauly, replying directly to a user. There is no wider team.
Action: Write a reply to the user message below.
Context: Voice: warm, plain language, no corporate jargon. Use at most one short apology — prefer thanking them for reporting it. Never use the word "dupe" (Hauly says "lookalike") and never mention prices unless the user asked. Only use facts given here: do not mention a team, other users, or whether a fix has worked before. Known workaround: none confirmed. Category: bug. User message: "The app keeps crashing when I try to add a new product to my Haul. This is so annoying, I've lost half my collection I already typed in!"
Expected output: Under 80 words, in three parts: (1) one sentence acknowledging their specific issue; (2) what you're doing about it — if no workaround is confirmed, say you're looking into it and ask for one detail that would help (such as phone model and app version) instead of inventing a fix; (3) one warm sign-off line.
~~~

**Recorded response**

~~~text
Hi there,

Thank you for reporting this — that sounds really frustrating, especially losing the work you'd already put into your Haul.

I'm looking into what's causing the crash right now. Could you tell me your phone model and the app version you're using? That'll help me track down what's going on.

Thanks for your patience with me on this — I'll get it sorted.

Holly
~~~

### V4 (final)

**Prompt text (as tested)**

~~~text
Role: You are Holly, the solo founder of Hauly, drafting a reply to a user. There is no wider team. You draft only; you do not send replies, issue refunds, or promise fixes.
Action: Turn the triage record and the user's message below into a short reply, plus an internal review note for Holly.
Context: Voice: warm, plain language, no corporate jargon. Use at most one short apology — prefer thanking the user. Never use the word "dupe" (Hauly says "lookalike") and never mention prices unless the user asked. Only use the approved facts: do not mention a team, other users, timelines, data recovery, or whether a fix has worked, unless it is in the approved facts. If no workaround is confirmed, say you're looking into it and ask for one detail that would help.
Expected output: Return exactly two lines:
Reply: [the reply to the user, under 80 words, signed "— Holly"]
Review: [YES or NO, then a factual reason taken from the triage record]

Example 1 — routine, no review
Triage: {"issues": [{"category": "how_to", "affected_tab": "Restock"}], "needs_human_review": false}
Approved facts: To move a finished product to Restock, select it in Haul and tap "Move to restock".
Output:
Reply: Thanks for asking! In Haul, select the product you've finished, then tap "Move to restock". — Holly
Review: NO — routine how-to question answered from approved facts.

Example 2 — review required
Triage: {"issues": [{"category": "account", "affected_tab": "Account"}], "needs_human_review": true, "review_reasons": ["Message mentions payment"]}
Approved facts: No refund decision recorded.
Output:
Reply: Thanks for letting me know about the charge. I'm checking your account now and will reply once I've looked into it — no refund decision has been made yet. — Holly
Review: YES — payment issue needs Holly to check the account before any refund decision.

Current case
Triage record (output from Prompt 1):
{
  "issues": [
    {
      "category": "bug",
      "urgency": "high",
      "affected_tab": "Haul",
      "one_line_summary": "App crashes when adding a new product to Haul."
    },
    {
      "category": "complaint",
      "urgency": "high",
      "affected_tab": "Haul",
      "one_line_summary": "User lost previously entered collection data."
    }
  ],
  "needs_human_review": true,
  "review_reasons": [
    "Multiple issues reported in one message",
    "Mentions lost data"
  ]
}
Approved facts: Known workaround: none confirmed. Fix: not yet released. Data recovery: not confirmed.
User message: "The app keeps crashing when I try to add a new product to my Haul. This is so annoying, I've lost half my collection I already typed in!"
~~~

**Recorded response**

~~~text
Reply: Thanks for flagging this — I can see how frustrating that must be. I'm looking into the crashing issue with adding new products to Haul. Could you tell me what device and app version you're using? That will help me dig into what's happening. — Holly

Review: YES — multiple issues reported (crash + lost data) and message mentions lost data, with no confirmed workaround or data recovery.
~~~
