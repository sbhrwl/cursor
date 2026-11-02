# Editing-tool choice practice

The supplied Git bundle contains a single practice snapshot. Its history differs from the instructor checkout; offline-snapshot.json records both revisions.

    git clone -b main tool-choice-starter.bundle tool-choice-practice
    cd tool-choice-practice
    git remote remove origin
    npm ci
    node --import tsx --test test/request-status.test.ts
    npm run typecheck

Use Node.js 22.12 or later within the Node 22 line. These focused tests need no database. Other starter tests belong to earlier lessons and have separate setup requirements.

The initial five tests should pass. First reproduce the lesson's comment correction and batch-label behavior. Choose direct editing, Inline Edit, or Agent deliberately; explain which work the tool helps perform.

For the independent exercise, add a batch helper that reuses canApproveRequest:

- Input: a readonly array of role strings.
- Output: a boolean array in the same order.
- Preserve repeated values and return an empty array for empty input.
- Leave the input and the scalar permission policy unchanged.
- Keep exact matching: reviewer is permitted; REVIEWER, padded values, requester, admin, and an empty role are not.

Define expected values before editing. Include mixed roles and a frozen input array in your tests. Inspect any generated tests for assumptions that differ from the stated policy.

Submit the code and tests, the before/after diff, relevant command results, and a short tool-choice record. Include one remaining limit of your evidence.

The instructor's observed-solution.patch reproduces the batch-label demonstration, including the comment correction. It does not solve the independent permission-batch exercise.
