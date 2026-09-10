> **Status: Draft.** Not yet reviewed. Subject to change.

# Stroopy model

Stroopy is the character layer. It is optional, and it is not identity.

## Character record

| Field | Notes |
| --- | --- |
| Number | Permanent, sequential, never reused |
| Owner | Independently verifiable, not implied by a profile reference |
| Seed | Determines traits; fixed at generation |
| Traits | Derived deterministically from the seed and asset pack |
| Renderer version | Which renderer produced a given rendering |
| Asset pack hash | Content hash of the pack the traits refer to |

## Determinism

The same seed, asset pack, and renderer version must always produce byte-identical
output. Renderer changes that alter output require a new renderer version;
existing characters keep rendering under the version they were generated with.

## Generation security

Generation must be resistant to manipulation. Specifically:

- a user must not be able to re-roll to a preferred outcome
- a user must not be able to predict and select an outcome before committing
- entropy assumptions must be written down and reviewed

No custom cryptographic construction may be introduced here without review.

## Relationship to identity

A profile may point at an active Stroopy. That pointer is a display preference.
It is not proof of ownership, and any surface presenting a character as owned
must verify ownership against the authoritative source.

Before mainnet minting exists, no surface may present a character as an owned
NFT.
