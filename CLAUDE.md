# Health — Claude Code Instructions

## Project Overview

A personal health knowledge base: plain markdown, no code, no build, no tests.
The user keeps their health data here; you reason over it.

| Path | What it is |
| --- | --- |
| `records/` | Raw facts: profile (`general-info-on-patient.md`), food and symptom diary, lab results (`records/labs/`, one dated file per test); `README.md` there is the index |
| `personal-protocols/` | Self-observed rules and reaction ledgers, one note per area; `README.md` there is the index and tag legend |
| `instructions-for-patient/` | Protocols written for the user to follow and take to a doctor; `README.md` there is the index |
| `.claude/skills/onboard/` | `/onboard`: first-run interview that fills the profile and seeds the notes |
| `.claude/skills/log/` | `/log`: puts a diary entry, lab result or observation into the right file |
| `.claude/skills/diagnose/` | `/diagnose`: how to answer a health question. Bayesian symptom work-up (ranked hypotheses, targeted questions, probability updates) plus the evidence, community-tips, product-link and tone rules |
| `.claude/skills/protocol/` | `/protocol`: the fixed layout of a patient-facing protocol in `instructions-for-patient/` (file naming and versioning, header, numbered section order, two-page length, house rules) |

For any health question, follow the evidence, community-tips, links and tone rules in the
`/diagnose` skill; run its full hypothesis loop whenever the user describes a symptom or
complaint. If `records/general-info-on-patient.md` is still empty, suggest `/onboard` once.

The files are the user's own records. Edit them only when asked (`/onboard` and `/log` count as
asking), and never rewrite history in the diary or protocols — append or amend the specific entry.

## Language

- Write every file and every reply in the language on the profile's `Language` line (English if
  unset).
- The user may type or dictate in any language. Treat it as ordinary input: do not mirror it, do
  not translate replies into it, and do not ask which language to use.
- Exceptions: quoting a source or a lab report verbatim, and cases where the user explicitly asks
  for output in another language.

**Why:** the reasoning should stay in one language end-to-end to avoid translation drift and
ambiguity; dictation language is an input-convenience choice, not a preference about output.

## Dates

Every update carries an explicit absolute date, taken from the session's current date — never
"today", "recently", or a guessed date.

- A file that has an `Updated ...` line in its header gets that line bumped whenever the file changes.
- A new fact that can go stale is dated inline: "as of 2026-09-14, ...".
- Diary headers, lab file names and inline stamps use ISO `YYYY-MM-DD`.
- Do not re-date entries you did not change.

## Local context

Country, healthcare route and preferred retailers come from the profile. Name the public route
for that country (NHS GP referral, statutory insurance, primary care physician, ...) plus private
and postal alternatives, and link products only from the profile's retailers. If the profile is
silent, ask once and offer to save the answer there.

## Model Delegation (main model reasons, Sonnet searches)

The interactive session keeps the reasoning; anything that burns tokens on raw text goes to
**Sonnet subagents** (Agent tool, `model: sonnet`, `subagent_type: general-purpose`).

**Always delegate:** WebSearch/WebFetch — literature and guideline lookups, Reddit and patient-forum
sweeps, product searches and stock/availability checks at the profile's retailers.

**Never delegate:** interpretation of the user's data, medical reasoning and recommendations,
follow-up questions, and everything written to the user or to these files.

**Subagent prompts:** name the exact question, sources to prefer, and the return format (raw
findings with URLs and dates, not a summary). Never put the user's name or other identifying
details into a web query — describe the case generically. Fan out independent lookups as parallel
subagents in one message.
