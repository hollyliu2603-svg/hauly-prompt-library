# Hauly Prompt Library — BUS4005 Assessment 1

Prompt portfolio for **BUS4005 — Individual Prompt Library, Oral Presentation
and Report** (La Trobe University, Term 5 2026).

**Business context:** Hauly is a solo-founder iOS app for cataloguing beauty
and skincare collections. As sole founder, Holly personally handles user
support, App Store review responses, Circle community moderation,
feature-request triage, and content planning — five jobs a small team would
normally divide among specialist roles. This library turns each into a
repeatable prompt.

The 10 prompts form one pipeline: **intake → response → moderation → content
planning → content drafting → reporting.**

New to the terms used here (RACE, v1/v2, debiasing, etc.)? See
[`GLOSSARY.md`](GLOSSARY.md) first — everything below is written to be
explainable out loud, not just read.

## Contents

| | |
| --- | --- |
| [`GLOSSARY.md`](GLOSSARY.md) | Plain-language definitions — read this first if presenting out loud |
| [`prompts/`](prompts/) | One file per prompt (1–10). Every prompt has a short "v1 → v2" note showing what changed and why; the two most-reworked (2 and 6) show the full before/after |
| [`evaluation.md`](evaluation.md) | Before/after comparison + real generated outputs for Prompts 2 and 6 |
| [`governance-and-business-case.md`](governance-and-business-case.md) | How risks are managed, and the why/what/how/impact business case |
| [`references.md`](references.md) | APA 7 reference list, checked against the actual source documents |

## Iteration history

Every prompt has a documented "v1 → v2" gap-and-fix note. Four go into full
before/after detail because they're the strongest evidence of the process;
the other six get a shorter version of the same thing.

| Prompt | v1 problem | v2 fix |
| --- | --- | --- |
| 1 — Support Ticket Triage | No fixed category/urgency list — AI could invent its own labels | Locked in a fixed set of options and a strict output format |
| 2 — Customer Support Reply Drafting | No Role/Context/Expected output — generic, over-apologetic replies | Added founder Role, brand-voice rules, and a 3-part reply structure |
| 3 — App Store Review Responses | No rule against a defensive tone | Added "no defensive tone even if the review is unfair" |
| 4 — Bug Report Summarisation | AI could guess at the technical cause freely | Only infer a cause with evidence; mark inferred steps clearly |
| 5 — Feature Request Evaluation | Didn't check requests against product principles | Added an explicit "flag if it conflicts with a stated principle" step |
| 6 — Social Media Trend Analysis | No safeguards at all — could repeat an unverified viral claim or a skewed sample uncritically | Full debiasing pass: inclusive-language rule, testing against different users, and a self-check step |
| 7 — Circle Community Moderation | No self-check; "remove" action implied automatic removal | Added a self-check step; renamed to "recommend_remove" — always a human decision |
| 8 — FAQ & Gazette Drafting | No fallback for an unclear "mode" — could silently guess wrong | Added an explicit "ask for clarification" fallback |
| 9 — Push Notification Copy | Missing Role field | Explicit Role added, caught by checking all 10 prompts against RACE |
| 10 — Weekly Trends Report | Could calculate a made-up percentage change with only one data point | Only calculate a percentage when both numbers are actually supplied |

Prompt 6's refinement is the most substantial — see
[`evaluation.md`](evaluation.md) for the full comparison and real generated
outputs showing v1 passing along an unverified "cures acne overnight" claim
that v2 catches and flags.

## Notes for the marker

- All business-impact claims are framed as **proposed pilot targets**, not
  measured results — see `governance-and-business-case.md`.
- Platform character-limit figures (Prompts 3 and 9) were checked against
  primary sources rather than assumed; see `references.md` and the relevant
  prompt files for what was actually verified.
- The RACE framework citation (Topic 3, Figure 1.9) was confirmed against the
  subject PDF; one attribution detail is flagged as unconfirmed in
  `references.md` pending a manual check.
