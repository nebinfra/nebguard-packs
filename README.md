# NebGuard Rule Packs

Versioned rule packs for [NebGuard](https://github.com/nebinfra/nebguard-dist). Each pack is an encrypted `.nebpack` container with a detached cosign signature bundle. NebGuard fetches and verifies packs itself; there is nothing to install manually from this repository.

## Layout

```text
packs/<pack-id>/<pack-id>-<version>.nebpack
packs/<pack-id>/<pack-id>-<version>.nebpack.bundle
packs/<pack-id>/<pack-id>-<version>.nebpack.sha256
```

Published pack versions are immutable: a version is never modified or removed after publication. Fixes and updates ship as a higher version.

## Verification

Every pack is signed with the NebGuard release key. The public key is published in [nebinfra/trust](https://github.com/nebinfra/trust). To verify a pack independently:

```bash
cosign verify-blob \
  --key cosign-keys/nebguard-prod.pub \
  --bundle <pack>.nebpack.bundle \
  <pack>.nebpack
```

The `.sha256` sibling carries the artifact digest in `shasum -a 256 -c` format.
