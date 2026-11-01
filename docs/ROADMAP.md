# Alpha engineering milestones

All production tasks below are pending. Completing documentation is not completing implementation.

1. Protocol spike: meet ADR 0001 evaluation gates, pin implementation, record ADR 0002.
2. Device identity: generate keys, protect storage, create revocable discovery codes, verify peer identities, handle unexpected key changes.
3. Relay: authenticated device queues, atomic acknowledgments, expiry worker, rate and size limits, no plaintext logs. Proposed queue maximum: seven days; finalize explicitly.
4. Two-client acceptance: sender online/recipient offline; later delivery; invalid ciphertext rejected; replay not shown twice; expired envelope unavailable; blocked connection cannot send; restart does not reuse session state unsafely.
5. Local history and lifecycle: encrypted storage, atomic state updates, disappearing policy events, loss/recovery behavior and truthful deletion UI.
6. Invite-only alpha: test actual mobile devices, accessibility, upgrade/rollback, operational alerts without content, incident procedure and independent review.
7. Public beta: address review findings, document actual retention/privacy behavior, establish security-report channel and release process.

Deferred: multi-device, attachments, groups, calls, backups, nearby transport and CERVEL adapter.

Deployment is intentionally absent until a working server and client pass relevant acceptance gates. GitHub CI currently checks prototype syntax only; it must never be presented as a security test suite.
