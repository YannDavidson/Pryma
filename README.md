# PRYMA

**Private by default. Yours by design.**

Production development foundation for a code-based private messenger. **Pre-alpha: this repository does not yet implement remote messaging or a production encryption protocol.**

## What exists
`apps/prototype/` preserves the original interactive browser prototype: local conversations, sample requests, retention controls, selected-message export, and an optional password-encrypted browser vault. It is not a secure messaging client. Do not enter sensitive data.

Run the prototype with Python 3:

```sh
python3 -m http.server 8080 --bind 127.0.0.1 --directory apps/prototype
```

Open http://localhost:8080. Check its JavaScript syntax with:

```sh
node --check apps/prototype/app.js
```

## Engineering decisions
- [ADR 0001: protocol direction and implementation gate](docs/decisions/0001-messaging-protocol.md)
- [Trust boundaries](docs/THREAT_MODEL.md)
- [Alpha milestones and acceptance tests](docs/ROADMAP.md)
- [Security policy](SECURITY.md)

## First release target
One-to-one text, one device per identity, changeable discovery codes, explicit requests, contact verification, encrypted device history, ciphertext-only relay queues, delivery acknowledgments and blocking. No phone discovery, address-book upload, AI content processing, automatic CERVEL capture, groups or calls.

## Intended future components
Mobile clients; a protocol adapter around a maintained library; code directory; authenticated expiring relay; integration tests across two clients. These are planned components, not working services.

## Release status
Only syntax validation is configured. No security audit, two-device test, deployment pipeline or production backend exists. The prototype's existing hosted deployment is separate; this repository does not contain its hosting identity or credentials.

No project-wide open-source license has been selected. Third-party dependencies must retain their licenses; library licensing and distribution review precedes adoption.
