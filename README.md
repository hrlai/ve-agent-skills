# ve-agent-skills

Reusable agent skills for Virtual Ecosystem (VE) research and data workflows.
Skills use the open [Agent Skills](https://agentskills.io) format: a
`SKILL.md` plus optional references.

These skills target data scientists and ecologists working in
[`ImperialCollegeLondon/ve_data_science`](
https://github.com/ImperialCollegeLondon/ve_data_science) with the upstream
model in [`ImperialCollegeLondon/virtual_ecosystem`](
https://github.com/ImperialCollegeLondon/virtual_ecosystem). They should explain
decisions in domain terms, protect user-managed data, and avoid making
scientific judgments outside the requested task.

## Skills

- [`ve-upstream-pr-unblock`](skills/ve-upstream-pr-unblock/SKILL.md): Assess one
  upstream VE PR against a scenario, prepare an approved pinned test setup, and
  hand over the run command. Never runs VE.

## Use in a consuming repository

This repository is a source library; tools do not automatically load its skills.
Copy or symlink a skill directory into the consuming repository's skill
location, such as `.github/skills/` or `.claude/skills/`, following that
tool's current documentation. For tools without native skill discovery, add a
short instruction in the consuming repository's `AGENTS.md` that points to the
installed skill's `SKILL.md`.

Keep reusable workflow rules in each skill. Put
`ve_data_science`-specific defaults in that skill's
`references/conventions.md`; inspect the target repository before applying
defaults. Keep agent instructions tool-agnostic where possible.
