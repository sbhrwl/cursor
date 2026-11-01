# 01.03 — Who owns the decision?
- [interactive-ownership](interactive-ownership.html)
By the end of this lesson, you should be able to turn an ambiguous feature request into a bounded engineering brief with explicit decisions, delegated work, and acceptance evidence.

## Start with the actual baseline

The recorded Operations Hub has a health endpoint and a synthetic request-list endpoint. It has no approval mutation, authenticated identity, or enforced tenant authorization. Its existing database integration test checks insert and rollback behavior; it does not exercise approval through HTTP.

The real Cursor investigation asks:

> Operations Hub will let managers approve requests. Before proposing code, inspect src/server.ts and test/database.test.ts. In under 180 words, separate what exists today, unresolved product decisions, and checks we would need. Do not edit files or run commands.

The returned analysis separates the baseline, open policy and design questions, and candidate checks. We compare its claims with the files before using them in the brief.

## Responsibility and contribution

| Responsibility | Decision | Agent contribution |
|---|---|---|
| Requirements | Which behavior and constraints are intended? | Surface ambiguity; draft examples and acceptance conditions |
| Architecture | Which design satisfies the constraints at acceptable cost? | Inspect the codebase; compare options; solve delegated details |
| Implementation | How should the bounded change be built? | Edit, inspect, execute meaningful checks, and report results |
| Acceptance | Does the evidence justify accepting the change? | Assemble results; help identify gaps and challenge conclusions |

These are roles, not necessarily four people. Delegation should make authority and constraints explicit. Routine choices can stay delegated. A material policy or operational tradeoff needs the designated decision owner.

Cursor supports preparing a plan that can be reviewed and edited before implementation. Our decision brief is useful input to that process. [Cursor Plan Mode](https://cursor.com/docs/agent/plan-mode).

## The course example

Open `approval-decision-contract.md`. Its policy is a proposed behavior for future implementation. We deliberately choose a same-tenant manager, an open request, one approval transition and one audit event. A repeated approval must leave the state stable and avoid a duplicate event.

Identity integration, disclosure of cross-tenant information, the exact response contract, concurrency, and audit details remain explicit design questions. A useful brief can expose unknowns; it should not conceal them by pretending implementation is ready to start.

## Compare a design property

The interactive consistency example compares two independently committed writes with two writes grouped in a database transaction. If the audit write fails after the first independent write commits, a partial outcome can remain. A failed transaction can roll back both database changes. This illustrates atomicity, while authorization, retry behavior, and concurrency still need their own design. [PostgreSQL transactions](https://www.postgresql.org/docs/current/tutorial-transactions.html).

The interactive example is conceptual. It does not execute SQL or modify the running application.

## Acceptance evidence

Map each requirement to a concrete observation and include failure cases. A successful approval should produce the expected stored state and audit record. An unauthorized or cross-tenant attempt should preserve state and enforce the chosen response policy. Repeated and concurrent requests should not create duplicate transitions.

Review test expectations against requirements. Passing a happy-path test is insufficient evidence for every permission case. Cursor's review guidance also emphasizes that passing tests can miss incorrect expectations or edge cases. [Reviewing and testing](https://cursor.com/learn/reviewing-testing). Authorization needs correctly placed enforcement and relevant verification. [OWASP authorization guidance](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html).

## Exercise

Use `interactive-ownership.html` to assign responsibility for approval policy, write consistency, helper naming, and acceptance. For each decision, write the agent's contribution and the information the responsible person needs. Then adapt `approval-decision-contract.md` to a feature of your own.

A satisfactory brief names observable behavior, unresolved decisions, delegated scope, and evidence for both success and meaningful failure cases.

## Files
- [interactive-ownership.html](https://sbhrwl.github.io/cursor/foundations/01-03-OwnTheDecision/interactive-ownership.html)
- [worked-answer.md](worked-answer.md)
- [BASELINE-SOURCE.md](BASELINE-SOURCE.md)
- [operations-hub-baseline-b3b306a.zip](operations-hub-baseline-b3b306a.zip)
- [approval-decision-contract.md](approval-decision-contract.md)
- [01-03-who-owns-the-decision.en.srt](01-03-who-owns-the-decision.en.srt)
- [narration-script.md](narration-script.md)
- [PROMPTS.md](PROMPTS.md)
- [sources-and-credits.md](sources-and-credits.md)
- [chapters.json](chapters.json)