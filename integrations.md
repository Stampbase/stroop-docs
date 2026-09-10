> **Status: Draft.** Not yet reviewed. Subject to change.

# Integrations

## Integration model

Stroop exposes one public integration surface: the SDK. Stampbase's own
applications use it on the same terms as any third party. If an integration
needs something the public SDK cannot do, that is a gap in the SDK.

## Resolution

```ts
resolve("@bastian")   // username -> profile
resolve("G...")       // wallet   -> profile
```

Consumers must handle four outcomes explicitly:

- found
- not found
- network mismatch
- resolver unavailable

Treating "resolver unavailable" as "not found" is a bug. It silently presents an
identity as nonexistent when it may exist.

## React

```tsx
<Stroopy address={address} />
<StroopName address={address} />
<StroopProfile address={address} />
```

Components must render accessible markup, expose loading and error states, and
work without a hosted dependency where the underlying data allows.

## Passport

Passport is a consumer. The boundary:

- Stroop does not depend on Passport
- Passport credential and attestation logic stays in StampRegistry
- profile creation from Passport is explicitly opt-in; no public profile is
  created without user consent
- a Discord username may *suggest* a candidate Stroop username; it never becomes
  the canonical authority
- Passport testnet wallet associations are tagged testnet and are never usable
  as a mainnet payment destination

## What resolution must never return

Public resolution returns profile-safe fields only. Data is not public merely
because it exists in Passport or another integrated application. Never surface:

- email addresses
- Discord identifiers
- authentication identifiers
- private Passport metadata
- private stamps
- session identifiers
