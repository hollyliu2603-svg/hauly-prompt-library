# Evaluation: Before vs After

For the two most-reworked prompts (2 and 6), I ran the old version (v1) and
the new version (v2) on the exact same test input and compared the actual
answers side by side — an A/B test, in Topic 3's terms — scored on
accuracy, consistency, readability, fit with the business, safety, and bias.

## Prompt 2 — Customer Support Reply Drafting

| Criterion | Prompt A (v1) | Prompt B (v2) |
| --- | --- | --- |
| Accuracy | Inconsistent, sometimes generic | More consistent — named the specific issue |
| Consistency | Tone/length varied run to run | Stayed under 80 words across runs tested |
| Alignment with business criteria | Not controlled | More reliably controlled through explicit constraints — not a guarantee |

**Sample test input (support message, category: bug):** "The app keeps crashing
when I try to add a new product to My Haul. This is so annoying, I've lost half
my collection I already typed in!"

**Prompt A (v1) actual output:** "Hi there! I'm so sorry to hear you're
experiencing this issue! We really appreciate you taking the time to reach out
to us, and we sincerely apologise for any inconvenience this may have caused.
Our team is aware of similar issues and we're working hard behind the scenes to
make sure everything runs smoothly for our valued users. Please don't hesitate
to reach out again if you need anything else. Thank you so much for your
patience and for being part of our community! 😊"
*(86 words — over the target length, generic, over-apologetic, no
acknowledgement of the specific crash-and-data-loss issue, and no workaround or
next step offered.)*

**Prompt B (v2) actual output:** "Thanks for flagging this — losing entries
you'd already logged in My Haul because of a crash is genuinely frustrating. We
haven't reproduced this exact crash yet — could you tell me your phone model
and app version? In the meantime, closing and reopening the app before each new
entry has worked around similar reports. I'll update you as soon as there's a
fix. — Holly"
*(62 words — names the specific issue, gives a concrete workaround and a next
step, stays under the 80-word limit, no banned wording.)*

## Prompt 6 — Social Media Trend Analysis & Gazette Planning

| Evaluation criterion | Prompt A (v1) | Prompt B (v2) | Lesson learned |
| --- | --- | --- | --- |
| Context relevance | Identifies general beauty trends | Connects trends to Hauly's Gazette and audience | Business context improves relevance |
| Evidence quality | May treat popularity as proof | Requires supplied evidence and states limitations | Evidence constraints reduce unsupported claims |
| Bias control | No explicit safeguards | Inclusive language and counterfactual checks | Debiasing needs to be stated, not assumed |
| Safety | May repeat skincare claims uncritically | Flags medical/exaggerated claims for review | Human review remains necessary |

**Sample test input (supplied trend evidence):** "1. Platform: TikTok. Caption:
'POV: my skin after slugging every night for a month ✨'. Trend: slugging
(occlusive moisturiser layering), shown mostly on fair/light-skin creators.
Date: Aug 2026. Engagement: 2.1M views on top video. 2. Platform: TikTok.
Caption: 'Ice rolling literally cured my cystic acne overnight!!'. Trend: ice
roller videos claiming an overnight cure for cystic acne. Date: Aug 2026.
Engagement: 4.8M views, trending audio."

**Prompt A (v1) actual output:** "Trend ratings — 1. Slugging: Relevance 4/5,
popular routine with strong content opportunity for Restock and Learn. 2. Ice
rolling for acne: Relevance 5/5, extremely high engagement (4.8M views) shows
strong audience interest. Content ideas: (1) 'The Ultimate Slugging Guide' —
Learn tab, step-by-step night routine; (2) 'Does Ice Rolling Really Cure Acne
Overnight?' — Gazette, capitalise on the viral trend and cover technique; (3)
'Get the Glass Skin Look with Slugging' — Learn, aesthetic inspiration."
This passes along the unverified "cures acne overnight" claim as a content
opportunity, treats view count as evidence the claim works, and never flags
that the supplied slugging examples skew toward one skin tone.

**Prompt B (v2) actual output (abridged to the sections that changed the
outcome):** "Trend overview — slugging: established (recurring, multiple
dates); ice rolling for acne: emerging, overnight-cure framing not
corroborated across supplied sources. Evidence limitations — two data points,
both TikTok, both Aug 2026; view counts reflect reach, not effectiveness. Bias
and inclusion review — supplied slugging content skews toward fair/light-skin
creators; flag this and use varied skin tones in any Hauly-produced visuals.
Editorial and safety risks — the 'cures cystic acne overnight' claim is an
unverified, medical-adjacent claim from a single viral source; do not repeat
or imply it in Hauly content. Recommendation status — slugging idea suitable
for founder review (with a sensitive-skin caution added); the ice-rolling idea
is not suitable for Gazette development as currently framed."
The evidence-limitation and bias-review steps are what catch the exaggerated
claim and the skin-tone skew that v1 missed — the improvement traces to the
added Expected-output sections, not to better-sounding prose.

These sample outputs were generated by running both prompt versions against
the same test input; wording will vary slightly on any given run of a language
model, but the *pattern* shown here — v1 passing an unverified claim through
uncritically, v2 catching it via the evidence and bias-review steps — was
consistent across the runs checked for this report.

## How the improvement process actually worked (Topic 3's 5-step loop)

Topic 3 teaches a 5-step way of improving a prompt: write a first version →
test it → work out what's wrong → fix it → test again. Prompt 2 walks
through it in full:

1. **First version:** "Reply to this user complaint about a bug in a friendly
   way: {{message}}" (v1).
2. **Test it:** v1 gave a generic, over-apologetic reply with no next step
   (see the actual output above).
3. **Work out what's wrong:** no Role, no brand-voice rule, no output
   structure — the problem was a missing Context and Expected output, not
   bad wording.
4. **Fix it:** v2 adds a Role (Holly, founder), a Context with the actual
   voice rules, and an Expected output with a word limit and structure.
5. **Test again:** the new version stayed under the word limit, never used
   the banned word, and gave the user a next step — a clear, visible
   improvement.

The same process was used for Prompt 6 (adding the debiasing checks), Prompt
7 (adding the self-check step), and Prompt 9 (adding the missing Role).
