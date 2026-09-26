---
name: log
description: Put a new fact into the records — a food or symptom diary entry, a lab result (pasted text, PDF, screenshot), a change to the supplement stack, or a repeatable reaction. Use when the user runs /log, pastes or attaches a lab report, or asks to note or write down something about food, symptoms, supplements, sleep or tests.
---

# Log — put a fact in the right file

Decide where it goes, write it, and say in one line where it went. No analysis unless asked; if
the entry looks like a red flag, say so in one line and offer `/diagnose`.

| Input | Goes to |
| --- | --- |
| Meal, symptom, stool, sleep, mood, a dose taken | `records/food-diary.md` |
| Lab result | `records/labs/YYYY-MM-DD-<test>.md` plus a row in the labs table of `records/README.md` |
| "X does Y to me", seen before | a row in `personal-protocols/food-reactions.md` or `supplement-reactions.md` |
| Started, stopped or changed a supplement or drug | `personal-protocols/supplements.md`, and the reaction ledger if it behaved badly |
| A rule the user wants to keep | the matching note in `personal-protocols/`, under **Sure** or **Not sure** |

## Diary

Append only. One `## YYYY-MM-DD` header per day (create it if missing), one `- HH:MM` line per
event, the user's words tightened but not reinterpreted. Stools as Bristol type when the user
gives one. Free text goes on a `Notes:` line.

## Lab file

```
# <Test name> — YYYY-MM-DD

*Recorded YYYY-MM-DD · ordered by <GP / specialist / private / self>*

| Marker | Value | Unit | Reference range | Flag |
| --- | --- | --- | --- | --- |

**Verdict:** <lab or doctor comment, verbatim where possible>

**Gap:** <what was not captured, e.g. only the verdict, no values>
```

- The file date is the sample date, not the report date.
- One file per test date; a panel drawn on one date is one file.
- Copy values, units and ranges exactly; do not convert or round. Out of range gets `H` or `L`.
- The index row: date, test, one-line result, link.

## Rules

- Dates are the date the thing happened. If the user did not say, use the session date and
  say so; never guess.
- Never edit an old diary entry or ledger row unless the user asks to amend that one.
- Do not commit unless asked.
