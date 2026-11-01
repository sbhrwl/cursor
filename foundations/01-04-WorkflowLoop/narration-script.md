# Narration script — The workflow loop

## 01_hook — A green test is only part of the story

Seven green tests. A running service that still gives us the old answer. Both can be true, and we're about to see exactly why. Today we'll take a small change through the whole engineering loop using Cursor, from the first observation to a reviewed revision in GitHub. The endpoint is small. The habits are the ones we'll need when the projects get much bigger.

## 02_outcome — The whole loop

In this lesson, we'll take one small API requirement through a complete engineering loop. Understand, plan, build, verify, integrate. Those names aren't magic. The useful part is what each stage leaves behind: an observation, a decision, a change, evidence, and a revision we can identify later. A bounded task lets us see the whole process clearly.

## 03_loop — The whole loop

Think of the loop as a set of useful questions. What happens today? What should happen instead? What's the smallest change that gets us there? How could we catch ourselves being wrong? And which exact revision are we accepting? A surprising answer sends us back to the relevant question. It doesn't mean the workflow failed. That's the workflow doing its job.

## 04_get — Understand the baseline

Here's our actual Operations Hub service. First, a normal request to the health endpoint. The command shows the response headers as well as the body. We get status two hundred, a connected database, and the existing environment baseline metadata. This establishes that the current process can answer the request. It doesn't establish every behavior that a health endpoint might need.

## 05_post — Understand the baseline

Now we send a POST request to the same endpoint. Look at that: two hundred again. The current handler checks the URL, but doesn't distinguish the request method. We're going to introduce an explicit contract: health supports GET and HEAD, and rejects other recognized methods. We're choosing new interface behavior. The original response alone doesn't establish a security bug.

## 06_contract — Plan observable behavior

The brief makes the important details visible. A healthy GET stays successful. HEAD checks health too, but sends no response body. A failed database probe still produces service unavailable. An unsupported method produces method not allowed, with an Allow header listing GET and HEAD. Reject that method before querying the database. The rejection should work even when the database is down.

## 07_scope — Plan observable behavior

Notice the scope boundary. We're preserving the demo listing and the unknown path response. We're not adding the approval feature from the previous lesson, introducing authentication, or moving to a new framework. A small task can quietly become a renovation project if nobody draws that line. Our plan needs enough structure to test this behavior, and a reason for any extra structure it introduces.

## 08_request — Plan observable behavior

I ask Cursor to inspect the repository and the contract before changing anything. The request asks for a short plan and an explanation of the test seam. That's simply the place where a test can substitute a controlled dependency, such as a database query function. We want to observe the real HTTP response while choosing whether that dependency succeeds or fails.

## 09_provider — Separate tool failure from code failure

Our first planning request hits a connection error from the model provider. No implementation has happened here. Changing application code would be a strange response to that evidence. I keep the requirement intact and retry the request. This is why the earlier distinction between model, context, tools, and runtime matters: first locate the failure, then choose an action that could actually address it.

## 10_plan — Inspect the proposed design

The retry produces a concrete plan. Extract a request handler, supply a health probe and a demo listing function, and test through an actual HTTP server. Production keeps using PostgreSQL. Tests can use controlled substitutes. I also catch a small sequencing problem in the written response: the original behavior must be captured before the edit. We already did that. Read the plan; don't just admire its formatting.

## 11_seam — Inspect the proposed design

The server in these tests listens on port zero. That asks the operating system for an available port, which the test then reads back. It doesn't compete with our development service on port thirty-one hundred. This is a useful boundary: real request and response handling, controlled database behavior. The separate database test remains responsible for the real database interaction it actually checks.

## 12_build — Build a bounded change

Now I hand Cursor the implementation task on a dedicated lesson branch. The original baseline is already recorded, and the behavior contract stays the same. The agent can edit and run the relevant checks. We leave committing and restarting the service for the review stage. That gives us a clean opportunity to compare what changed with what we asked for.

## 13_handler — Build a bounded change

Here's the important production change. The health branch rejects unsupported methods and returns immediately. Only GET and HEAD reach the health probe. The early return matters: setting a status code without stopping this path would still allow later work to run. The success and failure branches also handle HEAD without a response body. We can inspect those decisions directly in the diff.

## 14_test — Build a bounded change

The rejection test sends several methods through the HTTP server. It checks the response status, the Allow header, and the error body. Then it checks that the probe call count stayed at zero. That's an observable acceptance condition from our brief. A test that merely checked whether a helper existed would miss the reason we made this change in the first place.

## 15_initial_checks — Review and strengthen the evidence

Cursor's first implementation reports six passing tests and a successful type check. That's encouraging. It also states something very useful: the service on our development port is still running the old code. So we have evidence for the changed test target, and we still owe ourselves a runtime recheck. A careful completion report makes that distinction explicit.

## 16_review — Review and strengthen the evidence

During review, I ask for three focused improvements. Give test requests a timeout, so a future missing response fails clearly. Add OPTIONS to the rejected method cases. And check that a failed demo listing still returns service unavailable after the handler extraction. These checks strengthen our evidence around the changed code. The production scope stays the same.

## 17_checks — Verify the changed code

After the review changes, I run type checking and the complete test command in the Cursor terminal. Seven tests pass, with zero failures. The list includes the existing database rollback test, the health response cases, rejected methods, and the preserved demo behavior. These are the results of this command on this working tree. We still need to connect that evidence to the running process.

## 18_stale — Verify the running process

Here's the trap in plain sight. Tests pass, but this POST request to the development service still returns two hundred. The source file changed; the long-running process didn't reload it. Before rewriting a working handler, check which process answered your request. Code on disk and code already loaded into memory can tell two different stories.

## 19_restart — Verify the running process

I restart Operations Hub with the course environment helper. This is our setup script, not a built-in Cursor feature. It stops the previous service process, starts the application again with its existing private environment, and waits for a healthy response. Now the next request can tell us what the changed application does in this actual runtime.

## 20_post — Verify the running process

Now the same POST returns four oh five: method not allowed. The Allow header lists GET and HEAD, and the body contains the bounded error from our contract. This is the before-and-after observation we were missing. The test verifies that rejection skips the probe; the running service verifies this response from the process we just started.

## 21_preserved — Verify the running process

We also check the supported behavior. The HEAD request succeeds, the normal GET still returns the health metadata, and the synthetic demo listing remains available. The HTTP tests separately check the empty HEAD body and the failing-probe cases. Together, these checks cover different parts of the contract. A single successful request would leave several of those questions unanswered.

## 22_evidence — Connect evidence to its scope

Let's make those boundaries explicit. Controlled HTTP tests tell us about response behavior and dependency calls. The database test tells us about its real transaction. A runtime request tells us about the process that answered it. And a continuous integration result belongs to the code revision and jobs that ran. Combining those observations is stronger than treating one green indicator as a universal guarantee.

## 23_commit — Integrate an identifiable revision

Once the change is reviewed, I stage the three relevant files and inspect the staged summary. Then I commit them with a message describing the behavior. The resulting commit identifies a concrete revision we can compare, test, and return to. This is where a collection of working directory edits becomes a durable unit in the project's history.

## 24_pr — Integrate an identifiable revision

I push the lesson branch and open a pull request in our private course repository. Its description connects the original behavior, the resulting behavior, and the validation we performed. The pull request also names the head revision. We'll use that identifier to check the next piece of evidence, so we're talking about the same code throughout the workflow.

## 25_ci — Integrate an identifiable revision

The pull request checks are green. I inspect the corresponding workflow run and compare its head revision with our commit. They match. The run installed dependencies, initialized its database, checked types, and passed all seven tests. That gives us another environment's result for the proposed change. It still describes the checks that ran, rather than every possible production condition.

## 26_integrate — Integrate an identifiable revision

With the diff and matching checks reviewed, I merge the pull request and update our local main branch. The lesson branch keeps the original change commit, and main now includes the merge. Our course materials preserve the revision identifiers, the patch, and a source snapshot. The next lesson starts from an identifiable state, with the decisions and evidence available to inspect.

## 27_checkpoint — Your next useful action

Your turn. Open the companion exercise and choose the next useful action in each situation. Tests pass, but the live process behaves differently. A green workflow run belongs to another revision. Or a check reveals a response change outside the agreed scope. Don't just choose a button. Explain what your next action would establish. Pause here and work through all three cases.

## 28_answers — Your next useful action

For the first case, identify the running process, load the intended code, and repeat the request. For the second, connect the workflow result to the revision you're proposing. For the third, investigate the unexpected change and return to the scope and diff. Each answer moves the work forward by resolving a specific uncertainty. That's more useful than asking the agent to try harder.

## 29_close — Carry the loop forward

We've now connected an observation, a contract, a plan, a bounded implementation, several kinds of evidence, and a preserved change. Keep those connections visible as your tasks grow. In the next lesson, we'll look at the habits that separate fast code generation from engineering you can trust. Before moving on, write your own short completion report for the change we just made.
