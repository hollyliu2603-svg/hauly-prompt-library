# 3. App Store Review Response Generator

**What it does:** Drafts a public reply to an App Store review, for Holly to
approve before it's posted.

**Technique used:** RACE structure, with a length limit and a "no defensive
tone" rule built in.

> **Role:** You are the Hauly team, responding publicly to an App Store review.
>
> **Action:** Write a response to the review below.
>
> **Context:** This response is visible to all future readers of the review, not
> just the reviewer. Star rating: {{stars}}. Review text: "{{review}}"
>
> **Expected output:** Use a maximum of 350 characters as an internal drafting
> limit. No defensive tone even if the review is unfair, no pricing claims,
> signed off as "The Hauly Team." Output the response only — no explanation.

**v1 → v2 note:** The earliest draft of this prompt didn't rule out a
defensive tone, so on an unfair or harsh review it could come across as
snippy or make excuses — not a good look on a public, permanent reply. Adding
"no defensive tone even if the review is unfair" fixed that.

**Why it matters:** Public reviews shape whether people download the app;
unanswered or badly-worded replies look unprofessional and can't really be
taken back once posted.

**How much can run on its own:** High for drafting — but publishing always
needs Holly's sign-off, since it's public and permanent.

**Watch out for:** The AI can misjudge tone on sarcastic reviews. Also — I
checked the "350 characters" figure against the actual platform rules: it's
Google Play's real limit, not Apple's. Apple doesn't publish an official
limit for review replies; App Store Connect's own reply box shows a
4,000-character limit. 350 is kept here as a safely-short shared target for
both stores, not a claimed Apple rule — worth confirming the live limit in
each console before posting.
