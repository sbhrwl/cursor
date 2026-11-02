# Deliberate acceptance practice

Use the supplied `tab-status-starter.bundle`. Its single practice commit has separate history from the instructor's working repository; see `offline-snapshot.json`.

```sh
git clone -b main tab-status-starter.bundle tab-practice
cd tab-practice
git remote remove origin
npm ci
node --import tsx --test test/request-status.test.ts
```

Use Node.js 22.12 or later in the Node 22 line for this course baseline. The three status tests deliberately fail against the starter. No database is needed for these focused tests or the type check. The repository also contains earlier course material; its complete integration suite has additional setup requirements.

Open the folder in Cursor. Read `src/request-status.ts` and `test/request-status.test.ts`. Implement the stated contract using deliberate acceptance. Exact proposals will vary; manual corrections are allowed and should be described honestly.

Then add one more exact status, for example `rejected` → `Rejected`:

1. Write the expected behavior first.
2. Add a focused test for the new exact value. Keep `REJECTED` unknown if matching remains strict.
3. Inspect Tab's proposal. Make at least one explicit acceptance, rejection, or revision decision.
4. Review the diff and run the status tests and `npm run typecheck`.
5. Save the final diff and a short acceptance record.

A successful submission includes the requirement, the changed source and test, the actual check results, and one explained decision. It should not add unrequested normalization or unrelated statuses. Passing the helper tests does not establish live UI behavior.
