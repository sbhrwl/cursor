# 03.05 — Inspect diffs and distinguish checkpoints from Git recovery
- [Overview](#overview)
  - [interactive-recovery-lab](https://sbhrwl.github.io/cursor/editor-fluency/03-05-DiffsCheckpointsGitRecovery/interactive-recovery-lab.html)
- [The recorded experiment](#the-recorded-experiment)
- [The Git comparison](#the-git-comparison)
- [Source, destination, and paths](#source-destination-and-paths)
- [Practice and evidence](#practice-and-evidence)
- [Files](#files)
## Overview
- By the end, explain the state a recovery operation reads, the state it replaces, and the evidence needed afterward.
## The recorded experiment
- We start from a dedicated Operations Hub checkout at `f8a70116471a2529763946f2b3bacebc600c793f`.
- A manual sentence already exists in `docs/recovery-note.md` before the Agent request.
- Agent changes the exact open-status label from `Awaiting review` to `Needs review`, updates the matching comment and test expectations, and creates a marker through the terminal outside the repository.
- The proposal's nine tests pass because implementation and expected values describe the same experiment.
  - Passing tests support those expectations; they do not decide whether the experiment should be retained.
- In the installed Cursor interface, the curved arrow on the request opens a checkpoint confirmation.
  - After continuing, source and tests match their pre-request bytes, the earlier manual note remains, HEAD and the index are unchanged, and the external marker remains.
  - The conversation also retains the earlier report, which no longer describes the current files.
- These are observations of this prepared state.
  - They are not a promise that arbitrary manual edits, commands, services, or remote operations are recovered in the same way.
## The Git comparison
- A separate manual edit replaces the unknown-value fallback with `No label` while tests still expect `Unknown status`.
  - The full focused suite then has six passing tests and three failures.
- Preserve the diff before replacing file contents:
```sh
git diff --binary > ../before-git-restore.patch
git restore --source=HEAD --worktree -- src/request-status.ts
```
- The command explicitly reads the committed tree, replaces only the named working file, and leaves the index alone.
- Inspect status and diffs, read the separate note, and rerun the checks.
  - An empty source diff is evidence of comparison with the index; our independent snapshots also establish that HEAD and the index did not change during this experiment.
```sh
git status --short
git diff -- src/request-status.ts
cat docs/recovery-note.md
node --import tsx --test --test-reporter=spec test/request-status.test.ts
npm run typecheck
```
## Source, destination, and paths

| Choice | Meaning in the demonstrated command |
| --- | --- |
| Source | HEAD: the current committed tree |
| Destination | Working tree: the file you edit |
| Paths | src/request-status.ts only |
| Staging area | Left unchanged |
| Separate manual note | Left unchanged |
| External command effects | Checked independently |

- Without an explicit source, restoring the working tree normally reads the index.
  - If the staged contents differ from HEAD, these choices produce different results.
- The supplied original HTML model lets you compare both sources and explicit staging destinations for two tracked example files.
  - It does not execute Git.
  - Its supported combinations were compared with real Git in twelve disposable fixtures.
## Practice and evidence
- Follow [`practice.md`](practice.md) with the single-snapshot `recovery-starter.bundle`.
  - Its practice revision differs from the recording because it intentionally excludes earlier repository history.
  - Record that clone's own baseline.
  - Make two separate edits, preserve a patch, predict one-path recovery, execute it, and verify that the other edit remains.
- The downloadable recovery record has five fields: starting revision, operation, intended scope, observed result, and checks.
  - Keep claims tied to observations, especially when a conversation contains a report from before recovery.
## Files
- [interactive-recovery-lab.html](https://sbhrwl.github.io/cursor/editor-fluency/03-05-DiffsCheckpointsGitRecovery/interactive-recovery-lab.html)
- [practice.md](practice.md)
- [recorded-recovery-record.md](recorded-recovery-record.md)
- [before-checkpoint.patch](before-checkpoint.patch)
- [before-git-restore.patch](before-git-restore.patch)
- [manual-note-before-agent.patch](manual-note-before-agent.patch)
- [recovery-starter.bundle](recovery-starter.bundle)
- [offline-snapshot.json](offline-snapshot.json)
- [PROMPTS.md](PROMPTS.md)
- [narration-script.md](narration-script.md)
  - [03-05-inspect-diffs-and-distinguish-checkpoints-from-git-recovery.en.srt](03-05-inspect-diffs-and-distinguish-checkpoints-from-git-recovery.en.srt)
- [sources-and-credits.md](sources-and-credits.md)
- [chapters.json](chapters.json)
