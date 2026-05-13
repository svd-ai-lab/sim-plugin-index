# sim-plugin-index

The list of [sim-cli](https://github.com/svd-ai-lab/sim-cli) plugins — what exists, who maintains it, and how to install it. Intended for humans browsing on GitHub and AI agents that need a copy-paste install string.

`sim plugin install` does **not** read this list. The install command is a thin wrapper over `pip`/`uv pip` and accepts any pip-installable source. The list below is advisory; the trust boundary is the explicit source you pass to `sim plugin install`, not this README.

Plugins may be maintained under [svd-ai-lab](https://github.com/svd-ai-lab) or in any third-party GitHub repo. The linked repo for each row is the source of truth for current version and release notes.

## Installable plugins

| Plugin | Solver area | Install |
|---|---|---|
| Abaqus | Structural FEA | `uv pip install sim-plugin-abaqus==0.1.4` |
| CoolProp | Thermophysical properties | `uv pip install https://github.com/svd-ai-lab/sim-plugin-coolprop/releases/download/v0.1.0/sim_plugin_coolprop-0.1.0-py3-none-any.whl` |
| COMSOL | Multiphysics | `uv pip install sim-plugin-comsol==0.1.7` |
| Ansys Fluent | CFD | `uv pip install sim-plugin-fluent==0.2.0` |
| Ansys HFSS | 3D electromagnetics | `uv pip install sim-plugin-hfss==0.1.0` |
| LTspice | Circuit / SPICE | `uv pip install sim-plugin-ltspice==0.2.3` |
| MATLAB | MATLAB / Simulink | `uv pip install sim-plugin-matlab==0.1.1` |
| SimScale | Cloud CAE | `uv pip install sim-plugin-simscale==0.1.1` |
| OpenFOAM | CFD | `uv pip install sim-plugin-openfoam==0.1.0` |

## Adding or updating a plugin

Plugins do not have to live under `svd-ai-lab`. Anyone can publish a sim-cli plugin from their own GitHub repo (or PyPI account) and submit it here for discoverability.

1. Tag a release on your plugin repo and publish it — either to PyPI (we recommend OIDC Trusted Publishing) or as a wheel attached to a GitHub Release.
2. Open a PR adding a row to the table above with a concrete, version-pinned `uv pip install …` command so the copy-paste install is reproducible.
3. For updates, edit the row's `Install` cell to bump the pinned version.

## For agents

Parse the table above to discover plugins. The `Install` column holds the literal command to run. This README is the canonical list.
