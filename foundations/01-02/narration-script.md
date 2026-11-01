# 01.02 — Model, context, tools, and runtime

Selected English narration.

## 01_hook

Same code. Same machine. One request fails, and the next one works. We did not replace the model. We changed the address we were asking the machine to contact. That is a small example of a much bigger habit: before you ask an agent to try harder, figure out which part of the system can actually explain the failure.

## 02_map

In this lesson, we will separate the model, the context, the tools, and the runtime. This is our engineering map for diagnosing a workflow. It is not a claim about four boxes hidden inside Cursor. By the end, you should be able to look at a failed task and choose a useful first investigation, instead of changing everything at once.

## 03_model

Start with the model. It takes the information available to it and produces a response, which can include a proposed action. That proposal may be excellent, confused, or somewhere in between. But a proposed command has not magically run. If the answer says, I checked the database, the next question is wonderfully boring: where is the tool call and its result?

## 04_context

Context is the information available for that step. It can include instructions, project rules, relevant files, your messages, and observations returned by tools. Notice the word relevant. Giving the agent a thousand unrelated files is not the same as giving it the permission rule it needs. A missing requirement can make a beautifully implemented feature the wrong feature.

## 05_tools

Tools connect the conversation to actions and observations. Reading a file, searching a repository, editing code, and running a shell command are different operations. Each has inputs, an execution path, and a result to inspect. A tool refusing an action is also a result. It is not the same event as the application running and returning an error.

## 06_runtime

The runtime is where an action actually happens. Which checkout is open? What is the working directory? Is the executable installed? Is the database running? Can this machine reach that address? A brilliant explanation of a test does not put Node on the path. Sometimes the most productive next move is checking one very ordinary environmental assumption.

## 07_instructions

These layers influence one another. Instructions guide how the agent works, tools can bring new information into context, and the runtime determines what an executed command can observe. Cursor coordinates the model and its tools. Our job is to make the objective and constraints clear, then inspect enough of that interaction to know why the next step makes sense.

## 08_question

Let us make the map concrete in Cursor. We are using the Operations Hub server from the previous lesson. The question is deliberately narrow: trace the health endpoint, identify the database operation, and explain what happens if that operation throws. We are asking for an explanation of the current implementation. We are not asking the agent to modify the service.

## 09_picker

The model controls are worth reading carefully. In this recorded setup, the menu identifies Cursor Grok four point six as the model, while High is the effort setting. Those are different choices. Available labels can change with the product and your account. Learn to inspect the selected configuration, rather than assuming every word beside the chat box is a model name.

## 10_attach

Here, I attach the actual server file with an at mention. That makes the relevant source explicit in the request. If I did not know the location, I could ask the agent to search first. Attaching a file does not mean every other input disappears, and it does not prove the agent will reason correctly. It gives us a specific piece of context we can point to.

## 11_scope

Read the rest of the prompt too. We ask for file and line references, forbid edits and command execution for this particular task, and keep the response short. The important part is the bounded objective. We want an explanation grounded in this file. We are not turning a small reading question into a request to redesign the application.

## 12_answer

The response identifies the health route, the small database query, and the error response. We can compare that directly with the source on the left. The handler waits for the query before returning success. The catch block sets a service unavailable response when something inside the protected block throws. This is an explanation we can inspect against the current code.

## 13_activity

Now expand the activity instead of stopping at the polished answer. This run shows a file read, a project skill, and a repository search. That is useful evidence about how the answer was assembled. It also reminds us that our typed message was not the only instruction in play. Project guidance can shape the workflow around the model.

## 14_static_limit

There is a limit to this result. Reading the handler and describing its catch block is not a runtime test of the failure path. Keep two kinds of evidence separate: code inspection tells us about a possible execution path. A runtime check tells us what actually happened during an execution. Both matter, and each has limits.

## 15_roundtrip

The simplified round trip looks like this. A request supplies the question. The model proposes a tool action. The tool executes under its configured conditions and returns an observation. That observation becomes information for the next decision. A useful agent can revise its approach from that result. If the result is hidden or misunderstood, the next step is built on a shaky foundation.

## 16_machine

Now we move from reading code to checking the machine. In this terminal, the working directory is the Operations Hub checkout, and Node is available. Those are modest observations, but they remove two possible sources of confusion. A command run from a different directory, or through a different terminal environment, might not see the same files or executables.

## 17_wrong_port

For this demonstration, I deliberately request the health endpoint on port thirty-one oh one. Our service is configured on thirty-one hundred. The first request fails to connect. This is an intentional wrong-address exercise, not a spontaneous production incident. We have not changed the application, stopped the database, or asked the model to repair anything yet.

## 18_interpret

What does that failure establish? The client did not establish a connection to the address it tried, at that moment. It does not establish that the handler has a bug, because we did not get as far as executing that handler through this request. Before rewriting code, compare the requested address with the address the service is actually configured to use.

## 19_correct

Change the request to the configured port and run it again. Now the health response comes back, including the database connection status. In this controlled example, correcting the address explains the difference we observed. We keep both results: the failed attempt and the successful check. The failed attempt is part of the diagnosis, not something embarrassing to erase.

## 20_no_swap

Notice what we did not need here: a tournament of models. We needed a hypothesis about the environment, one changed input, and another observation. That does not mean models never make reasoning mistakes. It means a model comparison is a poor substitute for checking an address when the evidence already points to an address problem.

## 21_budget

Context has a budget too. Files, instructions, conversation, and tool results consume space, and long conversations may be summarized. Do not build your workflow around one remembered capacity number for every model. Preserve the requirements, decisions, and useful evidence where the next step can recover them. We will explore Cursor context controls in detail when we work on larger changes.

## 22_boundaries

The same reasoning applies when work moves to a Cloud Agent. The remote machine needs its own checkout, dependencies, configuration, and running services. A file saved only on your laptop does not become a remote file because both agents can discuss it. When a result differs across environments, compare the inputs and machine state before deciding which layer is responsible.

## 23_checkpoint

Your checkpoint is to choose a first investigation, not to pretend every failure has exactly one cause. A terminal cannot find Node. An agent implements a feature without a requirement it was never given. The tool boundary refuses an edit. And an agent draws a conclusion broader than its evidence. Pause and assign a starting layer to each case.

## 24_answers

For the missing executable, start with the runtime. For the missing requirement, inspect the context and clarify the behavior. For the refused edit, inspect the action and its permitted scope. For the unsupported conclusion, challenge the reasoning and ask for an evidence map. These are starting points for investigation. They are not verdicts that rule out every other contributing factor.

## 25_next_check

The next check should reduce a specific uncertainty. Which executable can this terminal find? Which permission requirement reached the conversation? Was the requested tool action allowed? Which observation supports that conclusion? You can ask those questions calmly and precisely. A longer prompt with more exclamation points does not make the missing evidence appear.

## 26_close

Keep this map beside you: model, context, tools, runtime. Read the actual request, inspect the actual action, and connect the result to the place it ran. That gives you a much better starting point when an agent gets stuck. Next, we will decide who owns the requirements, the architectural choices, the implementation, and the final judgment that a change is ready.
