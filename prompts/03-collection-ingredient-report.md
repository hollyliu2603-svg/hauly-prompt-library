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
