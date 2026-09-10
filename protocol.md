> **Status: Draft.** Not yet reviewed. Subject to change.

# Protocol

Registry operations and the authority required for each. Nothing in this
document is implemented yet; it is the specification to build against.

## Authority model

Every state-changing operation names its authority explicitly. Operations fail
closed: if authority cannot be established, the operation is rejected rather
than falling back to a weaker check.

| Operation | Authority | Notes |
| --- | --- | --- |
| Create profile | The controller being registered | Emits a creation event |
| Claim username | Profile controller | Global uniqueness enforced at write time |
| Release username | Profile controller | Semantics unspecified — see identity-model.md |
| Link wallet | Profile controller **and** proof of control of the wallet | Replay-resistant |
| Unlink wallet | Profile controller | |
| Set active avatar | Profile controller | Reference validity checked |
| Set payment destination | Profile controller | Mainnet only; explicit user action |

## Username normalization

Normalization happens exactly once, through shared canonical logic used by every
layer. Two inputs that normalize to the same canonical form are the same
username, and the registry must reject the second claim.

Current rules:

- 3 to 24 characters
- lowercase letters, digits, hyphen, underscore
- must not begin or end with a hyphen or underscore
- must contain at least one letter
- a reserved set is held back for protocol and network names

The Unicode policy is deliberately unspecified. Do not add Unicode support
without a written specification — homoglyph collisions are an impersonation
vector, not a feature request.

## Events

Every state change emits an event carrying enough information for an indexer to
reconstruct state without replaying full history. Events must not contain
private data.

## Network separation

Contract identifiers, RPC endpoints, and payment destinations are network-tagged
at every layer. A resolver response states the network it describes. Consumers
must treat a network mismatch as an error, never as a fallback.
