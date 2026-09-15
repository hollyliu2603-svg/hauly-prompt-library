# 9. Push Notification & Announcement Copywriter

**What it does:** Drafts a push notification and a matching in-app banner
for one announcement, in Hauly's voice.

**Technique used:** RACE structure, with length and tone rules built in.

## v1 (first draft)

> **Action:** Write a push notification and an in-app banner for the announcement
> below.
>
> **Context:** Hauly's brand voice: plain, warm, never salesy. Announcement:
> "{{announcement}}"
>
> **Expected output:** Keep the push notification concise, targeting a maximum
> of 40 characters for readability. Banner max 25 words. No exclamation mark
> stacking, no urgency/FOMO language ("don't miss out", "limited time"). Output
> as: `{"push": "...", "banner": "..."}`

**Problem with v1:** No stated Role at all — it just opened with an
instruction. Every other prompt in the library states a Role explicitly;
this got caught only by checking all 10 prompts against the RACE framework
side by side.

## v2 (fixed — Role added)

> **Role:** You are Hauly's in-house copywriter, writing user-facing announcement
> copy.
>
> **Action:** Write a push notification and an in-app banner for the announcement
> below.
>
> **Context:** Hauly's brand voice: plain, warm, never salesy. Announcement:
> "{{announcement}}"
>
> **Expected output:** Keep the push notification concise, targeting a maximum
> of 40 characters for readability. Banner max 25 words. No exclamation mark
> stacking, no urgency/FOMO language ("don't miss out", "limited time"). Output
> as: `{"push": "...", "banner": "..."}`

A small fix, but a real example of using a structural framework (RACE) to
catch a gap that reading the prompt on its own didn't reveal.

**Why it matters:** Marketing copy for feature launches or reminders needs
to go out quickly and consistently, without a copywriter on staff.

**How much can run on its own:** High — low-risk, high-frequency task, though
still worth a quick check for tone before publishing.

**Watch out for:** Left unconstrained, an AI defaults to generic
app-marketing tone (urgency, exclamation marks) — hence the explicit rule
against it. Also — I checked the "40 characters" figure against actual
platform behaviour: no platform enforces one single hard limit for push
notifications; it depends on the device and OS. Rough real-world guidance:
iOS titles show in full up to about 25–50 characters (bodies cut off around
150), Android titles up to about 65 (bodies around 240). 40 is used here as
a safely-short shared target, not a documented rule, and is worth checking
on the actual devices before publishing.
