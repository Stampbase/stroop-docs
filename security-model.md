> **Status: Draft.** Not yet reviewed. Subject to change.

# Security model

This is the threat model. For reporting a vulnerability, see
[SECURITY.md](./SECURITY.md).

## Assets worth attacking

| Asset | Consequence if compromised |
| --- | --- |
| Payment destination | Value redirected to an attacker |
| Profile controller | Full identity takeover |
| Username registry | Impersonation of a known identity |
| Wallet association | False claim of association with a wallet |
| Resolver responses | Downstream applications act on false identity data |

## Highest-severity class: network confusion

A testnet account presented as a mainnet payment destination sends real value
to an address the recipient may not control. Mitigations:

- network is explicit in every stored record, API response, and UI surface
- payment destinations are mainnet-only by construction
- setting a payment destination requires explicit user action
- there is no fallback path from a testnet association to a payment destination

## Impersonation via normalization

If two distinct inputs normalize to the same username, or if normalization is
implemented twice and the implementations disagree, an attacker can claim a name
that resolves like someone else's. Mitigations:

- one canonical normalization implementation, shared by every layer
- the registry is authoritative; client checks are advisory
- collision tests are part of the contract test suite
- Unicode is unsupported until a reviewed specification exists

## Authorization

Every state-changing operation names its authority and fails closed. The test
suite proves rejection, not only success: for each operation there is a test
that an unauthorized caller is refused.

Wallet linking requires proof of control of the wallet being linked, and that
proof is replay-resistant.

## Client trust

Client-side validation is a user-experience affordance. Availability shown in a
UI is advisory; the registry decides at write time. No surface may present a
username as claimed before the registry confirms it.

## Supply chain

- dependencies are pinned by lockfile
- GitHub Actions are pinned to immutable commit SHAs
- workflow permissions are read-only by default
- secrets are never exposed to workflows triggered by untrusted pull requests
- secret scanning runs on every pull request, with findings redacted in logs

## Privacy

Stroop profiles are public identity constructs, but public status is
deliberate, never incidental. Only explicitly profile-safe fields appear in
resolver responses.

## Logging

Never logged: signatures, authorization challenges carrying session context,
cookies, access tokens, secret keys, complete request headers, environment
variables, or private user information. Wallet addresses are public identifiers
but are logged only when operationally necessary.
