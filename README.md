This repository reproduces a bug in pnpm where a missing dev dependency causes `pnpm deploy --prod` to fail.

```console
$ pnpm run clean

> @ahaines/example-monorepo@ clean ~/pnpm-deploy-missing-workspace-package
> rm -rf dist node_modules packages/*/node_modules

$ pnpm install --frozen-lockfile
Scope: all 2 workspace projects
Lockfile is up to date, resolution step is skipped
Packages: +66
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
Progress: resolved 66, reused 66, downloaded 0, added 66, done

devDependencies:
+ @ahaines/example-dev 0.0.0 <- packages/dev

Done in 503ms

$ pnpm --filter=./packages/prod deploy --prod dist
Packages are cloned from the content-addressable store to the virtual store.
  Content-addressable store is at: ~/Library/pnpm/store/v3
  Virtual store is at:             dist/node_modules/.pnpm
 ERR_PNPM_WORKSPACE_PKG_NOT_FOUND  In : "@ahaines/example-dev@workspace:*" is in the dependencies but no package named "@ahaines/example-dev" is present in the workspace

This error happened while installing a direct dependency of ~/pnpm-deploy-missing-workspace-package

Packages found in the workspace:
Progress: resolved 0, reused 1, downloaded 0, added 0
