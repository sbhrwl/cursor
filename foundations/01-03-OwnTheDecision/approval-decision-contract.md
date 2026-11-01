# Operations Hub — approval decision contract

**Status:** Proposed behavior for a future implementation. The current baseline has no approval endpoint.

## Behavior chosen for the course example

- An authenticated manager can approve an open request in the same tenant.
- A successful transition changes the stored status and creates one approval audit record.
- Repeating an approval leaves the approved state unchanged, creates no second approval audit event, and explains that the request is already approved.
- An unauthorized attempt changes no request state and creates no successful-approval audit event. Separate security logging remains possible.

## Resolve before implementation

- How is authenticated identity established, and how are tenant membership and manager authority obtained?
- What may a response reveal about a request in another tenant? Decide the error contract deliberately.
- Which endpoint, method, response codes and schema implement the behavior?
- How will simultaneous approvals avoid duplicate transitions and audit events?
- Which audit fields, retention rules and operational failure behavior are required?

## Design investigation delegated to the agent

Use the existing service and database. Propose the authorization point, state transition, audit write, and checks. Explain how the status change and audit write remain consistent.

A transaction is a candidate for grouping the two database writes. It does not, by itself, settle authorization, retries, or concurrent-request behavior.

Bring back a tradeoff if the approach needs a new service, a dependency with meaningful operational cost, or a policy change. Choose routine implementation details within existing conventions.

## Acceptance evidence to collect

| Requirement | Observation needed |
|---|---|
| Same-tenant manager approves an open request | Successful response; stored status approved; one matching approval audit record |
| Unauthorized actor attempts approval | Refused action; request state unchanged; no successful-approval audit record |
| Actor targets another tenant | Chosen disclosure policy enforced; state unchanged; no approval event |
| Approval is repeated | Already-approved response; stable stored state; no duplicate transition event |
| Status/audit operation fails partway | Neither write partially committed; failure handled according to the agreed contract |
| Approvals arrive concurrently | At most one state transition and its matching approval audit event |

## Completion report

For each requirement, include changed files, the command or interaction used, the observed result, and the code revision. State remaining uncertainty and untested cases. Attach the diff and preserve failures that led to a correction.

The existing database rollback test is baseline evidence. It does not verify an approval endpoint, manager role, tenant isolation, or audit behavior.

## Responsibility

Product and engineering owners choose policy and material tradeoffs. The agent can investigate, propose, implement within scope, and collect evidence. The responsible reviewer or release owner judges acceptance against this contract.
