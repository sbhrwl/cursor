# 01.01 — Start with evidence

## A result you can inspect

A confident answer is cheap. A working change? That needs evidence. In this course, we're going to connect the code, the test, the pull request, and the machine that actually runs it. And when one of those pieces disagrees with the agent, well, that's where the engineering starts.

## A result you can inspect

Welcome to Superposition. We're building an engineering workflow in Cursor, from the first small change all the way to a system with multiple services and agents. You'll learn the features, sure. But the more useful skill is knowing what to ask, what to inspect, and when you have enough evidence to move on.

## A result you can inspect

By the end of this lesson, you'll be able to separate three things: a claim, an observation, and a conclusion. That sounds a little academic. It's not. It's the difference between an agent saying, 'Done,' and you knowing which requirement was actually met. Let's start with something we can inspect.

## Meet the starting system

This is Operations Hub, our starting service. Right now, it's deliberately small: an API, a database, and synthetic requests from two organizations. You're looking at real data returned by the running service. This is the foundation we will grow during the course, not a finished application hiding behind a demo screen.

## Meet the starting system

Notice the title, the status, and the organization identifier on each request. A laptop approval belongs to one organization. A training request belongs to another. Later, that organization boundary becomes a serious design constraint. A user from one company must not be able to read another company's requests.

## Meet the starting system

And here's our first useful distinction. Seeing two different organization identifiers does not prove that access is isolated. It only proves those values came back in this response. To establish isolation, we'll need identities, server-side permission checks, and tests that attempt access across the boundary. The conclusion has to stay inside the evidence.

## Meet the starting system

Now look at the health endpoint. The service reports that its database is connected. In this baseline, the handler actually sends a small query to PostgreSQL before returning success. That's more informative than a hardcoded green light. But it still doesn't tell us whether a manager can approve a request correctly.

## Read the mechanism

Let's connect that response to the code. Here's the route, here's the database query, and here's the response it constructs. You don't need to memorize every symbol yet. Follow the cause and effect: an incoming request selects a handler, the handler talks to a dependency, and the caller gets a result.

## Read the mechanism

Cursor gives an agent tools to search, edit, and run commands around a model. That makes it powerful enough to do useful work, and powerful enough to make a plausible mistake. Our job is to give it a clear objective, relevant context, and a way to check the result. Then we inspect what happened.

## What a passing check means

Here's a database integration test from our baseline. It writes a synthetic record inside a transaction, rolls the transaction back, and checks that the record is absent. Watch the result. When that passes, we have evidence for the behavior this test exercises. We do not suddenly have evidence for every feature we plan to build.

## What a passing check means

The same repository also has a real GitHub Actions run. The workflow installs the locked dependencies, initializes a fresh database, checks the TypeScript, and runs the integration test. Running away from this desktop matters. It gives us a chance to catch assumptions that only happen to be true on the machine where we wrote the code.

## What a passing check means

There's a detail here that's easy to skip: the commit. A passing check belongs to a particular version of the code. If I change the code after that run, the old green badge doesn't verify the new change. So we'll keep connecting our evidence to the version it actually tested. Tiny habit. Huge reduction in confusion.

## Review the change

This pull request added our cloud startup configuration. Look at the files changed, rather than trusting the title. The configuration points to an installation script and a startup script. The startup script brings up the database and the API. We can inspect those responsibilities before we accept the change into the main branch.

## Review the change

During setup, we found a real problem in the final health check. If the API failed to become healthy, the script printed a warning and continued to a ready message. That's a success-shaped failure. The correction makes that path return an error. We'll keep coming back to this idea: failure needs to stay visible to the system coordinating the work.

## The machine is part of the workflow

And here's the follow-through: a normal Cloud Agent run on the merged version. Its job was only to inspect startup. No manual installation, no manual service launch, and no code edits. The API responded, the demo data was available, and PostgreSQL was accepting connections. The startup status was successful too.

## The machine is part of the workflow

That tells us this starting environment worked on this run. It doesn't promise that every future change will work. A cloud machine needs dependencies, configuration, and running services just like your laptop does. Later, we'll deliberately break startup and learn to diagnose it. For now, notice that we're checking the machine as well as the code.

## Where the course goes

We'll grow three connected projects. Operations Hub becomes a business application for requests and approvals. Evidence Desk becomes a service that answers questions using authorized sources. Engineering Control Plane becomes a system for coordinating engineering work. Those are the destinations. We'll build and verify the capabilities step by step, rather than pretending the starting repositories already contain them.

## Where the course goes

The complexity will come from the behavior: permissions, state transitions, background work, failures, and changes that cross a service boundary. Adding more agents won't automatically make those problems easier. Sometimes the best design is one agent with a focused task. Sometimes parallel work helps. We'll make that decision from dependencies and measured results.

## The working agreement

Our recurring workflow is simple enough to remember. Understand the request. Make a plan that can be checked. Build a bounded change. Verify the behavior and inspect the diff. Then integrate it. If a check fails, return to the step that needs better information. A loop without a useful check is just repetition with a bigger bill.

## Your first checkpoint

Your first checkpoint is a judgment call. An agent says, 'The approval feature is complete. The server starts and the page looks right.' Pause here. Write down two things that evidence supports, and two things it does not establish. Then choose one additional check that would reduce the most important uncertainty.

## Your first checkpoint

It supports that the server started in that environment, and that the observed page rendered. It doesn't establish that approval permissions are enforced, or that an approved request is saved correctly. A useful next check could attempt an approval as a user who lacks permission, then inspect both the response and the stored state. The best check depends on the requirement.

## Carry the evidence forward

That's the working agreement for this course. We can use AI to move quickly, while staying precise about what we know. Follow the request into the system, connect checks to a specific version, and keep the conclusion no bigger than the evidence. Next, we'll unpack the model, context, tools, and runtime so you know which part to fix when an agent gets stuck.
