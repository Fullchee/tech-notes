## Package Managers

### `npm`

comes with `node`

### `yarn`

-   Facebook created yarn because npm was slow

### `pnpm`

-   uses symbolic links and caching
    -   every dependency is installed once
        -   `~/.pnpm-store/`
-   if two dependencies (or nested dependencies) have the same grand dependencies,
    -   they can just point to the same package
    -   no need to install it twice!
-   drop in replacement for `npm`
- [pnpm patch <pkg> | pnpm](https://pnpm.io/cli/patch)
	- modify the source code of your dependencies

What is package hoisting????

### Workspaces

[workspaces | npm Docs](https://docs.npmjs.com/cli/v8/using-npm/workspaces)

aka managing multiple repos in a single repo

-   aka monorepo

Avoid manually using `npm link`

Introduced in npm v7

#### Why are `pnpm` workspaces better?

[Workspace | pnpm](https://pnpm.io/workspaces)

-   built-in support for monorepos
-   don't technically need

At Forma, we had a package

```json
{
  "dependencies": {
    "forma-package": "workspace:*"
  }
}
```

Direct link to the package directory in the monorepo if you look at the `pnpm-lock.yaml`


## [JS Monorepos](js-monorepos.md)
