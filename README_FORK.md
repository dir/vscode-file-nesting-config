# Fork

A personal fork of [antfu](https://github.com/antfu)'s [File Nesting Config for VS Code](https://github.com/antfu/vscode-file-nesting-config). 

## Changes

- Env files (`.env.*`, `.envrc`, `*.env`, `env.d.ts`) are no longer nested under framework (or Deno) configs. They do still self-nest under `.env`.

## Usage

### VSCode Extension
Install the [File Nesting Updater](https://marketplace.visualstudio.com/items?itemName=antfu.file-nesting) extension and add the following to your VSCode `settings.json`:

```json
"fileNestingUpdater.upstreamRepo": "dir/vscode-file-nesting-config",
"fileNestingUpdater.upstreamBranch": "fork"
```

After updating your settings, you may want to manually run the `File Nesting Updater: Update config now` VSCode command palette action.

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
> Although it is handled automatically by the [`update`](.github/workflows/update.yml) Github Action workflow, you may still manually run `update.mjs` and commit the output.

### Syncing with Upstream

Merge `main` into `fork` to pull in upstream updates.
