# OrangeCheck

**Six verbs. One Bitcoin address. The protocol surface of the sovereign web.**

Identity, confidentiality, legitimacy, provenance, authority, commitment —
six composable protocols on Bitcoin. No custody. No token. No issuer. Every
artifact verifies offline, forever.

A small Bitcoin balance, left unspent for a while, is the cheapest credible
economic signal on the open internet. OrangeCheck is the family of open
protocols that turns that signal into portable, cryptographic, platform-neutral
proofs — for sybil resistance, end-to-end encryption, sovereign declarations,
stake-weighted polls, scoped agent delegation, and bonded commitments.

> No custody. No KYC. No aggregated reputation score. No captured intermediary.
> Honest users pay nothing but time; attackers pay real Bitcoin opportunity
> cost — ruinous at scale.

**Hosted reference apps · docs · sign-in:**
[**ochk.io**](https://ochk.io) ·
[**docs.ochk.io**](https://docs.ochk.io)

---

## The family — six verbs of sovereign sociality

Every protocol shares the same shape: a BIP-322 signature from a Bitcoin
address over a canonical, human-readable message. Learn that one shape and the
rest of the family pattern-matches.

| Verb         | Protocol                                              | Subdomain                                          | What it does                                                                                                                |
| ------------ | ----------------------------------------------------- | -------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| **am**       | [**OC Attest**](https://attest.ochk.io)               | [`attest.ochk.io`](https://attest.ochk.io)         | Sybil resistance via proof of Bitcoin stake. Sign one message; any verifier checks N sats unspent for N days. The base layer. |
| **whisper**  | [**OC Lock**](https://lock.ochk.io)                   | [`lock.ochk.io`](https://lock.ochk.io)             | End-to-end encryption addressed to a Bitcoin address. X25519 device keys bound via BIP-322. No key server, no account.        |
| **decide**   | [**OC Vote**](https://vote.ochk.io)                   | [`vote.ochk.io`](https://vote.ochk.io)             | Stake-weighted, sybil-resistant polls. Three canonical weight modes. Deterministic, cross-impl-testable tally.              |
| **declare**  | [**OC Stamp**](https://stamp.ochk.io)                 | [`stamp.ochk.io`](https://stamp.ochk.io)           | Bitcoin-block-anchored signed statements. BIP-322 + OpenTimestamps. Replaces PGP + OTS + C2PA in one envelope.              |
| **delegate** | [**OC Agent**](https://agent.ochk.io)                 | [`agent.ochk.io`](https://agent.ochk.io)           | Scoped, revocable, BIP-322-bound delegation authority. Every agent action is signed, scoped, non-repudiable.                |
| **swear**    | [**OC Pledge**](https://pledge.ochk.io)               | [`pledge.ochk.io`](https://pledge.ochk.io)         | Forward-looking, bond-backed commitments to future-verifiable propositions. Enforcement by exposure, never by custody.       |

The family is **closed at six.** OC Attest is the base layer; the other five
are peers that may optionally reference an Attest proof as a stake-at-signing
signal. Every protocol's specification, threat model, and reference impls live
in their own repo. Everything composes — gate predicates, vote-resolved
disputes, stamp-published pledges, agent-signed envelopes — but no protocol
depends on another at the wire level.

---

## Spec repos

Every protocol ships under the same canonical layout:
`README.md / PROTOCOL.md / SPEC.md / WHY.md / SECURITY.md / CHANGELOG.md /
LICENSE / test-vectors/ /examples/`. Specs are CC-BY-4.0; example code is MIT.

| Repo                                                                                         | Spec for                                          |
| -------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| [`oc-attest-protocol`](https://github.com/orangecheck/oc-attest-protocol)                    | OC Attest — proof of Bitcoin stake (the base layer) |
| [`oc-lock-protocol`](https://github.com/orangecheck/oc-lock-protocol)                        | OC Lock — sealed envelopes addressed to a BTC address |
| [`oc-vote-protocol`](https://github.com/orangecheck/oc-vote-protocol)                        | OC Vote — stake-weighted polls + tally           |
| [`oc-stamp-protocol`](https://github.com/orangecheck/oc-stamp-protocol)                      | OC Stamp — BIP-322 + OpenTimestamps envelopes    |
| [`oc-agent-protocol`](https://github.com/orangecheck/oc-agent-protocol)                      | OC Agent — delegation + scope grammar            |
| [`oc-pledge-protocol`](https://github.com/orangecheck/oc-pledge-protocol)                    | OC Pledge — bonded commitments + resolution      |

A **protocol-level conformance vector** in any spec repo is a `(input,
expected_output)` JSON tuple that every reference implementation MUST pass
byte-identically. A new implementation joins the family by passing every
vector for the protocols it implements.

---

## Reference implementations

| Repo                                                                                | Contents                                                                |
| ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| [**`oc-packages`**](https://github.com/orangecheck/oc-packages)                     | Monorepo. 22 published `@orangecheck/*` packages on npm + the Python SDK. |
| [**`oc-www`**](https://github.com/orangecheck/oc-www)                               | Hosted umbrella site + auth host (ochk.io / signin / dashboard / JWKS). |
| [**`oc-docs`**](https://github.com/orangecheck/oc-docs)                             | Unified docs site (docs.ochk.io). 80 MDX pages — one section per protocol + shared concepts + SDK reference. |
| [**`oc-attest-web`**](https://github.com/orangecheck/oc-attest-web)                 | Reference app at attest.ochk.io.                                        |
| [**`oc-lock-web`**](https://github.com/orangecheck/oc-lock-web)                     | Reference app at lock.ochk.io.                                          |
| [**`oc-vote-web`**](https://github.com/orangecheck/oc-vote-web)                     | Reference app at vote.ochk.io.                                          |
| [**`oc-stamp-web`**](https://github.com/orangecheck/oc-stamp-web)                   | Reference app at stamp.ochk.io.                                         |
| [**`oc-agent-web`**](https://github.com/orangecheck/oc-agent-web)                   | Reference app at agent.ochk.io.                                         |
| [**`oc-pledge-web`**](https://github.com/orangecheck/oc-pledge-web)                 | Reference app at pledge.ochk.io.                                        |

All code is MIT. Specs are CC-BY-4.0. Fork, re-implement, self-host — that's
the point.

---

## Published packages

### npm · `@orangecheck/*` (22 packages)

**Core (one per protocol):**

| Package                                                                                              | Protocol  | Role                                                                |
| ---------------------------------------------------------------------------------------------------- | --------- | ------------------------------------------------------------------- |
| [`@orangecheck/sdk`](https://www.npmjs.com/package/@orangecheck/sdk)                                 | Attest    | TypeScript core — `check`, `verify`, `createAttestation`.           |
| [`@orangecheck/lock-core`](https://www.npmjs.com/package/@orangecheck/lock-core)                     | Lock      | Sealed-envelope format + `seal()` / `unseal()`.                     |
| [`@orangecheck/lock-crypto`](https://www.npmjs.com/package/@orangecheck/lock-crypto)                 | Lock      | Narrow crypto primitives (X25519, HKDF, AES-GCM).                   |
| [`@orangecheck/lock-device`](https://www.npmjs.com/package/@orangecheck/lock-device)                 | Lock      | Device-key management + Nostr kind-30078 directory.                 |
| [`@orangecheck/vote-core`](https://www.npmjs.com/package/@orangecheck/vote-core)                     | Vote      | Reference impl + the deterministic `tally()` pure function.         |
| [`@orangecheck/stamp-core`](https://www.npmjs.com/package/@orangecheck/stamp-core)                   | Stamp     | Canonical message + envelope format + `stamp()` / `verify()`.       |
| [`@orangecheck/stamp-ots`](https://www.npmjs.com/package/@orangecheck/stamp-ots)                     | Stamp     | OpenTimestamps calendar client + proof helpers.                     |
| [`@orangecheck/agent-core`](https://www.npmjs.com/package/@orangecheck/agent-core)                   | Agent     | Delegation + action envelopes, scope parser, BIP-322 verifier.      |
| [`@orangecheck/agent-signer`](https://www.npmjs.com/package/@orangecheck/agent-signer)               | Agent     | Helpers for signing delegations + actions.                          |
| [`@orangecheck/agent-mcp`](https://www.npmjs.com/package/@orangecheck/agent-mcp)                     | Agent     | Model Context Protocol bridge for LLM tool calls.                   |

**Integrations + middleware:**

| Package                                                                                              | Use when                                                            |
| ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| [`@orangecheck/gate`](https://www.npmjs.com/package/@orangecheck/gate)                               | Drop-in HTTP middleware (Express / Next / Fastify / Hono / Workers). |
| [`@orangecheck/react`](https://www.npmjs.com/package/@orangecheck/react)                             | React components: `<OcBadge>`, `<OcGate>`, `<OcChallengeButton>`.   |
| [`@orangecheck/vote-react`](https://www.npmjs.com/package/@orangecheck/vote-react)                   | React components for OC Vote poll creation + tally rendering.       |
| [`@orangecheck/wallet-adapter`](https://www.npmjs.com/package/@orangecheck/wallet-adapter)           | Normalizes UniSat / Xverse / Leather / Alby behind `sign(message)`. |
| [`@orangecheck/auth-client`](https://www.npmjs.com/package/@orangecheck/auth-client)                 | `<OcSessionProvider>` + `useOcSession()` for cross-subdomain auth.  |
| [`@orangecheck/auth-core`](https://www.npmjs.com/package/@orangecheck/auth-core)                     | Crypto-only Ed25519 JWT verify + cookie helpers (consumer side).    |
| [`@orangecheck/relay-filter`](https://www.npmjs.com/package/@orangecheck/relay-filter)               | Strfry / Nostr-relay plugin — reject events from unbonded npubs.    |
| [`@orangecheck/airdrop-gate`](https://www.npmjs.com/package/@orangecheck/airdrop-gate)               | Filter candidate addresses into a sybil-resistant airdrop allowlist. |

**CLIs:**

| Package                                                                                          | Bin                       |
| ------------------------------------------------------------------------------------------------ | ------------------------- |
| [`@orangecheck/cli`](https://www.npmjs.com/package/@orangecheck/cli)                             | `oc`                      |
| [`@orangecheck/stamp-cli`](https://www.npmjs.com/package/@orangecheck/stamp-cli)                 | `stamp` · `git-stamp`     |
| [`@orangecheck/vote-cli`](https://www.npmjs.com/package/@orangecheck/vote-cli)                   | `oc-vote`                 |
| [`@orangecheck/agent-cli`](https://www.npmjs.com/package/@orangecheck/agent-cli)                 | `oc-agent`                |

### PyPI · `orangecheck`

[`pip install orangecheck`](https://pypi.org/project/orangecheck/) — sync +
async client against the OrangeCheck hosted API, plus offline canonical
primitives. Shares conformance vectors with `@orangecheck/sdk`; a byte-identity
drift in either implementation breaks the other's CI.

---

## Quickstart

**Sybil-gate a route in five lines:**

```ts
import { ocGate } from '@orangecheck/gate';

app.post(
    '/post',
    ocGate({ minSats: 100_000, minDays: 30, address: { from: 'header' } }),
    postHandler,
);
```

**Sign in with Bitcoin** end-to-end (cross-subdomain auth host):

```bash
yarn add @orangecheck/auth-client
```

```tsx
import { OcSessionProvider, OcSignInButton, useOcSession } from '@orangecheck/auth-client';

function App() {
    return (
        <OcSessionProvider>
            <Page />
        </OcSessionProvider>
    );
}

function Page() {
    const { status, account } = useOcSession();
    return status === 'authenticated' ? <Dashboard /> : <OcSignInButton />;
}
```

Per-protocol quickstarts: [docs.ochk.io](https://docs.ochk.io). One-page
narrative for any new reader: [docs.ochk.io/getting-started/which-protocol](https://docs.ochk.io/getting-started/which-protocol).

---

## What OrangeCheck is NOT

Read this list twice. These are visible refusals — design constraints, not
omissions.

- **Not custodial.** No protocol in the family ever holds sats. Funds never
  move. Bonds and stake are economic signals, not balances under contract
  control.
- **Not slashing-based.** No actor — protocol, counterparty, voter, oracle —
  can seize bonded sats. Ever. Teeth come from public records, not lockup.
- **Not aggregated reputation.** Every protocol ships raw metrics
  (`sats_bonded`, `days_unspent`, `kept_count`, `broken_count`) and refuses
  to ship a canonical score. Platforms compose policy from raw queries.
- **Not proof of personhood.** One address can be one human, ten, or zero.
  For one-human-one-vote, look at World ID or BrightID.
- **Not legal.** Produces evidence admissible in jurisdictions that recognise
  digital signatures. Does not produce judgements. Does not replace courts.
- **Not a smart-contract platform.** No VM, no gas, no on-chain state writes.
  Everything is off-chain canonical envelopes plus reads of public Bitcoin
  and Nostr state.

If your design only works on Ed25519 (no economic layer, no non-malleable
time, no enumerable identity namespace), it doesn't belong in this family.

---

## Contribute

- **Bug or spec question?** Open an issue on the relevant
  [`oc-*-protocol`](https://github.com/orangecheck) repo (specification),
  the relevant [`oc-*-web`](https://github.com/orangecheck) repo (reference
  app), or [`oc-packages`](https://github.com/orangecheck/oc-packages)
  (publishable code).
- **Writing a new implementation** (Rust, Swift, Go, Elixir, anything)? Start
  from the conformance vectors in the relevant `oc-*-protocol` repo. If your
  implementation passes the vectors byte-identically, it agrees with the
  reference TypeScript and Python implementations exactly.
- **Building something on top?** [Get in touch](https://ochk.io/contact) —
  happy to wire up gate predicates, pledge resolution mechanisms, or
  custom integrations.
- **Licensing.** Specs CC-BY-4.0 · Code MIT · No CLA.
