# Narration — 03.02

## Keep the useful part; own the result

That gray suggestion is a proposal. Before it becomes your code, you get a choice: take it, take a piece, or dismiss it. Let's make those choices deliberately in Cursor. We'll turn a tiny status helper into tested behavior, using real Tab suggestions. And we'll catch a setting that makes the partial acceptance shortcut behave very differently. Fast typing is nice. Knowing what you just accepted is better.

## Define the behavior before inviting a completion

Here's our practice helper. An open request should display Awaiting review. An approved request should display Approved. Every other exact string should display Unknown status. No trimming, no changing the case, no clever guessing. The starter just returns its input, so it doesn't meet that contract yet. These comments and the tests are prepared exercise material. The suggestions we're about to inspect come from Cursor Tab.

## Read the independent checks

The tests cover both supported values and a group of unrecognized strings. That group includes an empty string, uppercase OPEN, a value padded with spaces, and other unknown values. Why be this explicit? Because a completion can look perfectly reasonable while quietly changing your requirements. These checks give us a concrete target before we edit. They're focused on this helper; they don't exercise a live interface or the whole application.

## Enable partial acceptance in this installation

In Cursor Settings, open Tab. This installation has a separate switch for partial acceptance. Turn it on to accept a suggestion incrementally with Control, Right Arrow on Linux. During rehearsal, with the switch off, that key moved the caret instead. So if your shortcut doesn't do what you expect, inspect the setting and the installed binding. Don't keep pressing keys and hope the editor reads your mind.

## Pause on the actual proposal

Select the starter return line and begin an if condition that compares status. Pause after the comparison operator. The editor offers gray text that completes the condition for open. Read the proposal and the surrounding code before accepting it. The gray portion is still a suggestion. You've already changed the file by typing, but you haven't accepted the gray text. Keep those two states separate.

## Dismiss a suggestion without undoing your typing

Press Escape. The suggestion disappears, while the condition we typed remains. That's a rejection of the proposal, not an undo of our own edit. You can dismiss a perfectly sensible suggestion because you're not ready to use it. You can also continue typing your intended code. The useful habit is to keep control of the next edit, instead of treating every gray line as an instruction.

## Accept a smaller piece and inspect it

Here we have a fresh suggestion ready to inspect. With Partial Accepts enabled, use Control, Right Arrow, then pause and inspect what became real text. Repeat once to accept another piece. In this example the quote and the word are separate steps. Punctuation boundaries can be surprising. Watch the caret and the text color; don't assume one keypress always inserts a whole expression.

## Accept the remainder of the current proposal

Now press Tab to accept the remainder of the condition. Cursor then offers the body as another proposal. Stop again. We need the review label for open, the approved label for approved, and an explicit unknown fallback. A second suggestion is a second decision. Accepting the condition didn't automatically approve every later line the model might offer.

## Accept only after reading the branches

This proposal follows our three outcomes and uses exact comparisons. Accept it, then save the file. The gray code becomes ordinary source text. That change of color tells us it was inserted; it doesn't tell us the behavior is correct. We'll inspect the actual diff and run the checks next. Your completion may be shaped differently. Evaluate it against the same contract instead of chasing identical ghost text.

## Review the change as ordinary code

Open the diff and compare the helper with its starting version. The raw return has become explicit branches. Check the returned strings, the fallback, and the scope of the edit. Only this source file should need to change for the exercise. Formatting deserves attention too, but a beautifully aligned wrong label is still wrong. Review behavior first, then keep the code consistent with the surrounding project.

## Run focused behavior and type checks

Run the focused status tests, then the TypeScript check. We want a successful exit from both commands, and we want to read what actually ran. The tests check the supported labels and the unknown values. The type check catches a different class of problems. Together they provide evidence for this bounded change. They aren't a certificate that every possible input or the whole product has been verified.

## Test a tempting change to the requirements

Here's an original course exercise. Choose an input and compare an exact mapping with a version that trims and lowercases first. For open, both may look fine. For uppercase OPEN or a padded value, they disagree. Our contract says those values are unknown. Normalization can be a useful feature, but adding it here would change the requirement. A helpful-looking completion still needs that conversation.

## Choose acceptance by evidence

Checkpoint. A suggestion adds normalization we didn't request. What should you do? Reject or revise that part, then verify the intended behavior. Now suppose the condition is useful but you're still reviewing the rest. Partial acceptance can help you take a smaller step. It doesn't remove the need to read the remaining proposal, and it doesn't make an incomplete intermediate state ready to commit.

## Know the escape hatch and the limits

The Cursor Tab status control lets you inspect whether suggestions are enabled and gives you ways to pause them. Use that when you need a quiet editing moment. Tab can also suggest larger edits or another editing location. We aren't depending on those features in this exercise. Read the current suggestion and its scope each time, and inspect your installed controls when their behavior differs from the reference.

## Record the decision and the checks

Keep a small acceptance record: the behavior you wanted, the file you changed, the part you accepted or rejected, and the checks you ran. Include the revision and the actual result. This isn't a form you need for every keystroke. It's practice in making your reasoning visible. When a teammate reviews the change, the contract and the evidence matter far more than how many suggestions you accepted.

## Make a new bounded change independently

For your exercise, start from the supplied practice snapshot and define one additional status before asking for a completion. Write its expected label and add a focused test. Inspect whatever Tab actually suggests, accept deliberately, and verify the result. If it adds unrelated behavior, remove that behavior or reject the proposal. Keep a before and after diff, and explain one decision you made instead of simply pressing Tab.

## Acceptance is an editing decision

You now have three useful moves: accept the whole proposal, accept a smaller piece, and dismiss it while keeping your own typing. We used those moves inside a loop: define the behavior, inspect the change, and run the relevant checks. That's how autocomplete becomes an engineering tool. Before the next lesson, what extra behavior would make you reject a suggestion that otherwise looked pretty good?