# sim-plugin-index

Curated public index of [sim-cli](https://github.com/svd-ai-lab/sim-cli)
plugins. `sim plugin install <name>` resolves bare names against
[`index.json`](./index.json) on this repo's `main` branch:

```
https://raw.githubusercontent.com/svd-ai-lab/sim-plugin-index/main/index.json
```

The CLI fetches `index.json` over plain HTTPS — no `gh`, no `git` is
required for end users; the `latest_wheel_url` points at a wheel asset on
the plugin repo's GitHub Release page.

## Schema

```json
{
  "schema_version": 1,
  "plugins": [
    {
      "name": "<solver>",
      "summary": "<one-line description>",
      "homepage": "https://github.com/svd-ai-lab/sim-plugin-<solver>",
      "license_class": "oss",
      "git": "https://github.com/svd-ai-lab/sim-plugin-<solver>",
      "latest_version": "<X.Y.Z>",
      "latest_wheel_url": "https://github.com/.../releases/download/v<X.Y.Z>/<wheel>.whl"
    }
  ]
}
```

The CLI's resolver consults each field in this order when a bare name is
installed (see `sim._plugin_install.resolve_source`):

1. `latest_wheel_url` — direct HTTPS install (preferred, no git required).
   **Important:** the resolver returns immediately on `latest_wheel_url`
   and does **not** fall back to `git` if the wheel 404s. Only set this
   field once the release tag and asset exist.
2. `git` — used when `latest_wheel_url` is absent. Always safe to set.
3. else — assume `pip install sim-plugin-<name>` from PyPI (currently no plugins
   live on PyPI; the GitHub-only convention is the policy)

`name@<version>` install paths require `latest_version` to match, so
keep that field in lock-step with the active release tag.

## Adding a plugin

1. Open a PR with the plugin's entry under `plugins`. At minimum: `name`,
   `summary`, `homepage`, `license_class`, `git`. Bare-name install via
   `git+https://` works as soon as this lands.
2. Tag a release (`vX.Y.Z`) on the plugin repo and attach the built wheel
   as a release asset.
3. Open a follow-up PR adding `latest_version` + `latest_wheel_url` so
   the resolver prefers the direct-HTTPS path.

## Commercial plugins

Commercial plugins are listed in the **private** mirror
`svd-ai-lab/sim-plugin-index-commercial`, consulted only when
`sim plugin install --include-commercial` is passed and the user has
`gh auth`. Phase 3 of the plugin extraction refactor stands that up.
