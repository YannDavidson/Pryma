# PRYMA initial threat model

Status: design requirements; controls are not yet implemented unless marked prototype-only.

## Assets and boundaries
- Device: plaintext, private identity/session keys, encrypted local history. Protect native keys with platform secure storage where supported.
- Directory: public keys and discovery records. A compromised directory can substitute keys; verification and key-change blocking are essential. Key transparency is a later design decision.
- Relay: authenticated routing and expiring ciphertext. No plaintext, private keys, address book or conversation index.
- Push provider: opaque wake-up signal only. Timing and device metadata can still exist.
- CERVEL: separate permission and storage domain. Selected export is explicit and creates a new copy.

## Threats and intended controls
| Threat | Required treatment |
| --- | --- |
| Network observer or compromised relay | Maintained E2EE protocol plus TLS; no claim to hide all timing, IP or routing metadata. |
| Directory key substitution | Out-of-band key verification, persistent trust state, blocking on verified identity changes. |
| Replayed/tampered envelopes | Protocol authentication, replay handling, bounded message state and idempotent relay acknowledgments. |
| Code enumeration and spam | High-entropy codes, scoped rate limits, requests, blocking, bounded queues and quotas. |
| Lost or stolen device | Native protected key storage, local lock, explicit recovery design. No server password reset that silently restores identity keys. |
| Recipient copying content | Disappearing messages are cooperative cleanup, not guaranteed erasure of copies. |
| Application/logging compromise | No analytics SDK access to chats; redact errors; minimize retained metadata; review updates and supply chain. |

Compromised endpoints, screenshots, recipients sharing content, and traffic-analysis resistance are not solved by content encryption. Retention schedules, recovery and abuse reporting require dedicated designs before alpha release.

## Prototype limits
The browser prototype is single-tab/local. Password encryption is local at-rest protection. Unlocked tabs expose plaintext; browser data can be deleted or rolled back. Expiration runs when the app is active or unlocked. Sample identities are not verified contacts. External font loading is removed from this repository copy to avoid that third-party request.
