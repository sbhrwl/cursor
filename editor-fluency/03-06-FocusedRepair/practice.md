# Practice — repair one display decision

Start from the supplied `focused-repair-starter.bundle`. The bug is intentional. Use a new practice folder so that your other work remains available.

```sh
git clone -b main focused-repair-starter.bundle focused-repair-practice
cd focused-repair-practice
git remote remove origin
git switch -c practice/zero-count
npm ci
node --import tsx --test --test-reporter=spec test/queue-summary.test.ts
npm run typecheck
node --watch --import tsx src/preview-server.ts
```

Open [the preview](http://127.0.0.1:3106). The three synthetic snapshots have pending counts of `4`, `0`, and `null`. The prepared implementation incorrectly displays `Not loaded` for zero. No database or external service is needed for this preview. Use another terminal for tests while the preview server runs.

1. Record the exact input, observed display, expected display, and starting commit.
2. Search for the visible label in Cursor. Trace the value from the preview server through `summarizeQueue` to the rendered card.
3. Add a regression test for zero. Keep all five existing queue tests. Run the tests and confirm the new test fails for the reported mismatch.
4. Select the responsible assignment. Request a focused repair with explicit behavior for zero, positive counts, and null. Review the proposal before accepting it.
5. Inspect the actual Git diff. Explain every changed file and why the patch preserves the surrounding fields and navigation.
6. Run the queue tests, the earlier request-status tests, and the type check. Refresh the preview and try the support queue link.
7. Download a completed repair record from the interactive companion. Include evidence and limits, not just a statement that the task is done.

Run the relevant checks after your repair:

```sh
node --import tsx --test --test-reporter=spec test/queue-summary.test.ts test/request-status.test.ts
npm run typecheck
git --no-pager diff --stat
git --no-pager diff
```

Challenge your repair with a positive count of `1`. Explain which checks would fail if the implementation simply returned `'0'` for every input. The prepared input contract accepts nonnegative integers and null; adding runtime validation or changing data fetching is a separate task.

Completion evidence: a meaningful failing-before/passing-after regression, a bounded diff, a corrected preview, preserved neighboring behavior, and a repair record another engineer can assess. Stop your preview server with Ctrl+C when finished.
