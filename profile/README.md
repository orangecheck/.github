# OrangeCheck

**Proof of Bitcoin stake for the open web.**

A small Bitcoin balance, left unspent for a while, is the cheapest credible sybil-resistance signal on the open internet. OrangeCheck turns that signal into a portable, cryptographic, platform-neutral proof any app can verify in one API call.

> No custody. No account. No KYC. Honest users pay nothing but time; attackers pay real Bitcoin opportunity cost — ruinous at scale.

**Hosted verifier · docs · sign-in:** [**ochk.io**](https://ochk.io) · [**ochk.io/docs**](https://ochk.io/docs)

---

## Repos

| Repo | What's in it |
|---|---|
| [**oc-protocol**](https://github.com/orangecheck/oc-protocol) | The normative spec (SPEC.md, PROTOCOL.md, NIP_ORANGECHECK.md), the extension + scoring registry, the `/conformance/vectors/` test-vector set any implementation must pass, and minimal runnable `/examples/`. |
| [**oc-packages**](https://github.com/orangecheck/oc-packages) | Monorepo for the seven published JS packages + the Python SDK. Build + test + publish flow lives here. |

All code is MIT-licensed; the protocol spec is CC-BY-4.0. Fork, re-implement, self-host — that's the point.

---

## Published packages

### npm · `@orangecheck/*`

| Package | Use when |
|---|---|
| [`@orangecheck/sdk`](https://www.npmjs.com/package/@orangecheck/sdk) | TypeScript / Node / browser. `check`, `verify`, `createAttestation`, plus every lower-level building block. |
| [`@orangecheck/gate`](https://www.npmjs.com/package/@orangecheck/gate) | Drop-in sybil-gate middleware for Express, Next, Fastify, Hono, Cloudflare Workers. |
| [`@orangecheck/react`](https://www.npmjs.com/package/@orangecheck/react) | React components: `<OcBadge>`, `<OcGate>`, `<OcChallengeButton>`. |
| [`@orangecheck/wallet-adapter`](https://www.npmjs.com/package/@orangecheck/wallet-adapter) | Normalizes UniSat, Xverse, Leather, Alby behind one `sign(message)` API. |
| [`@orangecheck/cli`](https://www.npmjs.com/package/@orangecheck/cli) | `oc` shell interface — `oc check --addr ...`, `oc verify`, etc. |
| [`@orangecheck/relay-filter`](https://www.npmjs.com/package/@orangecheck/relay-filter) | Sybil filter for Nostr relays. Ships a Strfry plugin. |
| [`@orangecheck/airdrop-gate`](https://www.npmjs.com/package/@orangecheck/airdrop-gate) | Filter candidate addresses into a sybil-resistant airdrop allowlist. |

### PyPI · `orangecheck`

[`pip install orangecheck`](https://pypi.org/project/orangecheck/) — sync + async client against the hosted API plus offline canonical primitives (`build_canonical_message`, `attestation_id`, `score_v0`). Drives the same [conformance vectors](https://github.com/orangecheck/oc-protocol/tree/main/conformance/vectors) as the TypeScript SDK, so a byte-identity drift in either implementation breaks the other's CI.

---

## Quickstart

**Gate an Express route:**

```bash
yarn add @orangecheck/gate
```

```ts
import { ocGate } from '@orangecheck/gate';

app.post(
    '/post',
    ocGate({ minSats: 100_000, minDays: 30, address: { from: 'header' } }),
    postHandler
);
```

30-second interactive walkthrough: [ochk.io/docs/quickstart](https://ochk.io/docs/quickstart). Minimal runnable examples: [`oc-protocol/examples/`](https://github.com/orangecheck/oc-protocol/tree/main/examples) (Express, Next.js App Router, Hono).

---

## What OrangeCheck is NOT

- **Not reputation.** "Reputation" implies social judgment. This is a stake receipt. Don't sell it as karma.
- **Not identity.** Proof of address control + self-asserted handles ≠ proof of a human.
- **Not custody.** Funds never move. No deposits. No escrow.
- **Not on-chain.** Every attestation is an off-chain signed message. Bitcoin chain state is read, not written.

See [VISION.md](https://github.com/orangecheck/oc-protocol/blob/main/VISION.md) for the full framing.

---

## Contribute

- **Found a bug or have a spec question?** Open an issue on [oc-protocol](https://github.com/orangecheck/oc-protocol/issues) or [oc-packages](https://github.com/orangecheck/oc-packages/issues) as appropriate.
- **Writing a new implementation** (Rust, Swift, Go, ...)? Start from the [conformance vectors](https://github.com/orangecheck/oc-protocol/tree/main/conformance). If your implementation passes the 20 vectors, it agrees with the reference TS and Python SDKs byte-for-byte.
- **Licensing.** Spec under CC-BY-4.0; code under MIT. No CLA.
