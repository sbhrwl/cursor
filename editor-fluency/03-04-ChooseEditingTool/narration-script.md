# Narration — 03.04

## Choose the assistance the work needs

A one-word correction doesn't need to become a space mission. But when a change involves reading code, updating tests, and running checks, coordinating that work can be useful. In this lesson, we'll compare direct editing, Inline Edit, and Agent using real work in our practice repository. The goal is to choose a tool for a reason you can explain, then verify the result with the same care whichever route you take.

## Consider understanding, changing, and checking

Start with three kinds of effort: understanding the task, making the change, and checking the result. If you already know the exact edit, direct editing may be quickest. If you can describe a transformation within a selected range, Inline Edit can help. If exploration, file changes, and commands need coordination, consider Agent. These aren't rigid categories. The useful question is where assistance reduces effort without making the result harder to understand.

## Make a known comment correction directly

Here's a deliberately prepared typo in the contract comment. Labels is misspelled. We know the replacement and we aren't changing the behavior of either helper, so select the word, type the correction, and save. That's a complete tool choice: the editor already gives us what we need. You can still use AI for a correction like this, but there should be some benefit beyond using the newest button.

## Check the actual scope of the direct edit

The Git diff shows one comment correction. The function bodies haven't changed. This is the kind of evidence appropriate to a spelling fix in a comment; it doesn't require inventing a new behavior test. Keep that distinction in mind. Verification should respond to what could actually be affected. We'll leave this small edit in the working tree and explicitly tell the next tool to preserve it.

## Revisit the bounded Inline Edit example

This is footage from the previous lesson. We selected the display helper, described one exact label change, and reviewed the resulting proposal. Inline Edit was a useful fit because the target was known and the transformation was bounded. Direct editing would also have been reasonable if we already knew the implementation. Choosing Inline Edit didn't remove the need to review the code or run the existing behavioral checks.

## Define a coordinated change before delegating it

Now the task has several related pieces. We want a helper that converts a list of status values into display labels. Reuse the existing scalar helper. Preserve the input order and repeated values, return an empty list for empty input, and leave the input untouched. We'll also need tests for those requirements. This is a small example where we can inspect all the coordination before applying the same habits to larger features.

## Give Agent a bounded task and concrete checks

In the Agent panel, name the new helper, its behavior, and the two files that may change. Ask for tests covering mixed values, duplicates, empty input, and a frozen array. Preserve the existing labels, permission policy, and comment correction. We also specify the commands to run and exclude unrelated work. The instruction gives the agent useful room to implement the task while keeping the expected result and the review scope concrete.

## Observe the native Agent workflow

Submit the request and watch the actual workflow. Here, the agent reads code, changes the implementation and tests, and runs commands. That's the coordination we're asking it to handle. The exact sequence and waiting time can vary. Keep an eye on what it's doing; a clear request still needs supervision appropriate to the work. For this exercise, everything stays in our dedicated practice checkout and the task involves only the two named files.

## Treat the completion report as a review guide

The agent reports which files it modified and the checks it ran. That's useful as a guide to the review, but the report isn't our only evidence. Open the actual files and inspect the behavior. Notice that the earlier spelling fix is mentioned separately from the new helper. Keeping track of earlier working-tree changes matters: otherwise, you can accidentally attribute every change in the final diff to the most recent agent request.

## Read the generated implementation

The new helper maps each input through the existing scalar label function. That reuses our exact matching and unknown-label behavior. There is no need to duplicate the label branches or change the permission helper. Read the implementation against each requirement: order, duplicates, empty input, and no mutation. This implementation is short enough to understand directly. Using Agent doesn't mean we should stop understanding the code it leaves behind.

## Review generated tests against the requirement

The new tests cover mixed exact and unknown values, repeated values, an empty array, and a frozen input. Look at the expected arrays, not just the test names. Do those expectations match the behavior we requested? The frozen input case checks both the returned labels and the original array. When the same agent writes implementation and tests, compare both with the independent requirement. Matching mistakes in both files can still produce a green test run.

## Keep the reviewed work and inspect the file set

After reviewing the implementation and tests, keep the changes and inspect the repository diff. There are two modified files. The source contains our earlier comment correction and the new batch helper; the test file imports that helper and adds the new cases. Keeping the agent's changes does not create a commit. The diff still needs to tell a coherent story, including work that was already present before the agent started.

## Run the checks in the actual checkout

Run the status test file in the terminal, then run the TypeScript check. All nine tests pass: five existing cases and four new cases. The type check also completes successfully. This verifies the bounded helper work we just inspected. It doesn't demonstrate a live application screen or a complete authorization system. The value of the agent's coordination is now connected to code and results that we can examine ourselves.

## Practice choosing a route without rigid rules

Try the decision exercise. A known typo favors direct editing. A selected helper transformation can fit Inline Edit. A coordinated implementation and test change can fit Agent, although direct editing remains valid if you already know the work. Then look at the unclear permission request. No editing tool can supply the missing product decision responsibly. Investigate the intended policy first. File count alone doesn't tell you which route is sensible.

## Write expected behavior independently

Use this original expected-value model to think through the batch contract. Mixed values preserve their positions. Duplicates stay duplicated. Empty input produces an empty result. You can enter your own array and calculate the expected labels. This page doesn't run the repository code; it helps you state expectations before comparing them with the real tests. Check input immutability in the actual checkout, using a frozen array as one concrete case.

## Record the tool choice and the observed outcome

Save a short decision record: the starting revision, desired behavior, chosen tool, changed files, and the checks you observed. Explain what work the tool helped with. In this example, we made the known correction directly. Then Agent coordinated implementation, tests, and commands. Another engineer might reasonably make the whole change directly. A useful record explains the choice and the result without pretending there is only one correct workflow.

## Repeat with a permission batch helper

For practice, add a batch helper that reuses the existing approval-decision function. Keep the role policy unchanged, and preserve order, duplicates, empty input, and the original array. Choose your own route and justify it. Inspect the implementation and tests, run the relevant checks, and record one limit of your evidence. The exercise is about choosing assistance deliberately. You don't need to reproduce our exact sequence of buttons to demonstrate that skill.

## Choose assistance deliberately and retain judgment

You now have a practical way to choose among direct editing, Inline Edit, and Agent. Ask what you already understand, what needs coordination, and how you'll verify the outcome. A small known edit can stay small. A broader task can benefit from an agent without losing a concrete review boundary. Before moving on, name one task you'd edit directly and one where Agent would save meaningful coordination work. Explain the difference in the work, not just the tool names.