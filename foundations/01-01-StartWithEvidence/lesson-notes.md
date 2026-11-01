# 01.01 — Start with evidence
- [Overview](#overview)
- [Recurring workflow](#recurring-workflow)
- [Demonstration](#demonstration)
- [Follow the evidence](#follow-the-evidence)
- [Checkpoint](#checkpoint)
  - [interactive-checkpoint](https://sbhrwl.github.io/cursor/foundations/01-01-StartWithEvidence/interactive-checkpoint.html)
- [Course destinations](#course-destinations)
- [Demonstration version](#demonstration-version)
- [Files](#files)
## Overview 
- Distinguish `a claim`, `an observation`, and `a justified conclusion`
- Connect a running behavior to `code`, `a check`, and `a specific revision`.
## Recurring workflow
- `Understand → plan → build → verify → integrate`.
- Return to the step that needs better information when a check fails.
- A useful loop needs `a signal` and `a stopping condition`.
## Demonstration
- The demonstrated starting system is
  - API
  - PostgreSQL database
- It is a `development baseline`, `not the finished Operations Hub product`.
  - Organization identifiers alone do not `establish authorization` or `tenant isolation`.
## Follow the evidence

| Observation | What it supports | What it does not establish |
|---|---|---|
| `/demo/requests` returns two synthetic records | The endpoint returned those records on that run | A caller cannot access another organization's data |
| `/health` succeeds after a database query | The service reached PostgreSQL for that query | Approval policy and persistence are correct |
| `Integration test` passes | The exercised transaction/rollback behavior passed | Every planned product requirement is implemented |
| `CI succeeds` at a commit | Those checks passed for that revision in CI | Later untested changes also pass |
| Fresh Cloud Agent startup succeeds | That environment started the API and database on that run | Future changes cannot break startup |

## Checkpoint
- An agent reports: “The approval feature is complete. The server starts and the page looks right.”
  - Write two observations that statement supports.
  - Write two requirements it does not establish.
  - Choose one next check and explain which uncertainty it reduces.
- See [`worked-answer.md`](worked-answer.md) after attempting the checkpoint.
  - The interactive companion is provided as [`interactive-checkpoint.html`](https://sbhrwl.github.io/cursor/foundations/01-01-StartWithEvidence/interactive-checkpoint.html) and runs locally in a browser.
## Course destinations
- **Operations Hub** is a business application with request, approval policy, tenant boundaries, background work and audit history.
- **Evidence Desk** is a service that retrieves authorized sources and provides evidence-backed answers, with evaluations.
- **Engineering Control Plane** is a coordinator with explicit task dependencies, execution state and failure recovery.
- These capabilities will be built in later lessons. The current repositories are starter foundations.
## Demonstration version
- Cursor Desktop 3.19.13, recorded September 6, 2026.
  - Operations Hub main commit: `b3b306ab7bd13091db4780ca5e853f7727be67af`.
  - AgentBox/CI PostgreSQL 17; verified Cloud environment PostgreSQL 16.15.
## Files
- [interactive-checkpoint.html](https://sbhrwl.github.io/cursor/foundations/01-01-StartWithEvidence/interactive-checkpoint.html)
- [worked-answer.md](worked-answer.md)
- [PROMPTS.md](PROMPTS.md)
- [narration-script.md](narration-script.md)
  - [01-01-start-with-evidence.en.srt](01-01-start-with-evidence.en.srt)
- [sources-and-credits.md](sources-and-credits.md)
- [chapters.json](chapters.json)