<!-- markdownlint-disable -->

# Hardening Report: hmarr--auto-approve-action/v3.2.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **hmarr--auto-approve-action/v3.2.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/ci.yml references actions using mutable version tags instead of pinned full-length SHA commit hashes. Specifically: `uses: actions/checkout@v3` and `uses: actions/setup-node@v3`. These tag-based references can be silently updated to point to different (potentially malicious) commits, creating a supply-chain risk.

Locations:

- `.github/workflows/ci.yml:8`
- `.github/workflows/ci.yml:11`

### missing-permissions (severity: medium)

The workflow file .github/workflows/ci.yml has no top-level `permissions:` key and the single job `test` also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (e.g., write access to contents, pull-requests, etc.). Explicit minimal permissions should be declared.

Locations:

- `.github/workflows/ci.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/ci.yml: (1) Pinned actions/checkout@v3 to full SHA a37ce9120846195fa4ece8f58b268e6043cb2f26 and actions/setup-node@v3 to full SHA 3235b876344d2a9aa001b8d1453c930bba69e610, preserving version tags as comments. (2) Added top-level `permissions: {}` to deny all permissions by default, and job-level `permissions: contents: read` for the test job since it needs to check out the repository code.

