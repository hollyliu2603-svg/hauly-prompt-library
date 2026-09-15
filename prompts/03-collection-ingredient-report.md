# Prompt 3 — Collection Ingredient Report

**Workflow stage:** Response

## Intended task

Check all the products in a user's collection and report ingredient pairings to be careful with, and active ingredients that appear in more than one product.

## Problem being solved

Hauly's existing Label report (the report shown after scanning a product's ingredients) looks at one product at a time. Users with many products have no way to see pairing cautions across their whole collection, and an unconstrained AI may give safety reassurances Hauly avoids.

## Prompting techniques

Role framing with a "not medical advice" limit; approved data from Hauly's own ingredient database (the pairing list); constraints (no "safe", no diagnosis, mark unknown ingredients); a three-section structured report; a required disclaimer.

## Automation potential

**Medium.** The report is general information, so it could run whenever a user asks. Any change to the pairing list must be checked by Holly first.

## Risks and limitations

- The report is only as accurate as Hauly's pairing list; a wrong list gives confident-sounding wrong results.
- Ingredient names vary, so some matches can be missed — the "not recognised" section makes those gaps visible.
- Skincare information can be mistaken for medical advice, so the disclaimer is required.

## What the versions illustrate

| Version | What changed | What to notice in the response |
| --- | --- | --- |
| V1 | One line: "which ones shouldn't be used together" | Its own list; missed retinol + vitamin C (on Hauly's list); said "No concern here" and "a beneficial pairing"; suggested a routine; no disclaimer |
| V2 (final) | Adds Hauly's pairing list, bans "safe" and diagnosis, requires disclaimer and "not recognised" | Exactly the five pairings matching Hauly's list, niacinamide listed as repeated, "Botanical Complex X" not recognised, disclaimer included |

**Discussion:** Both versions used the same collection. **Where the pairing list comes from:** Hauly's built-in ingredient database marks retinoids with AHAs, BHAs or vitamin C, and benzoyl peroxide with retinoids, AHAs, BHAs or vitamin C, as combinations to introduce carefully; the wording "can be harsh together — introduce them gradually or on alternate days" is the app's own. Giving the AI approved data turned an open health question into a checkable lookup. **Naming note:** the tested prompt text calls the app feature "Ingredient Report"; on the app screen it is titled "Label report". The name is left unchanged in the prompt text so it matches what was tested.

## Final prompt — reusable template (V2)

> **Role:** You are Hauly's collection assistant. You give general skincare information, not medical advice.  
>
> **Action:** Review the user's collection below and report pairing cautions and repeated active ingredients across products.  
>
> **Context:** Hauly's Ingredient Report already checks one product at a time; this report looks across the whole collection. Products and ingredient lists: {{collection}}  
> You may ONLY flag pairings from Hauly's pairing list — do not add any others: retinoids (e.g. retinol, retinal, adapalene, retinyl esters) with AHAs, BHAs or vitamin C (ascorbic acid); benzoyl peroxide with retinoids, AHAs, BHAs or vitamin C.  
> If an ingredient name is unclear or not recognised, say "not recognised" — do not guess what it is.  
>
> **Expected output:** Three sections. (1) Pairing cautions — for each: the two products, the matching ingredients, and the note "These can be harsh together — introduce them gradually or on alternate days." (2) Repeated actives — ingredient, and which products contain it. (3) Not checked — unrecognised ingredients. Never say a product or combination is "safe", never diagnose or promise results, and end with: "This is general information, not medical advice — patch test new products and speak to a pharmacist or dermatologist if you have a skin condition or reaction." If nothing matches the list, say "No pairing cautions found" — do not invent one.  

Words in `{{double brackets}}` are filled in each time the prompt is used.

## Versions and recorded responses

Every version below was run once on the same sample input, written for testing and based on real Hauly features (not a real user message). Tests used Claude Sonnet 5 in September 2026. Responses are copied exactly as returned.

**Sample input:**

~~~text
1. Night serum — Aqua, Glycerin, Retinol, Tocopherol.
2. Exfoliating toner — Aqua, Glycolic Acid, Niacinamide.
3. Morning serum — Aqua, Ascorbic Acid, Niacinamide, Ferulic Acid.
4. Spot gel — Aqua, Benzoyl Peroxide, Carbomer.
5. Face oil — Squalane, Bakuchiol, "Botanical Complex X".
~~~

### V1

**Prompt text (as tested)**

~~~text
Look at these products and their ingredients and tell me which ones shouldn't be used together. Products: 1. Night serum — Aqua, Glycerin, Retinol, Tocopherol.
2. Exfoliating toner — Aqua, Glycolic Acid, Niacinamide.
3. Morning serum — Aqua, Ascorbic Acid, Niacinamide, Ferulic Acid.
4. Spot gel — Aqua, Benzoyl Peroxide, Carbomer.
5. Face oil — Squalane, Bakuchiol, "Botanical Complex X".
~~~

**Recorded response**

~~~text
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
~~~

### V2 (final)

**Prompt text (as tested)**

~~~text
Role: You are Hauly's collection assistant. You give general skincare information, not medical advice.
Action: Review the user's collection below and report pairing cautions and repeated active ingredients across products.
Context: Hauly's Ingredient Report already checks one product at a time; this report looks across the whole collection. Products and ingredient lists: 1. Night serum — Aqua, Glycerin, Retinol, Tocopherol.
2. Exfoliating toner — Aqua, Glycolic Acid, Niacinamide.
3. Morning serum — Aqua, Ascorbic Acid, Niacinamide, Ferulic Acid.
4. Spot gel — Aqua, Benzoyl Peroxide, Carbomer.
5. Face oil — Squalane, Bakuchiol, "Botanical Complex X".
You may ONLY flag pairings from Hauly's pairing list — do not add any others: retinoids (e.g. retinol, retinal, adapalene, retinyl esters) with AHAs, BHAs or vitamin C (ascorbic acid); benzoyl peroxide with retinoids, AHAs, BHAs or vitamin C.
If an ingredient name is unclear or not recognised, say "not recognised" — do not guess what it is.
Expected output: Three sections. (1) Pairing cautions — for each: the two products, the matching ingredients, and the note "These can be harsh together — introduce them gradually or on alternate days." (2) Repeated actives — ingredient, and which products contain it. (3) Not checked — unrecognised ingredients. Never say a product or combination is "safe", never diagnose or promise results, and end with: "This is general information, not medical advice — patch test new products and speak to a pharmacist or dermatologist if you have a skin condition or reaction." If nothing matches the list, say "No pairing cautions found" — do not invent one.
~~~

**Recorded response**

~~~text
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
~~~

## Prompt Lab check (GPT-4.1 mini)

To check the results weren't specific to one AI model, the final version (and in some cases the first version) was re-run in La Trobe Prompt Lab using GPT-4.1 mini, with exactly the same prompt text. Prompt Lab's prompt review, where run, scores the prompt itself out of 100.

**What GPT-4.1 mini did:**

- **V1 — same problems as Claude Sonnet 5:** it gave its own pairing list, added retinol + bakuchiol (not on Hauly's list), missed retinol + vitamin C and vitamin C + benzoyl peroxide, reassured that vitamin C and niacinamide have "No strong contraindication", suggested a routine, and gave no disclaimer.
- **V2 — same result as Claude Sonnet 5:** exactly the five pairings on Hauly's list, niacinamide as the repeated active, "Botanical Complex X" not recognised, and the required disclaimer. It never used the word "safe".
- **Prompt Lab review:** V1 scored 72.25/100 (lowest for constraints, 60/100); V2 scored 90.5/100 (95/100 for constraints and hallucination risk).

### Prompt Lab — V1

**Recorded response (GPT-4.1 mini)**

~~~text
Let's analyze the potential interactions between the products based on their key active ingredients:

### Products and Key Actives:
1. **Night serum**: Retinol, Tocopherol (Vitamin E)
2. **Exfoliating toner**: Glycolic Acid (AHA), Niacinamide
3. **Morning serum**: Ascorbic Acid (Vitamin C), Niacinamide, Ferulic Acid
4. **Spot gel**: Benzoyl Peroxide
5. **Face oil**: Squalane, Bakuchiol (a gentler retinol alternative), Botanical Complex

---

### Potential Incompatibilities or Cautions:

1. **Retinol (Night serum) + Glycolic Acid (Exfoliating toner)**  
- Both are active ingredients that can cause irritation and increase skin sensitivity.  
- Using strong exfoliants (glycolic acid) and retinol simultaneously can lead to redness, peeling, and irritation.  
- Recommended: Use on alternate nights or separate times (e.g., glycolic acid in the evening and retinol on a different night).

2. **Retinol (Night serum) + Benzoyl Peroxide (Spot gel)**  
- Benzoyl peroxide can oxidize retinol, reducing its effectiveness and causing irritation.  
- Using these together can be too harsh and drying to the skin.  
- Recommended: Apply benzoyl peroxide in the morning and retinol at night, or use on alternate days.

3. **Ascorbic Acid (Morning serum) + Niacinamide**  
- Historically, it was thought that vitamin C and niacinamide cancel each other out or cause flushing, but recent studies show they are generally compatible and can be used together without problems.  
- No strong contraindication here.

4. **Benzoyl Peroxide + Glycolic Acid**  
- Both are exfoliating and acne-fighting agents that can be drying and irritating if combined.  
- Recommended: Use at different times of day or alternate days.

5. **Retinol + Bakuchiol (Face oil)**  
- Both have similar effects (anti-aging, cell turnover).  
- Using both together might increase irritation, especially for sensitive skin.  
- However, bakuchiol is milder and often touted as a gentler alternative to retinol.  
- If used together, be cautious of irritation.

---

### Summary of What Shouldn't Be Used Together or Use with Caution:
- **Night serum (Retinol) + Exfoliating toner (Glycolic Acid)**: avoid same time application.  
- **Night serum (Retinol) + Spot gel (Benzoyl Peroxide)**: avoid same time application.  
- **Exfoliating toner (Glycolic Acid) + Spot gel (Benzoyl Peroxide)**: avoid same time application or alternate.  
- **Night serum (Retinol) + Face oil (Bakuchiol)**: use cautiously; may increase irritation.

---

### Recommended Usage Suggestions:
- **Morning**: Morning serum (Vitamin C + Niacinamide + Ferulic Acid) + Face oil.  
- **Evening**:  
  - On exfoliation nights: Exfoliating toner + Face oil.  
  - On retinol nights: Night serum + Face oil (bakuchiol presence might be redundant; consider skipping face oil or ensuring it is gentle).  
  - Spot gel can be applied as needed, preferably not with retinol or glycolic acid at the same time.

---

If you want, I can help you create a sample routine based on these products!
~~~

**Prompt Lab review:** overall score 72.25/100

~~~text
Rubric Scores
Clarity: 85/100 - The prompt is mostly clear in asking for product compatibility but could specify the context (e.g., skin type, usage frequency) for better clarity.
Constraints: 60/100 - The prompt lacks explicit constraints such as focusing only on active ingredients, specifying the type of incompatibility (e.g., irritation, chemical neutralization), or usage timing.
Structure: 70/100 - The prompt lists products and ingredients clearly but does not guide the assistant on how to organize the response or what format to use.
Verifiability: 65/100 - The prompt provides ingredient lists but does not request evidence-based or referenced explanations, which would improve verifiability.
Hallucination Risk: 80/100 - The prompt is factual and ingredient-based, reducing hallucination risk, but vague phrasing could lead to assumptions about "shouldn't be used together" without context.
Overall Score
Overall score: 72.25/100

Top Improvements
Specify the type of incompatibility to assess (e.g., chemical interaction, skin irritation, efficacy reduction).
Request evidence-based or referenced explanations to improve verifiability.
Provide guidance on the desired format or structure of the response for better clarity and usability.
Suggested Rewrite
Please analyze the following skincare products and their ingredients to identify any combinations that should be avoided or used with caution due to potential chemical interactions, skin irritation, or reduced effectiveness. For each identified incompatibility, explain the reason based on known dermatological or chemical principles. The products are:

Night serum — Aqua, Glycerin, Retinol, Tocopherol
Exfoliating toner — Aqua, Glycolic Acid, Niacinamide
Morning serum — Aqua, Ascorbic Acid, Niacinamide, Ferulic Acid
Spot gel — Aqua, Benzoyl Peroxide, Carbomer
Face oil — Squalane, Bakuchiol, "Botanical Complex X"
Please organize your response by product pairs and provide clear recommendations on how to use these products safely together, including timing or frequency suggestions if relevant.
~~~

### Prompt Lab — V2

**Recorded response (GPT-4.1 mini)**

~~~text
(1) Pairing cautions  
- Night serum (Retinol) and Exfoliating toner (Glycolic Acid) — retinol and AHA  
- Night serum (Retinol) and Morning serum (Ascorbic Acid) — retinol and vitamin C  
- Night serum (Retinol) and Spot gel (Benzoyl Peroxide) — retinol and benzoyl peroxide  
- Exfoliating toner (Glycolic Acid) and Spot gel (Benzoyl Peroxide) — AHA and benzoyl peroxide  
- Morning serum (Ascorbic Acid) and Spot gel (Benzoyl Peroxide) — vitamin C and benzoyl peroxide  

These can be harsh together — introduce them gradually or on alternate days.

(2) Repeated actives  
- Niacinamide: Exfoliating toner, Morning serum  

(3) Not checked  
- Botanical Complex X (Face oil) — not recognised  

This is general information, not medical advice — patch test new products and speak to a pharmacist or dermatologist if you have a skin condition or reaction.
~~~

**Prompt Lab review:** overall score 90.5/100

~~~text
Rubric Scores
Clarity: 90/100 - The prompt is mostly clear with defined roles, actions, and expected output sections, but some phrasing could be simplified for easier understanding.
Constraints: 95/100 - The prompt provides strong constraints on which pairings to flag, how to handle unrecognized ingredients, and output format, minimizing scope creep.
Structure: 90/100 - The prompt is well-structured with clear sections (role, action, context, constraints, expected output), though the output format could be more explicitly formatted for easier parsing.
Verifiability: 85/100 - The prompt references a specific pairing list and ingredient recognition rules, which supports verifiability, but it relies on the assistant’s knowledge of Hauly’s pairing list without providing it explicitly.
Hallucination Risk: 95/100 - The prompt explicitly forbids inventing cautions or guessing unrecognized ingredients, strongly reducing hallucination risk.
Overall Score
Overall score: 90.5/100

Top Improvements
Provide the exact pairing list or a link/reference to it within the prompt to improve verifiability.
Simplify some wording for clarity, especially around the expected output format.
Explicitly format the expected output sections (e.g., bullet points, headings) to guide the assistant’s response structure.
Suggested Rewrite
Role: You are Hauly's collection assistant. Provide general skincare information only; do not give medical advice.
Action: Review the user's skincare product collection below. Identify any pairing cautions and repeated active ingredients across the products.
Context: Hauly's Ingredient Report checks one product at a time; this report compares all products together.
Products and ingredients:

Night serum — Aqua, Glycerin, Retinol, Tocopherol
Exfoliating toner — Aqua, Glycolic Acid, Niacinamide
Morning serum — Aqua, Ascorbic Acid, Niacinamide, Ferulic Acid
Spot gel — Aqua, Benzoyl Peroxide, Carbomer
Face oil — Squalane, Bakuchiol, Botanical Complex X
Constraints:

Only flag pairings from Hauly's pairing list:
Retinoids (retinol, retinal, adapalene, retinyl esters) with AHAs, BHAs, or vitamin C (ascorbic acid)
Benzoyl peroxide with retinoids, AHAs, BHAs, or vitamin C
If an ingredient is unclear or unrecognized, say "not recognised" without guessing.
Do not invent cautions or say any product or combination is "safe."
End with: "This is general information, not medical advice — patch test new products and speak to a pharmacist or dermatologist if you have a skin condition or reaction."
Expected output:

Pairing cautions — list each pair of products, the matching ingredients, and the note: "These can be harsh together — introduce them gradually or on alternate days." If none, say "No pairing cautions found."
Repeated actives — list each repeated active ingredient and the products containing it.
Not checked — list unrecognized ingredients and their products.
~~~

**Note on the reviews' suggestions:** the V2 review suggested adding "the exact pairing list" to the prompt, but the list is already written into the Context section, so this suggestion was not applied. The V1 review's suggested rewrite asks for "known dermatological or chemical principles" rather than Hauly's own list, which would reintroduce the risk V2 was designed to remove, so it was also not applied.
