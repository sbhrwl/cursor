# 03.02 — Inspect, partially accept, and reject Tab suggestions
- [Overview](#overview)
  - [interactive-tab-lab](https://sbhrwl.github.io/cursor/editor-fluency/03-02-InspectTabSuggestions/interactive-tab-lab.html)
  - [Cursor Tab completion](https://cursor.com/help/ai-features/tab)
  - [Cursor keyboard shortcuts](https://cursor.com/docs/reference/keyboard-shortcuts)
- [The exercise contract](#the-exercise-contract)
- [The controls used](#the-controls-used)
- [A useful editing loop](#a-useful-editing-loop)
- [References](#references)
- [Files](#files)
## Overview
- Use Cursor Tab to make a bounded edit while keeping responsibility for its behavior.
- The recorded environment uses Cursor 3.19.13 on Linux.
- Suggestions are variable; your completion does not need to match the recording.
## The exercise contract
- `requestStatusLabel(status: string)` must return:

| Exact input | Required output |
| --- | --- |
| `open` | `Awaiting review` |
| `approved` | `Approved` |
| Any other string | `Unknown status` |

- The exercise deliberately excludes trimming and case conversion.
  - `OPEN` and ` open ` are unknown values.
  - These choices define this exercise; they are not universal product requirements.
- The initial implementation returns the input unchanged.
  - Three prepared tests fail against that stub.
  - The helper is not yet connected to a live UI or endpoint.
## The controls used

| Intent | Linux control | Important distinction |
| --- | --- | --- |
| Accept the current suggestion | Tab | A following suggestion is a new decision. |
| Accept incrementally | Ctrl + Right Arrow | Enable **Cursor Settings → Tab → Partial Accepts**. Punctuation can form its own acceptance boundary. |
| Dismiss a suggestion | Escape or keep typing | Your existing typed edit remains. This is not Undo. |
| Inspect or pause Tab | Cursor Tab status control | Read the active state and scope. |

- During rehearsal, Partial Accepts was disabled.
  - Ctrl + Right Arrow moved the caret instead of accepting the proposal.
  - With the setting enabled and a suggestion present, incremental acceptance worked.
- Inspect settings, focus, and installed keybindings when behavior differs.
  - Do not repeatedly press a key without reading the resulting editor state.
## A useful editing loop
- Define a small behavior and inspect its relevant checks.
- Read the actual gray proposal, including its scope and surrounding code.
- Accept, partially accept, dismiss, or manually revise it.
- Inspect the diff as ordinary code.
  - Look for unrequested changes.
- Save and run the focused tests and type check.
- Acceptance is not evidence of correctness.
  - A green type check also does not establish the intended labels.
  - The focused tests and the type check answer different questions.
```sh
node --import tsx --test test/request-status.test.ts
npm run typecheck
git diff -- src/request-status.ts
git status --short
```
- The browser companion is an original course exercise.
  - It evaluates the same example inputs with exact matching and with normalization so you can observe where the results differ.
  - It does not imitate Cursor or generate model suggestions.
  - Download your acceptance record before closing; the page does not automatically save entries.
## References
- [Cursor Tab completion](https://cursor.com/help/ai-features/tab)
- [Cursor keyboard shortcuts](https://cursor.com/docs/reference/keyboard-shortcuts)
- Primary reference checked September 7, 2026.
  - Installed settings and recorded behavior are noted separately from documentation.
## Files
- [interactive-tab-lab.html](https://sbhrwl.github.io/cursor/editor-fluency/03-02-InspectTabSuggestions/interactive-tab-lab.html)
- [practice.md](practice.md)
- [observed-tab-acceptance-record.md](observed-tab-acceptance-record.md)
- [observed-solution.patch](observed-solution.patch)
- [tab-status-starter.bundle](tab-status-starter.bundle)
- [offline-snapshot.json](offline-snapshot.json)
- [PROMPTS.md](PROMPTS.md)
- [narration-script.md](narration-script.md)
  - [03-02-inspect-partially-accept-and-reject-tab-suggestions.en.srt](03-02-inspect-partially-accept-and-reject-tab-suggestions.en.srt)
- [sources-and-credits.md](sources-and-credits.md)
- [chapters.json](chapters.json)
