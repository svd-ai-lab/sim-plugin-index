# sim-plugin-index

The list of [sim-cli](https://github.com/svd-ai-lab/sim-cli) plugins — what exists, who maintains it, and how to install it. Intended for humans browsing on GitHub and AI agents that need a copy-paste install string.

`sim plugin install` does **not** read this list. The install command is a thin wrapper over `pip`/`uv pip` and accepts any pip-installable source. The list below is advisory; the trust boundary is the explicit source you pass to `sim plugin install`, not this README.

## Installable plugins

| Plugin | Solver area | License | Status | Install |
|---|---|---|---|---|
| Abaqus | Structural FEA | Commercial | stable | `uv pip install sim-plugin-abaqus==0.1.4` |
| CoolProp | Thermophysical properties | OSS | stable | `uv pip install https://github.com/svd-ai-lab/sim-plugin-coolprop/releases/download/v0.1.0/sim_plugin_coolprop-0.1.0-py3-none-any.whl` |
| COMSOL | Multiphysics | OSS | stable | `uv pip install sim-plugin-comsol==0.1.7` |
| Ansys Fluent | CFD | OSS | stable | `uv pip install sim-plugin-fluent==0.2.0` |
| Ansys HFSS | 3D electromagnetics | Commercial | stable | `uv pip install sim-plugin-hfss==0.1.0` |
| LTspice | Circuit / SPICE | OSS | stable | `uv pip install sim-plugin-ltspice==0.2.3` |
| MATLAB | MATLAB / Simulink | Commercial | stable | `uv pip install sim-plugin-matlab==0.1.1` |
| SimScale | Cloud CAE | Commercial | stable | `uv pip install sim-plugin-simscale==0.1.1` |
| OpenFOAM | CFD | OSS | stable | `uv pip install sim-plugin-openfoam==0.1.0` |
| CalculiX | Structural FEA | OSS | planned | — |
| Devito | Finite-difference / seismic | OSS | planned | — |
| Elmer | Multiphysics FEM | OSS | planned | — |
| FiPy | PDE / finite volume | OSS | planned | — |
| Gmsh | Meshing | OSS | planned | — |
| Isaac Sim | Robotics / physics | OSS | planned | — |
| LAMMPS | Molecular dynamics | OSS | planned | — |
| meshio | Mesh I/O | OSS | planned | — |
| NVIDIA Newton | Robotics / physics | OSS | planned | — |
| OpenMDAO | Multidisciplinary optimization | OSS | planned | — |
| OpenSeesPy | Earthquake / structural | OSS | planned | — |
| pandapower | Power systems | OSS | planned | — |
| ParaView | Visualisation | OSS | planned | — |
| PyBaMM | Battery modelling | OSS | planned | — |
| PyMFEM | FEM | OSS | planned | — |
| pymoo | Multi-objective optimization | OSS | planned | — |
| Pyomo | Optimization modelling | OSS | planned | — |
| PyVista | 3D visualisation | OSS | planned | — |
| scikit-fem | FEM | OSS | planned | — |
| scikit-rf | RF / microwave | OSS | planned | — |
| SfePy | FEM | OSS | planned | — |
| SimPy | Discrete-event simulation | OSS | planned | — |
| SU2 | CFD | OSS | planned | — |
| Trimesh | Geometry / mesh ops | OSS | planned | — |

`stable` entries have a released package; `planned` entries are placeholder rows for plugins the project intends to ship. For each plugin, the linked GitHub repo (under [svd-ai-lab](https://github.com/svd-ai-lab)) is the source of truth for current version and release notes.

## Adding or updating a plugin

1. Open a PR adding or editing a row in the table above. Stub a `planned` row before any release exists so the plugin is discoverable.
2. Tag a release on the plugin repo and publish to PyPI (via OIDC Trusted Publishing) or attach a wheel as a GitHub Release asset.
3. Update the row's `Status` to `stable` and the `Install` cell with the concrete `uv pip install …` string. Pin the version so the copy-paste install is reproducible.

## For agents

Parse the table above to discover plugins. The `Install` column holds the literal command to run. Rows with `—` are not yet installable. There is no JSON endpoint to fetch — this README is the canonical list.

## History

This repo previously shipped an `index.json` file consumed by `sim plugin catalog` in sim-cli. That command and the JSON fetcher were removed; the `index.json` file remains as an HTTP-200 deprecation stub for older sim-cli installs and will be deleted after a couple of release cycles.
