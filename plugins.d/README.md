# `plugins.d/` — Catalog plugin registry

Each `plugins.d/<name>.yml` declares a **catalog plugin** that is mechanically
generated from the canonical skills in `skills/<Product>/`. The build script
`.github/scripts/build-plugins.sh` reads every file in this directory and
fully regenerates the corresponding `plugins/<name>/` directory:

- `plugins/<name>/skills/<skill>/` — real-dir copies rsynced from `skills/`
  (Codex `plugin add` does not follow symlinks, so we ship real files)
- `plugins/<name>/.claude-plugin/plugin.json` — Claude Code manifest
- `plugins/<name>/.codex-plugin/plugin.json` — Codex CLI manifest
- An entry in `.claude-plugin/marketplace.json` and/or
  `.agents/plugins/marketplace.json`, controlled by `marketplace_enabled:`
  (see below)

## Defaults

`plugins.d/_defaults.yml` holds the NVIDIA-corp-wide fields that almost every
plugin shares (author, license, homepage, brand color, policy URLs, etc.).
The build script applies it to every `<name>.yml` and any per-plugin field
overrides the default. Merge is shallow — if you re-declare a nested mapping
like `author:`, supply all of its keys.

Filenames starting with `_` are treated as include files and are never built
into a plugin themselves.

## Marketplace publishing

Each plugin defaults to being listed in our self-hosted (aka local)
marketplaces (avilable to codex and claude):

- `.claude-plugin/marketplace.json` — Claude Code marketplace
- `.agents/plugins/marketplace.json` — Codex CLI marketplace

To opt out, add this in a plugin's yaml:

```yaml
marketplace_enabled:
  claude: false   # omit from .claude-plugin/marketplace.json
  codex:  false   # omit from .agents/plugins/marketplace.json
```

Note: A plugin with both flags `false` is still fully built into `plugins/<name>/`
so it can be hand-delivered to upstream external marketplaces, but appears in neither
of ours. See `plugins.d/nvidia.yml` for an example.

## Hand-maintained inside each plugin (all optional)

- `plugins/<name>/assets/<file>` — referenced by `logo:`, `composer_icon:`,
  or `screenshots:` in the yaml
- `plugins/<name>/README.md` — plugin-specific notes

The build script never overwrites `assets/` or `README.md`.

## Optional Codex interface assets

These map to the Codex `interface.*` fields most upstream plugins ship and
are emitted only when set in the yaml:

```yaml
logo: ./assets/<name>.png            # interface.logo
composer_icon: ./assets/<name>.png   # interface.composerIcon (small UI icon;
                                     # may reuse the logo or be a smaller SVG)
screenshots:
  - ./assets/screenshot-1.png        # interface.screenshots
  - ./assets/screenshot-2.png
```

Any local `./assets/*` path declared by these fields is checked for existence
at build time; missing files emit a warning (not a hard error).

## Plugins outside this registry

If a plugin needs to be hand-edited beyond what the yaml schema covers (e.g.
unusual cross-product curation that doesn't fit the defaults model), drop a
`plugins/<name>/.skills-manifest.yml` listing the skills to materialize and
omit it from `plugins.d/`. The build script will rsync only the `skills/`
tree and leave `.claude-plugin/`, `.codex-plugin/`, and the marketplace
entries fully under your control.

No plugin currently uses this path; it exists for future flexibility.

## See also

`components.d/` is the analogous registry that drives the upstream skills
sync into `skills/<Product>/`. This dependency must run first to sync skills trees.
