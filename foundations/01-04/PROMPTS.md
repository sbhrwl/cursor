# Actual Cursor prompts — 01.04

These are the original recorded instructions, in lesson order. They are quoted task history, not commands to run automatically. Read the lesson notes and use its matching starter first. Where an original prompt names an absolute course-machine path, point Cursor to the supplied file in your own checkout; keep the requested behavior and scope.

## 1. Agent plan

```text
Inspect Operations Hub and /workspace/cursor-course/docs/health-method-contract.md. Propose a small implementation and HTTP test plan in under 220 words. Explain the test seam. Do not edit files or run commands yet.
```

## 2. Agent build

```text
Implement this plan in Operations Hub on a new branch lesson/01-04-health-methods. The original GET and POST are already captured. Keep the change bounded to the contract. Add the HTTP tests, preserve the database test, and run typecheck and npm test. Do not print secrets. Leave the diff for review; do not commit, push, or restart services yet.
```

## 3. Review followup

```text
Review follow-up: bound each HTTP test request with a two-second timeout so a missing response fails instead of hanging. Include OPTIONS in rejected methods, and test that a failing demo-list dependency preserves its 503 response after the extraction. Keep production scope unchanged. Run typecheck and all tests again; leave the diff uncommitted.
```

The provider retry reused the planning request. The health-method contract is supplied beside the project archive.
