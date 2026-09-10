# Contributing to Stroop Docs

Thanks for considering a contribution.

## Before you start

Read [`README.md`](./README.md), [`SECURITY.md`](./SECURITY.md), and
[`CLAUDE.md`](./CLAUDE.md). `CLAUDE.md` is written for AI coding agents, but its
rules on secrets, privacy, authorization, and authorship apply to everyone.

**Found a vulnerability? Do not open an issue.** Follow
[`SECURITY.md`](./SECURITY.md). Unresolved, exploitable vulnerabilities must
never be discussed in public issues or pull requests.

## Development setup

This repository is Markdown. Clone it and edit.

```bash
git clone https://github.com/Stampbase/stroop-docs.git
```

No build step.

## Testing

CI checks that every relative link resolves and runs a secret
scan. Review prose changes for accuracy against the implementation — where the
specification and an implementation disagree, open an issue rather than
silently editing the specification to match the code.

## Branches and commits

- Branch from `main`: `feat/short-description`, `fix/short-description`,
  `docs/short-description`, `chore/short-description`.
- Keep commits focused. Conventional-commit prefixes (`feat:`, `fix:`, `docs:`,
  `test:`, `chore:`) are preferred but not enforced.
- `main` is protected: changes land through a pull request with passing CI.

### Authorship

Commits must carry only human or organization authorship. Do not add
`Co-Authored-By` trailers for AI tools, "Generated with" lines, or any other
AI provenance metadata to commits, pull requests, issues, releases, source
comments, documentation, or package metadata. If you use an AI assistant, you
are the author and you are responsible for the change.

## Issues

Use the issue forms. A good issue states the problem, the intended behaviour,
and acceptance criteria that make it unambiguous when the work is done.

Do not include in a public issue: credentials, real user data, private
deployment detail, or exploitable vulnerability detail.

## Pull requests

A pull request should say what changed, why, how it was tested, and what the
security or privacy impact is. Link the issue it closes. Include screenshots
for user-visible changes.

Requirements:

- tests and lint pass
- no secrets, credentials, or `.env` files
- no real user data — see below
- protocol behaviour changes ship with tests **and** documentation in the same
  pull request
- no AI co-author or generated-by attribution

## Test data

All tests and fixtures use synthetic data. Never use real Passport users, real
private keys, production credentials, personal email addresses, or private
wallet metadata.

For Stellar tests, generate deterministic accounts that exist only for tests,
and label them clearly:

```
# TEST ONLY — NOT A REAL KEY
```

Never construct an example that could be mistaken for production secret
material.

## Code of Conduct

This project follows the [Contributor Covenant](./CODE_OF_CONDUCT.md).
