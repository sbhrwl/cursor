# Worked answer — Keep the loop honest

**A — Tests pass, but the live service still accepts POST with 200.** Check which process is running and which code it loaded. Restart the intended service, then repeat the request. Do not infer the process revision from an isolated test result.

**B — CI is green for a different commit.** Identify the proposed revision and inspect the corresponding workflow run and jobs. A passing result for unrelated or older code does not establish the proposed change's result.

**C — A check exposes an unrelated response change.** Return to the requirement and diff. Investigate the regression and repair the bounded change. Do not delete evidence merely because it complicates the story.

A strong completion report states the requirement, changed files, commands, outcomes, commit and remaining gaps. It distinguishes local checks, runtime observations and CI. A concise report can still be precise.
