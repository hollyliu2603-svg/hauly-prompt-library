# Prompt 6 — Trend Analysis and Gazette Planning

**Workflow stage:** Content planning (approved ideas feed Prompt 8)

## Intended task

Assess social media trends Holly has collected, and recommend whether any should become an article in the Gazette (Hauly's in-app editorial section).

## Problem being solved

Beauty trends often come with exaggerated claims and one narrow beauty standard. Choosing topics without checking can spread misinformation or leave many users out.

## Prompting techniques

Role framing; a seven-section structure (decomposition); a "use only supplied information" rule (constraint); the three debiasing techniques from Module 1, Topic 3 — inclusive-language guidance, testing against different types of users (counterfactual prompting), and a self-check (self-critique); allowed status labels.

## Automation potential

**Medium.** It organises and checks evidence Holly has already gathered. It can't search social media itself, and nothing is published without Holly's approval.

## Risks and limitations

- The AI still adds some outside information despite the rule.
- The bias check tests five types of users — it lowers the risk of excluding people but doesn't prove content is inclusive.
- A narrow sample of trends gives a narrow result.

## What the versions illustrate

| Version | What changed | What to notice in the response |
| --- | --- | --- |
| V1 | Relevance score and content ideas | Flags the acne claim as medical (2/5) but still proposes three ice-roller articles, invents Gazette sections ("Nighttime Routines", "Trend Watch"), and doesn't question one-video evidence |
| V2 | Adds seven sections, evidence rule, bias checks, status labels | Lists evidence limits, runs five user checks, marks the acne trend "Not suitable for Gazette development" — but adds outside facts, e.g. slugging is "a widely known, long-standing skincare technique" |
| V3 (final) | Adds: no outside facts; list them as research questions instead | Most outside facts become research questions; slugging rated "Needs more evidence"; a few general statements remain (e.g. "a routine cosmetic practice") |

**Discussion:** All three versions used the same two trends. Each added rule reduced invented information but none removed it completely, so a human fact-check is still required before any article is written.

## Final prompt — reusable template (V3)

> **Role:** You are Hauly's beauty editorial strategist.  
>
> **Action:** Analyse the supplied social media trends, decide which are relevant to Hauly's audience and Gazette, and produce a content recommendation — including a check of your own recommendation for bias and exclusion before finishing.  
>
> **Context:** Hauly is an app for organising a makeup and skincare collection. The Gazette is Hauly's in-app editorial section (inside Learn, in the Studio tab) with practical beauty and skincare education, not product selling. Use only the supplied information as evidence; do not invent engagement figures, sources, audience reactions, or popularity. Consider whether each trend supports Hauly's educational purpose, could become a lasting (evergreen) article, and whether it creates medical, safety, misinformation or exaggerated-claim risk. Use inclusive language and do not assume one skin tone, gender, age, skin type, budget, or routine represents all Hauly users; do not describe a trend as suitable for everyone. Do not add background facts that are not in the supplied information (for example how to do a technique, which products it uses, who it suits, or its history). If background knowledge would help, write it as a question in a "Questions to research" list inside section (2) instead of stating it as fact. Supplied trends: "{{trends}}"  
>
> **Expected output:** For each trend, seven sections: (1) Trend overview — what the evidence shows, and whether it looks established, emerging, or unclear (use "unclear" when the evidence is thin); (2) Evidence limitations — what's missing, and any claims that shouldn't be treated as proven; (3) Relevance to Hauly — with a 1–5 score; (4) Content recommendation — working title, angle, target reader, three key learning points, format, and evergreen / seasonal / trend-led; (5) Bias and inclusion review — test the recommendation against a beginner, a budget-conscious user, a user with sensitive skin, a user from a different cultural background, and a user with a minimal routine, and name any assumptions found; (6) Editorial and safety risks; (7) Status — one of "suitable for founder review", "needs more evidence", or "not suitable for Gazette development". This output must be reviewed and approved by the founder before anything is published.  

Words in `{{double brackets}}` are filled in each time the prompt is used.

## Versions and recorded responses

Every version below was run once on the same sample input, written for testing and based on real Hauly features (not a real user message). Tests used Claude Sonnet 5 in September 2026. Responses are copied exactly as returned.

**Sample input:**

~~~text
1. Platform: TikTok. Caption: 'POV: my skin after slugging every night for a month ✨'. Trend: slugging (layering a thick occlusive moisturiser at night), shown mostly on fair/light-skin creators. Date: Aug 2026. Engagement: 2.1M views on top video. 2. Platform: TikTok. Caption: 'Ice rolling literally cured my cystic acne overnight!!'. Trend: ice roller videos claiming an overnight cure for cystic acne. Date: Aug 2026. Engagement: 4.8M views, trending audio.
~~~

### V1

**Prompt text (as tested)**

~~~text
Role: You are a content strategist for Hauly.
Action: Rate each supplied trend for relevance, then propose content ideas.
Context: Hauly is an app for organising a makeup and skincare collection. The Gazette is Hauly's in-app editorial section (inside Learn, in the Studio tab) with practical beauty and skincare education, not product selling. Fit criteria: organising not shopping, no prices, no medical claims. Supplied trends: "1. Platform: TikTok. Caption: 'POV: my skin after slugging every night for a month ✨'. Trend: slugging (layering a thick occlusive moisturiser at night), shown mostly on fair/light-skin creators. Date: Aug 2026. Engagement: 2.1M views on top video. 2. Platform: TikTok. Caption: 'Ice rolling literally cured my cystic acne overnight!!'. Trend: ice roller videos claiming an overnight cure for cystic acne. Date: Aug 2026. Engagement: 4.8M views, trending audio."
Expected output: A 1–5 relevance score per trend, then up to 3 content ideas with title, angle, and where in the app it would appear.
~~~

**Recorded response**

~~~text
# Trend Relevance Ratings

**1. Slugging (occlusive night layering) — 4/5**
Strong fit: it's a routine/technique trend, not a product push, and maps naturally onto organising nightly steps, ingredient categories, and product shelf-life — all core to Hauly's "organise, don't sell" mandate. Minor flag: source videos skew toward fair-skin creators, so any Gazette piece should broaden representation and skin-type nuance.

**2. Ice rolling "cures cystic acne overnight" — 2/5**
Poor fit as-is: "cured cystic acne" is an explicit medical claim about a dermatological condition, and the underlying claim is misleading. Can't be covered at face value. There's a narrow opportunity to cover skin *tools* from a purely organisational/hygiene angle, or to gently myth-bust — but the acne-cure claim itself must be avoided entirely.

---

# Content Ideas

## Trend 1: Slugging

**1. "Build Your Slugging Shelf: The Occlusive Layer Checklist"**
- Angle: Practical guide to sequencing a slugging step at the end of a routine, and how to categorise/tag occlusives in your collection so they surface at the right step.
- Placement: Gazette → Nighttime Routines

**2. "What Counts as an Occlusive? A Texture & Ingredient Primer"**
- Angle: Educates on identifying occlusive vs. humectant vs. emollient products (petrolatum, balms, thick creams) so users can label items correctly in their Hauly collection — inclusive of a range of skin types/tones in examples.
- Placement: Gazette → Ingredient Basics

**3. "Slugging Balms: How Long Do They Really Last Once Opened?"**
- Angle: General shelf-life/PAO education for thick occlusive products, tying into Hauly's expiry-tracking feature.
- Placement: Gazette → Expiry & Shelf Life

---

## Trend 2: Ice Rolling

**1. "Where Do Skin Tools Belong in Your Routine? Organising Rollers, Gua Sha & More"**
- Angle: Purely organisational — how to log and sequence tools (ice rollers, gua sha, jade rollers) alongside products in your Hauly collection. No claims about skin outcomes.
- Placement: Gazette → Tools & Extras

**2. "Viral Skin Trends, Decoded: Separating Routine from Remedy"**
- Angle: A measured explainer noting that viral claims (like overnight cures) are anecdotal, not medical advice, and encouraging users to consult a dermatologist for skin concerns — positions Hauly as a trustworthy, non-medical educational source.
- Placement: Gazette → Trend Watch

**3. "Tool Care 101: Cleaning & Storing Your Ice Roller"**
- Angle: Hygiene and storage best practices for reusable skin tools — practical, non-medical, fits organising theme.
- Placement: Gazette → Hygiene & Care
~~~

### V2

**Prompt text (as tested)**

~~~text
Role: You are Hauly's beauty editorial strategist.
Action: Analyse the supplied social media trends, decide which are relevant to Hauly's audience and Gazette, and produce a content recommendation — including a check of your own recommendation for bias and exclusion before finishing.
Context: Hauly is an app for organising a makeup and skincare collection. The Gazette is Hauly's in-app editorial section (inside Learn, in the Studio tab) with practical beauty and skincare education, not product selling. Use only the supplied information as evidence; do not invent engagement figures, sources, audience reactions, or popularity. Consider whether each trend supports Hauly's educational purpose, could become a lasting (evergreen) article, and whether it creates medical, safety, misinformation or exaggerated-claim risk. Use inclusive language and do not assume one skin tone, gender, age, skin type, budget, or routine represents all Hauly users; do not describe a trend as suitable for everyone. Supplied trends: "1. Platform: TikTok. Caption: 'POV: my skin after slugging every night for a month ✨'. Trend: slugging (layering a thick occlusive moisturiser at night), shown mostly on fair/light-skin creators. Date: Aug 2026. Engagement: 2.1M views on top video. 2. Platform: TikTok. Caption: 'Ice rolling literally cured my cystic acne overnight!!'. Trend: ice roller videos claiming an overnight cure for cystic acne. Date: Aug 2026. Engagement: 4.8M views, trending audio."
Expected output: For each trend, seven sections: (1) Trend overview — what the evidence shows, and whether it looks established, emerging, or unclear (use "unclear" when the evidence is thin); (2) Evidence limitations — what's missing, and any claims that shouldn't be treated as proven; (3) Relevance to Hauly — with a 1–5 score; (4) Content recommendation — working title, angle, target reader, three key learning points, format, and evergreen / seasonal / trend-led; (5) Bias and inclusion review — test the recommendation against a beginner, a budget-conscious user, a user with sensitive skin, a user from a different cultural background, and a user with a minimal routine, and name any assumptions found; (6) Editorial and safety risks; (7) Status — one of "suitable for founder review", "needs more evidence", or "not suitable for Gazette development". This output must be reviewed and approved by the founder before anything is published.
~~~

**Recorded response**

~~~text
# Hauly Gazette — Social Trend Content Recommendation Report

**Prepared for founder review | Date: 2026-09-15**
**Scope:** Analysis of two supplied TikTok trends for potential Gazette (Learn > Studio) development.

---

## Trend 1: Slugging

### 1. Trend Overview
The evidence shows a single TikTok video ("POV: my skin after slugging every night for a month ✨") with 2.1M views, dated Aug 2026, depicting the slugging technique — layering a thick occlusive moisturiser overnight. The creators shown are mostly fair/light-skinned. Slugging itself is a widely known, long-standing skincare technique (not new to 2026), so the *practice* appears established, but the evidence supplied here is a single trend snapshot, not proof of broad or lasting relevance to Hauly's specific audience. Status: **established technique, but supplied evidence is a narrow snapshot.**

### 2. Evidence Limitations
- No data on who is engaging (age, skin type, geography) beyond what's visibly shown in the video.
- "Cured," transformative, or before/after claims implied by "✨" are anecdotal — no clinical or dermatological source provided.
- Engagement figure (2.1M) tells us reach, not sentiment, accuracy, or suitability for all skin types.
- No information on skin type of creators (occlusives are not universally recommended for oily/acne-prone or fungal-acne-prone skin) — cannot be assumed safe for all users.
- Representation is narrow (mostly fair/light skin); no evidence this reflects Hauly's actual user base.

### 3. Relevance to Hauly
**Score: 4/5**
Slugging is a legitimate, well-established practical skincare method that fits Hauly's core purpose — helping users understand and organise routines/products (occlusives, moisturisers). It's educational, not sales-driven, and has evergreen potential. Score isn't 5 because the trend itself doesn't provide diversity of skin type/tone evidence, which the Gazette article would need to independently address.

### 4. Content Recommendation
- **Working title:** "Slugging 101: What It Is, Who It's For, and Who Should Skip It"
- **Angle:** Educational breakdown of the technique, its purpose (occlusion, moisture retention), and honest guidance on which skin types may benefit vs. which may want to avoid or modify it — reframing a viral trend into balanced, practical guidance.
- **Target reader:** Any Hauly user curious about night routines, from skincare beginners to those refining an existing routine.
- **Three key learning points:**
  1. What slugging is and the science of occlusion (in plain terms).
  2. Skin types/conditions where caution or modification is advised (e.g., acne-prone, fungal-acne-prone skin).
  3. How to try it affordably using products already owned, rather than buying a new "slugging product."
- **Format:** Short-to-medium educational article with a simple decision-style visual (e.g., "Is slugging right for you?").
- **Evergreen / seasonal / trend-led:** Evergreen, with a trend-led entry point.

### 5. Bias and Inclusion Review
- **Beginner:** Needs the concept explained from scratch — addressed by "What it is" section; ensure no assumed prior knowledge of terms like "occlusive."
- **Budget-conscious user:** Recommendation explicitly notes using existing products, avoiding implication that a specific/new product is required.
- **Sensitive skin user:** Article must include caution language, not treat slugging as universally safe — addressed via "who should skip it."
- **User from different cultural background:** Original trend evidence shows mostly fair/light-skinned creators; article and any imagery must not visually or verbally imply this technique or its results are specific to one skin tone.
- **User with minimal routine:** Should not frame slugging as a "must-add" step; frame as optional, not essential to a "complete" routine.
- **Assumptions found:** Initial trend evidence assumes visual "results" are universal and desirable; assumes occlusion is safe for all skin types by default. Both must be corrected in the article.

### 6. Editorial and Safety Risks
- Risk of implying occlusives are universally safe — must explicitly caveat for acne-prone/fungal-acne-prone skin.
- Risk of the ✨-style "glow-up" framing overselling results not evidenced.
- Must avoid dermatological/medical claims (e.g., "repairs skin barrier") without qualification — use cautious, general language.

### 7. Status
**Suitable for founder review** — solid evergreen educational angle exists, but must be developed with explicit caveats and inclusive imagery/language before publication.

---

## Trend 2: Ice Rolling for Cystic Acne "Overnight Cure"

### 1. Trend Overview
A single TikTok video claims ice rolling "literally cured" cystic acne overnight, with 4.8M views and a trending audio, dated Aug 2026. This is a viral claim, not a documented or established skincare method for treating cystic acne. Status: **unclear/emerging** — high engagement does not equal accuracy, and the core claim is a dramatic personal assertion, not a supported technique.

### 2. Evidence Limitations
- No clinical, dermatological, or scientific source is supplied to support the claim that ice rolling cures cystic acne.
- "Overnight cure" is a strong, absolute claim — the supplied evidence gives no before/after verification, no medical context, no information on the individual's routine, medication use, or acne severity.
- High view count reflects virality/entertainment value, not credibility or reproducibility.
- No information on risks (skin barrier, frostbite, rebound inflammation) is included in the trend evidence — this doesn't mean risks don't exist, only that this evidence doesn't address them.

### 3. Relevance to Hauly
**Score: 1/5**
Cystic acne is a medical/dermatological condition, not something resolved through cosmetic tools or overnight routines. Presenting or engaging with this trend — even to "debunk" it — carries meaningful risk of being associated with misinformation, and it sits outside Hauly's stated purpose (practical beauty/skincare education, not medical claims). Any Gazette content here would need to firmly distance itself from the "cure" framing.

### 4. Content Recommendation
- **Working title:** *Not recommended for direct trend coverage.* If addressed at all, only as: "What Ice Rolling Can (and Can't) Do for Your Skin"
- **Angle:** If pursued, this would need to be a myth-clarification piece explicitly stating cystic acne is a medical condition requiring professional care, and ice rolling has cosmetic (temporary de-puffing/soothing) use only — not a treatment or cure.
- **Target reader:** Users encountering this trend and seeking clarity, particularly those experiencing acne who may be vulnerable to misleading claims.
- **Three key learning points (only if pursued):**
  1. Cystic acne is inflammatory/hormonal and requires professional dermatological guidance — not a cosmetic-tool fix.
  2. Ice rolling's realistic, evidenced-limited cosmetic use (temporary puffiness reduction).
  3. When and why to see a dermatologist rather than rely on viral routines.
- **Format:** Short myth-vs-fact explainer, if developed.
- **Evergreen / seasonal / trend-led:** Trend-led only, and only as a corrective/myth-busting piece — not standalone celebratory content.

### 5. Bias and Inclusion Review
- **Beginner:** Could easily misunderstand "cure" as literal and delay seeking proper care — high risk for this group specifically.
- **Budget-conscious user:** Ice rollers are marketed as a low-cost "fix," which could exploit budget-conscious users seeking cheap alternatives to professional care.
- **Sensitive skin user:** Ice application can be irritating for some sensitive or reactive skin; not addressed in original trend evidence.
- **User from different cultural background:** No demographic information supplied about the trend's audience — cannot assess representation either way.
- **User with minimal routine:** May be drawn to this as a "quick fix" appealing to low-effort routines, increasing risk of misplaced reliance instead of appropriate care.
- **Assumptions found:** The trend assumes a single anecdote generalises to all cystic acne cases; assumes a cosmetic tool can address an inflammatory medical condition — both are unsafe assumptions that any Hauly content must actively reject, not repeat.

### 6. Editorial and Safety Risks
- **High medical/safety risk:** Cystic acne is a dermatological condition; suggesting or even ambiguously referencing a "cure" via cosmetic tools risks real harm (delayed proper treatment) and reputational/misinformation liability for Hauly.
- **Misinformation risk:** Directly repeating or lending visibility to the "cured overnight" framing — even to critique it — could inadvertently amplify the claim if not handled very carefully.
- **Exaggerated-claim risk:** High engagement/trending audio may pressure inclusion for reach, which conflicts with Hauly's stated non-promotional, educational purpose.

### 7. Status
**Not suitable for Gazette development** — the core claim is a medical overreach with no supporting evidence; the trend as presented conflicts with Hauly's educational, non-medical-claim purpose. If the founder wants to address it, it should only be as a clearly labelled myth-correction piece emphasising professional care, developed with dermatological input — not as trend-led "content."

---

## Summary for Founder Decision

| Trend | Relevance Score | Status |
|---|---|---|
| Slugging | 4/5 | Suitable for founder review |
| Ice rolling "cure" claim | 1/5 | Not suitable for Gazette development |

**Note:** Neither recommendation should be published without founder approval. The ice rolling trend in particular should not proceed without explicit founder sign-off given its medical-claim risk profile.
~~~

### V3 (final)

**Prompt text (as tested)**

~~~text
Role: You are Hauly's beauty editorial strategist.
Action: Analyse the supplied social media trends, decide which are relevant to Hauly's audience and Gazette, and produce a content recommendation — including a check of your own recommendation for bias and exclusion before finishing.
Context: Hauly is an app for organising a makeup and skincare collection. The Gazette is Hauly's in-app editorial section (inside Learn, in the Studio tab) with practical beauty and skincare education, not product selling. Use only the supplied information as evidence; do not invent engagement figures, sources, audience reactions, or popularity. Consider whether each trend supports Hauly's educational purpose, could become a lasting (evergreen) article, and whether it creates medical, safety, misinformation or exaggerated-claim risk. Use inclusive language and do not assume one skin tone, gender, age, skin type, budget, or routine represents all Hauly users; do not describe a trend as suitable for everyone. Do not add background facts that are not in the supplied information (for example how to do a technique, which products it uses, who it suits, or its history). If background knowledge would help, write it as a question in a "Questions to research" list inside section (2) instead of stating it as fact. Supplied trends: "1. Platform: TikTok. Caption: 'POV: my skin after slugging every night for a month ✨'. Trend: slugging (layering a thick occlusive moisturiser at night), shown mostly on fair/light-skin creators. Date: Aug 2026. Engagement: 2.1M views on top video. 2. Platform: TikTok. Caption: 'Ice rolling literally cured my cystic acne overnight!!'. Trend: ice roller videos claiming an overnight cure for cystic acne. Date: Aug 2026. Engagement: 4.8M views, trending audio."
Expected output: For each trend, seven sections: (1) Trend overview — what the evidence shows, and whether it looks established, emerging, or unclear (use "unclear" when the evidence is thin); (2) Evidence limitations — what's missing, and any claims that shouldn't be treated as proven; (3) Relevance to Hauly — with a 1–5 score; (4) Content recommendation — working title, angle, target reader, three key learning points, format, and evergreen / seasonal / trend-led; (5) Bias and inclusion review — test the recommendation against a beginner, a budget-conscious user, a user with sensitive skin, a user from a different cultural background, and a user with a minimal routine, and name any assumptions found; (6) Editorial and safety risks; (7) Status — one of "suitable for founder review", "needs more evidence", or "not suitable for Gazette development". This output must be reviewed and approved by the founder before anything is published.
~~~

**Recorded response**

~~~text
# Hauly Gazette — Trend Analysis & Content Recommendation

**Prepared for:** Founder review
**Date:** 2026-09-15
**Scope:** Two supplied TikTok trends assessed for Gazette suitability

---

## Trend 1: Slugging

### (1) Trend overview
The evidence shows a single TikTok video captioned "POV: my skin after slugging every night for a month ✨," referencing the practice of layering a thick occlusive moisturiser at night, with 2.1M views on the top video. The supplied context notes it is shown "mostly on fair/light-skin creators." One video with a high view count is not enough to establish how widespread, sustained, or representative this trend is across creators or audiences. Status: **unclear** — the term "slugging" itself has enough general recognisability that it may be an established practice, but the evidence supplied only supports one data point, not an established trend.

### (2) Evidence limitations
- Only one video/engagement figure is supplied; no data on how many creators, how long the trend has run, or whether it's growing or fading.
- No demographic or skin-type breakdown beyond "mostly fair/light-skin creators" — this is a noted gap, not a confirmed audience.
- No information on what product(s) were used, in what climate, or over what baseline skin condition.
- The caption is a personal anecdote ("my skin after...") — this is a testimonial, not evidence of a general effect. It should not be treated as proof that the practice produces the shown result for all skin types or tones.
- Nothing in the supplied material confirms suitability for oily, acne-prone, or sensitive skin.

**Questions to research (not stated as fact here):**
- What does an occlusive/"slugging" practice technically involve, and what ingredient types are typically used?
- Is there guidance on which skin types or climates this may or may not suit?
- Are there known risks (e.g., for acne-prone or very oily skin)?
- Is there a history or origin of the term worth referencing editorially?

### (3) Relevance to Hauly — Score: 4/5
Fits Hauly's collection-organising purpose (relevant to nighttime routine layering/product use) and the Gazette's educational, non-selling remit. Scored 4 rather than 5 because the evidence base is thin (one video) and the visible creator demographic is narrow, so more supporting evidence and a broadened lens would strengthen the case before treating it as a confirmed audience interest.

### (4) Content recommendation
- **Working title:** "What Is Slugging? An Explainer, Not an Endorsement" (placeholder — to be refined pending research answers above)
- **Angle:** Educational explainer that presents slugging as one nighttime practice among several, framed with open questions rather than universal claims, until research questions are answered.
- **Target reader:** Hauly users curious about nighttime routine layering — explicitly not narrowed to one skin type or tone.
- **Three key learning points** (draft, pending research):
  1. What the practice involves at a basic descriptive level (pending research answers).
  2. Open questions about which skin types/conditions it may or may not suit (flag as unresolved, not answered, until researched).
  3. That one video's result is a personal anecdote, not proof of a universal outcome.
- **Format:** Short explainer article with an "unanswered questions" callout box.
- **Evergreen / seasonal / trend-led:** Potentially evergreen if researched properly (nighttime skincare layering is a recurring topic), but currently trend-led given the single-source evidence.

### (5) Bias and inclusion review
- **Beginner:** Risk — a beginner reader may assume this is a universally recommended step rather than one optional practice. Recommendation must state clearly it is not a required routine step.
- **Budget-conscious user:** Risk — nothing in the supplied evidence addresses cost; the article must avoid implying a specific product tier is needed.
- **Sensitive skin user:** Risk — the supplied evidence gives no information on sensitive-skin suitability; must not imply safety or unsuitability without evidence — flagged as a research question, not stated.
- **User from a different cultural background:** Risk identified — the visible creators are described as "mostly fair/light-skin," so the article must not visually or descriptively centre one skin tone as representative, and any imagery/example language should be reviewed for this.
- **User with a minimal routine:** Risk — framing slugging as "the" nighttime finishing step could pressure a minimal-routine user to add a step; the copy must frame it as optional.
- **Assumptions found:** Original trend evidence assumes fair/light skin as visual default; draft must actively counter this rather than replicate it.

### (6) Editorial and safety risks
- Low medical risk (occlusive moisturising is a routine cosmetic practice), but the article must not imply it treats or "cures" any skin condition, since no such claim is supplied or verified.
- Risk of over-generalising a single testimonial as proven outcome — must be worded as anecdote, not evidence.
- Representation risk: if published with imagery matching only the fair/light-skin creators shown in the trend, this would replicate the bias identified above.

### (7) Status: **Needs more evidence**
Rationale: Single video is insufficient to confirm trend establishment; demographic narrowness and unanswered technical/suitability questions must be resolved via research before drafting proceeds.

---

## Trend 2: Ice Rolling for Cystic Acne

### (1) Trend overview
The evidence shows a TikTok caption claiming "Ice rolling literally cured my cystic acne overnight!!" with 4.8M views on the top video and a trending audio track. The high view count and trending audio suggest wide reach, but reach alone does not confirm the claim is accurate — it confirms only that the content is circulating widely. Status: **unclear/high-risk** — engagement is high, but the core claim is medically unverified within the supplied evidence.

### (2) Evidence limitations
- No clinical, dermatological, or scientific source is supplied to support "cured...overnight" — this is an unverified personal claim in a caption.
- "Trending audio" indicates the video's sound is popular, which does not corroborate the claim itself, only its distribution.
- No information on what "cystic acne" case was involved, severity, prior treatment, or whether the outcome was durable.
- No supplied evidence distinguishes short-term cosmetic effects (e.g., temporary reduction in swelling/redness) from an actual "cure."

**Questions to research (not stated as fact here):**
- Is there any established dermatological view on ice application and inflammation/swelling generally?
- Is "cured overnight" a claim that any credible source substantiates, or does existing knowledge suggest temporary cosmetic effects only?
- Are there safety concerns with ice application on skin (e.g., frostbite, nerve sensitivity) that should be flagged?
- Should this topic mention when to seek professional/dermatological care for cystic acne specifically?

### (3) Relevance to Hauly — Score: 2/5
The topic touches skincare, which is within Hauly's general domain, but the specific claim ("cured overnight") is a medical-adjacent, exaggerated claim not suited to Hauly's non-medical, educational, non-selling editorial remit. Score reflects that the *topic area* (acne, cooling techniques) may have relevance, but the *trend as evidenced* (unverified cure claim) is not directly usable as the basis for content without substantial reframing and outside verification beyond what's supplied.

### (4) Content recommendation
- **Working title:** "Does Ice Rolling Really 'Cure' Cystic Acne? Separating Trend from Evidence" — **only if founder/legal approves addressing viral misinformation directly; otherwise recommend non-development.**
- **Angle:** If pursued, angle must be a myth-examination/critical-literacy piece — explicitly not an endorsement or how-to — clarifying that Hauly is not making or confirming the claim, and directing readers to the unanswered research questions above and to professional consultation for cystic acne specifically.
- **Target reader:** Users who may have seen this viral claim and want a grounded, non-alarmist perspective — not narrowed by skin type, age, or severity of acne.
- **Three key learning points** (draft, contingent on research/legal sign-off):
  1. High view counts and trending audio reflect reach, not proof of a medical claim.
  2. "Cured overnight" is not substantiated by the supplied evidence and should not be treated as fact.
  3. Cystic acne is a condition where professional guidance may be relevant — framed as a suggestion to seek that guidance, not as medical advice from Hauly.
- **Format:** Short "myth-check" style explainer, clearly labelled as commentary on a viral claim rather than a tutorial.
- **Evergreen / seasonal / trend-led:** Trend-led (reactive to this specific viral claim); not recommended as evergreen content given the unverified medical claim at its core.

### (5) Bias and inclusion review
- **Beginner:** Risk — a beginner could take the viral claim at face value; a myth-check format must be careful not to accidentally reinforce the claim through repetition without sufficient framing.
- **Budget-conscious user:** Lower relevance here since no product/cost claim is involved, but the article must not imply ice rolling is a "free alternative" to professional care without evidence.
- **Sensitive skin user:** Significant risk — no supplied evidence addresses whether ice application is safe for sensitive or reactive skin; must not state or imply safety.
- **User from a different cultural background:** No demographic data supplied for this trend, so no specific bias identified from the evidence itself, but the piece should still avoid assuming one presentation of "cystic acne" (severity, skin tone visibility of acne) represents all users.
- **User with a minimal routine:** Risk — framing acne "cures" could pressure minimal-routine users toward unverified interventions; must be avoided.
- **Assumptions found:** The original trend assumes a single anecdote generalises to all cystic acne cases — this assumption must be explicitly dismantled, not repeated, in any Hauly content.

### (6) Editorial and safety risks
- **High risk:** "Cured overnight" is an exaggerated, medically unverified claim; repeating or lending it credibility (even to debunk) carries misinformation risk if not framed very carefully.
- **Safety risk:** Ice application to skin can carry physical risks (e.g., skin damage) — not confirmed in supplied evidence, but flagged as a research/safety question that would need expert input before publication.
- **Reputational risk:** Given Hauly's stated non-medical, non-selling educational purpose, directly engaging with an "overnight cure" claim — even critically — requires careful legal/founder sign-off to avoid appearing to validate or amplify the claim.
- Recommend this topic not proceed without dermatological or medical-safety consultation beyond the supplied evidence.

### (7) Status: **Not suitable for Gazette development** (at this time)
Rationale: The core claim is an unverified, exaggerated medical-adjacent statement with a single-source anecdotal basis. High engagement reflects distribution, not credibility. Proceeding — even in a myth-checking format — would require external medical/safety verification not available in the supplied evidence, plus explicit founder and legal review given the medical-claim sensitivity.

---

## Summary for Founder Decision

| Trend | Status | Key blocker |
|---|---|---|
| Slugging | Needs more evidence | Single video source; narrow visible demographic; unanswered suitability questions |
| Ice rolling for cystic acne | Not suitable for Gazette development | Unverified "cure" claim; medical/safety risk; no supporting evidence beyond one anecdote |

**Next step recommended:** Founder to advise whether research questions (listed under each trend) should be commissioned before either topic proceeds to drafting, and whether the ice-rolling myth-check angle should be pursued at all given its risk profile.
~~~

## Prompt Lab check (GPT-4.1 mini)

To check the results weren't specific to one AI model, the first and final versions were re-run in La Trobe Prompt Lab using GPT-4.1 mini, with exactly the same prompt text. Prompt Lab's prompt review scores the prompt itself out of 100.

**What GPT-4.1 mini did — noticeably different from Claude Sonnet 5:**

| Check | Claude Sonnet 5 (V2 / V3) | GPT-4.1 mini V2 | GPT-4.1 mini V3 |
| --- | --- | --- | --- |
| Slugging classification | Established technique, narrow snapshot / "Unclear" | "Emerging" | "Established" |
| Ice-rolling status | "Not suitable for Gazette development" (both) | "Suitable for founder review" | "Suitable for founder review" |
| Outside facts | Several / a few | Many, e.g. "no credible scientific evidence", "may temporarily reduce redness or inflammation", "cold compresses"; recommended "dermatologist quotes" that don't exist | Many, e.g. the overnight cure is "medically unlikely", cystic acne "requires professional treatment"; recommended "expert quotes" |
| Questions to research | — / inside section (2) | Not asked for in V2 | Listed once at the very end |

- **Prompt Lab review:** V2 scored 91.5/100 and V3 scored 90.5/100 — both high, and almost the same — even though both outputs broke the prompt's own rules (for example, using "emerging" or "established" when only one video was supplied).

**What this adds:** a high review score does not guarantee a well-behaved output, and the same prompt behaved differently on two models. On GPT-4.1 mini, the V3 "no outside facts" rule made no clear difference. The output itself, not just the prompt, has to be checked by a person.

### Prompt Lab — V2

**Recorded response (GPT-4.1 mini)**

~~~text
Trend 1: Slugging on TikTok

(1) Trend overview  
Slugging involves applying a thick occlusive moisturizer at night to lock in hydration. The trend is currently emerging, as shown by 2.1M views on a top TikTok video from August 2026. The content mainly features fair/light-skinned creators, suggesting some demographic concentration but not necessarily exclusivity.

(2) Evidence limitations  
The evidence is primarily anecdotal and visual, without scientific backing or clinical studies. The trend’s benefits are implied rather than objectively measured. There is no information about long-term effects or suitability for all skin types. Claims about slugging’s effectiveness should not be treated as universally proven.

(3) Relevance to Hauly: 4/5  
Slugging relates directly to skincare routine organization and education. It can support teaching about moisturizing techniques, occlusive products, and skin barrier care. However, since it may not suit all skin types or climates, caution is advised.

(4) Content recommendation  
- Working title: “Slugging 101: What It Is, Who It’s For, and How to Do It Safely”  
- Angle: Educational deep-dive into the slugging trend focusing on moisturizing science, skin barrier health, and suitability considerations.  
- Target reader: Skincare enthusiasts curious about hydrating techniques, including beginners and those expanding routines.  
- Three key learning points:  
  1. What slugging is and how occlusive moisturizers work  
  2. Skin types and conditions that may benefit or may want to avoid slugging  
  3. How to incorporate slugging safely into a skincare routine without over-moisturizing or causing breakouts  
- Format: Illustrated article with dermatologist quotes, product types explained, and step-by-step application guide  
- Evergreen / seasonal / trend-led: Evergreen with a trend-led hook

(5) Bias and inclusion review  
- Beginner: Clear explanations, avoids jargon, includes step-by-step guidance  
- Budget-conscious: Highlights accessible occlusive moisturizers and DIY alternatives without promoting specific products  
- Sensitive skin: Advises patch testing and consulting a dermatologist before trying occlusive layering  
- Cultural background: Avoids skin tone assumptions; acknowledges that slugging may feel different in various climates and cultural skincare traditions  
- Minimal routine: Suggests slugging as optional and adaptable, not mandatory  
- Assumptions found: The trend’s visual emphasis on fair/light skin creators may unconsciously bias perceived suitability; the recommendation actively counters this by emphasizing inclusivity and skin type variation.

(6) Editorial and safety risks  
- Risk of promoting overuse of heavy moisturizers causing clogged pores or irritation if readers do not adapt to their skin’s needs  
- No exaggerated claims; content carefully avoids promising universal benefits  
- Encourages dermatologist consultation and patch testing to mitigate safety risks

(7) Status  
Suitable for founder review

---

Trend 2: Ice rolling claiming overnight cure for cystic acne

(1) Trend overview  
Ice rolling videos with captions claiming an overnight cure for cystic acne are trending on TikTok with 4.8M views in August 2026. The trend is emerging but lacks scientific validation.

(2) Evidence limitations  
There is no credible scientific evidence supporting ice rolling as a cure for cystic acne, especially not overnight. The claim is anecdotal and potentially misleading. Information about risks, skin types, and proper usage is absent.

(3) Relevance to Hauly: 2/5  
While relating to skincare tools, the exaggerated claim risks misinformation. Hauly’s educational mandate advises caution in promoting claims that could mislead users or delay professional treatment.

(4) Content recommendation  
- Working title: “Ice Rolling and Acne: What Science Says About This Trend”  
- Angle: Educational myth-busting article explaining what ice rolling is, its potential benefits and limitations, and why it’s not a cure for cystic acne  
- Target reader: Users interested in skincare tools and acne management seeking reliable information  
- Three key learning points:  
  1. What ice rolling is and how it may temporarily reduce redness or inflammation  
  2. Why cystic acne requires professional care and cannot be cured overnight by topical tools  
  3. Safe ways to integrate cooling techniques without risking skin damage or delaying treatment  
- Format: Q&A style article with expert input and warnings against misleading claims  
- Evergreen / seasonal / trend-led: Trend-led with evergreen educational value

(5) Bias and inclusion review  
- Beginner: Uses simple language and explains medical terms  
- Budget-conscious: Does not promote expensive tools; focuses on accessible alternatives like cold compresses  
- Sensitive skin: Highlights potential risks of ice rolling on sensitive or damaged skin  
- Cultural background: Avoids assumptions about skin types or acne causes; includes diverse examples  
- Minimal routine: Encourages focusing on core acne treatments rather than trendy tools  
- Assumptions found: None significant; the article counters hype rather than endorsing it.

(6) Editorial and safety risks  
- High risk of spreading misinformation if the claim is repeated uncritically  
- Important to clearly state that ice rolling is not a substitute for dermatological care  
- Avoids exaggerated claims; prioritizes safety and evidence-based advice

(7) Status  
Suitable for founder review
~~~

**Prompt Lab review:** overall score 91.5/100

~~~text
Rubric Scores
* Clarity: 90/100 - The prompt is mostly clear with detailed instructions and expected output format, but some sentences are long and complex, which could be simplified for easier comprehension.
* Constraints: 95/100 - The prompt strongly constrains the assistant to use only supplied information, avoid inventing data, and focus on specific risks and inclusivity, which is excellent.
* Structure: 90/100 - The prompt provides a well-organized, stepwise output structure, but the dense paragraph format could be improved with clearer bulleting or numbering for readability.
* Verifiability: 90/100 - The prompt emphasizes using only supplied data and avoiding invented claims, supporting verifiability, though it could explicitly require citing supplied data points in the output.
* Hallucination Risk: 95/100 - The prompt explicitly forbids inventing engagement figures or audience reactions and requires bias and safety checks, minimizing hallucination risk effectively.
Overall score: 91.5/100
Top Improvements
* Simplify and break down complex sentences to improve clarity and ease of understanding.
* Use bullet points or numbered lists in the prompt to better highlight the expected output sections and instructions.
* Explicitly instruct the assistant to reference or quote supplied data points in the output to further enhance verifiability.
(Suggested rewrite: same content as the prompt, reformatted into bullet points and numbered sections.)
~~~

### Prompt Lab — V3 (final)

**Recorded response (GPT-4.1 mini)**

~~~text
**Trend 1: Slugging (TikTok, Aug 2026)**

(1) **Trend overview**  
Slugging involves layering a thick occlusive moisturizer at night. The trend appears established on TikTok with 2.1M views on the top video, mainly demonstrated by fair/light-skin creators. It is presented as a nighttime skincare step.

(2) **Evidence limitations**  
The claim that slugging benefits skin after consistent use is anecdotal. The trend shows limited diversity in skin tones and types, mainly fair/light skin. There is no clinical evidence provided for its efficacy or safety across all skin types. The thick occlusive layer might not suit everyone and could potentially cause issues for some skin types or climates. No long-term effects or risks are discussed.

(3) **Relevance to Hauly**  
Score: 3  
Slugging is relevant because it involves a skincare routine step that users might want to track or learn about. However, the lack of diverse representation and potential limitations for certain skin types reduce its universal appeal. It aligns with Hauly’s educational focus if presented with nuance.

(4) **Content recommendation**  
- Working title: “Is Slugging Right for Your Nighttime Skincare Routine? What You Need to Know”  
- Angle: An educational overview of slugging, explaining the concept, potential benefits, and considerations for different skin types and climates, emphasizing critical evaluation of trends.  
- Target reader: Hauly users curious about new skincare techniques and looking to understand if slugging fits their routine.  
- Three key learning points:  
  1. What slugging is and how it fits into a skincare routine.  
  2. Which skin types or conditions might benefit or be cautious with slugging.  
  3. Importance of patch testing and monitoring skin response.  
- Format: Article with expert quotes and user experience snapshots.  
- Evergreen / seasonal / trend-led: Evergreen with trend-led origins.

(5) **Bias and inclusion review**  
- Beginner: Content explains terms simply without assuming prior knowledge.  
- Budget-conscious: Does not assume access to high-end products; emphasizes adapting with available moisturizers.  
- Sensitive skin: Explicit discussion of potential risks or unsuitability included.  
- Different cultural backgrounds: Avoids assumptions about skin types or climates; acknowledges variation.  
- Minimal routine: Suggests slugging as optional, not mandatory, respecting minimal routines.  
- Assumptions found: The trend’s visual dominance by fair/light skin creators could bias readers into thinking it suits all skin tones equally; the article mitigates this with inclusive language.

(6) **Editorial and safety risks**  
- Risk of endorsing slugging as universally beneficial mitigated by balanced presentation.  
- No exaggerated claims or medical advice given.  
- Encourages caution and consultation with skincare professionals.  
- No product endorsements, so minimal commercial bias.

(7) **Status**  
Suitable for founder review.

---

**Trend 2: Ice Rolling Claims (TikTok, Aug 2026)**

(1) **Trend overview**  
Ice rolling videos claim an overnight cure for cystic acne, trending with 4.8M views on TikTok. The trend presents ice rolling as a quick fix for severe acne.

(2) **Evidence limitations**  
The claim of an “overnight cure” is unsubstantiated and medically unlikely. No clinical evidence supports ice rolling as a cure for cystic acne. Potential risks or side effects are unaddressed. The trend risks misleading users about the seriousness and treatment timelines of cystic acne.

(3) **Relevance to Hauly**  
Score: 1  
Due to exaggerated claims and medical misinformation risk, this trend is poorly aligned with Hauly’s educational goals. While skincare routines are relevant, promoting unproven cures contradicts Hauly’s responsible education mission.

(4) **Content recommendation**  
- Working title: “Ice Rolling and Acne: Separating Fact from Fiction”  
- Angle: Debunking the myth of ice rolling as an overnight cystic acne cure; educating about realistic acne management and the limits of topical tools.  
- Target reader: Users encountering acne trends online and seeking trustworthy information.  
- Three key learning points:  
  1. What ice rolling is and what it can and cannot do for skin.  
  2. Why cystic acne requires professional treatment and realistic expectations.  
  3. How to critically evaluate viral skincare claims.  
- Format: Fact-check article with expert commentary and myth-busting section.  
- Evergreen / seasonal / trend-led: Trend-led with evergreen educational value.

(5) **Bias and inclusion review**  
- Beginner: Uses clear language, explaining terms and medical context.  
- Budget-conscious: Does not assume expensive treatments but emphasizes professional advice.  
- Sensitive skin: Highlights that cystic acne is serious and requires care, not quick fixes.  
- Different cultural backgrounds: Avoids assumptions about access to care but stresses importance of professional consultation.  
- Minimal routine: Acknowledges some users may not have complex routines but warns against relying on unproven quick fixes.  
- Assumptions found: Assumes access to healthcare or dermatology services, which may not be universal; this is stated carefully as a recommendation rather than a requirement.

(6) **Editorial and safety risks**  
- High risk of misinformation if content is not clear about limits of ice rolling.  
- Must avoid implying ice rolling replaces medical treatment.  
- Risks of users delaying proper care if misled must be explicitly addressed.  
- No product promotion to avoid commercial bias.

(7) **Status**  
Suitable for founder review.


---

**Summary:**  
Both trends offer educational opportunities aligned with Hauly’s editorial mission if approached critically and inclusively. Slugging can be presented as an optional technique with caveats, while ice rolling requires myth-busting to prevent misinformation. Both require founder review before publishing.  

**Questions to research:**  
- What clinical evidence exists about occlusive moisturizers’ effects for different skin types?  
- Are there dermatological guidelines on slugging or thick occlusive layering?  
- What are the medically recommended treatments for cystic acne, and what is the role of home tools like ice rollers?  
- How do different skin tones and types respond to slugging and ice rolling respectively?
~~~

**Prompt Lab review:** overall score 90.5/100

~~~text
Rubric Scores
Clarity: 90/100 - The prompt is detailed and mostly clear, but the dense instructions and multiple nested requirements could be streamlined for easier comprehension.
Constraints: 95/100 - The prompt strongly constrains the assistant to use only supplied information, avoid inventing data, and avoid background facts, which is excellent.
Structure: 85/100 - The prompt specifies a clear multi-section output format, but the complexity and length of instructions could be better organized or broken down for clarity.
Verifiability: 90/100 - The prompt emphasizes using only supplied information and flags unsupported claims, supporting verifiability well.
Hallucination Risk: 95/100 - The prompt explicitly forbids inventing engagement figures, sources, or background facts, minimizing hallucination risk effectively.
Overall Score
Overall score: 90.5/100

Top Improvements
Simplify and break down instructions into numbered or bullet points to improve readability and reduce cognitive load.
Clarify the expected output format upfront with a concise template or example to guide the assistant.
Explicitly highlight the importance of neutrality and inclusivity earlier in the prompt to reinforce these constraints.
Suggested Rewrite
Role: You are Hauly's beauty editorial strategist.

Context: Hauly is an app for organizing makeup and skincare collections. The Gazette is Hauly’s in-app editorial section focused on practical beauty and skincare education, not product selling.

Task: Analyze the supplied social media trends and decide which are relevant to Hauly’s audience and the Gazette. For each trend, produce a content recommendation that:

Uses only the supplied information; do not invent engagement figures, sources, audience reactions, or background facts.
Considers whether the trend supports Hauly’s educational purpose, could become a lasting (evergreen) article, and whether it poses medical, safety, misinformation, or exaggerated-claim risks.
Uses inclusive language and avoids assuming one skin tone, gender, age, skin type, budget, or routine represents all Hauly users.
Does not describe a trend as suitable for everyone.
If background knowledge would help, list it as a question in a "Questions to research" section instead of stating it as fact.
For each trend, provide seven sections:

Trend overview — summarize the evidence and classify the trend as established, emerging, or unclear.
Evidence limitations — identify missing information and unproven claims.
Relevance to Hauly — score from 1 to 5.
Content recommendation — include working title, angle, target reader, three key learning points, format, and whether it is evergreen, seasonal, or trend-led.
Bias and inclusion review — test the recommendation against a beginner, budget-conscious user, sensitive skin user, different cultural backgrounds, and minimal routine user; name any assumptions found.
Editorial and safety risks — identify any risks or concerns.
Status — choose one: "suitable for founder review," "needs more evidence," or "not suitable for Gazette development."
The output must be reviewed and approved by the founder before publishing.

Supplied trends:

TikTok, Aug 2026: "POV: my skin after slugging every night for a month ✨" — slugging (layering a thick occlusive moisturizer at night), mostly shown by fair/light-skin creators, 2.1M views on top video.
TikTok, Aug 2026: "Ice rolling literally cured my cystic acne overnight!!" — ice roller videos claiming an overnight cure for cystic acne, 4.8M views, trending audio.
~~~
