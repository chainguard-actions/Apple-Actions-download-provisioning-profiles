<!-- markdownlint-disable -->

# Hardening Report: Apple-Actions--download-provisioning-profiles/v4.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Apple-Actions--download-provisioning-profiles/v4.0.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All four workflow files use mutable version-tag refs instead of pinned 40-character SHA digests, making them vulnerable to supply-chain attacks if the upstream action tags are moved or compromised. Failing references: actions/checkout@v4.2.2, actions/setup-node@v4.4.0, actions/upload-artifact@v4.6.2.

Locations:

- `.github/workflows/check-dist.yml:21`
- `.github/workflows/check-dist.yml:27`
- `.github/workflows/check-dist.yml:47`
- `.github/workflows/eslint.yml:18`
- `.github/workflows/eslint.yml:24`
- `.github/workflows/knip.yml:18`
- `.github/workflows/knip.yml:24`
- `.github/workflows/prettier.yml:18`
- `.github/workflows/prettier.yml:24`

### missing-permissions (severity: medium)

None of the four workflow files declare a top-level `permissions:` key, and none of the individual jobs declare job-level `permissions:` keys. Without explicit permissions, GitHub Actions defaults to the repository's default token permissions, which may be overly broad (e.g., write access to contents). Each workflow should declare the minimal required permissions.

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

1. unpinned-uses: Replaced all mutable version-tag refs with full 40-character SHA digests, preserving the tag as a comment:
   - actions/checkout@v4.2.2 → @11bd71901bbe5b1630ceea73d27597364c9af683 # v4.2.2
   - actions/setup-node@v4.4.0 → @49933ea5288caeca8642d1e84afbd3f7d6820020 # v4.4.0
   - actions/upload-artifact@v4.6.2 → @ea165f8d65b6e75b540449e92b4886f43607fa02 # v4.6.2

2. missing-permissions: Added top-level `permissions: contents: read` to all four workflow files. These workflows only checkout code and run build/lint tools, so read access to contents is the minimal required permission.

