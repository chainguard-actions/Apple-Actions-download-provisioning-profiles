<!-- markdownlint-disable -->

# Hardening Report: Apple-Actions--download-provisioning-profiles/v5.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Apple-Actions--download-provisioning-profiles/v5.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All four workflow files reference GitHub Actions using mutable version tags (e.g., @v6.0.0, @v5.0.0) instead of immutable full 40-character SHA commit hashes. This exposes the workflows to supply-chain attacks if a tag is moved or a dependency is compromised. Affected references: actions/checkout@v6.0.0, actions/setup-node@v5.0.0, actions/upload-artifact@v5.0.0.

Locations:

- `.github/workflows/check-dist.yml:22`
- `.github/workflows/check-dist.yml:29`
- `.github/workflows/check-dist.yml:52`
- `.github/workflows/eslint.yml:18`
- `.github/workflows/eslint.yml:24`
- `.github/workflows/knip.yml:18`
- `.github/workflows/knip.yml:24`
- `.github/workflows/prettier.yml:18`
- `.github/workflows/prettier.yml:24`

### missing-permissions (severity: medium)

None of the workflow files define a top-level `permissions:` key, and none of the individual jobs define job-level `permissions:` blocks. Without explicit permissions, workflows run with the default token permissions (which may include write access to repository contents, packages, etc.), violating the principle of least privilege.

Locations:

- `.github/workflows/check-dist.yml:1`
- `.github/workflows/eslint.yml:1`
- `.github/workflows/knip.yml:1`
- `.github/workflows/prettier.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all four workflow files (.github/workflows/check-dist.yml, eslint.yml, knip.yml, prettier.yml):
1. unpinned-uses: Pinned all action references to full 40-character SHA hashes — actions/checkout@v6.0.0 → @1af3b93b6815bc44a9784bd300feb67ff0d1eeb3, actions/setup-node@v5.0.0 → @a0853c24544627f65ddf259abe73b1d18a591444, actions/upload-artifact@v5.0.0 → @330a01c490aca151604b8cf639adc76d48f6c5d4. Original tags preserved as inline comments.
2. missing-permissions: Added top-level `permissions: contents: read` block to all four workflow files, granting only the minimum access needed for checkout and build operations.

