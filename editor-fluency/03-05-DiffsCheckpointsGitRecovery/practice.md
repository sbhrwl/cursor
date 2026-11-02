# Recovery practice — lesson 03.05

Use the supplied recovery-starter.bundle to create a disposable practice checkout. Its single snapshot contains the committed starting files, including the verified scalar and batch status helpers and a baseline note. It contains no authentication credentials and does not establish a GitHub connection.

## Start locally

    git clone -b main recovery-starter.bundle recovery-practice
    cd recovery-practice
    git remote remove origin
    npm ci
    node --import tsx --test --test-reporter=spec test/request-status.test.ts
    npm run typecheck
    git log -1 --oneline
    git status --short

Use Node.js 22.12 or newer. npm ci needs package-registry access unless the required packages are already cached. The focused status tests do not require the course database. Record the new practice commit shown by Git; it differs from the filmed repository revision because the bundle intentionally contains one clean snapshot.

## Predict, then restore one file

1. Append a sentence to docs/recovery-note.md. Save it.
2. In src/request-status.ts, deliberately change the unknown-value fallback label from Unknown status to No label. Keep the tests unchanged.
3. Inspect git status --short and git diff. Run the focused tests and identify which expectations reject the experiment.
4. Preserve the tracked edits in a patch outside the repository before restoring:

       git diff --binary > ../recovery-practice-before.patch

5. Predict what the following command changes. Identify its source, destination, and path:

       git restore --source=HEAD --worktree -- src/request-status.ts

6. Run it only in your disposable practice checkout. Inspect the source diff and the note diff separately. Verify that the note still contains your sentence, and rerun the focused tests and typecheck.
7. Download your recovery record from interactive-recovery-lab.html. Include the actual revision, exact operation, preserved edit, command results, and one remaining evidence limit.

## Explain the difference

In the interactive model, the implementation has different values in HEAD, the index, and the working tree. Compare restoring the implementation from HEAD with restoring it from the index. Explain why an explicit source matters when staged contents differ from the committed tree.

The model is an explanation of tracked-file state. It does not run Git or connect to your repository.

## Optional Cursor experiment

Open a separate practice clone in Cursor. Establish the current diff before asking Agent to make a small display-label experiment and matching test updates. Inspect the current checkpoint control, preserve work you may want, and compare the actual resulting files after restoration. Record observations of your installed version. Do not assume a file checkpoint reverses terminal, database, or remote actions.
