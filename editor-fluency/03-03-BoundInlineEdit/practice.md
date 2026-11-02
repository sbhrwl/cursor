# Bounded Inline Edit practice

The supplied bundle is a single practice snapshot with separate history from the instructor repository. Its provenance and hash are in offline-snapshot.json.

    git clone -b main inline-edit-starter.bundle inline-practice
    cd inline-practice
    git remote remove origin
    npm ci
    node --import tsx --test test/request-status.test.ts

Use Node.js 22.12 or later in the Node 22 line for this baseline. The focused tests need no database. Other tests in the starter cover earlier course material and require their own setup.

The starting snapshot has four passing tests and one deliberately failing test for the missing rejected label. Reproduce the lesson's bounded change first. Keep the permission helper unchanged and verify all five tests plus npm run typecheck.

Then make an independent change:

1. Define one additional exact display label, such as archived → Archived.
2. Add tests for the exact value, uppercase, and padded versions before editing.
3. Select the display helper and relevant comment. State the intended change, preserved behavior, and excluded work.
4. Inspect the generated proposal and the actual Git diff. Reject or refine any unrelated change.
5. Run the relevant tests and type check. Record their actual results.

Submit your changed code and tests, a before/after diff, and a short scope record. Explain one preserved behavior and how you checked it. Do not count a passing type check as evidence for all product behavior.

If you need the instructor's completed demonstration, inspect observed-solution.patch after trying the exercise. It addresses the rejected case, not your independent archived case.
