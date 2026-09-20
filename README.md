# Marechiaro Print Agent Releases

Public distribution repository for signed Marechiaro Print Agent updates.

## Current status

**No update channel is active yet.** This repository does not currently contain a production manifest or an installable release.

The updater must remain disabled until all of the following are complete:

- the application embeds the approved Ed25519 manifest-verification public key;
- both Windows computers trust the approved Authenticode certificate;
- the GitHub origin and redirect policy is pinned and tested;
- installation, health-check, rollback and power-loss recovery pass on both Windows versions;
- a signed, immutable release is published and independently verified.

## Distribution layout

- `channels/stable.json` - signed pointer for production releases.
- `channels/test.json` - signed pointer for controlled test releases.
- GitHub Releases - immutable installers and detached signatures.
- `docs/RELEASE-POLICY.md` - mandatory publishing and rollback rules.

Channel manifests are created only when a real signed release exists. Placeholder manifests are intentionally forbidden.

## Security model

Every update must pass all configured checks:

1. HTTPS origin and redirect allowlist.
2. Ed25519 signature over canonical manifest bytes.
3. Channel, version, architecture, minimum Windows build, size and expiry.
4. SHA-256 of the downloaded installer.
5. Authenticode signature and approved certificate thumbprint.
6. Anti-downgrade, anti-replay and contradictory-release protection.
7. ADMIN authorization, print-engine drain, health check and rollback.

Transport hosting is not trusted to authorize an update. Possession of the private signing keys is required.

## Repository rules

- Never commit private keys, PFX/P12 files, passwords, tokens, customer data, orders, logs or machine identities.
- Never commit installers to the Git history; attach them to immutable GitHub Releases.
- Never replace an existing release asset or move an existing version tag.
- Publish the signed channel manifest only after the release assets have been uploaded and verified.
- Production uses `stable`; switching channels requires explicit ADMIN authorization.

Copyright © Marechiaro. All rights reserved.
