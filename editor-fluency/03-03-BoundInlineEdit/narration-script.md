# Narration — 03.03

## One label, one bounded change

We need one new label. Somehow, that's also a great opportunity to accidentally change who can approve a request. Let's avoid that little adventure. In this lesson, we'll use Inline Edit on a specific piece of code, describe the behavior we want, and check what actually changed. The useful skill is setting a boundary and then verifying it. A highlighted selection helps communicate intent. It doesn't do your code review for you.

## Continue from the tested helper

We're continuing with our status helper. Open and approved already have display labels, and everything else gets Unknown status. The new requirement is narrow: the exact value rejected should display Rejected. Uppercase and padded versions should remain unknown. This is prepared exercise code, so we can inspect the whole behavior without getting lost in the application. We'll keep the existing branches and add the new case deliberately.

## Separate display from permission

Look just below the display helper. There's a separate function that decides whether a role can approve a request. Its policy belongs to a different decision. Adding a display label gives us no reason to change that policy. This neighboring function makes our boundary visible: the display helper may change; the permission helper must stay exactly as it is. When two responsibilities live close together, proximity isn't permission to edit both.

## Make the intended difference testable

The prepared tests spell out the new label and two inputs that must remain unknown. Another test checks the existing permission policy. We still have the earlier label tests too. Read those expectations before opening the editing tool. Otherwise, a polished suggestion can become the specification by accident. Here, the requirement and the checks already exist, so we can judge the proposed change against something independent.

## Read the failing baseline

Run the focused tests against the starting version. The new label test fails because the helper still returns Unknown status for rejected. That's the gap we're here to close. The existing behavior checks pass. A failure is useful when you understand its cause and expect it at this stage. Keep the baseline result separate from the result after editing; otherwise, you lose the evidence that the change addressed the missing behavior.

## Select the intended editing target

Return to the source file and select the display helper with its contract comments. Leave the permission helper outside the selection. Now open Inline Edit with Control, K on this Linux installation. Check the highlighted range before writing the instruction. Including the contract comment lets the edit keep the explanation consistent with the implementation. Selecting everything would make the intended boundary harder to see, even for a tiny file.

## State the change and the invariants

Give the instruction three useful ingredients. First, the change: add the exact rejected label. Second, what must stay true: the existing labels, exact matching, and the unknown result. Third, the exclusions: no normalization, no permission changes, and no other files. We also ask to keep the explicit branches. That's a concrete editing request. Notice how little depends on telling the model to be brilliant or to try really, really hard.

## Submit and wait for an inspectable proposal

Submit the instruction and let the edit finish. The amount of waiting and the exact proposal can vary. Read the result before using the acceptance controls. Our request was for a small change in the selected code, but the selection isn't a security boundary or proof that every constraint was obeyed. We'll inspect the proposed changes here, then inspect the actual repository diff after accepting them.

## Review each changed part

There are two changes to inspect in this proposal. The contract comment names the new label, and a new branch returns Rejected for the exact rejected value. Check that the previous branches and the unknown result remain in place. Then read the neighboring permission helper. An accurate comment is useful, but it can't compensate for incorrect code. The comment and implementation should describe the same behavior.

## Accept after the review

The visible changes match our request, so accept them and save the file. If your proposal adds extra behavior, reject it or refine the instruction before keeping it. The installed interface has controls for reviewing changes, including individual changed sections. We're accepting this complete proposal because we've read both parts. That decision keeps the edit; it doesn't create a Git commit, and it doesn't replace running the tests.

## Inspect the actual changed-file set

Open the Git diff. We want the comment update and the new exact branch, with no unrelated file changes. Compare the surrounding code as well as the highlighted additions. The permission helper should be unchanged. This second review matters because the final working tree is what you'll test and eventually commit. Your instruction describes an intention; the diff describes the code you actually have.

## Verify the new behavior and the invariants

Run the status tests again, then the TypeScript check. Now all five tests pass, including the new label and the permission regression check. Read the result and confirm that the intended test file ran. These checks support the helper change we made. They do not show a live user interface or prove the whole authorization system is correct. Keep the conclusion as specific as the evidence.

## Practice choosing the selection

In this original course exercise, choose an editing scope for the same request. The display helper and its contract comment are a sensible target. The permission helper is unrelated, and selecting both functions adds unnecessary ambiguity. This is a teaching model, not a replacement for the editor. Use it to explain why you chose a range, then verify that range in your actual code before invoking Inline Edit.

## Spot a helpful-looking scope violation

Now inspect three candidate changes. One adds the exact label. Another normalizes the input, changing the result for uppercase and padded values. A third also changes permission behavior. Only the first matches this request. The other changes might belong in separately discussed work, but they aren't justified by adding a display label. A small change can still carry a big product decision. Read what the code means, not just how many lines changed.

## Make the boundary reviewable

Record the requested change, the selected range, the behavior you preserved, and the checks you actually ran. Include the starting revision and the changed-file set. Keep it short enough that a teammate would read it. The purpose isn't paperwork. It's making the decision easy to inspect: here's what I asked for, here's what changed, and here's the evidence that the important behavior stayed intact.

## Repeat with a different exact label

For your independent exercise, add one more exact display label from the supplied practice snapshot. Define its expected text and its negative cases first. Use a bounded selection and a specific Inline Edit instruction. Review the proposal, inspect the final diff, and run the status tests and the type check. Leave the permission helper unchanged. If your model takes a different route, judge the behavior and explain your decision instead of copying our output line for line.

## A selection communicates intent; evidence checks it

You can now take a narrow requirement through Inline Edit without handing over the whole decision. Choose a range, describe the change and its limits, inspect the proposal, then verify the working tree. In the next lesson, we'll decide when direct editing, Inline Edit, or Agent is the right tool for the job. Before moving on, name one behavior in your own code that must stay unchanged during an apparently simple edit. That's where your review should get specific.