# Contributing

How a change lands in any NetstarGlobal repository. This file is the single source for the
commit grammar and the pull-request body; the handbook cites it and does not restate it.
The rules behind it — issue-first, the merge tiers, review turnaround — are in
[handbook/project-tracking.md](https://github.com/NetstarGlobal/handbook/blob/main/project-tracking.md).

## 1. Start from an issue

Every unit of work is an issue before it is a branch, and every pull request closes at least
one (`Closes #N` in the body — the `pr-issue-link` check refuses a PR without it). Use the
issue forms; they carry the right labels.

## 2. Branch

```
<type>/<issue>-<short-slug>        fix/42-port-dropped-on-scheme-relative
```

`main` is always releasable. Branches are short-lived and are deleted on merge.

## 3. Run the gate before you commit

Every system repo carries `hack/gate.sh`. It is the same command CI runs, so "gate green" means
one thing everywhere:

```sh
hack/gate.sh
```

It is fail-closed: a missing tool or a step that cannot run is red, never a skip. A gate that
cannot run on your machine is reported as **not run**, with the reason, in the PR body — not
as green.

## 4. Commit grammar

Commits follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <summary>

<why: what was wrong, why this shape, the alternative rejected, the constraint that forced it.
Wrap at 72–80. Do not restate the diff.>

Closes #<issue>
```

- **`type`** is one of, and only one of: `feat` · `fix` · `docs` · `test` · `refactor` · `perf`
  · `build` · `ci` · `chore` · `revert`. A `perf` body carries a measurement. A `revert` body
  names the reverted sha and why.
- **`scope`** is the directory of the package or subsystem changed — literally what `ls`
  prints (`pkg/store`, `cmd/migrate`, `docs`, `hack`). Do not invent a scope the tree does not
  have; omit it for a genuinely repo-wide change.
- **`summary`** is imperative, lowercase, no trailing period, and the whole subject is at most
  72 characters. **One commit does one thing** — a subject that needs "and" is two commits.
- **Breaking changes** — a removed or renamed wire field, a changed encoding, a changed
  artifact layout — are marked both ways: `!` after the scope and a `BREAKING CHANGE:` footer
  saying what breaks and how to migrate.
- Stage by explicit path. No co-author or attribution trailers.

## 5. The pull request

PRs are squash-merged, so **the PR title is the future commit subject** and follows the same
grammar. The body follows the template, every heading kept; a section with nothing to report
says "None."

| Section | Carries |
|---|---|
| **Summary** | What changed and why, and the `Closes #N` line |
| **Gate** | The exact command that proves the change; verdict `pass` or `not run (why)`; evidence as *failing before → passing after* or, for a measurement, a table with a column saying what each row measures; whether `hack/gate.sh` was green locally |
| **Merge preconditions** | What must land first, or "None." |
| **Review** | The merge tier, and notes: every behaviour change marked *intended* or *preserved*; every seam added or removed; every cost moved somewhere else; every trade-off with its number, each marked **verified** or **inferred**; the alternatives rejected and what rejected them |
| **Ledger** | Documents, status pages, decision records, or audit files riding the PR |
| **Checklist** | Gate, tests, docs, decision record |

**Every number in a PR body has a command behind it**, run against the commit under review. A
number from memory, or from a run at an earlier sha, is not evidence. Say what did not improve
and why.

## 6. What happens next

Review is tiered by what the change can break, not by who wrote it. Tier A needs one
non-author approval; Tier B is self-merge on green CI; Tier C needs a named owner. Expected
first response is one business day for Tier A and two for Tier C; a reviewer who cannot meet
it says so rather than holding the queue. What a review must contain is in
[handbook/review-standard.md](https://github.com/NetstarGlobal/handbook/blob/main/review-standard.md).

A change that chooses a database, vendor, service, or crosses a team boundary is a proposal
until it has a decision record. Open one before the PR, not in it.

## 7. Security

A live exposure is not an issue. See [SECURITY.md](SECURITY.md).
