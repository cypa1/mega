# S01E03 — what it shows

The support desk merged **412 reports about dates into ticket #4471** and marked it known.
#4471 does not hold one problem: it holds **two**, with different causes and different fixes.
The desk's own page (its `CauseTable` component) shows the split, while its prose still says
"one issue".

## Tickets

One GitHub issue per problem, each with the number of reports it covers:

- **parser — 379 reports.** The shared date parser reads every date month-first; every tenant
  on file writes the day first, so their dates flip.
- **hint — 33 reports.** `booking-v3` prints `MM/DD/YYYY` under its date field while the form
  reads the value day-first. Form reports from `alder.physio`, `copper.studio`, `pale.harbour`.

379 + 33 = 412. The 5 reports in `desk-notes.json` that the desk read as "one-day moves" are
counted inside `parser` here, exactly as the desk filed them.

**Desk update:** #4471 is closed 05 Oct. `parser` is fixed (`fix(dates): parse dd/mm for eu
locales`); `hint` won't fix, because the booking-v3 form was retired. Both tickets are closed
to match.

## The page

`kb/src/routes/kb/incidents/4471-split/+page.svx` is the page added to the kb. It is signed:
its frontmatter carries the `signature` and it ends with `<RenderStamp {signature} />`.

`render/4471-split.html` and `render/4471-split.png` are the page as the desk will see it: the
table is computed from the exported reports at render time, so the two counts and the one-day
footnote come from the data, not from a sentence.
