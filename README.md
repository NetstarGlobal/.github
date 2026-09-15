# .github — organization-level defaults

Scaffold. This repo holds the defaults every **public** NetstarGlobal repo inherits, plus
reusable workflows any repo can call.

Its private counterpart, `.github-private`, holds the member-only organization landing page.

## What belongs here

| Path | Holds | Specified by |
|---|---|---|
| `profile/README.md` | The public organization landing page | — |
| `.github/ISSUE_TEMPLATE/` | Default issue forms | `handbook/project-tracking.md` |
| `.github/PULL_REQUEST_TEMPLATE.md` | Default PR template | `handbook/project-tracking.md` |
| `SECURITY.md` | How to report a vulnerability | `handbook/security.md` |
| `CONTRIBUTING.md` | How to contribute | `handbook/operating-model.md` |
| `workflows/` | **Reusable** workflows repos call rather than copy | `handbook/repos.md` |

## Status

Placeholders only. The CI quality gate and branch-protection rulesets are not yet written
here — see the handbook pages above for what they must enforce.
