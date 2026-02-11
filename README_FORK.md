# Fork

A personal fork of [antfu](https://github.com/antfu)'s [File Nesting Config for VS Code](https://github.com/antfu/vscode-file-nesting-config).

## Changes

### Nesting

In no particular order, this fork makes the following changes to the nesting config:

- Adds the [shadcn/ui `components.json`](https://ui.shadcn.com/docs/components-json) file to the nesting config. ([`fd6ad81`](https://github.com/dir/vscode-file-nesting-config/commit/fd6ad819d21a46cb430973eec4c8378d3beb51f9))
- Env files
  - No longer nest under framework (or Deno) configs. ([`917a2e6`](https://github.com/dir/vscode-file-nesting-config/commit/917a2e66b2ef3416c39f0635c6713f291f75cf56))
  - Will also be nested under `.env.local` in addition to `.env` (with `.env` taking precedence, if present). ([`140c9cd`](https://github.com/dir/vscode-file-nesting-config/commit/140c9cd93e9e3741f695d639e025d061616f35cd))

### Miscellaneous

Other miscellaneous changes include:

- Adds a `purge-jsdelivr-cache` job to the [`update.yml`](.github/workflows/update.yml) Github Action that immediately purges the JsDelivr cache used by the VSCode extension to retrieve the config from the repo.

## Usage

### VSCode Extension
Install the [File Nesting Updater](https://marketplace.visualstudio.com/items?itemName=antfu.file-nesting) extension and add the following to your VSCode `settings.json`:

<!-- eslint-skip -->

```jsonc
"fileNestingUpdater.upstreamRepo": "dir/vscode-file-nesting-config",
"fileNestingUpdater.upstreamBranch": "fork",
```

> [!IMPORTANT]
> After updating your VSCode settings, you may want to manually execute the `File Nesting Updater: Update config now` command from the command palette to sync your editor with the fork settings.

### Manual

Refer to the [Update Manually](./README.md#update-manually) section of the original README.

## Developing

### Branches

| Branch | Purpose |
|--------|---------|
| `main` | Mirror of upstream. Do not commit directly. |
| `fork` | Default branch. All customizations live here. |

### Making Changes

1. Branch off `fork`.
2. Edit [`update.mjs`](./update.mjs) — this is the only file you need to touch for nesting changes.
3. Open a PR targeting `fork`.
4. On merge, the [`update`](.github/workflows/update.yml) GitHub Action automatically runs `update.mjs` and commits the regenerated config snippet in `README.md`.

> [!NOTE]
> Although handled automatically by the [`update`](.github/workflows/update.yml) Github Action, you may manually run `update.mjs` and commit the output.

### Syncing with Upstream

Merge `main` into `fork` to pull in upstream updates.

> [!TIP]
> After making any changes to the fork, you may want to manually run the VSCode extension's update config command (as described [here](#vscode-extension)) to get the latest changes in your editor.
