<!-- markdownlint-disable -->

# Hardening Report: hmarr--auto-approve-action/v3.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **hmarr--auto-approve-action/v3.2.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/ci.yml references two actions using mutable version tags instead of full 40-character commit SHA digests. This exposes the workflow to supply-chain attacks if the tag is moved or the upstream repository is compromised. Failing references: `actions/checkout@v3` and `actions/setup-node@v3`. Each should be pinned to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v3`.

Locations:

- `.github/workflows/ci.yml:9`
- `.github/workflows/ci.yml:12`

### missing-permissions (severity: medium)

The workflow file .github/workflows/ci.yml has no top-level `permissions:` key and the only job (`test`) also has no job-level `permissions:` block. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions. A minimal permissions block (e.g. `permissions: read-all` or specific scopes like `contents: read`) should be added at the top level or on each job.

Locations:

- `.github/workflows/ci.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Pinned actions/checkout@v3 to @a37ce9120846195fa4ece8f58b268e6043cb2f26 and actions/setup-node@v3 to @3235b876344d2a9aa001b8d1453c930bba69e610. Added top-level `permissions: contents: read` block to restrict GITHUB_TOKEN to the minimum required for this CI workflow.

