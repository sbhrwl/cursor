# Operations Hub — health method contract

Status: proposed lesson change. The captured baseline accepts POST /health with 200.

## Behavior to deliver

- `/health` supports GET and HEAD. The healthy response remains 200 with the existing health metadata. HEAD has no response body.
- When the database probe fails, GET and HEAD return 503; HEAD still has no body.
- A recognized but unsupported method at `/health`, such as POST, returns 405 and `Allow: GET, HEAD`. Return a bounded JSON error and do not query the database on this rejection path.
- Preserve `/demo/requests` and the existing unknown-path 404 behavior. Do not add approval, authentication, new dependencies, or a framework migration.

## Evidence required

1. Capture the original GET and POST results before changing code.
2. Test observable HTTP status, headers and body. Include healthy GET, healthy HEAD, failing probe, unsupported methods, and unknown paths.
3. Verify the rejected method does not call the database probe. Keep existing database tests passing.
4. Run type checking and the full test command. Recheck the running service after restarting the changed process.
5. Review the diff, commit a bounded change, and verify the same revision in GitHub Actions before integrating the private course pull request.

## Implementation freedom

Inspect the existing code first. Choose the smallest maintainable design that can be tested without binding tests to port 3100 or requiring the real database for every HTTP case. A small handler extraction is acceptable if it earns its complexity. Explain that choice before editing.

## Completion report

State the changed files, commands and results, revision, CI result, and any untested cases. Passing tests support the checked behavior; they do not prove every possible deployment state.

## Source

[RFC 9110, section 15.5.6 — 405 Method Not Allowed](https://www.rfc-editor.org/rfc/rfc9110.html#name-405-method-not-allowed) requires the Allow field in a 405 response. GET/HEAD support here is the course's explicit endpoint contract.
