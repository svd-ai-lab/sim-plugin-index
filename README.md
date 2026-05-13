# sim-plugin-index

The list of [sim-cli](https://github.com/svd-ai-lab/sim-cli) plugins — what exists, who maintains it, and how to install it. Intended for humans browsing on GitHub and AI agents that need a copy-paste install string.

`sim plugin install` does **not** read this list. The install command is a thin wrapper over `pip`/`uv pip` and accepts any pip-installable source. The list below is advisory; the trust boundary is the explicit source you pass to `sim plugin install`, not this README.

Plugins may be maintained under [svd-ai-lab](https://github.com/svd-ai-lab) or in any third-party GitHub repo. The linked repo for each row is the source of truth for current version and release notes.

## Installable plugins

| Plugin | Solver area | Install |
|---|---|---|
| COMSOL | Multiphysics | `uv pip install sim-plugin-comsol` |
| Ansys Workbench | Multiphysics project schematic | `uv pip install sim-plugin-workbench` |
| Ansys Workbench Mechanical | Structural FEA | `uv pip install sim-plugin-mechanical` |
| Ansys HFSS | 3D electromagnetics | `uv pip install sim-plugin-hfss` |
| Ansys Fluent | CFD | `uv pip install sim-plugin-fluent` |
| MATLAB / Simulink | MATLAB / Simulink | `uv pip install sim-plugin-matlab` |
| SimScale | Cloud CAE | `uv pip install sim-plugin-simscale` |
| OpenFOAM | CFD | `uv pip install sim-plugin-openfoam` |
| LTspice | Circuit / SPICE | `uv pip install sim-plugin-ltspice` |
| Fusion 360 | CAD | `uv pip install git+https://github.com/svd-ai-lab/sim-plugin-fusion360.git` |
| Blender | 3D modelling | `uv pip install git+https://github.com/svd-ai-lab/sim-plugin-blender.git` |

Install strings resolve to the latest version. For a reproducible install, pin a version yourself — `uv pip install sim-plugin-comsol==X.Y.Z` for PyPI, or `…@vX.Y.Z` for git URLs.

## Adding or updating a plugin

Plugins do not have to live under `svd-ai-lab`. Anyone can publish a sim-cli plugin from their own GitHub repo (or PyPI account) and submit it here for discoverability.

1. Publish your plugin — either to PyPI (we recommend OIDC Trusted Publishing) or as a public GitHub repo with a `pyproject.toml` at the root.
2. Open a PR adding a row to the table above. Use `uv pip install <pkg-name>` for PyPI, or `uv pip install git+https://github.com/<owner>/<repo>.git` for a GitHub repo.

## For agents

Parse the table above to discover plugins. The `Install` column holds the literal command to run. This README is the canonical list.
