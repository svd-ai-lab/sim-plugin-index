# sim-plugin-index

Discovery catalogue for [sim-cli](https://github.com/svd-ai-lab/sim-cli) plugins. The catalogue answers **"what plugins exist and how do I install them?"** for humans and AI agents.

`sim plugin install` does **not** read this catalogue. The catalogue is advisory metadata — each entry's `install` field is a copy-paste string the user or agent passes to `sim plugin install`. The trust boundary is the explicit install source you choose, not the catalogue.

`sim plugin catalog` (added in `sim-cli` v0.4) fetches and renders this file for human-friendly discovery; agents can also fetch it directly:

```
https://raw.githubusercontent.com/svd-ai-lab/sim-plugin-index/main/index.json
```

## Schema (v2)

```json
{
  "schema_version": 2,
  "plugins": [
    {
      "id":            "ltspice",
      "name":          "LTspice",
      "distribution":  "pypi",
      "install":       "sim-plugin-ltspice==0.2.3",
      "version":       "0.2.3",
      "summary":       "LTspice driver for sim — ...",
      "homepage":      "https://github.com/svd-ai-lab/sim-plugin-ltspice",
      "license_class": "oss"
    },
    {
      "id":            "fluent",
      "name":          "Ansys Fluent",
      "distribution":  "wheel",
      "install":       "https://cdn.svdailab.com/wheels/sim_plugin_fluent-0.1.4-py3-none-any.whl#sha256=abcd…",
      "version":       "0.1.4",
      "summary":       "Ansys Fluent driver wrapper.",
      "homepage":      "https://example.com/fluent-plugin",
      "license_class": "commercial"
    }
  ]
}
```

### Field semantics

| field | required | notes |
|---|---|---|
| `id` | yes | Short slug, e.g. `ltspice`. Stable identifier. |
| `name` | yes | Human-readable display name. |
| `distribution` | recommended | `pypi`, `wheel`, or `git`. Advisory tag for the catalog reader. |
| `install` | recommended | **Literal argument to `sim plugin install`** — a PyPI spec, a wheel URL (with `#sha256=...` if available), or a `git+https://…` URL. If absent, the entry is treated as a placeholder with no shippable artifact yet. |
| `version` | recommended | Currently advertised version. Keep in lock-step with releases. |
| `summary` | optional | One-line description. |
| `homepage` | optional | URL for further docs. |
| `license_class` | optional | `oss` or `commercial` (informational only). |

The `install` field carries everything needed to install. There is no separate `package` / `wheel_url` / `sha256` — for wheel URLs the SHA-256 hash lives in the `#sha256=...` fragment so normal Python tooling participates in verification.

### Legacy v1 entries (still readable)

`sim-cli` continues to read the older v1 shape (entries with `name` as slug, `latest_version`, `latest_wheel_url`, `git`, `package`) and synthesizes an `install` string from those fields. Catalogue maintainers can migrate entries to v2 incrementally.

## Adding a plugin

1. Open a PR adding the entry under `plugins`. At minimum: `id`, `name`, `summary`, `homepage`, `license_class`. This makes the plugin discoverable via `sim plugin catalog` even before any release exists.
2. Tag a release on the plugin repo and either publish to PyPI (via OIDC Trusted Publishing) or attach a wheel as a GitHub Release asset.
3. Open a follow-up PR adding `distribution`, `install`, and `version`.

For wheel URLs, including a `#sha256=…` fragment is recommended so callers get integrity checking via standard pip/uv behavior.

## Commercial plugins

Commercial plugin availability depends on third-party license conditions. Contact <contact@svd-ai-lab.com> to discuss commercial plugin access.
