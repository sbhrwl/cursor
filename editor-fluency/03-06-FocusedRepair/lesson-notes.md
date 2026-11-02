# 03.06 — Repair a focused issue without rewriting the component
- [Overview](#overview)
  - [interactive-focused-repair-lab](https://sbhrwl.github.io/cursor/editor-fluency/03-06-FocusedRepair/interactive-focused-repair-lab.html)
- [The recorded workflow](#the-recorded-workflow)
- [Evidence and boundaries](#evidence-and-boundaries)
- [Interactive companion](#interactive-companion)
- [Files](#files)
## Overview
- The outcome is a small, reviewable repair supported by a failing regression test, a corrected preview, and checks of neighboring behavior.
- The prepared Operations Hub preview receives three synthetic queue snapshots.
  - Before the repair, it displays `Not loaded` for a queue whose pending count is zero.
  - The input contract treats zero as a real count and null as missing data.

| Input | Expected display | Before repair | After repair |
|---|---|---|---|
| `4` | `4` | `4` | `4` |
| `0` | `0` | `Not loaded` | `0` |
| `null` | `Not loaded` | `Not loaded` | `Not loaded` |

- The original conditional uses the count as a truthiness test.
  - Both zero and null evaluate as false, so they reach the same fallback.
- The recorded proposal replaces that decision with an explicit null check:
```ts
const pendingText = queue.pendingCount === null
  ? 'Not loaded'
  : String(queue.pendingCount);
```
- The expression above is formatted across lines for reading; the recorded patch keeps the assignment on one line.
- The input boundary is assumed to supply a nonnegative integer or null.
  - This lesson does not add runtime validation for arbitrary data.
## The recorded workflow
- Reproduce the visible mismatch and inspect the actual local API inputs.
- Use Cursor workspace search to locate the visible label.
  - Read the helper and the preview's call to it.
- Run the five existing queue tests and the type check.
  - Both pass despite the zero-count bug.
- Add a regression assertion expecting `'0'` for a zero input.
  - The new test fails while the original five pass.
- Select the display assignment and open Inline Edit with Ctrl+K on the installed Linux configuration.
  - State the three input behaviors and preservation constraints.
- Review the proposed assignment and surrounding code, accept it, and save.
- Inspect the diff.
  - Run six queue tests, nine earlier request-status tests, and the type check.
- Refresh the original preview, try the support queue link, and compare the unchanged input snapshots.
- The recorded request:
```
> Fix only this assignment: zero must display '0'; null must remain 'Not loaded'; positive counts must retain their value. Preserve all other code and files. No refactor.
```
- This is a course-authored prompt, not a universal formula.
  - Direct editing would also be reasonable for this small change.
  - The value of the demonstration is defining scope and assessing the actual result.
## Evidence and boundaries
- Before fixing the implementation, the queue suite has five passes and one failure.
- After the repair, all six queue tests and all nine request-status tests pass.
  - The type check exits successfully.
  - The repository diff contains only the changed display assignment and the added regression test.
- The input fixtures, preview server, HTML renderer, dependency files, earlier status implementation, and earlier status tests are byte-identical across the repair.
  - The zero regression test is unchanged between the failing and passing runs.
  - Queue identity, title, team, priority, and navigation values also remain unchanged in the API output.
- The production baseline commit is `78429f59f88d4cc5e30578540265be03f3e39756`.
  - The student bundle has its own portable snapshot commit, listed in `offline-snapshot.json`; its README includes standalone setup instructions.
  - A fresh clone of that bundle was checked with `npm ci`, the five baseline queue tests, and the type check.
- These checks establish the bounded local exercise.
  - They do not establish production readiness, database behavior, external integrations, or correctness for every possible input.
  - Passing tests are useful evidence for the behavior those tests actually cover.
## Interactive companion
- The companion provides a repair contract, four fixed candidate expressions, a review checklist, a downloadable repair record, and an independent assessment.
  - The candidate table evaluates positive, zero, and null inputs.
  - Its expressions are original teaching examples, not generated Agent output.
  - It does not edit your repository.
- Use [`practice.md`](practice.md) and the starter bundle to repeat the method.
  - Keep the meaningful regression test and challenge your fix with neighboring cases.
  - Complete and download the repair record before closing the local companion page.
## Files
- [interactive-focused-repair-lab.html](https://sbhrwl.github.io/cursor/editor-fluency/03-06-FocusedRepair/interactive-focused-repair-lab.html)
- [practice.md](practice.md)
- [focused-repair-record.md](focused-repair-record.md)
- [recorded-repair.patch](recorded-repair.patch)
- [focused-repair-starter.bundle](focused-repair-starter.bundle)
- [starter-readme.md](starter-readme.md)
- [offline-snapshot.json](offline-snapshot.json)
- [PROMPTS.md](PROMPTS.md)
- [narration-script.md](narration-script.md)
  - [03-06-repair-a-focused-issue-without-rewriting-the-component.en.srt](03-06-repair-a-focused-issue-without-rewriting-the-component.en.srt)
- [sources-and-credits.md](sources-and-credits.md)
- [chapters.json](chapters.json)
