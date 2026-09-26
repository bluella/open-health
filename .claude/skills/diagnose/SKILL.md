---
name: diagnose
description: Bayesian symptom work-up. Use when the user describes something that is wrong with them (a symptom, a complaint, a change) and wants to know what it could be. Builds a ranked hypothesis list with probabilities, then asks targeted questions and updates the probabilities after each answer.
---

# Diagnose — Bayesian symptom work-up

The user describes what bothers them. Your job is to produce a ranked list of hypotheses with
probabilities, then narrow it down by asking the questions whose answers would move the
probabilities the most. This is a reasoning loop, not a one-shot answer.

## Before the first hypothesis

Read the project context first; the priors come from it, not from population base rates alone:

- `records/general-info-on-patient.md` — baseline (age, sex, country, history). If it is empty,
  ask for age, sex and relevant history in the first question round and suggest `/onboard`
  afterwards; do not guess them.
- `records/README.md` and `records/labs/` — what has already been tested and ruled out.
- `personal-protocols/test-yourself.md` — what this symptom has usually meant for this user before.
- `personal-protocols/food-reactions.md`, `supplement-reactions.md`, `supplements.md` — current
  stack and known triggers.
- `instructions-for-patient/` — any active protocol the symptom may belong to.
- `records/food-diary.md` — only if the symptom is plausibly diet-linked.

A hypothesis already excluded by a lab result (see the labs index) gets a low prior and a note
saying why, not silent omission.

## Round 1: hypotheses

Output a table:

| # | Hypothesis | Probability | Why (for / against, from the user's data) |

Rules:

- 3–7 hypotheses. Include a "something else / not enough information" row so the column sums
  to roughly 100%.
- Probabilities are rough, honest, and explicitly labelled as priors. Prefer 5% steps.
- Always include the dangerous-but-unlikely option if one exists, and say what red flag would
  raise it.
- Say in one line which hypothesis the user's own history favours (from `test-yourself.md`).
- Reasoning is evidence-based: name the mechanism, cite current consensus or peer-reviewed
  findings where they exist, and flag when evidence is weak, mixed, or emerging. Note risk
  factors and contraindications that apply to this user's profile and stack.

## Round 1: questions

Ask 3–5 questions when they could meaningfully change the picture, chosen by expected information
gain: each question should split the top hypotheses, not confirm the leader. For each question say
in a few words which hypotheses it separates. Onset, timing, triggers, what makes it better or
worse, associated symptoms, recent changes (food, supplements, sleep, training, stress, travel,
medication).

Do not ask what the records already answer.

## Round 2+: update

After each answer, output the same hypothesis table with updated probabilities and a one-line
"what moved and why" per changed row. Then ask the next 1–3 questions. Stop when:

- one hypothesis is above ~70% and the rest are below ~10%, or
- the remaining uncertainty can only be resolved by a test or a doctor.

Finish with:

- The leading hypothesis and what to do about it, tied to existing protocols where they apply.
- Which test or doctor visit would settle it, via the route for the user's country, and any red
  flags that mean "go now".
- **Community-sourced tips**, clearly labelled as anecdotal and kept separate from the clinical
  reasoning: what people on Reddit (r/AskDocs, condition-specific subs) and patient forums have
  found helpful for the leading hypothesis, with specific products, routines or hacks and their
  caveats.
- **Links** for any product recommended, from the retailers named in the profile, verified by a
  subagent to open and to be in stock. No link, no recommendation.
- If the answer calls for an ongoing plan, offer `/protocol`.

## Delegation

Literature, guideline and forum lookups go to Sonnet subagents per CLAUDE.md, fanned out in
parallel and described generically. Typical asks: differential diagnosis of the symptom in a
person of the profile's age and sex, likelihood ratios for the discriminating questions,
patient-forum experience for the top two hypotheses, product availability and working links. Use
them to sharpen priors and to pick better questions.
The interpretation, the probabilities, and everything written to the user stay with the main
session.

## Tone and format

Direct and specific, no preamble. Short paragraphs, not walls of text. Bold the key takeaway
in each round. Explain in a few words why each question matters, so the user can answer the
question actually being asked.

## Record keeping

If the work-up ends in a new observation the user confirms, offer to append it to
`personal-protocols/test-yourself.md` with the date. Do not write anything without being asked.
