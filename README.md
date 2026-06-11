# sim-plugin-index

Public index of sim-cli solver plugin packages: what exists, where the public
source repository lives, and which package spec to install into a project
environment.

Plugins are usually installed from GitHub rather than PyPI. Treat the GitHub
repository URL in the table as the source of truth for current versions, release
notes, solver requirements, and plugin-owned skills.

## Installing plugins

Install `sim-cli-core` plus the solver plugin package into the same Python
environment that will run the solver workflow. The examples use `uv`, but the
same package specs can be adapted to pip, conda, Poetry, or the package manager
already used by the project.

If Git CLI is available:

```bash
uv add sim-cli-core "sim-plugin-mechanical @ git+https://github.com/svd-ai-lab/sim-plugin-mechanical.git@<tag-or-commit>"
```

If Git CLI is not available, use a GitHub archive URL:

```bash
uv add sim-cli-core "sim-plugin-mechanical @ https://github.com/svd-ai-lab/sim-plugin-mechanical/archive/<tag-or-commit>.zip"
```

After adding packages, verify from that same project environment:

```bash
uv run sim plugin list
uv run sim check <solver>
uv run sim plugin doctor <solver> --deep
```

## Common plugins

These are common public repos, including the solver skill families currently
bundled with Huanjing Studio Desktop. Desktop bundles skills as instructions;
live solver execution still requires installing `sim-cli-core` and the matching
plugin package in the project environment.

| Plugin | Solver area | Python package | Public GitHub URL |
|---|---|---|---|
| COMSOL | Multiphysics | `sim-plugin-comsol` | `https://github.com/svd-ai-lab/sim-plugin-comsol` |
| Autodesk Fusion | CAD | `sim-plugin-autodeskfusion` | `https://github.com/svd-ai-lab/sim-plugin-autodeskfusion` |
| Abaqus | Structural FEA | `sim-plugin-abaqus` | `https://github.com/svd-ai-lab/sim-plugin-abaqus` |
| Ansys Fluent | CFD | `sim-plugin-fluent` | `https://github.com/svd-ai-lab/sim-plugin-fluent` |
| Ansys Workbench | Multiphysics project schematic | `sim-plugin-workbench` | `https://github.com/svd-ai-lab/sim-plugin-workbench` |
| Ansys Workbench Mechanical | Structural FEA | `sim-plugin-mechanical` | `https://github.com/svd-ai-lab/sim-plugin-mechanical` |
| Flotherm | Electronics thermal simulation | `sim-plugin-flotherm` | `https://github.com/svd-ai-lab/sim-plugin-flotherm` |
| STAR-CCM+ | CFD | `sim-plugin-starccm` | `https://github.com/svd-ai-lab/sim-plugin-starccm` |
| Ansys HFSS | 3D electromagnetics | `sim-plugin-hfss` | `https://github.com/svd-ai-lab/sim-plugin-hfss` |
| MATLAB / Simulink | MATLAB / Simulink | `sim-plugin-matlab` | `https://github.com/svd-ai-lab/sim-plugin-matlab` |
| SimScale | Cloud CAE | `sim-plugin-simscale` | `https://github.com/svd-ai-lab/sim-plugin-simscale` |
| OpenFOAM | CFD | `sim-plugin-openfoam` | `https://github.com/svd-ai-lab/sim-plugin-openfoam` |
| LTspice | Circuit / SPICE | `sim-plugin-ltspice` | `https://github.com/svd-ai-lab/sim-plugin-ltspice` |
| Blender | 3D modelling | `sim-plugin-blender` | `https://github.com/svd-ai-lab/sim-plugin-blender` |

## Package spec patterns

Use the repository URL from the table above.

With Git CLI:

```bash
uv add sim-cli-core "<package-name> @ git+<public-github-url>.git@<tag-or-commit>"
```

Without Git CLI:

```bash
uv add sim-cli-core "<package-name> @ <public-github-url>/archive/<tag-or-commit>.zip"
```

Equivalent pip form:

```bash
python -m pip install "sim-cli-core" "<package-name> @ <public-github-url>/archive/<tag-or-commit>.zip"
```

## Adding or updating a plugin

Plugins do not have to live under `svd-ai-lab`. Anyone can publish a sim-cli
plugin from their own public GitHub repo or PyPI account and submit it here for
discoverability.

1. Publish your plugin, either to PyPI or as a public GitHub repo with a
   `pyproject.toml` at the root.
2. Open a PR adding a row to the table above.
3. Include the full public GitHub URL and the Python package name.
4. Keep package specs installable by both Git CLI and archive URL patterns when
   possible.

## For agents

Parse the table above to discover public plugin repos and package names. Install
`sim-cli-core` plus the plugin package into the user's project environment, then
run `sync-skills`, `check`, and `doctor` from that same environment when the
user is working outside a desktop bundle that already includes solver skills.
