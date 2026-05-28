# Hardening Report: peter-evans--autopep8/v2.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **peter-evans--autopep8/v2.0.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml uses a Docker image reference with a mutable version tag instead of an immutable SHA digest. `image: docker://peterevans/autopep8:2.0.0` can be silently replaced by a different image if the tag is overwritten on the registry, enabling a supply-chain attack. It should be pinned to a SHA digest, e.g. `image: docker://peterevans/autopep8@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:13`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced mutable Docker image tag `docker://peterevans/autopep8:2.0.0` with immutable SHA digest `docker://peterevans/autopep8@sha256:6c914552981db6fc3fdbd72f69c005a8ad06034462f45b52e60fdb33359e1ee2` in action.yml line 13. The original tag `2.0.0` is preserved as a comment outside the YAML quotes for readability.

