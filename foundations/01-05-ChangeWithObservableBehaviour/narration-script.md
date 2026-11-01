# Narration script — A small change with observable behavior

## 01_hook — One header, a better test

One line of production code. Eight new assertions. And before we add that line, four test groups fail for a reason we can actually explain. That's a useful small change. In this lesson, we'll use Cursor to turn a requirement into evidence, then trace the paths a happy-path check would miss. The size of the diff is small. The thinking is the part we're practicing.

## 02_outcome — One requirement, observable evidence

Your turn to make the loop useful. We're adding one requirement to Operations Hub: every response from the exact health route should send Cache-Control, no-store. Success, failure, even a rejected method. We'll define the behavior, watch a meaningful test fail, make the smallest useful change, and check what the actual service sends. One header gives us plenty to think about.

## 03_meaning — Define the contract

Quick distinction before we touch code. No-store tells a compliant cache not to retain this exchange or reuse the response for another request. That's the standard's meaning. We haven't caught a browser serving an old health response here, and this header isn't a privacy guarantee. Our job in this lesson is narrower: make the origin send the directive consistently.

## 04_baseline — Inspect the starting state

We start from the main revision we integrated in the previous lesson. The working tree is clean. The health request still succeeds, and the response includes the existing JSON content type. But there is no Cache-Control header. That's the starting observation. A successful status and a missing new requirement can coexist quite happily. Tests need to know what we're asking for.

## 05_paths — Define the contract

The word every is doing real work in this requirement. A healthy GET is one path. HEAD has no response body. A failed probe takes the exception path. An unsupported method returns early, before the database probe. If we only check the happy path, we can get a green test and still miss most of the contract.

## 06_test_first — Observe an expected failure

Here's the discipline: change the expectations before changing the handler. Ask Cursor to add the HTTP assertions, run that test file, and stop at the result. A useful red test says the new behavior is missing. A syntax error or an unreachable server says something else. Read the reason for the failure before celebrating the color.

## 07_request — Give Cursor a bounded stopping point

The request gives Cursor a deliberate stopping point. Read the contract, create the lesson branch, add the assertions, and run the health test file. Keep production code unchanged. This is useful orchestration at a very small scale: the agent can inspect and execute, while we keep the decision to implement separate from the first evidence review.

## 08_failure — Read the actual failure

Cursor adds the header assertions to the existing HTTP tests. The health test file reports four failures and two passes. Now I run the healthy GET case on its own so the important detail fits on screen. The response arrives, but the cache control field is undefined. The assertion expected no-store. This is a real failure against the new requirement.

## 09_assertions — Read the actual failure

One subtlety: a failing assertion stops the rest of that test. It doesn't prove that every later assertion ran. In the grouped method test, the first failure prevents later methods from being checked on that run. We inspect where it stopped, then rerun after the change. A completion summary can be helpful, but the test code and the actual output decide what was checked.

## 10_diagnosis — Classify the failure

Compare that with a refused connection or a broken import. Those failures would tell us to inspect the test setup before judging the product behavior. Here, the request reaches the handler and fails on the missing header. That's why this red result is useful. We can connect one explicit expectation to one observable response, without asking a model whether the code looks right.

## 11_implement — Implement the bounded change

Now we can authorize the implementation. Keep the assertions, satisfy the health contract, and run type checking plus the full test suite. We also ask for a short explanation of the header's placement. The interesting decision is which control-flow paths it covers. There's no prize for making a one-header requirement look like a framework migration.

## 12_placement — Trace the implementation

The production change is one line inside the exact health-route branch. It sets the header before checking the method and before awaiting the probe. A rejected method therefore keeps it on the early return. If the probe throws, the catch block changes the status and body, while the header remains set. Other routes never enter this branch.

## 13_checks — Verify beyond the agent summary

Type checking passes, and the complete suite reports seven passing tests. That count includes the separate database transaction test. The health tests now reach the assertions that the earlier failures had interrupted. We keep checking the old behavior too: status codes, empty HEAD bodies, the Allow header, probe calls, and the routes outside this change.

## 14_restart — Inspect the running service

Next, restart the actual Operations Hub service with the course helper. This makes the runtime check about the changed handler instead of a process that loaded yesterday's code. Then inspect the response headers again. The same habit matters whether the change is one line or a major feature: know which process and revision your evidence describes.

## 15_live — Inspect the running service

The restarted service now sends no-store on a healthy GET, alongside the existing metadata. HEAD keeps the same directive and no response body. POST is still rejected, and its response includes both no-store and the allowed methods. The demo listing stays available without the new header. We can point to the specific responses instead of treating a green test summary as the whole story.

## 15_scope — Keep the claim precise

The controlled-probe tests cover the failure path without taking down our real database. The live requests check the running service. Neither observation tests every cache in a deployment. Our conclusion is precise: the checked health responses send the required directive, and the bounded tests preserve the surrounding behavior. That is a useful result we can review and reproduce.

## 16_integrate — Preserve the reviewed change

We keep the reviewed change as a commit, push the lesson branch, and open the private course pull request. The successful CI run identifies the same change revision. After merging, we bring main up to date. The small feature now has a traceable result: starting state, failing expectations, implementation, checks, and the accepted revision. The exercise files preserve that trail for your own practice.

## 17_checkpoint — Challenge the evidence

Try this before revealing the answer. Suppose the header is set after awaiting the health probe. A healthy GET test passes. Which two response paths should you challenge next, and why? Trace the early return and the exception path in your head. Pause here and explain the expected behavior before you choose the next check.

## 18_answer — Challenge the evidence

Check rejected methods and probe failures. A rejected method returns before that proposed header assignment. A failing probe jumps over it into the catch block. Both can miss the directive even when healthy GET passes. Our implementation sets the header at the start of the health branch, so those paths inherit it. The assertions check the response, not just whether a certain line exists.

## 19_close — Practice the complete habit

Take the starting snapshot and try the exercise yourself. Write the expectation, read the failure, trace the paths, and keep the change bounded. Then explain what your checks establish and what they leave open. That's the habit to carry forward. Which path would you have forgotten first: the early return, or the exception? Your answer tells you where to aim the next test.
