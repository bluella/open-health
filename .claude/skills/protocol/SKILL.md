---
name: protocol
description: How to write or revise a patient-facing protocol in instructions-for-patient/. Use when the user asks for a protocol, management plan, test-first plan or routine for a condition, or asks to bump an existing one to a new version. Fixes the file layout, section order, length and house rules so every protocol reads the same.
---

# Protocol — patient-facing instruction document

A protocol is the actionable output of a `/diagnose` work-up: one file in
`instructions-for-patient/` that the user follows day to day and brings to a GP or specialist.
It is written for the patient, not for a clinician and not for the model. The reasoning that
produced it stays in the conversation; only the conclusions and the rules go into the file.

## File and versioning

- Path `instructions-for-patient/<Condition>_<Kind>_Protocol_vN.md`, e.g.
  `IBS_Management_Protocol_v2.md`, `Iron_Deficiency_Test-First_Protocol_v1.md`,
  `Acne_Protocol_v1.md`.
- A revision is a new file with the next version number, never an edit in place. The old file
  is deleted unless it holds evidence the new one dropped (literature, product links, logged
  episodes); then it stays as the archive and the new header says so.
- Every new or bumped version gets a row in `instructions-for-patient/README.md` (document,
  one-line summary, version and date) and the README's `Updated` line is bumped. A superseded
  file's row is rewritten to "Superseded by vN. Kept as ...".
- Register a cross-reference when one protocol changes another's decision: say which line of
  the other protocol it supersedes, by section number.

## Header

```
# <Condition> — <Kind> Protocol vN

*Updated YYYY-MM-DD · vN · supersedes vN-1 (YYYY-MM-DD), which stays as the evidence archive*
```

The italic line carries the date, the version and one of: `supersedes ...`, `companion to ...`,
or nothing for a first standalone version. Dates are absolute, per CLAUDE.md.

## Sections, in this order, numbered `## 1.` onwards

1. **What is going on** (or **Why this document exists** for a companion document). Working
   diagnosis with a confidence percentage, the main alternatives with theirs, and whether the
   alternatives change the management. The mechanism as a numbered list of steps in plain
   words. What has already been excluded, with the test and month. Facts that set expectations
   when the condition is chronic or cosmetic ("refills within a month no matter what").
2. **Tests** as a table: Priority · Test · Why · Route (public route, referral, private, postal
   kit, with named providers and prices where verified). For a non-medical topic this section
   becomes **What works and what does not**: Approach · Verdict · Evidence.
3. **Medication and supplements** (or **Routine**), grouped by labels in bold: **Core** with
   dose, timing and ceiling; **Escalation** and who prescribes it; **Keep** for the unchanged
   stack; **Rescue kit**; **Closed, do not retry** as an explicit list so old trials are not
   repeated.
4. **How to eat and behave**: numbered rules, each one testable, with the bold lead phrase being
   the rule itself. Include the "when you break a rule" recovery step and what to log so the
   record becomes referral evidence.
5. **Products** when anything is to be bought: "Stock verified YYYY-MM-DD", product, why it is
   the first choice, retailer (from the profile), price, URL. Alternatives seen but not verified
   are listed without links and marked "recheck before buying". No link, no recommendation.
6. **Community tips**, only if a forum sweep produced something worth keeping, labelled
   "anecdotal" in the heading and kept out of the clinical sections.
7. **Red flags, go now**: one line of symptoms separated by middle dots, or "None expected"
   plus the one sign that would point away from the diagnosis. A companion document inherits
   the parent's list by reference and adds only its own.

Conditional branches (**If positive**, **If negative**, **Until the result**) go between the
tests and the red flags when the protocol hinges on a test result.

Optional trailing parts:

- **Sources**: one paragraph, author-year-journal, separated by middle dots, ending with
  "Prices and links checked YYYY-MM-DD". Only when the file cites trials by name.
- Footer, always: `*Structured input for GP and <specialty> conversations, not a substitute for
  them.*` Add where the dropped evidence lives if a version was cut down.

## Length

Two pages is the target: 700–900 words for a management protocol, up to about 1,600 when it
carries test criteria and treatment regimens the patient cannot look up elsewhere. Longer
documents turn into archives nobody re-reads. When a new version would go past 1,600 words, move
the evidence into the previous version or a `records/` note and cite it from the footer.

## House rules

- Written for the patient in the second person or in imperatives ("Take 1,000 mg at once",
  "Do not stack rescue on rescue"). No preamble, no reassurance filler.
- Every number is specific: dose, ceiling, gap in hours, weeks to judge an effect, percentage
  from a trial with its sample size, price with the date it was checked.
- Confidence and alternatives are stated as percentages, as in the `/diagnose` table, and the
  file says plainly when a treatment working is not proof of the diagnosis.
- Local context from the profile: the public route named concretely (what to write on the
  referral, which units run the test), private and postal alternatives with the threshold for
  choosing them ("if the public route is more than about eight weeks away").
- Interactions with the user's existing stack are spelled out (4-hour gaps, what to pause
  before a test, what resumes when). Read `personal-protocols/supplements.md` and
  `supplement-reactions.md` before writing section 3.
- Tables for anything with three or more comparable rows; numbered lists for rules and
  mechanisms; bold lead phrases so the document can be skimmed at the pharmacy.
- Prescription-only and unlicensed drugs are flagged as such, with who initiates them and the
  private price if the public path is uncertain.
- Evidence weight is stated where it is weak: "retrospective, non-randomised", "no clinical
  trials, dermatologist consensus only", "theory only".

## Process

1. The protocol follows a `/diagnose` work-up or an explicit user decision; do not write one
   speculatively.
2. Literature, guideline, provider and stock lookups go to Sonnet subagents per CLAUDE.md,
   fanned out in parallel, described generically. Ask for raw findings with URLs, prices and
   dates.
3. Draft the file, update the README row, then show the user the word count and the rows in
   the tests and products tables that depend on lookups they may want to re-verify.
4. Do not commit unless asked.
