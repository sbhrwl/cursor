# 01.02 — Model, context, tools, and runtime
- [interactive-diagnostic-map](https://sbhrwl.github.io/cursor/foundations/01-02-ModelContextToolsRuntime/interactive-diagnostic-map.html)
- By the end of this lesson, you should be able to choose an evidence-producing first investigation when an agent task fails.
## The diagnostic map

| Layer | Inspect | Useful question |
|---|---|---|
| Model | Proposed action or inference | Does this conclusion follow from the observations? |
| Context | Requirements, relevant files, instructions and returned observations | Which requirement or fact was available at this step? |
| Tools | Requested arguments, allowed scope, execution result | What action actually ran, and what did it return? |
| Runtime | Checkout, working directory, executable, processes and network | Where did the action run, and what was available there? |

- This is an original teaching map for diagnosis.
  - Cursor describes its agent through instructions, tools and a selected model.
  - The runtime is added here as a practical dimension of investigation.
  - [Cursor Agent overview](https://cursor.com/docs/agent/overview).

## The recorded Cursor request
- We attach the actual `src/server.ts` file and ask:
```
> Read the attached Operations Hub server. Trace GET /health from request to response. Identify the database operation and what happens if it throws. Cite the file and line numbers. Do not edit files or run commands. Keep the answer under 150 words.
```
- The observed response describes the `select 1` query and the catch path that returns HTTP 503.
- The expanded activity lists a source read, a project skill and a repository search.
- The working tree remained clean.
  - This verifies an explanation against the source
  - It does not constitute a runtime test of the thrown-query path.
- At mentions make known relevant context explicit.
  - When the location is unknown, the agent can search.
  - Context also includes other instructions and observations, and long conversations can be summarized. [Cursor prompting documentation](https://cursor.com/docs/agent/prompting).
- The recording shows Cursor Grok 4.6 with a separate High effort setting. This is the observed configuration on the recording date, not a promise about every account's model menu.
## Deliberate wrong-address exercise
- In the course's isolated Operations Hub terminal:
```bash
pwd
node --version
curl --max-time 2 -sS http://127.0.0.1:3101/health
curl --max-time 2 -sS http://127.0.0.1:3100/health
```

- Port 3101 is deliberately incorrect for this configured baseline.
  - Its request fails to connect.
  - Port 3100 returns the real health response with `database: connected`.
  - No application repair or model swap is performed between these checks.
- The first result concerns the attempted connection.
  - It does not establish that the handler ran and failed.
  - Change one relevant input, rerun the check, and keep both observations.
- `127.0.0.1` refers to the machine or network namespace in which the command runs.
  - If you adapt the exercise to another environment, inspect that environment's configured address rather than assuming the recording's port is universal.
  - Cloud Agents have their own execution environment.
  - [Cursor Cloud Agents](https://cursor.com/docs/cloud-agent).

## Exercise
- Open `interactive-diagnostic-map.html`.
- For each scenario:
  - Select the first layer you would inspect.
  - Name one concrete check and the uncertainty it reduces.
  - State what the current observation does not establish.
- A satisfactory answer distinguishes a missing executable, a missing requirement, a refused tool action and an unsupported inference.
  - It also acknowledges that an incident can involve several layers.

## Carry forward

Before retrying a failed task, write: **observed result → working hypothesis → next check**. In 01.03, we will connect these checks to ownership of requirements, design choices, implementation and acceptance.

## Files
- [interactive-diagnostic-map.html](https://sbhrwl.github.io/cursor/foundations/01-02-ModelContextToolsRuntime/interactive-diagnostic-map.html)
- [worked-answer.md](worked-answer.md)
- [BASELINE-SOURCE.md](BASELINE-SOURCE.md)
- [operations-hub-baseline-b3b306a.zip](operations-hub-baseline-b3b306a.zip)
- [PROMPTS.md](PROMPTS.md)
- [narration-script.md](narration-script.md)
  - [01-02-model-context-tools-runtime.en.srt](01-02-model-context-tools-runtime.en.srt)
- [sources-and-credits.md](sources-and-credits.md)
- [chapters.json](chapters.json)
