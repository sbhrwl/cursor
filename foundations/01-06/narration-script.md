# Narration script — Entry assessment and learning paths

## 01_hook — Can you find the next useful check?

A clean working tree. A passing test. A healthy service. Three reassuring signals, and three different questions. Before we move into the bigger projects, let's see whether you can connect them. We'll trace one real behavior through Cursor, then work through four short cases. The result is a practice plan you can explain, instead of a score you can brag about.

## 02_outcome — Build an evidence trail

Open the assessment beside the course workspace. Your job is to locate the implementation, find a test that challenges it, inspect the running service, and record the revision. Then decide what each observation leaves unanswered. If something feels unfamiliar, good: you've found a concrete place to practice. Nobody gets better at debugging by pretending the terminal was obvious.

## 03_revision — Identify the repository state

First, establish where we are. Git status shows main and no listed file changes. Then we ask Git for the current commit identifier. These commands describe the checkout. They don't prove the service has reloaded that checkout, and a clean working tree doesn't prove the application works. Keep the revision in your notes so later evidence has an anchor.

## 04_navigation — Find the behavior in Cursor

Now locate the behavior without asking an agent to rewrite it. I use Quick Open in this Linux workspace to open the handler file. Inside the exact health branch, the cache directive is assigned before the method check and before the probe. Follow the early return and the exception path. Explain why both keep the header before you move on.

## 05_test — Connect code to a test

Next, open the health test file and find the healthy GET case. Read the assertion for the response header, but also inspect how the request reaches the handler. This test starts its own server with controlled dependencies. That's useful isolation. It also means the test isn't a request to the long-running Operations Hub service on our usual port.

## 06_run — Run one focused check

Run that one named test. On this checkout, it reports one pass and zero failures. The result tells us that this checked path satisfied these assertions in the test setup. It doesn't stand in for the other health paths or the complete suite. Running one specific case helps you investigate. Bring back the broader checks before you integrate a change.

## 07_runtime — Inspect the running service

Now make a separate request to the actual service. We see a successful response and the no-store directive. This is another piece of evidence, from a different execution path. The response doesn't identify a Git commit by itself. In the previous lesson, we restarted the service after the change; for your own run, record that startup context instead of guessing from a green response.

## 08_report — Write the smallest useful report

Put the observations together in a short report: checkout revision, handler location, test command and result, live request and result, then the remaining limits. Notice how little prose this takes. A teammate should be able to repeat your check without reverse-engineering your conversation with Cursor. The report is a handoff artifact, not a victory speech.

## 09_case_one — Case one: a confident completion message

First case. An agent says, done, tests pass, but its answer contains no command output or revision. What should happen next? Choose the action that improves the evidence for the claimed result. Pause and give a reason before clicking. We're assessing your next engineering move, not whether you can spot the answer with the longest label.

## 10_answer_one — Case one: inspect the supporting evidence

Inspect the relevant diff and obtain the actual check results for the current change. A confident summary can point you toward evidence, but it can't replace it. Starting another agent to repeat the same reassurance doesn't close the gap. If this case was difficult, practice a bounded task with an explicit stopping point and a small completion report.

## 11_case_two — Case two: red before the assertion

Second case. A request fails with connection refused, before the test receives any response. Does that establish that the new response header is wrong? No. Inspect the server lifecycle and test setup first. Once a request can reach the intended handler, the header assertion becomes meaningful. The failure is real; the conclusion still has to match where execution stopped.

## 12_case_three — Case three: a changed checkout and an old process

Third case. You edit the handler, save the file, and a request still shows the old behavior. The process was started earlier without a watcher. Before asking Cursor for a second implementation, check which process is serving the request and restart it through the project's documented command. Then repeat the request. A source file and a running process aren't the same thing.

## 13_case_four — Case four: CI for a different revision

Fourth case. A pull request has a successful check for an earlier commit. Another change was pushed afterward. Is that earlier result evidence for the new revision? It tells you about the earlier revision. Inspect the check's commit identifier and obtain the relevant checks for the current head. The branch name can stay the same while the code underneath it changes.

## 14_paths — Turn gaps into a practice plan

The assessment records your first choices and lets you revisit every explanation. Use the pattern to choose a practice focus. If navigating files or starting services was difficult, begin with the workspace and editor modules. If you confused a setup failure with a behavior failure, revisit the small-change exercise and spend extra time on checks and debugging.

## 15_ai_path — Practice AI collaboration and integration

If an agent's summary felt sufficient, focus on modes, context, and explicit acceptance criteria. If the revision mismatch was easy to miss, practice Git first, then the pull-request and CI module. These are priorities within the course, not permission to skip prerequisites. Everybody still builds the shared workspace and follows the project dependencies before tackling the advanced workflows.

## 16_transfer — Complete the hands-on transfer

Now do the hands-on part without copying my narration. Trace HEAD or a rejected method through the handler, find its assertions, and run the relevant check. Record a live response and explain how its evidence differs from the controlled test. You can consult the notes. The useful test is whether you can produce and explain the trail yourself.

## 17_rubric — Judge the artifact, not the confidence

Use three levels for each part of your report: demonstrated independently, completed with a reference, or needs another attempt. Attach the command, location, or result that supports your choice. Don't average away a missing prerequisite with points from an easier question. Choose one gap, practice it, and revisit the same task until you can explain your decisions.

## 18_close — Bring one concrete goal to the next module

You've finished the foundations when you can connect a requirement to code, checks, runtime evidence, and a recorded revision, while keeping the limits visible. Save your report and one specific practice goal. Next, we'll build the reproducible workspace that the larger projects depend on. Which step took the most effort to verify? That's your starting point, and now you have a way to work on it.
