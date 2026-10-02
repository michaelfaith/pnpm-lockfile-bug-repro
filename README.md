# PNPM Frozen Lockfile Bug

This repo reproduces a bug introduced in pnpm 12.8.0. If one package references another package using `file:` path, and the consumed package has an optional peer dependency, then running install with `--frozen-lockfile` always fails with

```sh
Scope: all 2 workspace projects
Error: ERR_PNPM_OUTDATED_LOCKFILE

  × installing dependencies
  ╰─▶ Cannot install with "frozen-lockfile" because pnpm-lock.yaml is not up to date with package.json.

        Failure reason:
        local dependency "root-package" at ".." is outdated
  help: Regenerate the lockfile with `pnpm install --lockfile-only` so that pnpm-lock.yaml reflects the current package.json, then re-run `pnpm install --frozen-lockfile`.
```

## Repro Steps

1. `cd e2e`
2. `pnpm install` just to confirm that the lockfile is unchanged
3. `pnpm install --frozen-lockfile`
