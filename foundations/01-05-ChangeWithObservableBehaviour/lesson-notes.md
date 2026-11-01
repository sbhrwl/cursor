# A small change with observable behavior
- [interactive-health-contract](interactive-health-contract.html)
By the end of this lesson, you can express a small requirement as a response assertion, read a meaningful failure, guide a bounded Cursor edit, and explain the limits of the resulting evidence.

## The change

Operations Hub's exact `/health` route must send `Cache-Control: no-store` on healthy GET/HEAD responses, probe failures and rejected methods. Existing status, body, `Allow` and dependency-call behavior remain part of the contract. Other routes keep their current header behavior.

## The test-first stopping point

The first Cursor request allows inspection, a lesson branch, test changes and execution. It explicitly leaves production code unchanged. The new assertions produce four failing health test groups and two passing non-health groups. A focused healthy GET run makes the failed assertion readable: the response's `cache-control` header is `undefined`, while the expected value is `no-store`.

An assertion failure stops the remaining statements in that test. In a loop, later iterations may not run. Read the actual failing line before claiming what the red run verified. Rerun after implementing the contract so the remaining assertions can execute.

## Why the implementation is placed there

Set the header as soon as the exact health route matches, before the unsupported-method return and before awaiting the probe. A probe exception then reaches the existing catch block with the header already set. Routes outside that branch do not acquire an application-wide cache policy.

The resulting bounded change is one production line plus eight response assertions. The complete suite has seven tests: six HTTP groups and one database transaction test. Passing those tests is evidence for those cases, not every possible input or deployment.

## Practice

Use `practice.md`, the starting source ZIP and `test-first.patch`. Try the exercise before inspecting the final implementation patch. The standalone HTML exercise asks you to trace an alternative header placement and identify which response paths it would miss.

## Source

The interpretation of the response directive comes from [RFC 9111 §5.2.2.5](https://www.rfc-editor.org/rfc/rfc9111.html#section-5.2.2.5). This lesson introduces a product requirement; it does not claim to have caught an existing client caching an old response. Origin-header checks do not test every cache or establish a privacy guarantee.
