# sim-plugin-index

The public index of sim-cli solver plugin packages: what exists, who maintains
it, and which package spec to add to a uv project.

Plugins may be maintained under [svd-ai-lab](https://github.com/svd-ai-lab) or
in third-party GitHub repos. The linked repo for each row is the source of
truth for current version, release notes, solver requirements, and plugin-owned
skills.

## Installable plugins

| Plugin | Solver area | Package spec | Add command |
|---|---|---|---|
| COMSOL | Multiphysics | `sim-plugin-comsol` | `uv add sim-cli-core sim-plugin-comsol` |
| Ansys Workbench | Multiphysics project schematic | `sim-plugin-workbench` | `uv add sim-cli-core sim-plugin-workbench` |
| Ansys Workbench Mechanical | Structural FEA | `sim-plugin-mechanical` | `uv add sim-cli-core sim-plugin-mechanical` |
| Ansys HFSS | 3D electromagnetics | `sim-plugin-hfss` | `uv add sim-cli-core sim-plugin-hfss` |
| Ansys Fluent | CFD | `sim-plugin-fluent` | `uv add sim-cli-core sim-plugin-fluent` |
| MATLAB / Simulink | MATLAB / Simulink | `sim-plugin-matlab` | `uv add sim-cli-core sim-plugin-matlab` |
| SimScale | Cloud CAE | `sim-plugin-simscale` | `uv add sim-cli-core sim-plugin-simscale` |
| OpenFOAM | CFD | `sim-plugin-openfoam` | `uv add sim-cli-core sim-plugin-openfoam` |
| LTspice | Circuit / SPICE | `sim-plugin-ltspice` | `uv add sim-cli-core sim-plugin-ltspice` |
| Autodesk Fusion | CAD | `sim-plugin-autodeskfusion @ git+https://github.com/svd-ai-lab/sim-plugin-autodeskfusion.git` | `uv add sim-cli-core "sim-plugin-autodeskfusion @ git+https://github.com/svd-ai-lab/sim-plugin-autodeskfusion.git"` |
| Blender | 3D modelling | `sim-plugin-blender @ git+https://github.com/svd-ai-lab/sim-plugin-blender.git` | `uv add sim-cli-core "sim-plugin-blender @ git+https://github.com/svd-ai-lab/sim-plugin-blender.git"` |

After adding packages, sync skills and verify from the same uv project:

```bash
uv run sim plugin sync-skills --target .agents/skills --copy
uv run sim check <solver>
uv run sim plugin doctor <solver> --deep
```

## Adding or updating a plugin

Plugins do not have to live under `svd-ai-lab`. Anyone can publish a sim-cli
plugin from their own GitHub repo or PyPI account and submit it here for
discoverability.

1. Publish your plugin, either to PyPI or as a public GitHub repo with a
   `pyproject.toml` at the root.
2. Open a PR adding a row to the table above.
3. Use a package spec in the `Package spec` column and the full
   `uv add sim-cli-core <plugin-package-spec>` command in the `Add command`
   column.

## For agents

Parse the table above to discover plugin package specs. Add packages with
`uv add sim-cli-core <plugin-package-spec>`, then run `sync-skills`, `check`,
and `doctor` from that same uv project.
