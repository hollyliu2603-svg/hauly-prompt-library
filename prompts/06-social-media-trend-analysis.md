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
