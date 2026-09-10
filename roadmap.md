> **Status: Draft.** Not yet reviewed. Subject to change.

# Roadmap

Sequencing, and what is deliberately deferred. No dates: this is dependency
order, not a schedule.

## V0 — Validation

Prove the identity architecture end to end on testnet before building breadth.

## V1 — Identity Registry

Profiles, controllers, canonical usernames, verified wallet linking, avatar
references, payment destinations.

## V1 — Resolver + SDK

The public read path. Username and wallet resolution, a versioned response
schema, a public resolver service, and direct protocol fallback.

## V1 — Stroopy

Character protocol, deterministic renderer, asset manifest, character routes.

## V1 — Integrations

Passport as a consumer, plus worked examples for third-party integrators.

## Future

Explicitly out of scope for V1, and listed to make the boundary clear rather
than to imply commitment:

daily character auctions, seasonal asset packs, an artist contribution system,
community treasury, DAO membership and governance, organization profiles,
application identities, advanced payment routing, Soroban Domains
interoperability, additional SDK languages, wallet-specific avatar overrides,
advanced profile recovery, character customization, marketplace support.

## Implementation order

1. Finalize identity invariants. No contract code should outrun the identity
   model.
2. Implement testnet profile creation and the username registry, so that
   `@bastian` exists canonically.
3. Implement SDK resolution, so that `resolve("@bastian")` returns the canonical
   profile.
4. Connect the existing reservation UI to the real testnet path, replacing mock
   availability and claiming.
5. Implement wallet linking, only once the controller model is stable.
6. Build the initial Stroopy renderer.
7. Integrate Passport through the same public SDK interfaces.
