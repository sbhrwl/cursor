# Checkpoint — one worked answer
- The evidence supports that the server started in the observed environment and the observed page rendered.
  - It does not establish authorization or that an approved request persists correctly.
- One useful next check is an approval attempt by a caller without the required permission.
  - Inspect both the response and the stored state: a rejection is incomplete if the database changed anyway.
  - The expected response and permitted roles must come from the requirements, not from whatever the implementation happens to do.
- Other defensible checks may address persistence, permitted approval transitions, duplicate requests, or concurrency.
  - Prioritize by the actual acceptance criteria and consequences of failure.
- **Self-assessment:**
  - Can you state the expected result before running the check, and explain what a pass would still leave unknown?
