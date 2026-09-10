> **Status: Draft.** Not yet reviewed. Subject to change.

# Architecture

```
                         STAMPBASE
                             |
                       STROOP PROTOCOL
              Registry + Resolver + SDK
                             |
          +------------------+------------------+
          |                  |                  |
          v                  v                  v
      stroop.id          stroopy.me         Passport
    identity app       character app     credential app
```

Stroop is an identity layer. The registry holds canonical identity state, the
resolver reads it, and the SDK is how everything else — including Stampbase's
own applications — reaches it.

## Responsibilities

Each layer owns a distinct concern. Keeping them separate is what makes the
protocol integrable by parties who do not use the rest of the stack.

### Stroop ID

- profile identity
- username registry
- verified wallet associations
- payment destination
- avatar reference
- resolution

### Stroopy

- visual character
- ownership
- traits
- rendering
- character pages

### Passport / StampRegistry

- attestations
- credentials
- participation history

## Boundaries that must hold

**Passport is a consumer of Stroop, not a dependency of it.** Stroop must
function fully with Passport absent. Passport uses the same public SDK
interfaces available to any third party.

**Credential state stays out of the identity registry.** StampRegistry already
owns attestations. Duplicating that logic inside `IdentityRegistry` would
create two sources of truth for whether a credential is valid.

**Character ownership is not profile identity.** A profile may reference an
active Stroopy, but that reference is a pointer, not proof of ownership.
Ownership must be independently verifiable.

**Resolution must not require Stroop-operated infrastructure.** A hosted
resolver is a convenience. The SDK must be able to read canonical identity data
directly from the protocol, and must document what degrades when the hosted
service is unavailable.

## Repositories

| Repository | Layer |
| --- | --- |
| `stroop-contracts` | Canonical state — Soroban contracts |
| `stroop-sdk` | Read path — resolution and typed APIs |
| `stroop-web` | stroop.id application |
| `stroopy` | stroopy.me application |
| `stroop-docs` | This specification |
