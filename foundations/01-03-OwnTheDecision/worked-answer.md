# Worked answer — decision ownership

| Decision | Useful assignment | Needed information |
|---|---|---|
| Who may approve which requests? | Product/engineering owner accountable for policy | User roles, tenant relationships, allowed states, intended disclosure |
| Must status and audit change together? | Architecture owner, informed by requirements | Consistency requirement, storage boundary, failure modes, operational cost |
| What is a local helper called? | Implementation delegate within conventions | Existing naming patterns and the helper's purpose |
| Is the feature ready to accept? | Responsible reviewer or release owner | Requirement map, diff, checks, actual results, revision and remaining uncertainty |

The agent can help in every row. Contribution does not automatically assign authority. A single engineer can hold all four responsibilities while delegating implementation details to the agent.

## Example evidence row

**Requirement:** a non-manager cannot approve a request.

**Check:** authenticate a known non-manager in a synthetic test tenant, attempt the approval through the actual application boundary, then inspect the agreed response and stored state.

**Expected observation:** the action is refused under the chosen contract, the request remains unchanged, and no successful-approval event is created. Separate security-event logging may still occur.

**Limit:** this check alone does not establish cross-tenant isolation, repeated-request behavior, concurrency correctness or every role configuration. Add the relevant cases from the contract.

The course's existing rollback test is useful baseline coverage. It cannot establish any approval result because it does not call an approval endpoint.
