# Update channels

This directory intentionally contains no active channel manifest yet.

The first `test.json` or `stable.json` file may be published only after:

- a real immutable GitHub Release exists;
- the installer has a verified SHA-256 and Authenticode signature;
- the manifest has a valid Ed25519 signature;
- the updater's GitHub origin policy has passed automated tests;
- the corresponding Windows update and rollback test is authorized.

A missing channel manifest means **updates unavailable**, which is the required fail-closed state.
