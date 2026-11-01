# Operations Hub — health cache contract

## Outcome

Every response from the exact `/health` route sends `Cache-Control: no-store`.

- Healthy GET and HEAD: retain status 200, existing metadata, and an empty HEAD body.
- Failed health probe: retain status 503, existing JSON for GET, and an empty HEAD body.
- Unsupported methods: retain status 405 and `Allow: GET, HEAD`; do not call the health probe.
- Keep `/demo/requests` and unknown paths unchanged. The new header is scoped to `/health`.

## Evidence before implementation

Start from the previous lesson's clean main revision. Capture the actual headers. Add externally observable HTTP assertions using the existing test seam. Run the health test file before changing production code. Read the assertion failure: is the header missing, or did the test fail to reach the handler? Retain that failing test state.

## Bounded implementation

Use the existing handler and dependencies. No new package, framework migration, route generalization, database schema change or application-wide cache policy. Place the header so it survives each health response path, including an exception from the health probe.

## Completion evidence

Review the diff, run type checking and the complete test suite, restart the actual service, and inspect live GET/HEAD/POST headers. Record which failure cases are covered by controlled-dependency tests. Preserve the commit and the CI result for that revision.

## Meaning and limits

This is a new course product requirement. We have not demonstrated an existing client caching the previous response. The directive tells compliant caches not to retain or reuse this exchange; it is not a privacy guarantee. Checking the origin's header does not test every browser or proxy.

Source: [RFC 9111 §5.2.2.5](https://www.rfc-editor.org/rfc/rfc9111.html#section-5.2.2.5).
