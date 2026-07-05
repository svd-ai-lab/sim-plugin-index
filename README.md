# sim-plugin-index

Public index of sim-cli solver plugin packages: what exists, where the public
source repository lives, and which package spec to install into a project
environment.

This repo can also host small ad hoc guidance for solver families that are not
first-party sim-cli plugins yet. Desktop bundles can vendor that guidance so
agents still have offline discovery notes when a user's network is unreliable.

For public maintained plugins, prefer the PyPI package spec when the package is
published there. Treat the GitHub repository URL in the table as the source of
truth for release notes, solver requirements, plugin-owned skills, and fallback
source installs.

## Installing plugins

Install `sim-cli-core` plus the solver plugin package into the same Python
environment that will run the solver workflow. The examples use `uv`, but the
same package specs can be adapted to pip, conda, Poetry, or the package manager
already used by the project.

For plugins published on PyPI:

```bash
uv add sim-cli-core sim-plugin-icepak
```

For an exact PyPI version:

```bash
uv add sim-cli-core "sim-plugin-icepak==0.1.0"
```

For source installs when PyPI is unavailable or a specific commit is required,
use the GitHub URL from the table. If Git CLI is available:

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

| Plugin | Solver area | Python package | Default install spec | Public GitHub URL |
|---|---|---|---|---|
| COMSOL | Multiphysics | `sim-plugin-comsol` | `sim-plugin-comsol` | `https://github.com/svd-ai-lab/sim-plugin-comsol` |
| Autodesk Fusion | CAD | `sim-plugin-autodeskfusion` | `sim-plugin-autodeskfusion @ git+https://github.com/svd-ai-lab/sim-plugin-autodeskfusion.git@main` | `https://github.com/svd-ai-lab/sim-plugin-autodeskfusion` |
| Abaqus | Structural FEA | `sim-plugin-abaqus` | `sim-plugin-abaqus` | `https://github.com/svd-ai-lab/sim-plugin-abaqus` |
| Ansys Fluent | CFD | `sim-plugin-fluent` | `sim-plugin-fluent` | `https://github.com/svd-ai-lab/sim-plugin-fluent` |
| Ansys Workbench | Multiphysics project schematic | `sim-plugin-workbench` | `sim-plugin-workbench` | `https://github.com/svd-ai-lab/sim-plugin-workbench` |
| Ansys Workbench Mechanical | Structural FEA | `sim-plugin-mechanical` | `sim-plugin-mechanical` | `https://github.com/svd-ai-lab/sim-plugin-mechanical` |
| Flotherm | Electronics thermal simulation | `sim-plugin-flotherm` | `sim-plugin-flotherm @ git+https://github.com/svd-ai-lab/sim-plugin-flotherm.git@main` | `https://github.com/svd-ai-lab/sim-plugin-flotherm` |
| STAR-CCM+ | CFD | `sim-plugin-starccm` | `sim-plugin-starccm @ git+https://github.com/svd-ai-lab/sim-plugin-starccm.git@main` | `https://github.com/svd-ai-lab/sim-plugin-starccm` |
| Ansys HFSS | 3D electromagnetics | `sim-plugin-hfss` | `sim-plugin-hfss` | `https://github.com/svd-ai-lab/sim-plugin-hfss` |
| Ansys Icepak | Electronics thermal simulation | `sim-plugin-icepak` | `sim-plugin-icepak` | `https://github.com/svd-ai-lab/sim-plugin-icepak` |
| HyperMesh | Meshing / model deck prep | `sim-plugin-hypermesh` | `sim-plugin-hypermesh @ git+https://github.com/svd-ai-lab/sim-plugin-hypermesh.git@main` | `https://github.com/svd-ai-lab/sim-plugin-hypermesh` |
| MATLAB / Simulink | MATLAB / Simulink | `sim-plugin-matlab` | `sim-plugin-matlab` | `https://github.com/svd-ai-lab/sim-plugin-matlab` |
| Stata | Statistics / econometrics | `sim-plugin-stata` | `sim-plugin-stata @ git+https://github.com/svd-ai-lab/sim-plugin-stata.git@main` | `https://github.com/svd-ai-lab/sim-plugin-stata` |
| SimScale | Cloud CAE | `sim-plugin-simscale` | `sim-plugin-simscale` | `https://github.com/svd-ai-lab/sim-plugin-simscale` |
| OpenFOAM | CFD | `sim-plugin-openfoam` | `sim-plugin-openfoam` | `https://github.com/svd-ai-lab/sim-plugin-openfoam` |
| LTspice | Circuit / SPICE | `sim-plugin-ltspice` | `sim-plugin-ltspice` | `https://github.com/svd-ai-lab/sim-plugin-ltspice` |
| Blender | 3D modelling | `sim-plugin-blender` | `sim-plugin-blender @ git+https://github.com/svd-ai-lab/sim-plugin-blender.git@main` | `https://github.com/svd-ai-lab/sim-plugin-blender` |
| Rhino / Grasshopper | CAD / parametric modelling | Skill-only repo | Bundled skill or source checkout; no sim-cli Python package | `https://github.com/svd-ai-lab/sim-plugin-rhino` |

## Ad hoc external guidance

These entries are not first-party solver support. They are bundled markdown
guidance for agents to check local/user-configured third-party routes before
claiming a capability is unavailable.

| Capability | Status | Bundled skill path |
|---|---|---|
| FDTD electromagnetic simulation | External ad hoc | `skills/external-solver-discovery` |

## Package spec patterns

Use the table's default install spec directly:

```bash
uv add sim-cli-core "<default-install-spec>"
```

Use bare PyPI package names directly only when the package has a public PyPI
release:

```bash
uv add sim-cli-core "<package-name>==<version>"
```

Use the repository URL from the table above for source installs.

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

1. Publish your plugin, either to PyPI, as a public GitHub repo with a
   `pyproject.toml` at the root, or as a skill-only public repo when there is
   no sim-cli Python package.
2. Open a PR adding a row to the table above.
3. Include the full public GitHub URL and the Python package name.
4. If the plugin is on PyPI, include the PyPI package name exactly. If it is not
   on PyPI, keep package specs installable by both Git CLI and archive URL
   patterns when possible. For skill-only repos, say so directly instead of
   inventing a Python package name.

## For agents

Parse the table above to discover public plugin repos and package names. Prefer
the PyPI package spec when it exists; otherwise use the GitHub source or archive
spec. Install `sim-cli-core` plus the plugin package into the user's project
environment, then run `sync-skills`, `check`, and `doctor` from that same
environment when the user is working outside a desktop bundle that already
includes solver skills.

When a user asks for a solver family that is not listed as a common plugin,
check the ad hoc external guidance before assuming there is no usable route.
That guidance is a discovery aid for third-party tools, plugins, MCP servers,
or native APIs; it does not imply bundled solver availability.
