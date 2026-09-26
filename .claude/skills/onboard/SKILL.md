---
name: onboard
description: First-run interview that fills records/general-info-on-patient.md and seeds personal-protocols/. Use when the user runs /onboard, when the profile is still empty, or when the user wants to set up or refresh their baseline.
---

# Onboard — fill the profile

The profile sets the priors for every later `/diagnose`. Aim for a usable one in about ten
minutes; it can grow later.

## Interview

Read `records/general-info-on-patient.md` first and skip every field already filled, so the same
skill works for a refresh. Then ask in rounds of 3–5 questions, most important first:

1. Language for the files, country, healthcare route (public, insurance, private), where they
   buy supplements and products.
2. Sex, year of birth, height, weight.
3. Diagnosed conditions, past surgeries, allergies, family history.
4. Current medication and supplements; foods or substances known to disagree with them.
5. Activity, sleep, smoking, alcohol, and any metrics they track (resting heart rate, VO2 max,
   blood pressure, wearable).
6. What brought them here: a current complaint, a goal, or just keeping records.

"Skip" is always a valid answer. Leave the field blank; never guess or fill with a typical value.

## Writing

- Profile answers go into `records/general-info-on-patient.md`, keeping its field layout.
- The stack goes to `personal-protocols/supplements.md`; known reactions become rows in
  `food-reactions.md` or `supplement-reactions.md`, status **Not sure** unless the user says
  they have seen it repeatedly.
- Bump every `Updated` line you touch, per CLAUDE.md.

## Close

- Offer `/log` for any lab results they have (PDFs, screenshots, app exports).
- If they named a complaint, offer `/diagnose` for it.
- Finish with three lines: what was written where, and the single most useful next step.
