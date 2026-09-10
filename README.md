# Stroop Docs

> Canonical public technical documentation for the Stroop identity protocol.

Part of [Stroop](https://github.com/Stampbase), an open identity layer for
Stellar, built by [Stampbase](https://github.com/Stampbase).

## Contents

| Document | What it covers |
| --- | --- |
| [architecture.md](./architecture.md) | How the pieces fit together and what each owns |
| [identity-model.md](./identity-model.md) | Profiles, controllers, and the core invariants |
| [protocol.md](./protocol.md) | Registry operations and their authority |
| [stroopy-model.md](./stroopy-model.md) | Character protocol and its relationship to identity |
| [integrations.md](./integrations.md) | Integrating Stroop, including Passport |
| [security-model.md](./security-model.md) | Threat model and security posture |
| [roadmap.md](./roadmap.md) | Sequencing and what is deliberately deferred |

`security-model.md` is the threat model. [`SECURITY.md`](./SECURITY.md) is the
vulnerability reporting policy — they are different documents.

## Status

**Pre-alpha.** These documents describe an architecture that is largely not
yet implemented. Where a document describes behaviour, read it as a
specification to build against, not as a description of running code.

Nothing here is deployed to Stellar mainnet. Do not use any part of this
repository to custody value.

## Status of each specification

Every document states its own status at the top: **Draft**, **Reviewed**, or
**Implemented**. A specification marked Draft has not been reviewed and may
change without notice.

## Conflicts

Where a specification and an implementation disagree, that is a bug in one of
them. Open an issue. Do not silently edit the specification to match the code.

## Security

Do not report vulnerabilities through public issues. See
[`SECURITY.md`](./SECURITY.md) for private reporting.

## License

[Apache-2.0](./LICENSE).

## Related repositories

| Repository | Purpose |
| --- | --- |
| [`stroop-contracts`](https://github.com/Stampbase/stroop-contracts) | Soroban contracts: identity registry, usernames, wallet links |
| [`stroop-sdk`](https://github.com/Stampbase/stroop-sdk) | `@stroop-id/sdk` and `@stroop-id/react` |
| [`stroop-web`](https://github.com/Stampbase/stroop-web) | stroop.id — identity application |
| [`stroopy`](https://github.com/Stampbase/stroopy) | stroopy.me — character application |
| [`stroop-docs`](https://github.com/Stampbase/stroop-docs) | Protocol specifications |
