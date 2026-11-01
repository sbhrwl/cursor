# Entry assessment and learning paths
- [interactive-assessment](interactive-assessment.html)
Produce a short, reproducible evidence trail, then choose one concrete practice goal. The assessment is original course guidance. The hands-on artifact matters more than a quiz result.

If you are starting without a configured workspace, complete the four reasoning cases now and return to the hands-on trace after module 02. Follow the recorded demonstration in the meantime. Existing developers can attempt the trace with the supplied source and documented prerequisites.

## Trace the demonstrated behavior

Use the included `operations-hub-01-06.zip`, or the Operations Hub source snapshot from lesson 01.05. In the recording, main is `b11a543939b6c760e45af5b1c78157373a4cdbec`; the implementation change is `c88b4a38b19f50989325efd8a4671a1aabb7f1b8`. A source ZIP has no Git history. Record its supplied revision in your report; do not expect the original Git identifiers to exist in a new repository you initialize from that ZIP.

1. Identify your checkout with `git status --short --branch` and `git rev-parse HEAD` when using a Git clone. For a ZIP, record the archive and supplied revision instead.
2. In Cursor, open `src/handler.ts` with Quick Open. Trace the exact `/health` branch, the unsupported-method return, and the probe exception path. In this Linux setup, Quick Open uses Ctrl+P. Keybindings can be remapped; inspect your own Keyboard Shortcuts settings.
3. Open `test/health.test.ts`. The healthy GET case asserts `cache-control` equals `no-store`. Inspect `withServer`: it constructs an HTTP server with controlled handler dependencies, listens on a dynamically assigned loopback port, and closes it afterward.
4. Run the focused command below from the repository root. The recording reports one pass and zero failures.
5. Separately request the live service after following the documented project startup. The recording shows 200 and `Cache-Control: no-store`. The service was restarted after the implementation in lesson 01.05. The response itself does not identify its Git revision.

```bash
node --import tsx --test --test-name-pattern="healthy GET" test/health.test.ts
curl -i --max-time 2 http://127.0.0.1:3100/health
```

Dependencies must be installed before the test command. The local demo service and its database must be started before the live request. The test's controlled server and the long-running service are distinct.

## Use the four cases

Open `interactive-assessment.html` locally. For each scenario, explain the next action before selecting it. Your first selection is retained until reset/reload; retrying still reveals useful explanations. Download the practice plan to preserve your choices and goal. The page performs no network requests.

- A completion summary needs a relevant diff and actual check output for the current change.
- A refused connection calls for setup/lifecycle investigation before a claim about response contents.
- A saved edit does not reload a process that has no watcher.
- A previous CI success describes the revision checked by that run. Inspect the identifier for the current head.

## Practice priorities

| Evidence gap | Extra practice |
|---|---|
| File navigation or service startup | Modules 02 and 03 |
| Failure interpretation and test scope | Revisit 01.05; modules 11 and 12 |
| Agent summary treated as proof | Modules 04, 05 and 07 |
| Revision/check mismatch | Module 02, then module 20 |

These priorities do not waive prerequisites. Complete the common workspace baseline and follow project dependencies before advanced workflows.

## Deliver your own report

Use `assessment-report-template.md`. Trace HEAD or an unsupported method, inspect the relevant assertions, run the targeted test, and record a live request. For each artifact, mark one level: demonstrated independently, completed with a reference, or needs another attempt. Attach the evidence supporting the rating. A missing prerequisite remains a practice target even if other parts went well.

## Files
- [interactive-assessment.html](https://sbhrwl.github.io/cursor/foundations/01-06-EntryAssessment/interactive-assessment.html)
- [worked-example.md](worked-example.md)
- [practice.md](practice.md)
- [operations-hub-01-06.zip](operations-hub-01-06.zip)
- [assessment-report-template.md](assessment-report-template.md)

- [01-06-entry-assessment-and-learning-paths.en.srt](01-06-entry-assessment-and-learning-paths.en.srt)
- [narration-script.md](narration-script.md)
- [PROMPTS.md](PROMPTS.md)
- [sources-and-credits.md](sources-and-credits.md)
- [source-snapshot.json](source-snapshot.json)
- [chapters.json](chapters.json)
