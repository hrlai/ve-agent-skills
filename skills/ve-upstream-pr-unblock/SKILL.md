---
name: ve-upstream-pr-unblock
description: >-
  Help Virtual Ecosystem data scientists assess an upstream PR against one
  `ve_data_science` scenario, stage a safe test setup, and hand over a run
  command. Never runs VE.
---

# Prepare a scenario to test an upstream VE PR

Use when a user wants to check whether a scenario in
`ImperialCollegeLondon/ve_data_science` can run with a pull request from
`ImperialCollegeLondon/virtual_ecosystem` (for example, "test maliau_2 with VE
PR 1958"). Explain technical choices in plain language; do not assume the user
is a software developer.

This skill assesses one scenario, prepares an approved test environment, and
hands the run command to the user. It does not run simulations or assess
scientific validity.

## Safety and scope

- Never run `ve_run`, a simulation, or a command that starts model execution.
  Give the user the command only after setup and path checks succeed.
- Work on one named scenario and one upstream PR. Ask if either is unclear.
- Never recalibrate parameters, compare scientific results, or search for
  literature. Treat upstream parameter values as supplied, not validated.
- Never change active scenario data/config, combined configs, other scenarios,
  or `.gitignore`. Do not force-add ignored files.
- Scenario data and individual configs may be Globus-managed. Do not copy,
  generate, upload, or edit them without the user's explicit choice. Do not
  claim a Globus-only path exists when you cannot inspect it.
- Preserve existing user changes. Check `git status` before editing. If an
  existing change conflicts with the proposed setup, stop and ask; never
  overwrite or clean it.
- Pin VE to an exact, full commit SHA, not a branch or moving tag. Never open or
  update a PR unless asked.
- Only change the existing VE test pin and its lockfile as setup. Ask before
  widening scope or editing staged scenario files.

## Workflow

1. **Orient.** Read this skill's `references/conventions.md` and the consuming
   repository's instructions. Confirm repository root, requested scenario,
   PR, current pin/group, and working-tree status. Use repository conventions
   as defaults, not facts: inspect the actual config before changing it.
2. **Inspect the scenario.** Find its config and relevant paths without
   scanning large datasets. Identify which files are tracked, ignored, or
   externally managed. Do not infer a path or data availability from a
   scenario name.
3. **Triage the live PR.** Check its current state, base branch, head SHA,
   changed files, and relevant diffs. Read upstream docs or code at that SHA
   when needed to understand new inputs or config requirements. Summarize the
   change in non-specialist language and connect each requirement to the
   requested scenario. Distinguish the test SHA from any older SHA that
   supplied copied inputs. Do not rely on the PR title/body or this skill's
   example as technical evidence. If the PR is closed, merged, or its head
   changes during setup, report that and confirm which SHA to test.
4. **Agree on choices.** Use `references/decisions.md`. Explain recommended
   defaults and tradeoffs briefly. Ask only about choices that affect user-
   owned data, scientific provenance, or files outside the pre-approved VE
   pin. Wait for answers before making those changes. If choices are settled,
   state the agreed plan and proceed.
5. **Prepare the setup.** Repoint the existing pinned VE source/group in
   `pyproject.toml` to the approved full SHA, following its current syntax.
   Run `uv lock`, then `uv sync --group <group>`. Do not modify unrelated
   dependencies. If either command fails, report the error and stop; do not
   claim the environment is ready. Verify the installed VE source resolves to
   the same full SHA. Review the diff and report all changed files.
6. **Check paths without running VE.** Check the exact config and input paths
   against VE's path-resolution rules. Confirm accessible local files exist.
   Mark Globus-managed or otherwise inaccessible files as unverified and name
   who must provide them. Never substitute sample data silently.
7. **Hand over.** Provide one exact `uv run --locked --group <group> ve_run`
   command with the selected config paths only when setup succeeded and
   required paths are verified. Otherwise explain what blocks a safe command.
   Stop; the user runs it and evaluates outputs.

## Response format

Keep the report concise and distinguish completed work from proposed or
user-owned work. Do not show a runnable command when setup failed or required
paths remain unverified.

```markdown
## Decisions
- <choice>: <agreed option or recommendation and tradeoff>

## Touch
- <path>: <done or proposed change>

## Don't touch
- <path>: <reason>

## User-owned
- <task, including Globus upload if needed; or None>

## Setup
- VE test SHA: <full SHA or not set>
- Input provenance SHA: <full SHA, same, or not applicable>
- Lock/environment: <verified result or blocker>

## Run yourself
<exact command only when safe; otherwise state what must be resolved>

## Unknowns / risks
- <unverified path, stale/closed PR, or None>
```

## References

- `references/conventions.md`: defaults for `ve_data_science`; inspect the
  consuming repository before relying on them.
- `references/decisions.md`: choices to explain and resolve with the user.
- `references/example-pr1958.md`: worked historical example; never reuse its
  SHA, paths, or decisions as current instructions.
