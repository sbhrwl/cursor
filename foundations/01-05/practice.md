# Practice — make the response observable

Start with `operations-hub-01-05-start.zip`, the tracked source at main revision `b6747c5f38b8c1c540e808b173fef6814ecf3280`. It contains placeholder environment documentation, not the instructor's credentials or Git history. Install the documented dependencies. The focused HTTP tests use controlled dependencies and need no live database.

1. Read `health-cache-contract.md`. Before editing, explain where the header must be present and which routes should remain unchanged.
2. Ask Cursor to add externally observable header assertions while leaving production code unchanged. Compare your proposed assertions with `test-first.patch` only after your own attempt.
3. Run `node --import tsx --test test/health.test.ts`. Inspect the missing-header failure. Identify assertions that did not run because an earlier assertion threw.
4. Preserve your failing test state. Implement the smallest change that covers the health paths, including early returns and probe exceptions.
5. Rerun the focused tests, then follow the repository README to configure the database and run `npm run typecheck` and `npm test`.
6. Restart the service you intend to inspect and use `curl -i` and `curl -I` to inspect the actual headers. Explain which cases are proven by controlled tests and which by your live request.
7. Review the diff. Keep the revision and verification results together.

## Using the supplied test patch

From the unpacked `operations-hub` directory, `git apply --check /path/to/test-first.patch` verifies that the patch matches. Then `git apply /path/to/test-first.patch` applies the new expectations. A Git repository is not required for applying the patch to the files. This state is expected to fail four health test groups while the two non-health groups pass. Do not call that a finished implementation.

## Completion questions

- Why is a connection error different from an assertion about a missing response header?
- Which path returns before the health probe? Which path jumps to the catch block?
- Why does a failed assertion limit what you can claim about later assertions?
- What does checking the origin's header leave untested about caches?
