# Worked example — recorded GET trace

This is the instructor's observed example, not a prefilled claim about your computer.

- Checkout: clean main, `b11a543939b6c760e45af5b1c78157373a4cdbec`.
- Implementation: `src/handler.ts`, header set at the start of the exact `/health` branch, before the method guard and probe await.
- Controlled test: `test/health.test.ts`, healthy GET case. `withServer` starts an isolated HTTP server with controlled dependencies.
- Command: `node --import tsx --test --test-name-pattern="healthy GET" test/health.test.ts`.
- Result: one pass, zero failures. This focused run does not substitute for the full suite.
- Live command: `curl -i --max-time 2 http://127.0.0.1:3100/health`.
- Live result: 200 with `Cache-Control: no-store` and existing JSON metadata.
- Startup context: course service was restarted after the implementation in lesson 01.05. No handler changes were made for this assessment.
- Limits: response metadata does not identify a source commit; a clean working tree does not prove correctness; one live GET does not check every response path or deployment cache.

For the independent transfer, choose HEAD or a rejected method and produce your own report.
