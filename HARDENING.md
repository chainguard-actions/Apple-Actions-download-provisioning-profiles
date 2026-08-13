<!-- markdownlint-disable -->

# Hardening Report: Apple-Actions--download-provisioning-profiles/v4.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Apple-Actions--download-provisioning-profiles/v4.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All four workflow files reference GitHub Actions using mutable version tags (e.g. @v4.2.2, @v4.3.0, @v4.6.2) instead of immutable 40-character SHA commit digests. This exposes the workflow to supply-chain attacks if a tag is moved or overwritten. Affected references: actions/checkout@v4.2.2, actions/setup-node@v4.3.0, actions/upload-artifact@v4.6.2.

Locations:

- `.github/workflows/check-dist.yml:18`
- `.github/workflows/check-dist.yml:23`
- `.github/workflows/check-dist.yml:46`
- `.github/workflows/depcheck.yml:16`
- `.github/workflows/depcheck.yml:22`
- `.github/workflows/eslint.yml:16`
- `.github/workflows/eslint.yml:22`
- `.github/workflows/prettier.yml:16`
- `.github/workflows/prettier.yml:22`

### missing-permissions (severity: medium)

None of the four workflow files define a top-level or job-level 'permissions:' block. Without explicit permissions, workflows inherit the default repository token permissions (which may include write access), violating the principle of least privilege. Each workflow should declare minimal required permissions (e.g. 'contents: read').

Locations:

- `.github/workflows/check-dist.yml:1`
- `.github/workflows/depcheck.yml:1`
- `.github/workflows/eslint.yml:1`
- `.github/workflows/prettier.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all four workflow files (.github/workflows/check-dist.yml, depcheck.yml, eslint.yml, prettier.yml):

1. unpinned-uses: Replaced all mutable version tags with immutable 40-character SHA digests:
   - actions/checkout@v4.2.2 → @11bd71901bbe5b1630ceea73d27597364c9af683 # v4.2.2
   - actions/setup-node@v4.3.0 → @cdca7365b2dadb8aad0a33bc7601856ffabcc48e # v4.3.0
   - actions/upload-artifact@v4.6.2 → @ea165f8d65b6e75b540449e92b4886f43607fa02 # v4.6.2

2. missing-permissions: Added top-level `permissions: contents: read` block to all four workflow files. This is the minimum permission needed for the checkout step; no write permissions are required by any of these workflows.

