## Summary
<!-- 1–3 sentences: what changed and why. Keep the Closes line — the pr-issue-link check requires it. -->

Closes #

## Gate
- **Named gate**: `<the exact command that proves this change>`
- **Verdict**: pass | not run (<why>)
- **Evidence**: <failing before → passing after; for a new test, what it asserts; for a measurement, a table with a column saying what each row measures>
- **`hack/gate.sh`**: green | not run (<why>)

## Merge preconditions
None.

## Review
- **Tier**: A | B | C (handbook project-tracking.md §3)
- **Notes**: <behaviour changes, each marked intended or preserved; seams added or removed; costs moved; trade-offs with their numbers, each marked verified or inferred; rejected alternatives>

## Ledger
<docs, status, decision records or audit files riding this PR, or "None.">

## Checklist
- [ ] `hack/gate.sh` green locally (or "not run" stated above with the reason)
- [ ] Tests added or updated for the change
- [ ] Docs updated if behaviour changed
- [ ] Decision record opened or cited, if a choice crossed a team boundary
