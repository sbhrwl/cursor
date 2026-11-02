# Narration — 03.05

## Recover the state you actually intended

Restore is a comforting word. It doesn't tell you which state you're getting back. In this lesson, we'll inspect a real Agent experiment, restore its checkpoint, and compare the result with a targeted Git recovery. We'll track the code, a manual note, and a tiny file created by a terminal command. The useful skill is explaining what changed, what survived, and how you checked it.

## Separate code snapshots from external state

Start by naming the state. Cursor checkpoints support local Agent exploration. Git gives us committed snapshots we can identify and compare. Commands can also affect files and services beyond the edit we're reviewing. Those are separate things to check. Before recovering anything, inspect the current diff and preserve work you may want later. Then choose the operation that matches the state you actually intend to restore.

## Establish work that predates the Agent request

Here's our dedicated recovery checkout. I'm adding a manual note before asking Agent to change the code. The sentence gives us something concrete to track: preserve this sentence during the experiment. It lives in a different file from the implementation and tests. That distinction matters, because we want to observe the recovery boundary instead of assuming that every file in the workspace will behave the same way.

## Record the commit and current working-tree diff

The terminal shows our baseline commit and the current working-tree status. Only the note is modified. Its diff contains the sentence we just wrote. The implementation and tests still match the committed starting point, and the targeted checks pass. Save that starting evidence. After the experiment, three modified files will have different origins: one edit was already ours, while two files will contain the Agent's changes.

## Bound the reversible experiment

Ask Agent to explore one display change: open requests should say Needs review instead of Awaiting review. Update the contract comment and matching test expectations, preserving all nine tests and the other behavior. Keep the manual note untouched. We also ask for a tiny marker file through the terminal, outside the repository. That marker will help us check whether a file recovery operation also reverses this particular command's effect.

## Observe code changes and command execution

The real Agent reads the current work, edits the label and its expectations, then runs the focused tests and type check. It also creates the marker through a terminal command. Watch those as distinct actions. Changing source code and running a command can both happen in one conversation, but they don't automatically share one recovery mechanism. The task stays inside our isolated course environment, with no database or remote changes requested.

## Read the proposal before undoing it

The implementation diff changes the contract comment and the exact open-label branch. The unknown-value fallback, batch mapping, and permission helper remain unchanged. The Agent reports nine passing tests. That's useful evidence for this experiment, but green tests don't decide whether we want to keep the experiment. The expected label now matches the experiment. The test suite agrees with the new wording.

## Check the assumptions that changed with the code

Look at the expected values in the batch tests. Mixed inputs, duplicates, and the frozen-array result now use Needs review where an open status appears. Unknown values and rejected labels still have their existing expectations, and empty input stays empty. Both files describe the same experiment. Before recovery, we've preserved the actual diff so the experiment remains inspectable even after its files change again.

## Read the installed checkpoint control

The curved arrow attached to our request opens the checkpoint confirmation. In this version, the dialog asks whether to discard changes up to that checkpoint. Read the control you're actually using, and keep the current diff somewhere you can inspect later. We leave the confirmation enabled and continue with this isolated experiment. A familiar icon is a starting point for inspection, not a substitute for understanding the scope.

## Compare files instead of trusting the previous report

The open label is back to Awaiting review, and the experimental highlights disappear. Notice that the conversation still contains the earlier report. That report describes the experiment before we restored it. It is not a live statement of the current working tree. This is an easy trap: the files changed, while the written explanation stayed. After recovery, read the actual state again.

## Verify the preserved note and unchanged Git history

Run Git status and inspect the note. Only the manual note remains modified, and its sentence is still there. The implementation and test files match their contents before the Agent request. The baseline commit is unchanged too. In this experiment, the checkpoint recovered the Agent's file edits while preserving the note that already existed. Keep that claim specific to the state we established and the result we verified.

## Check the terminal effect independently

Now read the marker from the temporary directory. It's still there. The terminal command created that file outside our repository, and restoring this checkpoint did not remove it. That's a concrete boundary we can observe. We haven't tested every possible command or service. The lesson is to check external effects independently. A source file returning to an earlier version does not prove that a process, database, or remote operation was reversed.

## Test the recovered implementation and expectations

Run the status tests again, followed by the type check. All nine tests pass on the recovered files. We also compared the actual contents with the saved state from before the request. Those checks answer different questions: the comparison tells us which files returned, while the tests check their expected behavior. The preserved manual note and the remaining marker are part of the outcome, not clutter to hide from the result.

## Prepare a manual change with an observable failure

For the Git comparison, make a deliberate manual edit. Change the unknown-value fallback to No label, leaving the comment and tests unchanged. This is a prepared mistake in our disposable checkout. The earlier checkpoint experiment is already undone. Now the source has a new manual change, and the note still has its earlier sentence. We want to recover this one implementation file from the committed baseline.

## Inspect and preserve the path to be recovered

The focused diff shows exactly the fallback replacement. Our tests still expect Unknown status for unrecognized values. Before restoring the file, preserve the current changes in a patch outside the checkout. Git restore will replace contents in the path we select. Naming a source and a path makes the operation easier to review, but it doesn't make the current contents worth forgetting.

## Establish the failure before recovery

Run the full status test file before recovering anything. Six tests pass and three fail. The summary identifies the affected expectations, and the first failure shows the mismatch directly: actual No label, expected Unknown status. We have a specific observed failure caused by our manual change. Keep the expectations intact. We're recovering the implementation to the committed contract, so rewriting the tests would answer a different question.

## Restore one working file from the committed tree

Read the command before running it. The source is HEAD, our current commit. The destination is the working tree, and the path is only the status implementation. The staging area is left alone. Now run the restore and inspect Git status. Only the separate manual note remains modified. The focused source diff is empty. We also compare the saved file contents and revision independently, so we can explain the state we actually recovered.

## Verify behavior after the targeted Git recovery

Read the note again: the earlier sentence remains. Now rerun the status suite and the type check. All nine tests pass, and the type check completes successfully. The source matches our committed baseline; the tests were never rewritten for this manual mistake. That gives us a useful sequence: inspect the change, observe the failure, preserve the patch, recover one path, and verify the resulting behavior. The command is only one step in that sequence.

## Predict source and destination in a Git model

This original model separates the committed tree, staged contents, and working files. The example gives the implementation a different value in each. Choose the committed tree as the source, the working tree as the destination, and only the implementation path. Apply it to the model. The working value returns to Awaiting review. The staged value and the manual note stay as they were. No command executes in your repository here.

## Explain why the restore source matters

Reset the example and choose the index as the source. Restoring only the working file now copies the staged value, Needs review, instead of the committed value. That's why the source matters when the index differs from the commit. You can also explore explicit staging destinations with the committed source. Predict the affected cells first, then compare the result. This simplified model covers tracked files, not every situation Git can represent.

## Keep a record of the observed recovery

Save a short recovery record. Identify the starting revision, the operation, its intended scope, and what you actually observed. For our checkpoint experiment, the code and tests returned, the manual note remained, and the terminal marker still existed. We checked the files, Git state, and tests separately. A useful record connects the recovery action to evidence, including state that didn't change and limits we haven't tested.

## Practice recovering one path without losing another

Clone the supplied practice snapshot and record its baseline. Make two separate edits: change a display label and add a note. Inspect the diff and preserve a patch outside the checkout. Then restore only the implementation from the committed tree. Verify that your note remains and rerun the checks. Explain the source, destination, and path before pressing Enter. The exercise is complete when the resulting state matches your prediction.

## Recover deliberately and verify the resulting state

You now have two recovery routes you can explain. A checkpoint can help with local Agent exploration. Git can restore named paths from a committed state. Neither a familiar button nor an old conversation report proves the current result. Inspect before and after, keep the work you may need, and check external effects separately. Before the next lesson, name one piece of state you'd verify independently after restoring an Agent experiment.