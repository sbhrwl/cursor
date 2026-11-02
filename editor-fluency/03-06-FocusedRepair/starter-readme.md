# Focused queue repair — 03.06

This is the prepared Operations Hub course fixture. The queue summary contains the intentional zero-count display bug demonstrated in the lesson. Start from this snapshot to repeat the repair yourself.

Use Node.js 22.12+ and npm. The recorded environment used Node.js 22.23.2 and npm 10.9.8. Run these commands in the project folder:

```sh
npm ci
node --import tsx --test --test-reporter=spec test/queue-summary.test.ts
npm run typecheck
```

Five baseline queue tests pass even though zero displays `Not loaded`; your task includes the missing regression test.

Start the local preview:

```sh
node --watch --import tsx src/preview-server.ts
```

Open [the local preview](http://127.0.0.1:3106). It uses synthetic fixtures, with no database or external service. Stop it with Ctrl+C. If port 3106 is occupied, stop your own prior preview or choose a different local port deliberately.

The broader starter also contains earlier API/database exercises. They are outside this display repair. The focused commands above avoid those integration dependencies; a generic npm test may require the database from earlier lessons.

Work on a local practice branch. Keep positive counts, null fallback, metadata, priority and navigation intact. Save the final diff and a repair record. The Git bundle is a portable single-snapshot history; it does not configure GitHub authentication, MCPs or Cloud Agents.
