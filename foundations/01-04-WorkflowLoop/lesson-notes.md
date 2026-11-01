# 01.04 — The workflow loop
- [interactive-workflow](interactive-workflow.html)
## Outcome

Use Cursor to take a bounded HTTP behavior change through understand, plan, build, verify, and integrate. Explain the evidence produced at each stage and why a failed observation may send you back.

## The original behavior

Operations Hub initially returns 200 for both GET /health and POST /health. Its handler branches on the URL, without checking the method. The lesson deliberately introduces a method contract; the original observation alone does not establish a security flaw.

## The requested behavior

Read `health-method-contract.md`. GET and HEAD remain supported. HEAD has no body, including when the health probe fails. Other recognized methods at this route return 405 with `Allow: GET, HEAD`, before a database query. Preserve the synthetic listing and unknown-path behavior.

## Work in an inspectable loop

| Stage | Useful question | Artifact |
|---|---|---|
| Understand | What does the current process do? | Original request/response and relevant source |
| Plan | What should change, and how will we observe it? | Bounded contract and test plan |
| Build | Does the diff implement that contract? | Focused changes and tests |
| Verify | Which checks could expose a wrong assumption? | Test, type-check, runtime and review evidence |
| Integrate | Which reviewed revision are we accepting? | Commit, pull request and corresponding CI |

These are course workflow labels. They do not prescribe a particular Cursor mode or require five separate agent conversations.

## A useful test seam

The observed Cursor plan proposes extracting the request handler and injecting the health probe and demo-list functions. Tests can then use controlled functions while still sending real HTTP requests to an ephemeral local test server. This checks status, headers, bodies and whether the dependency was called. It complements the existing real-database test.

A test seam should earn its complexity. This example does not justify a framework migration or a general dependency-injection container.

## Read evidence narrowly

A passing HTTP test with a fake probe does not prove real database connectivity. A database rollback test does not prove endpoint method handling. A request to a running service describes that process, which may still have old code loaded. CI evidence belongs to the workflow, jobs, environment and revision that actually ran.

The first Cursor planning request hit a provider connection error. The retained retry completed the plan. Application changes are not a remedy for an observed model-provider connection failure.

## Practice

Open `interactive-workflow.html`. Choose the next useful action for each scenario and explain what it would establish. Then repeat a bounded change in your own isolated branch, keeping the baseline observation and final result together.

## Research

- [HTTP 405 — RFC 9110 §15.5.6](https://www.rfc-editor.org/rfc/rfc9110.html#name-405-method-not-allowed)
- [Node 22 HTTP API](https://github.com/nodejs/node/blob/v22.x/doc/api/http.md)
- [Node 22 test runner](https://github.com/nodejs/node/blob/v22.x/doc/api/test.md)
- [Cursor Agent](https://cursor.com/docs/agent/overview)
- [GitHub workflow run history](https://docs.github.com/en/actions/how-tos/monitor-workflows/view-workflow-run-history)

The release includes a separate evidence record for the actual implementation, tests and integrated revision.


## CI annotation visible in the recording
The successful GitHub job includes a runner warning about the Node runtime used by the pinned checkout/setup-node actions. This is distinct from the application Node version and from the seven passing tests. The warning is retained in the footage; this bounded endpoint change does not upgrade those action pins. Revisit supported action versions during the course CI maintenance workflow.
