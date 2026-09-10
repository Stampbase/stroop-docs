> **Status: Draft.** Not yet reviewed. Subject to change.

# Identity model

## Core invariants

These are architecture constraints, not implementation suggestions. A change to
any line here is a protocol change and requires review before implementation.

```
1 wallet -> maximum 1 canonical profile

1 profile -> multiple verified wallets

username -> optional

Stroopy -> optional

1 profile -> maximum 1 canonical username at a time

username -> globally unique

1 profile -> one active default avatar

profile -> optional explicit mainnet payment destination

testnet wallet != mainnet payment destination

wallet association != spending authority

profile ownership != NFT ownership

NFT ownership must be independently verifiable

credential state remains separate from identity registry
```

## Why each invariant exists

**One wallet maps to at most one canonical profile.** Without this, resolving a
wallet to an identity is ambiguous, and impersonation becomes possible by
claiming a wallet already associated elsewhere.

**A profile may hold many verified wallets.** People hold keys across devices
and networks. Forcing one wallet per identity would push users toward reusing a
single key, which is worse for their security.

**A username is optional and globally unique.** Identity must not require
claiming a scarce global name. Where a name is claimed, uniqueness is what
makes it meaningful as a payment destination.

**At most one canonical username per profile at a time.** Multiple simultaneous
canonical names would make reverse resolution ambiguous.

**A testnet wallet is never a mainnet payment destination.** This is the
highest-severity invariant in the system. Violating it sends real value to an
address the recipient may not control on mainnet. Network identity must be
explicit at every layer, and the default must fail closed.

**Wallet association is not spending authority.** Linking a wallet proves
control for identity purposes. It grants the protocol no authority to move
funds, and no integrator should treat it as though it does.

**Profile ownership is not NFT ownership.** A profile pointing at a Stroopy is
a reference. Anyone displaying a character as owned must verify ownership
independently rather than trusting the pointer.

## Open questions

These are unresolved and must not be implemented until specified and reviewed:

- rename and release semantics for usernames, including anti-squatting and the
  privacy implications of username history
- controller migration and profile recovery, including what happens to linked
  wallets and claimed usernames when a controller key is lost
- the Unicode policy for usernames beyond the ASCII subset
