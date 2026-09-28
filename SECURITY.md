# Security

## Reporting an exposure

**Do not open an issue.** An issue describing a live exposure is itself an exposure, and
repositories here are read by contractors, vendors, and a documentation mirror.

Report directly to an organization owner or to the architects team. Who that is today:

```sh
gh api "orgs/NetstarGlobal/members?role=admin" --jq '.[].login'
gh api orgs/NetstarGlobal/teams/architects/members --jq '.[].login'
```

State the repository, the credential or path affected, and how you found it. If it is a
credential, **rotation comes first**; the issue is opened after rotation, labelled
`type:security`, and merges at Tier C.

## The standard

The secrets and security standard every repository is held to — no plaintext secret in
history, a full-history scan on every push, TLS verification enforced by the gate, backlog
metrics on every event loop — is
[handbook/security.md](https://github.com/NetstarGlobal/handbook/blob/main/security.md).

## Supported versions

Report against `main`. Repositories publish a supported-versions statement with their first
tagged release.
