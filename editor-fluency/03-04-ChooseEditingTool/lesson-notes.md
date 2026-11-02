# 03.04 — Choose direct editing, Inline Edit, or Agent
- [Overview](#overview)
  - [interactive-tool-choice-lab](https://sbhrwl.github.io/cursor/editor-fluency/03-04-ChooseEditingTool/interactive-tool-choice-lab.html)
- [Demonstration](#demonstration)
- [Reviewing tests generated with the implementation](#reviewing-tests-generated-with-the-implementation)
- [Companion](#companion)
- [Version and evidence](#version-and-evidence)
- [Files](#files)
## Overview
- Choose assistance according to the understanding, editing, and verification work it helps perform.

| Starting situation | A reasonable route |
| --- | --- |
| You know the exact small edit | Direct editing |
| You can state a bounded transformation in a known selection | Direct editing or Inline Edit |
| Reading code, changing files, and running checks benefit from coordination | Agent |
| The desired behavior is unclear | Investigate and clarify before implementing |

- These are judgment calls.
  - File count alone does not choose a tool.
  - A known change in two files can be straightforward to edit directly; a sensitive one-line change may need substantial investigation.
## Demonstration
- The isolated practice checkout begins at `ed89838e2e5c42e77a719289b942dfe297c70565`, with five passing scalar-label and permission tests.
- Correct the prepared comment typo, `lables` → `labels`, directly in the editor.
  - Inspect the diff to confirm that only the comment changed.
- Revisit the actual Inline Edit footage from lesson 03.03.
  - The selected helper and contract comment were a concrete target for an exact label change.
- Ask the native Cursor Agent to add `requestStatusLabels(statuses: readonly string[]): string[]`.
  - Reuse `requestStatusLabel`; preserve order, duplicates, empty input, input immutability, scalar behavior, and the permission helper.
- Inspect the generated implementation and tests against the requirements.
  - The observed implementation uses `statuses.map(requestStatusLabel)`.
- Keep the reviewed changes and inspect the actual two-file diff.
- Run the status tests and TypeScript check in the checkout.
- Observed result: nine tests passed, consisting of five existing tests and four new batch tests.
  - The TypeScript check exited successfully.
  - The changed files were `src/request-status.ts` and `test/request-status.test.ts`.
  - No commit or push was part of this demonstration.
## Reviewing tests generated with the implementation
- Read expected values, rather than relying on test names.
- Check mixed exact and unknown values, repeated values, an empty array, and a frozen input array.
- Compare these expectations with the requirement you established before generating code.
  - Implementation and tests can share an incorrect assumption.
- A frozen input is one concrete way to check for unwanted mutation in this bounded helper.
  - This does not prove a complete authorization system or an application user interface.
## Companion
- Open [interactive-tool-choice-lab](https://sbhrwl.github.io/cursor/editor-fluency/03-04-ChooseEditingTool/interactive-tool-choice-lab.html).
  - It contains four decision scenarios, a tradeoff table, an expected-label calculator, a downloadable decision record, and independent practice checkpoints.
- The calculator is an original expected-value model.
  - It does not execute the repository's code or call an AI model.
## Version and evidence
- Recorded in the isolated Linux course environment with Cursor 3.19.13.
- The observed Agent panel used the existing High Fast selection.
  - Interface labels, model behavior, waiting times, and shortcuts can differ across versions or account settings.
- The earlier comment edit remains part of the final working-tree diff.
  - Keep that provenance separate from the changes the Agent added.
## Files
- [interactive-tool-choice-lab.html](https://sbhrwl.github.io/cursor/editor-fluency/03-04-ChooseEditingTool/interactive-tool-choice-lab.html)
- [practice.md](practice.md)
- [editing-tool-decision-record.md](editing-tool-decision-record.md)
- [observed-solution.patch](observed-solution.patch)
- [tool-choice-starter.bundle](tool-choice-starter.bundle)
- [offline-snapshot.json](offline-snapshot.json)
- [PROMPTS.md](PROMPTS.md)
- [narration-script.md](narration-script.md)
  - [03-04-choose-direct-editing-inline-edit-or-agent.en.srt](03-04-choose-direct-editing-inline-edit-or-agent.en.srt)
- [sources-and-credits.md](sources-and-credits.md)
- [chapters.json](chapters.json)
