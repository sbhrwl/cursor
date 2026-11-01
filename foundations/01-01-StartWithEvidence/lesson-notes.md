# 01.01 — Start with evidence
- [interactive-checkpoint](interactive-checkpoint.html)
**Outcome:** distinguish a claim, an observation, and a justified conclusion; connect a running behavior to code, a check, and a specific revision.

The demonstrated starting system is an API and PostgreSQL database. It is a development baseline, not the finished Operations Hub product. Organization identifiers alone do not establish authorization or tenant isolation.

## Follow the evidence

| Observation | What it supports | What it does not establish |
|---|---|---|
| `/demo/requests` returns two synthetic records | The endpoint returned those records on that run | A caller cannot access another organization's data |
| `/health` succeeds after a database query | The service reached PostgreSQL for that query | Approval policy and persistence are correct |
| Integration test passes | The exercised transaction/rollback behavior passed | Every planned product requirement is implemented |
| CI succeeds at a commit | Those checks passed for that revision in CI | Later untested changes also pass |
| Fresh Cloud Agent startup succeeds | That environment started the API and database on that run | Future changes cannot break startup |

## The recurring workflow

Understand → plan → build → verify → integrate. Return to the step that needs better information when a check fails. A useful loop needs a signal and a stopping condition.

## Course destinations

- **Operations Hub:** a business application with requests, approval policy, tenant boundaries, background work and audit history.
- **Evidence Desk:** a service that retrieves authorized sources and provides evidence-backed answers, with evaluations.
- **Engineering Control Plane:** a coordinator with explicit task dependencies, execution state and failure recovery.

These capabilities will be built in later lessons. The current repositories are starter foundations.

## Demonstration version

Cursor Desktop 3.19.13, recorded September 6, 2026. Operations Hub main commit: `b3b306ab7bd13091db4780ca5e853f7727be67af`. AgentBox/CI PostgreSQL 17; verified Cloud environment PostgreSQL 16.15.

## Checkpoint

An agent reports: “The approval feature is complete. The server starts and the page looks right.”

1. Write two observations that statement supports.
2. Write two requirements it does not establish.
3. Choose one next check and explain which uncertainty it reduces.

See `worked-answer.md` after attempting the checkpoint. The interactive companion is provided as `interactive-checkpoint.html` and runs locally in a browser.
