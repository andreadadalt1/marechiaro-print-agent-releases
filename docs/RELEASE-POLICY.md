# Release Policy

This policy applies to every Marechiaro Print Agent update distributed from this repository.

## Required release order

1. Build from a clean, reviewed source commit.
2. Produce the Windows x64 installer for the supported runtime.
3. Sign the installer with the approved Authenticode certificate.
4. Calculate the installer size and SHA-256.
5. Create the versioned manifest with an immutable asset URL.
6. Sign the canonical manifest bytes with the approved Ed25519 release key.
7. Verify the installer, manifest and signatures independently.
8. Create a new immutable GitHub Release and upload the installer and detached signatures.
9. Download the published assets and verify them again.
10. Publish the signed channel manifest last.
11. Test update, restart, health check and rollback on the authorized Windows test machine before promoting to `stable`.

## Immutability

- Every version receives a unique permanent tag.
- Published tags and release assets must never be replaced.
- A correction requires a higher version.
- Rollback is performed by the installed updater restoring its locally retained previous version, not by republishing an older release as current.
- The stable channel must never point to a lower or previously rejected version.

## Channels

- `test` is used for controlled validation.
- `stable` is used by production installations.
- Channel changes require an authenticated ADMIN action.
- Promotion copies verified metadata to the stable channel; it does not rebuild or replace the tested artifact.

## Key handling

Private Ed25519 and Authenticode keys must never be stored in:

- this repository;
- GitHub Actions variables, artifacts, logs or caches;
- application binaries;
- support archives;
- chat messages;
- the update server.

Only public verification material and certificate thumbprints may be committed. Private keys must be generated and stored in an approved offline or hardware-protected location with a documented recovery backup.

## Failure behavior

If the manifest, signature, hash, certificate, version, channel, architecture, Windows build, URL, redirect, size or local state cannot be verified, the updater must fail closed. It must not install, downgrade, retry a print job or clear an ambiguous printing state.

## Audit evidence

Each release record must preserve:

- source commit;
- builder version;
- application version;
- channel;
- artifact filename and size;
- SHA-256;
- signing certificate thumbprint;
- manifest signing key identifier;
- release timestamp;
- validation results for each supported Windows computer.

No customer data, orders, addresses, print payloads or secrets may appear in release evidence.
