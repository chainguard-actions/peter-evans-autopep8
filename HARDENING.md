<!-- markdownlint-disable -->

# Hardening Report: peter-evans--autopep8/v2.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **peter-evans--autopep8/v2.0.0** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

action.yml uses a Docker image referenced by a mutable tag rather than a SHA digest: `image: 'docker://peterevans/autopep8:2.0.0'`. This is vulnerable to supply-chain attacks if the tag is overwritten. It should use a SHA digest like `docker://peterevans/autopep8@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:13`

### unpinned-uses (severity: high)

Workflow files contain `uses:` references pinned to mutable tags/versions instead of full 40-character commit SHAs. Affected references: autopep8.yml — `actions/checkout@v2`, `peter-evans/create-pull-request@v3`, `peter-evans/create-or-update-comment@v1`; dockerhub-description.yml — `actions/checkout@v2`, `peter-evans/dockerhub-description@v2.4.1`; slash-command-dispatch.yml — `peter-evans/slash-command-dispatch@v2`. These should be pinned to full commit SHAs.

Locations:

- `.github/workflows/autopep8.yml:9`
- `.github/workflows/autopep8.yml:11`
- `.github/workflows/autopep8.yml:14`
- `.github/workflows/autopep8.yml:19`
- `.github/workflows/dockerhub-description.yml:13`
- `.github/workflows/dockerhub-description.yml:15`
- `.github/workflows/slash-command-dispatch.yml:9`

### missing-permissions (severity: medium)

None of the workflow files define a top-level `permissions:` key, and no job within them defines job-level `permissions:` either. This means workflows run with the default (broad) token permissions. Explicit minimal permissions should be declared in each workflow.

Locations:

- `.github/workflows/autopep8.yml:1`
- `.github/workflows/dockerhub-description.yml:1`
- `.github/workflows/slash-command-dispatch.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all findings across 4 files: (1) action.yml: pinned Docker image peterevans/autopep8:2.0.0 to SHA digest sha256:6c914552981db6fc3fdbd72f69c005a8ad06034462f45b52e60fdb33359e1ee2, preserving the tag and docker:// scheme. (2) autopep8.yml: pinned actions/checkout@v2, peter-evans/create-pull-request@v3, and peter-evans/create-or-update-comment@v1 to full commit SHAs; added top-level `permissions: {}`. (3) dockerhub-description.yml: pinned actions/checkout@v2 and peter-evans/dockerhub-description@v2.4.1 to full commit SHAs; added top-level `permissions: {}`. (4) slash-command-dispatch.yml: pinned peter-evans/slash-command-dispatch@v2 to full commit SHA; added top-level `permissions: {}`.

