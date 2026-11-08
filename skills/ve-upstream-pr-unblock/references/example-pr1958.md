# Historical example: ve_data_science#765 and virtual_ecosystem#1958

This example records one past setup only. PR state, file paths, decisions, and
SHAs can change; verify them from the live repositories for every new request.
Never copy this example's SHA or treat its decisions as defaults.

- Goal: test `maliau_2` with the microbial group and enzyme CSV inputs required
  by virtual_ecosystem PR 1958.
- Input provenance SHA: `cee8edd7f648f0aadb91c2e132e39b2b4d6db44e`.
- Approved test SHA at the time: `2febd6bd0732eeda6f70f7aa413e40b560d74c54`.
- Agreed then: stage inputs under `data/pr1958/`, config under
  `config/pr1958/`, reuse `dev-pinned`, and upload data through Globus.
- Planned edits: staged `soil_config.toml` plus `pyproject.toml` and `uv.lock`.
- Protected paths: combined config, its builder, `maliau_1`, `.gitignore`,
  active configs, and main data.
- Relative paths were considered during staging; verify them against the
  current VE path-resolution rules before any new run.
