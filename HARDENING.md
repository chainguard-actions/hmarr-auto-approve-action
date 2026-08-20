<!-- markdownlint-disable -->

# Hardening Report: hmarr--auto-approve-action/v3.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **hmarr--auto-approve-action/v3.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses action references pinned to mutable version tags instead of immutable full-length SHA commits. If the tag is moved (e.g. by a supply-chain compromise), the workflow will silently execute different code. Failing references: `actions/checkout@v2` (line 9) and `actions/setup-node@v2` (line 12). Each should be replaced with the corresponding 40-character commit SHA, e.g. `actions/checkout@<sha> # v2`.

Locations:

- `.github/workflows/ci.yml:9`
- `.github/workflows/ci.yml:12`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the only job (`test`) also has no job-level `permissions:` key. Without explicit permissions, GitHub grants the default token permissions (which can be write-all on some repository configurations), violating the principle of least privilege. A `permissions:` block with minimal required scopes (e.g. `contents: read`) should be added at the top level or on the job.

Locations:

- `.github/workflows/ci.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Pinned actions/checkout@v2 to SHA 0717577d45739eb3c851188b29f50ed6c0b2194e and actions/setup-node@v2 to SHA 7c12f8017d5436eb855f1ed4399f037a36fbd9e8 (both with # v2 comments). Added top-level `permissions: contents: read` block to enforce least-privilege token access.

