# Source snapshot and patch

`operations-hub-01-04.zip` contains the tracked Operations Hub files at change revision `57cee18a2e474d32164df0fb24316a833ba3fbb4`. Unzip it and follow the repository README's standalone bootstrap instructions. Supply your own local database password; `.env.example` contains a placeholder. The AgentBox MCP example documents machine-specific paths and must be adapted to another runtime.

`health-method-change.patch` is the three-file diff from baseline `b3b306ab7bd13091db4780ca5e853f7727be67af` to that change revision. Use it to study or apply the change to the matching baseline. A Git archive is a source snapshot, without repository history.

The private course pull request was merged as `b6747c5f38b8c1c540e808b173fef6814ecf3280`. Its tree matches the source snapshot. `change-evidence.json` records the observed local, runtime and GitHub results. Private GitHub links require access to the course owner's repository; the included snapshot and patch can be inspected locally.
