# [JS Monorepos](https://fullchee-reminders.netlify.app/link/1694)

## What a monorepo looks like

- clients
	- client1
	- client2
- packages
	- ESLint
	- frontend-core
	- TSConfig
	- storybook
	- tests

## Why monorepos

1. Consistency
	1. share config files
		1. ESLint 
	2. docs
	3. utils
	4. align & share node_modules
		1. share `node_modules`
2. CI/CD is easier to test/build/deploy together
3. need to make a change to core & client
	1. just one PR now!

## Problem with monorepos?

- They're huge
- Big tech companies have their own massive solutions
- 

## Options

-   npm/yarn/pnpm workspaces
	- npm link 🐢
- Smart build systems
	- Turborepo
	-   NX
		- Lerna: open source multi-package repos

## Smart build systems

built on top of workspaces

### Turborepo vs pnpm workspaces

-   Create a dependency tree between all the apps
-   smart caching
	- run the same thing twice -> get from the cache
-   run jobs in parallel
-   remote caching
    -   cache can be downloaded remotely


### Turborepo vs NX

????


### How does a client/app know that a local package updated?

-   is the `*` thing a workspace specific thing?
-   is it the workspace that links it??????

