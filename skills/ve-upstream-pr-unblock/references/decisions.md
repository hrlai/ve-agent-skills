# Choices to explain and resolve

Use these as conversation aids, not as permission to alter data. State a
recommended default and a short tradeoff. Ask only when the choice affects work
outside the approved VE pin or when the user's preference is not already clear.

## Obtain new upstream example inputs

- Default: Copy exact files from an approved full SHA; let the user stage or
  upload them.
- Tradeoff: Inputs stay reproducible with limited code changes; record source
  SHA, paths, and checksums. A duplicated generator can drift and needs
  maintenance.

## Which VE pin to use

- Default: Use the current full PR head SHA.
- Check: A newer head may differ from the input provenance SHA; record both. If
  the PR is closed, merged, or changes during setup, confirm which commit to
  test.

## Which dependency group to repoint

- Default: Reuse the repository's existing pinned test group.
- Tradeoff: Fewer groups and simpler lockfile; only one PR target can be active
  in that group. A separate group allows parallel pins but adds maintenance.

## Where to stage configs and inputs

- Default: Use sibling PR-specific directories only if local conventions and
  path resolution support them.
- Check: Equal directory depth can simplify later promotion, but relative paths
  still need verification. Do not move active files.

## Who stages or uploads scenario files

- Default: The user, commonly via Globus.
- Tradeoff: This avoids agent-written data in ignored or externally managed
  locations. The agent may prepare an exact file list and provenance record.

Do not ask the user to choose scientific parameter values as part of this
workflow. This skill does not evaluate whether upstream data or parameters are
scientifically appropriate.
