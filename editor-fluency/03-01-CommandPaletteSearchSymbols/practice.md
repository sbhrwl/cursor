# Practice — trace the unsupported method response

Keep the checkout unchanged. Use the same starter from lesson 02.06 or your course clone.

1. Locate the `/health` method guard.
2. Find the response status for an unsupported method.
3. Find a test that makes unsupported requests and checks the status.
4. Record each file, line and the actual revision of your checkout. Explain how you found it and what it establishes.
5. Confirm Source Control has no pending changes.

Try without the answer first. Search, symbols, definitions and references are tools; your explanation should connect behavior and verification.

## Hint

Search for `method_not_allowed` or `unsupported /health` across the whole relevant workspace.

## Answer at the filmed source snapshot

- `src/handler.ts:16`: method condition permits GET and HEAD; unsupported methods enter the branch.
- `src/handler.ts:17`: assigns status 405. The branch sets Allow, ends the response, and returns before probing the database.
- `test/health.test.ts:75`: test case starts. Its loop covers POST, PUT, DELETE, PATCH and OPTIONS.
- `test/health.test.ts:83`: asserts status 405; the case also checks allowed methods, no-store, the error body and no probe calls.

Line numbers are specific to the supplied code; inspect your copy. A successful navigation exercise locates the guard and actual assertion and explains their relationship. It does not claim that a newly edited implementation passes tests.
