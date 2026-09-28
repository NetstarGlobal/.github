# .github — organization-level defaults

The defaults every NetstarGlobal repository inherits unless it carries its own, plus the
reusable workflows a repository calls rather than copies. Its private counterpart,
`.github-private`, holds the member-only organization landing page.

| Path | Holds | Specified by |
|---|---|---|
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Branch, commit, and pull-request grammar — the single source | `handbook/project-tracking.md` |
| [`SECURITY.md`](SECURITY.md) | How to report an exposure, and to whom | `handbook/security.md` |
| [`.github/PULL_REQUEST_TEMPLATE.md`](.github/PULL_REQUEST_TEMPLATE.md) | The PR body: Summary · Gate · Merge preconditions · Review · Ledger · Checklist | `CONTRIBUTING.md` §5 |
| [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE/) | Issue forms: bug, feature, decision, audit finding — each applies its `type:` label | `handbook/project-tracking.md` §2 |
| [`.github/workflows/gate.yml`](.github/workflows/gate.yml) | **Reusable.** Runs the repo's `hack/gate.sh`, then a full-history secret scan | `handbook/repos.md` §3a · `security.md` §1 |
| [`.github/workflows/pr-issue-link.yml`](.github/workflows/pr-issue-link.yml) | **Reusable.** Refuses a PR that closes no issue | `handbook/project-tracking.md` §1 |
| [`.github/workflows/docs-register.yml`](.github/workflows/docs-register.yml) | **Reusable.** Refuses a document that points at a personal machine | `handbook/documents.md` §4 |

## Calling the workflows

A repository's own `.github/workflows/ci.yml` is three jobs and nothing else:

```yaml
name: ci
on: { pull_request: {}, push: { branches: [main] } }
jobs:
  gate:
    uses: NetstarGlobal/.github/.github/workflows/gate.yml@main
    secrets: inherit
  pr-issue-link:
    if: github.event_name == 'pull_request'
    uses: NetstarGlobal/.github/.github/workflows/pr-issue-link.yml@main
  docs-register:
    uses: NetstarGlobal/.github/.github/workflows/docs-register.yml@main
```

A documents-only repository (a program repo, the handbook) passes `with: { go: false }` to
the gate and carries a `hack/gate.sh` that checks what it does hold.

## Enforcement

These checks are **advisory until the organization is on a plan that supports rulesets on
private repositories**. On the Free plan a private repository has no branch protection, no
required status checks, and no push protection, so a red check does not block a merge and
`main` accepts a direct push. The decision to change that, and the ruleset that applies once
it does, are in `handbook/project-tracking.md` §3.

**`profile/` is deliberately absent.** A `profile/README.md` here becomes the organization's
public landing page. It stays unwritten until there is something to say publicly.
