# Narration — 03.01

## Find the code that answers the question

Somewhere in this repository, we tell clients not to cache the health response. Where? And which test checks it? Let's answer that ourselves in Cursor. We'll jump between a file, its symbols, the code that calls it, and the test that checks the response. The goal isn't a keyboard shortcut speedrun. It's arriving at the right evidence before we ask an agent to change anything.

## Choose navigation by the question

Start with what you already know. A command name belongs in the Command Palette. A filename belongs in Quick Open. A string belongs in Find or workspace Search. A function belongs in symbol navigation, definitions, or references. Those are different questions. Choosing the right one turns a huge codebase into a short investigation. We'll use this small, working starter to make each move visible.

## Discover commands by name

Open the Command Palette with Control, Shift, P on this Linux machine. Type Keyboard Shortcuts and read the actual result labels. We want the interactive settings page, so select Open Keyboard Shortcuts, without the JSON suffix. Similar names can open different views. The palette is a searchable command menu, and it often shows the assigned shortcut alongside the command. You don't have to memorize everything today.

## Inspect the active binding and its context

Search this settings page for Go to Definition. The binding is F twelve in this installation. Notice the When column: the editor needs the appropriate focus and definition support. A shortcut is more than a few keys; it's a command plus a context. If a shortcut behaves differently on your machine, inspect its binding here before assuming the feature is missing.

## Open a known file

Close settings and open Quick Open with Control, P. Type the path to the handler file, then choose the matching result. This searches filenames rather than file contents. Including the folder helps when several files share the same name. Check the breadcrumb after opening it: we're in the source folder, in handler dot T S, in the fresh clone from the previous lesson.

## Find text in the active file

With the editor focused, open Find and search for Cache Control, with a hyphen between the words. Here we have one match in this file. The line sets the response header to no store, inside the health route. Read the surrounding condition as well as the matching text. A highlighted string tells us where to look; its surrounding control flow tells us when that line runs.

## Search across the workspace

Now search the workspace for create Handler, written as one identifier. We get five text matches across three files in this checkout. There's the definition, the server that imports and calls it, and the test file that also builds a server. These are text results, grouped by file. They give us useful leads, but the count doesn't mean five runtime calls or five independent tests.

## Make the search scope explicit

Put S R C, slash, double star in the files to include field. The results narrow to three matches in two source files. The tests disappear because we excluded their folder from this search, not because the tests vanished from the project. Clear that filter and the test results return. Before trusting a missing result, check the open folder, include and exclude fields, and the search options.

## Navigate the current file by symbol

Back in the handler editor, open Go to Symbol in Editor with Control, Shift, O. Cursor lists the symbols recognized in this file. Filter for create Handler and select the function. We land at its definition. This uses language support to navigate code structure. It isn't a text search, and the at sign in this picker is not an instruction to attach code to an agent conversation.

## Follow a use to its definition

Open the server file and put the caret on the call to create Handler. Press F twelve. Cursor takes us to the function definition in the handler file. That's the relationship we wanted: this server constructs its request handler from that function. If navigation can't resolve a symbol in another project, check language support and project configuration. Guessing from a similar filename is a weaker substitute.

## Inspect references without losing the definition

From the definition, open references with Shift, F twelve. This inline view shows five locations, including the declaration in this example. Expand the test file and inspect its use of the same handler. References and text search happen to give the same count here. They are still different tools. Language references follow a recognized symbol; text search finds matching characters within its configured scope.

## Read the assertion and the case around it

Open the health test file and find the cache control header assertion. In the healthy GET case, the test makes a request and expects the response header to equal no store. Now we have a specific check tied to the behavior. Read the test setup and the assertion together. Merely finding the word health in a test name would not establish that this header is checked.

## Use command names across platforms

The lesson uses Linux shortcuts. The practice sheet includes common Windows and Mac defaults for the same commands, but your installed bindings are the authority. Extensions, remapping, keyboard layout, and focus can change what a key does. Use the Command Palette to find the command, then inspect its binding. That's a more portable skill than blindly replacing every Control key with Command.

## Preserve the checkout while investigating

Before recording our findings, check Source Control. There are no pending file changes. We navigated and read the code; we didn't need to rewrite it to understand these relationships. This is a useful habit before handing work to an agent: establish the current behavior, locate the relevant test, and know the starting state. Navigation evidence helps define a change, but it doesn't replace running the relevant checks.

## Retain an evidence map

Record four locations: the header assignment, the handler definition, the server's call, and the test assertion. Include the repository revision because line numbers can move. For each location, write what it establishes. Our map connects a concrete behavior to its implementation, its wiring, and a check. That's useful context for a future agent task, a code review, or another engineer joining the project.

## Diagnose a missing result

Quick checkpoint. You searched only the source folder and found no matching test. What's the next move? Inspect and widen the search scope. Don't conclude that coverage is missing from a filtered search. Second situation: you know a function's name but not its filename. Workspace text search can locate candidates; then use definition and reference navigation to inspect the actual symbol relationship.

## Trace a second behavior independently

Your exercise is to trace the unsupported method response on the health route. Locate the condition, find the response status, and identify the test that checks it. Record file paths and line references at your revision, plus how you found them. Keep the checkout unchanged. If you get stuck, choose the tool based on what you know: a filename, a string, a symbol, or a command.

## Navigate toward evidence

We can now move from a question to code, follow a symbol to the places that use it, and locate a relevant assertion. That's the foundation for working quickly without losing the plot. Next we'll use Cursor Tab for small edits and learn how to accept suggestions deliberately. Before moving on, which search filter could hide the very file you are trying to inspect?