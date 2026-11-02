# Foundations
- [Start with evidence](01-01-StartWithEvidence/lesson-notes.md)
  - [interactive-checkpoint](https://sbhrwl.github.io/cursor/foundations/01-01-StartWithEvidence/interactive-checkpoint.html)
  - Distinguish `a claim`, `an observation`, and `a justified conclusion`
  - Connect a running behavior to `code`, `a check`, and `a specific revision`.
- [Model, context, tools, and runtime](01-02-ModelContextToolsRuntime/lesson-notes.md)
  - [interactive-diagnostic-map](https://sbhrwl.github.io/cursor/foundations/01-02-ModelContextToolsRuntime/interactive-diagnostic-map.html)
  - We shall be able to choose an `evidence-producing investigation` when an `agent task fails`.
  - Before retrying a failed task, write (Carry forward): 
    - `observed result` → `working hypothesis` → `next check`. 
- [Who owns the decision?](01-03-OwnTheDecision/lesson-notes.md)
  - [interactive-ownership](https://sbhrwl.github.io/cursor/foundations/01-03-OwnTheDecision/interactive-ownership.html)
  - We shall be able to turn an ambiguous feature request into a `bounded engineering brief` with `explicit decisions`, `delegated work`, and `acceptance evidence`.
- [The workflow loop](01-04-WorkflowLoop/lesson-notes.md)
  - [interactive-workflow](https://sbhrwl.github.io/cursor/foundations/01-04-WorkflowLoop/interactive-workflow.html)
  - Recurring workflow
    - `Understand` → `plan` → `build` → `verify` → `integrate`.
    - Return to the step that needs better information when a check fails.
    - A useful loop needs `a signal` and `a stopping condition`.
- [A small change with observable behavior](01-05-ChangeWithObservableBehaviour/lesson-notes.md)
  - [interactive-health-contract](https://sbhrwl.github.io/cursor/foundations/01-05-ChangeWithObservableBehaviour/interactive-health-contract.html)
  - We shall be able to `express a small requirement` as a `response assertion`, `read a meaningful failure`, `guide a bounded Cursor edit`, and `explain the limits of the resulting evidence`.
- [Entry assessment and learning paths](01-06-EntryAssessment/lesson-notes.md)
  - [interactive-assessment](https://sbhrwl.github.io/cursor/foundations/01-06-EntryAssessment/interactive-assessment.html)
  - Produce a short, `reproducible evidence trail`, then `choose one concrete practice goal`.
- [Running the app](#running-the-app)
- Links
  - [Cursor Agent overview](https://cursor.com/docs/agent/overview)
  - [Cursor prompting](https://cursor.com/docs/agent/prompting)
  - [Cursor Cloud Agents](https://cursor.com/docs/cloud-agent)
  - [Cursor Plan Mode](https://cursor.com/docs/agent/plan-mode)
  - [Reviewing and testing](https://cursor.com/learn/reviewing-testing)
  - [OWASP authorization guidance](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html)
## Running the app
- Unzip the zipped file: operations-hub-baseline-b3b306a.zip
- Go to unzipped folder
- Create a copy of `.env.example` to `.env`
  - As i want to use existing postgresql DB
  - `DATABASE_URL=postgresql://gfc_db_01_user:VuxXSPgHW%3F-%7Dp9R1qeF%3Apz2%3E@localhost:5432/operations_hub`
  - Next run `npm run db:init`
    ```
    C:\Git\practice\cursor\foundations\01-02-ModelContextToolsRuntime\operations-hub-baseline-b3b306a\operations-hub>npm run db:init
    
    > operations-hub@0.0.1 db:init
    > node --env-file-if-exists=.env --import tsx scripts/init-db.ts
    ```
- run app `npm run dev`
    ```
    C:\Git\practice\cursor\foundations\01-02-ModelContextToolsRuntime\operations-hub-baseline-b3b306a\operations-hub>npm run dev

    > operations-hub@0.0.1 dev
    > node --env-file-if-exists=.env --import tsx src/server.ts
    
    Operations baseline listening on 3100
    ```
- Endpoints
  - `http://127.0.0.1:3100/health`
  - `http://127.0.0.1:3100/demo/requests`
