# Hands-on transfer

Complete the shared workspace setup before executing these commands. If your workspace is not ready, do the interactive cases first and revisit this exercise after module02.

Choose one path. Before running a command, predict the status, header, body and probe behavior from the code. Then compare your prediction with actual results.

## Option A — HEAD

```bash
node --import tsx --test --test-name-pattern="healthy HEAD" test/health.test.ts
curl -I --max-time 2 http://127.0.0.1:3100/health
```

Inspect the healthy HEAD test's status, content type, cache directive, empty-body and probe-count assertions. The controlled probe count does not come from the live curl response. Record the distinction in your report.

## Option B — unsupported method

```bash
node --import tsx --test --test-name-pattern="unsupported" test/health.test.ts
curl -i --max-time 2 -X POST http://127.0.0.1:3100/health
```

Inspect the grouped test. It checks multiple rejected methods, the required headers, the error body and zero probe calls. The single live POST checks one request to the running service. Do not call these equivalent coverage.

## Review your artifact

The goal is a reproducible report, not a source edit. Keep these claims separate:

- What you predicted from the handler and its control flow.
- What the assertions checked in the controlled server.
- What you observed from the live process.
- What you can establish about the checkout and running version.

Use one of the three rubric levels independently for each part. Attach evidence, then choose a practice task that addresses a specific gap. Before integrating an actual code change, return to the broader relevant test/typecheck/CI workflow.
