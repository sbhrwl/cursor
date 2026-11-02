# Narration — 03.06

## Fix the behavior without expanding the change

The support queue says, not loaded. The data says zero. Those are two very different messages to give a team. We're going to trace that mismatch, write a test that catches it, and use a tightly bounded edit to repair the behavior. No component makeover required. By the end, you'll have a small, reviewable change and evidence that the surrounding behavior still works.

## Define the repair contract

Before editing, pin down three things: the mismatch, the behavior to preserve, and the evidence that will make the repair complete. Here, zero is a real count. Null means the data isn't loaded. A fix also needs to preserve the other display fields and queue navigation. We'll use a failing regression test, a reviewed diff, and a refreshed preview to check that contract.

## Reproduce the visible mismatch

Here's the prepared Operations Hub preview. Data operations shows four pending requests. Support handoff says not loaded, and so does access requests. That screen alone doesn't tell us whether both teams are missing data. This is a local course fixture, so we can inspect the actual inputs without touching a production system. First, describe the visible symptom. Then investigate what the component received.

## Compare the screen with the actual input

Open the source snapshots. Support has a pending count of zero. Access has a pending count of null. Our contract treats zero as a real count and null as missing data. The screen has collapsed those two states into one label. That gives us a concrete reproduction: zero should display zero, while null should keep the missing-data message. We've narrowed the question before asking the model to change anything.

## Trace the label to its implementation

Back in Cursor, search the workspace for the visible label, not loaded. The results point to the queue summary helper and its existing test. Open the implementation result. This search gives us a candidate, not a diagnosis by itself. We still need to read the function and its callers. Here, the local preview uses this helper to prepare the values displayed by each queue card.

## Read the input contract and the display decision

The input type allows a number or null. The comment says zero is a real count. But the assignment uses the count directly as a condition. In JavaScript, both zero and null are falsy, so both reach the same fallback. That's the mismatch. The rest of this helper preserves identity, title, team, priority, and navigation. Those fields define useful boundaries for the repair.

## Inspect the existing verification gap

Run the existing queue tests and the type check before editing. Five tests pass, and the type check succeeds. We already know the preview is wrong for zero. There's no contradiction: the existing tests cover other cases, and this conditional is valid TypeScript. A green result only tells us about the checks we actually ran. Next, we'll add the missing behavior as a regression test.

## Add a test for the reported behavior

Here's the existing test file. I'm adding a regression test that passes zero into the same helper and expects the display text zero. The expectation comes from the contract and the observed input. It doesn't copy the current implementation's answer. Keep the existing tests intact. We want the new case to expose the bug while the previous checks continue to describe behavior we need to preserve.

## Observe the regression test fail before fixing code

Run the queue tests again. Five pass, and the new zero case fails. The assertion shows the important difference: the actual value is not loaded, while the expected value is zero. That's the same mismatch we saw in the browser. Now the failure is repeatable without clicking through the interface. We can use it to evaluate a candidate repair, while still checking the actual preview afterward.

## Select the decision that causes the mismatch

Select the assignment that chooses the pending display text, then open Inline Edit. The rest of the helper stays visible so we can review its surroundings. We've already located the bug and written a failing check. This request doesn't need a repository-wide redesign. Direct editing would also be reasonable here. We're using Inline Edit to practice giving a model a precise repair boundary.

## Describe the behavior and preservation constraints

The instruction names all three states. Zero must display zero. Null must keep not loaded. Positive counts must keep their value. Then it limits the edit to this assignment and asks to preserve the other code and files. That's a concrete contract the proposal can satisfy or violate. Once the model responds, we'll inspect the actual change. The prompt is an instruction, not proof of what happened.

## Inspect the proposed conditional and its surroundings

The proposal replaces the truthiness condition with an explicit check for null. If the count is null, the helper returns not loaded. Otherwise, it converts the count to text, including zero. Read the whole changed assignment, then scan the return object below it. The candidate keeps the surrounding fields. That's what we wanted, but we still need to accept, save, and verify the actual result.

## Accept the reviewed candidate

Accept the proposal and save the file. The helper now distinguishes missing data from a real count. Keep that new regression test; it captures the behavior that was missing from the original checks. Acceptance finishes the editing step. It doesn't finish verification. Next, we'll look at the repository diff, run the relevant tests, and refresh the same preview where we observed the problem.

## Inspect the actual repository patch

The changed-file summary lists the implementation and its test. The implementation diff replaces one assignment. The new test records the zero-count expectation; the previous tests are still there. No dependency change or component rewrite appears in this patch. That makes the review manageable. Read what changed, connect it to the reported behavior, and check that the surrounding code still matches the intended scope.

## Run the relevant behavioral and type checks

Run the six queue tests alongside the nine earlier request-status tests. All fifteen pass, including the zero regression and the existing neighboring behavior. Then run the type check; it succeeds too. This is stronger evidence than the original five passing tests because the reported failure is now represented. It's still a defined set of checks. We haven't tested a database, a production deployment, or every possible input.

## Refresh the same user-visible preview

Refresh the same preview. Support now displays zero. The first queue still shows four, and access still says not loaded. The data didn't change; the display decision did. That's the visible result we wanted. Our last check happens where the reported problem started, instead of ending at a green terminal. The code-level check and the refreshed interface now agree about the reported case.

## Check the queue link and preserved input

Open the support queue and return to the list. The link still reaches the right queue, and its title, team, and priority remain intact. Inspect the snapshots again: support still has zero, while access still has null. The fix doesn't rewrite those inputs to make the screen look right. Our intended change is the display decision. The surrounding behavior remains part of the verification contract.

## Challenge a tempting fix with neighboring cases

Try the candidates in this original course model. These are teaching examples, not the model's generated proposal. Using the value as a condition fails for zero. Now try always displaying zero. That fixes the reported example, but breaks the positive count and missing-data cases. One green example can hide a bad repair. The neighboring cases make that mistake visible immediately.

## Check the complete display contract

Choose the explicit null check and run the cases. Four stays four, zero stays zero, and null keeps not loaded. All three display cases pass. That supports this expression for the contract we've defined. It still doesn't verify every part of the surrounding component. Use the diff and the additional tests to check metadata, navigation, and input preservation. The table is one piece of evidence.

## Review the preserved behavior

A repair review has two sides. Confirm the changed behavior, then inspect what should have stayed the same. Check the existing fields, the queue link, and the input snapshot. Also scan the changed-file list for surprising edits or dependencies. If the model expands the scope, pause and investigate that expansion. A precise prompt helps, but the actual patch is what you need to assess.

## Save a reviewable repair record

Capture the evidence in the repair record. Include the reproduction and starting revision, the expected behavior, the actual patch scope, and the checks you ran. State the limits too: this is a synthetic local preview, with no production or database claim. Download the completed record so it survives closing the page. Another engineer should be able to understand the change and repeat the checks without reconstructing our whole session.

## Repeat the method from the starter

Use the supplied starter to repeat the repair in your own checkout. Reproduce the mismatch, trace the display decision, add the zero test, and watch it fail before changing the implementation. Then make a bounded repair and verify the preview. For an extra challenge, add a positive-count case using one. Explain which assertion would reject a fix that simply displays zero for every queue.

## Carry a verified repair into the next module

We started with a screen that confused zero with missing data. The workflow connected that symptom to an input, a decision in the code, and a regression test. That's the habit to keep: define the mismatch, bound the edit, and challenge the repair with neighboring cases. Next, we'll move into the Agents Window, modes, and conversations. Which neighboring case would you use first to challenge a proposed fix?