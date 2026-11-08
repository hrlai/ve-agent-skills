# Repo conventions (ve_data_science defaults; inspect before use)

- This is a research and workflow repository used by data scientists and
  ecologists, not a standalone Python package. Explain proposed changes in
  terms of the scenario and inputs, not only code internals.
- Data and individual model configs may be distributed through Globus. Git
  holds code, runners, and the changelog, not a second maintained copy of
  managed scenario data/config. Ask before creating or editing staged files.
- Scenario data commonly lives under
  `data/scenarios/<site>/<scenario>/data/`. PR test inputs may be staged under
  `data/<pr>/`; staged configs may be under `config/<pr>/`. Confirm paths and
  ignore rules locally; these are not guaranteed locations.
- Do not migrate existing `data/` paths to `data/main` unless authorised.
- The VE test pin commonly uses the `dev-pinned` uv group and
  `[tool.uv.sources]`. Inspect `pyproject.toml`; follow its current source
  pattern and group rather than older inline dependency examples.
- Common run command: `uv run --locked --group dev-pinned ve_run <configs>`.
  Run it only when the user explicitly does so; this skill never runs VE.
- An optional staged runner may live at
  `analysis/<domain>/pr_test/ve_run.sh`. Create one only when requested.
