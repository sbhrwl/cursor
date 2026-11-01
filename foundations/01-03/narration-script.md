# 01.03 — Who owns the decision?

## 01_hook

Let managers approve requests. That sounds like a feature. It is also a surprisingly effective way to hide a dozen decisions inside one short sentence. Which managers? Which requests? What happens when someone clicks twice? Cursor can help us uncover those decisions and build the result. Our job is to make sure the choices match the product we actually intend to ship.

## 02_outcome

Today we will build a decision contract for a future Operations Hub feature. We will inspect what exists, turn an ambiguous request into observable behavior, separate a product constraint from an implementation choice, and define the evidence needed for acceptance. The artifact we finish is a usable engineering brief. The approval endpoint itself comes later, after its foundations exist.

## 03_ownership

Think of four responsibilities: requirements, architecture, implementation, and acceptance. One person might hold several of them. On a team, they may be spread across product and engineering. An agent can contribute to every responsibility. Contribution and authority are separate questions. A useful delegation says which decisions the agent may make, which constraints it must preserve, and when it should bring back a tradeoff.

## 04_requirement

Requirements describe the behavior people need. In our example, a manager can approve an open request belonging to the same tenant. That sentence contains policy: the role, the starting state, and the tenant boundary. We should choose that policy deliberately. If the agent guesses that every signed-in person is a manager, beautifully organized code will not rescue the feature.

## 05_architecture

Architecture connects that behavior to a design. Where is authorization enforced? How does the status change stay consistent with its audit record? An agent can inspect the project, compare options, and explain costs. We can authorize it to choose within existing conventions. A new service or a new database is a larger decision because it changes what we must operate and maintain.

## 06_implementation

Implementation is where delegation can become very concrete. Given an agreed behavior and a bounded design, the agent can edit the relevant handler, add the data operation, and write checks. It should have room to solve ordinary details. We do not need a meeting about every variable name. We do need it to preserve the permission rule while solving those details.

## 07_acceptance

Acceptance asks whether the delivered change meets the agreed conditions. The agent can collect evidence and help review a diff. The person or team responsible for the release decides whether that evidence is sufficient. That responsibility is easiest to exercise when the change is understandable and the results are tied to specific requirements. A cheerful completion message is a useful update, not the acceptance record.

## 08_request

Here is the request we actually send in Cursor. We describe the future approval feature, then ask for three things before any code: what exists today, unresolved product decisions, and checks we would need. We name the server and the database test. For this investigation, we ask for no edits and no commands. That keeps the first step focused on reading and diagnosis.

## 09_result

Cursor identifies the current application as a read-only baseline with no approval path. It then separates existing behavior, open decisions, and possible checks. That is a productive use of an agent: it helps us discover the shape of the work before committing to a design. Now we verify the observations and make the choices, rather than treating the response as an approved specification.

## 10_source

Look at the actual server. There is a health route, a route that lists synthetic requests, and fallback error handling. The list includes a tenant identifier, but this file does not enforce a tenant permission boundary. A field named tenant does not implement tenant isolation. We have a starting point for the course, and we should describe that starting point accurately.

## 11_test

The existing database test opens a transaction, inserts a synthetic request, rolls it back, and checks that the inserted row is gone. That tells us something useful about database access and rollback. It does not call an approval endpoint or exercise a manager role. If this test passes after we add approval code, we still need evidence for the new behavior.

## 12_questions

The agent raises useful questions about who may approve, valid state transitions, audit records, tenant scope, repeated approvals, and the interface. These questions are candidates for a decision. Some belong to product policy. Others are technical choices we can delegate. Sorting them prevents an implementation detail from silently becoming a business rule. It also keeps an open question from disappearing inside a long chat.

## 13_brief

Here is the brief prepared for our course project. Its status says proposed behavior for a future implementation. Our choices are explicit: authentication, manager authority, a matching tenant, and an open starting state. We also require an audit record for a successful transition. These are deliberate choices for this example. A different product could choose different behavior and need different evidence.

## 14_repeats

Let us settle the repeated-click case. Once the request is approved, another approval attempt should leave the stored state unchanged and create no second approval audit event. The response will explain that the request is already approved. Notice how that describes a result we can observe. Later, we can design the exact response contract and verify the behavior under concurrent requests too.

## 15_denials

For an unauthorized request, the contract requires no state change and no successful-approval audit event. That does not forbid recording a separate security event. It keeps two meanings distinct. We also need a policy for what information the response reveals about a request in another tenant. We record that as a design question to resolve before implementation, instead of guessing a status code here.

## 16_tradeoff

Consider two designs for the state change and its audit event. Separate writes are straightforward to sketch, but one can succeed while the other fails. A transaction can keep the two database changes together. That does not automatically solve identity, permissions, retries, or concurrency. It answers one consistency question. Good architectural reasoning names the property an option provides and the problems that remain.

## 17_scope

Our delegation now has a useful boundary. Explore an approach using the existing service and database. Explain the authorization point, the state transition, the audit write, and the checks. If the approach requires a new service, a new dependency with meaningful operational cost, or a policy change, bring that decision back with reasons. Routine implementation details can stay inside the delegated work.

## 18_plan

Cursor has a planning workflow for researching the codebase and preparing a plan that you can inspect and edit before building. We will work through that interface in detail later. The habit matters here: review a plan against the behavior and constraints. A plan earns confidence by addressing the hard cases. Its length and formatting do not make the unresolved questions disappear.

## 19_evidence

Now map each requirement to evidence. A same-tenant manager approves an open request: verify the stored state and its audit record. An unauthorized actor attempts approval: verify the refusal and unchanged state. A repeated approval arrives: verify that it creates no duplicate transition event. Each row names behavior and an observation. That makes a missing check visible before somebody declares the feature finished.

## 20_counterexample

Here is a tempting shortcut: the happy-path test passes, so approvals are secure. The observation is narrower than that conclusion. A test can pass because the implementation and the test share the same mistaken assumption. Review the expectation against the requirement, then look for a case that would expose the mistake. In this example, try a different tenant and a non-manager identity.

## 21_handoff

A useful completion report links the requirement, the changed files, the command or interaction that checked it, and the observed result. It also states what remains untested. When a check fails, keep the failure and explain the next investigation. That gives the next reviewer something concrete to assess. It also lets an agent continue from durable evidence instead of reconstructing the task from memory.

## 22_checkpoint

Take a moment with the exercise and pause when you need to. Sort these four decisions: approval policy, consistency between the status and its audit record, the name of a local helper, and acceptance of the finished feature. For each decision, identify the responsible role. Then describe what the agent can contribute and what information the responsible person needs.

## 23_answer

Approval policy belongs with the people accountable for the product behavior. Consistency is an architectural responsibility informed by that policy. A helper name can usually be delegated within the codebase's conventions. Acceptance belongs to the responsible reviewer or release owner, supported by the collected evidence. These roles can overlap. The point is to make authority visible, not to invent a committee for a small change.

## 24_close

We now have a clearer task: a baseline we inspected, proposed behavior we chose, technical questions we recorded, a scope for delegation, and an evidence map. The feature is still unbuilt, and the brief tells us exactly what must happen next. In the next lesson, we will turn these responsibilities into a working loop: understand, plan, build, verify, and integrate.
