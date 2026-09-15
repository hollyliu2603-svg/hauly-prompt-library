# Appendix — Test Outputs

These are the full outputs (unchanged apart from removing code-formatting marks) from testing each prompt version once on the same sample input. The sample inputs were written for testing and are based on real Hauly features; they are not real user messages. Tests were run in September 2026 using Claude Sonnet 5, with no other instructions added.

## Prompt 1
### Support Ticket Triage

**Sample input:**

> Hi, I got charged twice for Hauly Plus this month and now my Restock tab won't load at all. Also, could you add a way to track how much I spend on products?

#### v1 output

<details><summary>Show output</summary>

```text
Here's the message sorted into distinct categories:

## 1. Billing Issue 💳
**Type:** Duplicate charge / Refund request
- Charged twice for "Hauly Plus" subscription this month
- **Priority:** High (financial/urgent)
- **Action needed:** Verify transaction history, process refund for duplicate charge

## 2. Bug Report 🐛
**Type:** Technical issue / App functionality
- "Restock" tab fails to load entirely
- **Priority:** High (blocking feature use)
- **Action needed:** Investigate load failure — possibly linked to account/billing issue above, or a separate technical bug

## 3. Feature Request 💡
**Type:** Product enhancement
- Requesting a spending tracker for products purchased
- **Priority:** Low/Medium (not urgent, no functionality broken)
- **Action needed:** Log for product team review; not time-sensitive

---

**Note:** Issues #1 and #2 might be related — sometimes a billing conflict (e.g., duplicate charge causing account flag) can cause premium features like "Restock" to malfunction. Worth checking if resolving the refund also fixes the tab loading issue.

Want me to draft a support response, or reformat this into a ticket/table for tracking?
```

</details>

#### v2 output

<details><summary>Show output</summary>

```text
{"category": "bug", "urgency": "high", "affected_tab": "Restock", "one_line_summary": "Double-charged for Hauly Plus; Restock tab not loading; also requests spending tracker feature."}
```

</details>

#### v3 output

<details><summary>Show output</summary>

```text
{"issues": [{"category": "account", "urgency": "high", "affected_tab": "Account", "one_line_summary": "User charged twice for Hauly Plus subscription this month"}, {"category": "bug", "urgency": "high", "affected_tab": "Restock", "one_line_summary": "Restock tab fails to load entirely"}, {"category": "feature_request", "urgency": "low", "affected_tab": "Unknown", "one_line_summary": "Add feature to track spending on products"}], "needs_human_review": true, "review_reason": "Multiple issues reported and message involves a payment/billing problem (double charge)"}
```

</details>

## Prompt 2
### Customer Support Reply Drafting

**Sample input:**

> The app keeps crashing when I try to add a new product to my Haul. This is so annoying, I've lost half my collection I already typed in!

#### v1 output

<details><summary>Show output</summary>

```text
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
```

</details>

#### v2 output

<details><summary>Show output</summary>

```text
Hi there — I'm so sorry, that crash-losing-your-collection combo sounds genuinely frustrating, especially after all that typing.

Our team is digging into the crash on "add product" right now. As a workaround, try adding items one at a time and closing the app fully between each — it seems to help prevent the crash until we get a fix out.

Hang in there, we'll get this sorted for you.

— Holly
```

</details>

#### v3 output

<details><summary>Show output</summary>

```text
Hi there,

Thank you for reporting this — that sounds really frustrating, especially losing the work you'd already put into your Haul.

I'm looking into what's causing the crash right now. Could you tell me your phone model and the app version you're using? That'll help me track down what's going on.

Thanks for your patience with me on this — I'll get it sorted.

Holly
```

</details>

## Prompt 3
### Collection Ingredient Report

**Sample input:**

> 1. Night serum — Aqua, Glycerin, Retinol, Tocopherol.
> 2. Exfoliating toner — Aqua, Glycolic Acid, Niacinamide.
> 3. Morning serum — Aqua, Ascorbic Acid, Niacinamide, Ferulic Acid.
> 4. Spot gel — Aqua, Benzoyl Peroxide, Carbomer.
> 5. Face oil — Squalane, Bakuchiol, "Botanical Complex X".

#### v1 output

<details><summary>Show output</summary>

```text
Here's a breakdown of the ingredients that clash (or are risky to layer) across these five products:

## ⚠️ Combinations to avoid

**1. Retinol (Night serum) + Glycolic Acid (Exfoliating toner)**
Both increase cell turnover and sensitize skin. Using them together (or even in the same routine) significantly raises the risk of redness, peeling, and a compromised moisture barrier. → **Alternate nights** instead of layering.

**2. Retinol (Night serum) + Benzoyl Peroxide (Spot gel)**
Benzoyl peroxide can oxidize and destabilize retinol, reducing its effectiveness, and the combo is very drying/irritating. → Use at **different times of day** (e.g., BP in AM as a spot treatment, retinol at night elsewhere on the face), or alternate nights.

**3. Ascorbic Acid/Vitamin C (Morning serum) + Benzoyl Peroxide (Spot gel)**
Benzoyl peroxide can oxidize vitamin C, degrading it before it has a chance to work. → Keep spot gel application away from vitamin C application (different times or spot-only application after the vitamin C has absorbed).

**4. Glycolic Acid (Toner) + Benzoyl Peroxide (Spot gel)**
Both are drying/irritating; combining them can overwhelm the skin barrier. → Avoid using on the same day if possible, especially over the same areas.

## ✅ Generally fine as designed

- **Vitamin C + Ferulic Acid + Niacinamide (Morning serum)** — this is a well-known, stable antioxidant combo. Ferulic acid actually stabilizes vitamin C. No concern here.
- **Retinol + Tocopherol (Vitamin E) in Night serum** — Vitamin E helps stabilize retinol; this is a beneficial pairing.
- **Niacinamide (Toner) + Vitamin C (Morning serum)** — the old "niacinamide deactivates vitamin C" myth has largely been debunked by modern formulations; using them at different times of day (as here) avoids any residual concern anyway.
- **Bakuchiol (Face oil)** is a gentler retinol-alternative — it can typically be layered with actives, but combining it with actual Retinol (Night serum) on the same night is somewhat redundant and could increase irritation without added benefit.

## 🔍 One caveat
"**Botanical Complex X**" in the Face oil is a vague/proprietary blend — I can't assess how it interacts with the other actives since the actual ingredients aren't disclosed. I'd recommend checking the manufacturer's full ingredient list or doing a patch test before combining it with exfoliants or retinol.

## Suggested simple routine
- **AM:** Morning serum (Vit C/Niacinamide/Ferulic) → Face oil (Bakuchiol) → SPF
- **PM (Night A):** Night serum (Retinol)
- **PM (Night B, alternate):** Exfoliating toner (Glycolic Acid)
- **Spot gel (Benzoyl Peroxide):** Apply only to blemishes, ideally at a different time than retinol/vitamin C application, or on non-retinol nights.
```

</details>

#### v2 output

<details><summary>Show output</summary>

```text
# Hauly Collection Report

## 1. Pairing Cautions

**Night serum** (Retinol) + **Exfoliating toner** (Glycolic Acid)
Matching category: Retinoid + AHA
These can be harsh together — introduce them gradually or on alternate days.

**Night serum** (Retinol) + **Morning serum** (Ascorbic Acid)
Matching category: Retinoid + Vitamin C
These can be harsh together — introduce them gradually or on alternate days.

**Spot gel** (Benzoyl Peroxide) + **Night serum** (Retinol)
Matching category: Benzoyl Peroxide + Retinoid
These can be harsh together — introduce them gradually or on alternate days.

**Spot gel** (Benzoyl Peroxide) + **Exfoliating toner** (Glycolic Acid)
Matching category: Benzoyl Peroxide + AHA
These can be harsh together — introduce them gradually or on alternate days.

**Spot gel** (Benzoyl Peroxide) + **Morning serum** (Ascorbic Acid)
Matching category: Benzoyl Peroxide + Vitamin C
These can be harsh together — introduce them gradually or on alternate days.

## 2. Repeated Actives

- **Niacinamide** — found in: Exfoliating toner, Morning serum

## 3. Not Checked

- **"Botanical Complex X"** (Face oil) — not recognised

---

This is general information, not medical advice — patch test new products and speak to a pharmacist or dermatologist if you have a skin condition or reaction.
```

</details>

## Prompt 4
### Bug Report Summary

**Sample input:**

> since the last update whenever i use scan ingredients on a product it just shows a spinning wheel forever then goes back to my haul. i have like 200 products in there. iphone

#### v1 output

<details><summary>Show output</summary>

```text
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
```

</details>

#### v2 output

<details><summary>Show output</summary>

```text
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
```

</details>

## Prompt 5
### Feature Request Scoring

**Sample input:**

> Can you show the price of each product and tell me where it's cheapest to restock? That would make Restock so much more useful.

#### v1 output

<details><summary>Show output</summary>

```text
**User Demand: 4/5**
14 requests in a single month for a niche organization app is a strong, concentrated signal that this isn't a fringe want — it's a recurring pain point tied to your most-used feature (Restock).

**Overall Value: 4/5**
It directly deepens the core Restock use case (turning "what do I need" into "what should I buy and where"), which could meaningfully increase engagement and justify premium pricing, though it's an enhancement rather than a new core capability.

**Build Effort: High**
Delivering accurate, up-to-date pricing and "cheapest retailer" comparisons requires either manual data entry (poor UX, high maintenance) or integrating/maintaining multiple retailer APIs or scrapers — a significant and ongoing engineering and data-maintenance burden for an indie team.
```

</details>

#### v2 output

<details><summary>Show output</summary>

```text
# Feature Request Scoring: Price Display + Cheapest Restock Location

**User Demand: 3/5**
14 requests in one month is a meaningful signal for a specific feature, but it's not (yet) an overwhelming groundswell — worth tracking for trend velocity next month.

**Product Principle Fit: 1/5**
🚩 **Direct conflict**: Hauly's core principle is explicitly "organising, not shopping — no prices or shopping features," with the *only* sanctioned exception being free-text prices on Rehome posts visible solely to the author. Showing product prices and price-comparison-for-purchase (cheapest restock location) is essentially a shopping/price-comparison feature — the exact thing the product has deliberately excluded.

**Build Effort: High**
Even setting the principle conflict aside, "cheapest place to restock" would require live retailer price feeds/integrations, ongoing price maintenance, and likely affiliate or scraping infrastructure — a significant scope and maintenance burden for a small team.

---

**Recommendation:** Decline or heavily reframe. This isn't a "not now" — it's a "not this," since it contradicts a stated product principle rather than just being low priority. If the underlying user need is "I want to know when I'm running low and remember where I usually buy this," consider a lighter-touch alternative that stays in "organising" territory — e.g., a free-text "usual restock notes" field per product (similar in spirit to the Rehome price exception) rather than live price comparison. That would address some of the intent without turning Hauly into a shopping/price tool.
```

</details>

## Prompt 6
### Trend Analysis and Gazette Planning

**Sample input:**

> 1. Platform: TikTok. Caption: 'POV: my skin after slugging every night for a month ✨'. Trend: slugging (layering a thick occlusive moisturiser at night), shown mostly on fair/light-skin creators. Date: Aug 2026. Engagement: 2.1M views on top video. 2. Platform: TikTok. Caption: 'Ice rolling literally cured my cystic acne overnight!!'. Trend: ice roller videos claiming an overnight cure for cystic acne. Date: Aug 2026. Engagement: 4.8M views, trending audio.

#### v1 output

<details><summary>Show output</summary>

```text
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
```

</details>

#### v2 output

<details><summary>Show output</summary>

```text
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
```

</details>

#### v3 output

<details><summary>Show output</summary>

```text
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
```

</details>

## Prompt 7
### Circle Community Moderation

**Sample input:**

> Honestly this Calm Barrier cream cleared up my eczema in a week, better than anything my doctor gave me. Jess Kim from my work put me onto it 💚

#### v1 output

<details><summary>Show output</summary>

```text
{"action": "remove", "rule_broken": "no real names or personal details; no medical claims about what a product treats or cures", "reason": "The post names a real person (Jess Kim) and claims the product cleared/cured eczema better than a doctor's treatment, violating both the personal details and medical claims rules."}
```

</details>

#### v2 output

<details><summary>Show output</summary>

```text
{"action": "recommend_remove", "rule_broken": "no medical claims about what a product treats or cures; no real names or personal details", "reason": "The post claims the product cleared eczema (a medical claim) and names a real person (Jess Kim) along with their workplace context, violating two rules regardless of the poster's tone or product type."}
```

</details>

## Prompt 8
### FAQ and Gazette Drafting

**Sample input:**

> (mode left blank) Resolved support thread: A user asked how to move a finished product from their Haul to Restock. Answer given: in Haul, select the product, then tap 'Move to restock'.

#### v1 output

<details><summary>Show output</summary>

```text
# FAQ Draft

**Question:** How do I move a finished product from my Haul to Restock?

**Answer:** Open your Haul, select the product you've finished, then tap "Move to restock." That's it — the item will now appear in your Restock list.

**Related tip:** Make sure you select the product first before looking for the "Move to restock" option — it only appears once an item is selected.

---

*Draft only — pending founder review and approval before publishing.*
```

</details>

#### v2 output

<details><summary>Show output</summary>

```text
needs_clarification
```

</details>

## Prompt 9
### Push Notification and Banner Copy

**Sample input:**

> New in Hauly: scan the ingredients list on any product and get a plain-English Ingredient Report (a Hauly Plus feature).

#### v1 output

<details><summary>Show output</summary>

```text
{"push": "Scan ingredients, get plain English", "banner": "Scan any product's ingredients list and get a plain-English report explaining what's inside. Available with Hauly Plus."}
```

</details>

#### v2 output

<details><summary>Show output</summary>

```text
{"push": "Scan a label for a plain-English report", "banner": "Scan any product's ingredients list and get a plain-English breakdown of what's inside, now available with Hauly Plus."}
```

</details>

## Prompt 10
### Weekly Operations Report

**Sample input:**

> Support: 42 messages this week (bug 18, how_to 12, feature_request 8, account 4). Last week: 30 messages. Bugs: 18 this week; top bug is 'Scan ingredients' spinning then returning to Haul, reported 11 times, severity blocking. Feature requests: price tracking asked for 14 times; more Circle friends on the free plan asked for 6 times.

#### v1 output

<details><summary>Show output</summary>

```text
# Weekly Ops Summary — Week of Sept 15, 2026

## Support
- **Volume:** 42 messages (vs. 30 last week) → **+40%**
- **Breakdown:** Bugs 18, How-to 12, Feature requests 8, Account 4
- **Top issue:** Bug reports are the largest category (43% of all support volume this week)

## Bugs
- **Volume:** 18 reports this week
- **% change vs. last week:** Not calculable — last week's total (30) wasn't broken down by category, so we don't have a bug-only baseline. *(Flag: worth tracking category-level volumes going forward.)*
- **Top issue:** "Scan ingredients" spinning and returning to the Haul screen — reported **11 times**, severity **blocking**. This single bug accounts for ~61% of all bug reports this week.

## Feature Requests
- **Volume (support inbox):** 8 requests logged in support
- **Top asks:** Price tracking (14 mentions), more Circle friends on the free plan (6 mentions)
- **Note:** These two counts (14 + 6 = 20) exceed the support category total (8), suggesting they're aggregated across multiple channels (e.g., Circle, social, support) rather than support tickets alone. Worth confirming the source so requests are compared consistently week over week.

## Circle Moderation, Content Performance, Social Media Trends
- No data provided this week — recommend including these in next week's report for full coverage.

---

## Cross-Section Theme
The **"Scan ingredients" bug** is the clear throughline: it's the top bug (11 reports, blocking severity), it's likely inflating the "how_to" support volume (users trying to figure out if it's them or the app), and it's plausibly connected to the overall 40% jump in support contacts this week.

## Recommended Action for Next Week
**Prioritize an emergency fix for the "Scan ingredients" spinning bug.**

**Reasoning:** It's the single largest driver of this week's support spike, it's rated blocking (core functionality broken), and it likely has downstream effects on how-to questions and user trust. Fixing it should reduce both bug and how_to volume next week, giving a cleaner read on organic demand for feature requests like price tracking and expanded free-plan Circle limits.

*Secondary note: Standardize how feature request mentions are counted (single source vs. aggregated) so week-over-week comparisons are accurate.*
```

</details>

#### v2 output

<details><summary>Show output</summary>

```text
# Hauly – Weekly Operations Summary
**Week of Sept 8–14, 2026** (prepared Sept 15, 2026)

---

## Support
- **Volume:** 42 messages this week vs. 30 last week → **up 40%** (calculated from the two given totals: +12 messages).
- **Breakdown given:** bug 18, how_to 12, feature_request 8, account 4.
- *Observation:* Bug-related messages are the largest category this week (18 of 42, ~43% of all support volume).

## Bugs
- **Volume:** 18 bug reports this week. **No comparison available** — no last week bug-specific total was given (only the overall support total had a prior-week figure).
- **Top issue:** "Scan ingredients" feature spins and returns to Haul.
  - Reported: 11 times
  - Severity: blocking
- *Observation:* This single bug accounts for 11 of the 18 bug reports this week (~61%), making it the dominant driver of bug volume.

## Feature Requests
- **Top requests given:**
  - Price tracking — 14 requests
  - More Circle friends on free plan — 6 requests
- **Volume comparison:** No comparison available — no last week figures were given for feature requests.
- *Observation:* These two requests total 20 mentions, which is higher than the "8" feature_request count logged in the Support breakdown. This is a discrepancy in the raw data (possibly different counting methods or sources) — flagging it rather than guessing the cause.

## Circle Moderation
Not provided this week.

## Content Performance
Not provided this week.

## Social Media Trends
Not provided this week.

---

## Cross-Section Theme
- **"Scan ingredients" / scanning reliability** and **overall support load** are linked: the bug category (18) is the single largest slice of total support volume (42), and one bug ("Scan ingredients") makes up the majority of bug volume. This suggests the support volume spike (+40%) is substantially tied to this one blocking bug — this is an **inference**, not a confirmed causal link, since no root-cause data was given.

---

## Recommended Action for Next Week
**Prioritize a fix for the "Scan ingredients" spinning bug.**

**Reasoning (data-linked):**
- It's the single most-reported bug (11 reports) and carries **blocking** severity — the highest urgency level given.
- Bugs are the top category driving this week's 40% jump in total support volume, and this one issue represents roughly 61% of all bug reports.
- Resolving it is likely to reduce both bug-report volume and overall support load next week — though this expected impact is an assumption, not a guaranteed outcome, since no data confirms causation.
```

</details>
