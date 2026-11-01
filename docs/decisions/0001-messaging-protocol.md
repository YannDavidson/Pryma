# ADR 0001 — Maintained asynchronous ratcheting protocol for PRYMA

Date: 2026-11-01
Status: Architectural direction accepted for this foundation; concrete library selection proposed, not approved for production.

## Context
PRYMA's September 2026 architecture requires device-held keys, authenticated one-to-one messaging, asynchronous delivery, and short-lived ciphertext queues. The existing browser vault protects local storage only. Its AES-GCM/PBKDF2 code is not a network messaging protocol and will not be reused as one.

## Decision
Use a maintained implementation of an authenticated asynchronous key agreement and ratcheting message protocol. Evaluate libsignal first for a native-client technical spike. Evaluate a current supported protocol profile, including PQXDH and the ratcheting options actually supported by the selected release; freeze its exact version and parameters in a follow-up ADR after testing. Do not implement cryptographic primitives or compose a custom messaging protocol.

The first alpha has one device per identity. Discovery codes are revocable lookup handles, never authentication secrets or encryption keys. Authenticate identity keys separately; provide out-of-band verification and block outgoing messages on unexpected verified-key changes until explicit approval. Do not claim Signal interoperability.

This ADR does not approve libsignal for release. Its upstream README states external use is unsupported and APIs may change. Its AGPLv3 license and the planned application distribution model need review before adoption. No libsignal dependency is added by this commit.

## Alternatives
| Option | Decision and reason |
| --- | --- |
| Maintained Signal-protocol implementation | Preferred evaluation direction: aligns with asynchronous one-to-one sessions and PRYMA's relay separation. Native bindings, upkeep and distribution remain gates. |
| Matrix Rust SDK and Matrix server architecture | Retain as an alternative if product requirements change. The SDK supplies encryption capabilities; adopting it requires an explicit assessment of server metadata, retention, rooms, and account semantics. This is an architectural fit question, not a claim that Matrix is insecure. |
| Custom Web Crypto handshake and encryption | Rejected for production. Encryption primitives alone do not supply authenticated session state, ratcheting, replay defense or compromise recovery. |
| TLS-only chat or server-readable messages | Rejected: does not satisfy device-only content access. |

## Required evidence before selecting the implementation
1. Pin upstream release/commit, supported platforms, build toolchain, license, dependency inventory and upgrade policy.
2. Build two independent clients with separate identity keys and stores.
3. Establish a session while the recipient is offline, then exchange authenticated encrypted text through an expiring relay.
4. Exercise message reordering, duplication, replay, tampering, concurrent sends and crash/restart state persistence.
5. Verify identity change blocking, contact verification and separation between code rotation and identity rotation.
6. Inspect relay storage, logs, notification payloads and crash handling for plaintext and private-key leakage.
7. Obtain distribution/license review and independent security review suitable for the release.
8. Record the chosen implementation and actual results in ADR 0002. If the candidate fails a gate, reconsider the implementation rather than silently weakening requirements.

## Consequences
Client framework selection follows the protocol-binding spike. TypeScript bindings alone do not prove browser or React Native compatibility. The product can be built around a tested library, but using a library does not certify PRYMA. Timeline and hosting choices remain open until the spike establishes requirements.

No remote delivery, post-quantum protection, end-to-end encryption, anonymity or production-readiness claim is made for the current prototype.

## Primary references (checked 2026-11-01)
- https://github.com/signalapp/libsignal — implementation, platform bridges, unsupported external-use notice and license.
- https://signal.org/docs/specifications/pqxdh/ — asynchronous agreement specification and authentication boundaries.
- https://signal.org/docs/specifications/doubleratchet/ — ratcheting protocol family; confirm supported profile against the pinned implementation.
- https://github.com/matrix-org/matrix-rust-sdk — alternative SDK and encryption component.

Product requirements derive from PRYMA_Architecture_Blueprint_v1.md, September 2026. This ADR is an implementation direction, not a replacement for its trust boundaries.
