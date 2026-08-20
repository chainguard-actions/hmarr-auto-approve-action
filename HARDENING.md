<!-- markdownlint-disable -->

# Hardening Report: hmarr--auto-approve-action/v3.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **hmarr--auto-approve-action/v3.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/ci.yml references two actions using mutable version tags instead of pinned full-length SHA commit hashes. This exposes the workflow to supply-chain attacks if the tag is moved or the upstream repository is compromised.

Failing references:
- `uses: actions/checkout@v2` (line 9) — should be pinned to a full 40-character SHA
- `uses: actions/setup-node@v2` (line 13) — should be pinned to a full 40-character SHA

Locations:

- `.github/workflows/ci.yml:9`
- `.github/workflows/ci.yml:13`

### missing-permissions (severity: medium)

The workflow file .github/workflows/ci.yml has no top-level `permissions:` key and no job-level `permissions:` key on the `test` job. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions. A minimal permissions block (e.g. `permissions: read-all` or specific scopes like `contents: read`) should be added.

Locations:

- `.github/workflows/ci.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Pinned actions/checkout@v2 to SHA 0717577d45739eb3c851188b29f50ed6c0b2194e and actions/setup-node@v2 to SHA 7c12f8017d5436eb855f1ed4399f037a36fbd9e8. Added top-level `permissions: contents: read` block to restrict GITHUB_TOKEN to the minimum required for a lint/test workflow.

