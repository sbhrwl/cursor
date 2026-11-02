# 03.03 — Bound an Inline Edit to the intended change
- [Overview](#overview)
  - [interactive-inline-edit-lab](https://sbhrwl.github.io/cursor/editor-fluency/03-03-BoundInlineEdit/interactive-inline-edit-lab.html)
  - [Cursor Inline Edit](https://cursor.com/help/ai-features/inline-edit)
- [The requirement](#the-requirement)
- [The recorded workflow](#the-recorded-workflow)
- [A concrete instruction](#a-concrete-instruction)
- [Reference](#reference)
- [Files](#files)
## Overview
- Turn a narrow requirement into a reviewed change in Cursor.
- The recorded environment uses Cursor 3.19.13 on Linux.
- The selected range communicates an editing target; it is not an enforcement or security boundary.
## The requirement
- Add exactly `rejected` → `Rejected` to `requestStatusLabel`.
- Preserve the existing open and approved labels, exact matching, and Unknown status for unknown strings.
- Do not trim or change case.
- Leave `canApproveRequest` unchanged.
- These helpers and tests are prepared course exercises.
  - The permission helper makes a separate responsibility visible; this lesson does not implement or verify a complete authorization system.
## The recorded workflow
- Read the implementation and independent tests.
  - Before the change, four tests pass and the new exact-label test fails.
- Select the display helper and its contract comments, leaving the permission helper outside the selection.
- Open Inline Edit with **Ctrl + K** on the demonstrated Linux installation.
- State the change, invariants, exclusions, and any justified structure preference.
- Submit and inspect the actual proposal.
  - The demonstration changes the contract comment and adds one exact branch.
- Accept after review and save.
- Inspect the Git diff and changed-file set, then run the status tests and TypeScript check.
- The demonstration finishes with five passing tests, a successful type check, one modified source file, and a byte-for-byte unchanged permission helper.
  - Saving and accepting do not create a Git commit.
## A concrete instruction
```
> Update only the selected display helper and its contract comment: exact rejected must return Rejected. Preserve the open and approved labels, exact matching, and Unknown status fallback. No trimming or case conversion. Leave canApproveRequest and all other files unchanged. Keep the explicit branches.
```
- This is an exercise-specific instruction.
  - Your generated result can differ.
  - Inspect its behavior and actual scope before accepting it.
  - Use installed controls and bindings when your version differs.
```sh
git status --short
git diff -- src/request-status.ts
node --import tsx --test test/request-status.test.ts
npm run typecheck
```
- Review both the requested difference and the behavior that must remain unchanged.
  - A type check alone does not establish the required labels.
  - Helper tests do not demonstrate a live interface or full system correctness.
- The supplied HTML lab is original course material.
  - Its selection and candidate-diff exercises are not a simulated Cursor response.
  - Download your scope record before closing; entries are not automatically saved.
## Reference
- [Cursor Inline Edit](https://cursor.com/help/ai-features/inline-edit), checked September 7, 2026.
  - Installed controls and recorded outcomes are separate observations.
## Files
- [interactive-inline-edit-lab.html](https://sbhrwl.github.io/cursor/editor-fluency/03-03-BoundInlineEdit/interactive-inline-edit-lab.html)
- [practice.md](practice.md)
- [inline-edit-scope-record.md](inline-edit-scope-record.md)
- [observed-solution.patch](observed-solution.patch)
- [inline-edit-starter.bundle](inline-edit-starter.bundle)
- [offline-snapshot.json](offline-snapshot.json)
- [PROMPTS.md](PROMPTS.md)
- [narration-script.md](narration-script.md)
  - [03-03-bound-an-inline-edit-to-the-intended-change.en.srt](03-03-bound-an-inline-edit-to-the-intended-change.en.srt)
- [sources-and-credits.md](sources-and-credits.md)
- [chapters.json](chapters.json)
