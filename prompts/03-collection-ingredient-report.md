# Prompt 3 — Collection Ingredient Report

**Workflow stage:** Response

| | |
| --- | --- |
| **Task** | Check all the products in a user's collection and report ingredient pairings to be careful with, and active ingredients that appear in more than one product. |
| **Problem it solves** | Hauly's existing Ingredient Report looks at one product at a time. Users with many products have no way to see pairing cautions across their whole collection. |
| **Prompting techniques** | Role framing with a clear "not medical advice" limit; a fixed list of allowed pairings taken from Hauly's own ingredient data (constraints); a three-section report (structured output); a required disclaimer. |

## Final prompt (v2)

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

## How the prompt was improved

All versions were tested on the same sample message (written for testing, based on real Hauly features): *"1. Night serum — Aqua, Glycerin, Retinol, Tocopherol.
2. Exfoliating toner — Aqua, Glycolic Acid, Niacinamide.
3. Morning serum — Aqua, Ascorbic Acid, Niacinamide, Ferulic Acid.
4. Spot gel — Aqua, Benzoyl Peroxide, Carbomer.
5. Face oil — Squalane, Bakuchiol, "Botanical Complex X"."*

**Where the pairing list comes from:** Hauly's built-in ingredient database already marks which ingredient types should be introduced carefully together: retinoids with AHAs, BHAs or vitamin C, and benzoyl peroxide with retinoids, AHAs, BHAs or vitamin C. The note in the prompt ("can be harsh together — introduce them gradually or on alternate days") is the wording the app already uses.

**v1** — one line: *"Tell me which ones shouldn't be used together."*

- **Result:** it gave its own list of "combinations to avoid" and missed retinol + vitamin C, which is on Hauly's list. It told the user some pairings had "No concern here" or were "a beneficial pairing" — the kind of safety reassurance Hauly avoids. It also suggested a full routine and gave no medical disclaimer.

**v2 (final)** — limited it to Hauly's pairing list, banned the word "safe" and any diagnosis, required the disclaimer, and told it to mark unknown ingredients as "not recognised".

- **Result:** it flagged exactly the five pairings that match Hauly's list, listed niacinamide as appearing in two products, marked "Botanical Complex X" as not recognised, and ended with the disclaimer. It gave no reassurances.

Full test outputs: [Appendix — Prompt 3](../appendix-test-outputs.md#prompt-3).

## Automation potential

**Medium.** The report is general information, so it could run whenever a user asks for it. Any change to the pairing list must be checked by Holly first.

## Risks and limitations

- The report is only as accurate as Hauly's pairing list. If the list is wrong or out of date, the report will be wrong in a confident-sounding way.
- Ingredient names on labels vary, so some matches can be missed — the "not recognised" section makes those gaps visible.
- Skincare information can be mistaken for medical advice, which is why the disclaimer is required.
