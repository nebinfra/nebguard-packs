# Security Policy

## Reporting a vulnerability

Report security issues privately through GitHub: open the [Security tab](https://github.com/nebinfra/nebguard-packs/security) of this repository and choose **Report a vulnerability**, or email <security@nebinfra.com>.

Please do not open public issues or pull requests for security reports.

We aim to acknowledge new reports within 3 business days and to keep you informed while we investigate. We follow coordinated disclosure: we ask that you give us a reasonable window to ship a fix before publishing details. There is no paid bounty program at this time; we are happy to credit reporters in the release notes on request.

## Scope

This repository distributes rule packs for NebGuard. In scope here:

- Integrity or authenticity problems with any published pack artifact: a `.nebpack` container, its `.nebpack.bundle` signature file, or its `.sha256` digest sibling.
- A published pack version whose bytes change after publication (published versions are immutable by policy).
- Anything in this repository's verification instructions that could lead users into an unsafe state.

Vulnerabilities in the NebGuard binaries themselves, including policy-bypass techniques, belong in [nebinfra/nebguard-dist](https://github.com/nebinfra/nebguard-dist) per its security policy. Issues with the published verification keys belong in [nebinfra/trust](https://github.com/nebinfra/trust).

## Verifying pack artifacts

Every pack ships with a sibling `.bundle` file containing the cosign signature and the Rekor transparency-log inclusion proof; see this repository's [README](README.md#verification). Public keys live in [nebinfra/trust](https://github.com/nebinfra/trust); keys rotate quarterly and archived keys remain available for older packs.

```bash
cosign verify-blob \
  --key https://raw.githubusercontent.com/nebinfra/trust/main/cosign-keys/nebguard-prod.pub \
  --bundle <pack-id>-<version>.nebpack.bundle \
  <pack-id>-<version>.nebpack
```

A pack that fails verification is itself a security report: please tell us immediately through the channels above. NebGuard refuses unverified packs on its own, so a failing pack degrades enforcement rather than injecting content, but we still want to know.

## Supported versions

Published pack versions are immutable; fixes ship forward as a higher version of the affected pack, and only the newest version of each pack is supported. Older versions stay downloadable and remain signature-verifiable (archived keys in [nebinfra/trust](https://github.com/nebinfra/trust)), but they do not receive fixes.
