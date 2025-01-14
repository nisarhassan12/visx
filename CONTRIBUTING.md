# Contributing

Contributions welcome! Please follow the [code of conduct](./CODE_OF_CONDUCT.md).

## Overview

[Yarn workspaces](https://yarnpkg.com/lang/en/docs/workspaces/) are used to manage dependencies and
build config across packages in the umbrella `visx` monorepo, and
[lerna](https://github.com/lerna/lerna/) is used to manage versioning.

## Project structure

```
visx/
  lerna.json
  package.json
  packages/
    visx-package-1/
      src/
      test/
      build/
      package.json
      ...
    visx-package-2/
      ...
    ...
```

## Local development

Run the following to setup your local dev environment:

```sh
# Install `yarn`, alternatives at https://yarnpkg.com/en/docs/install
curl -o- -L https://yarnpkg.com/install.sh | bash

# Clone or fork `visx`
git clone git@github.com:airbnb/visx.git # or your fork
cd visx

# install dependencies, and have `yarn` symlink within-`visx` dependencies
yarn

# build packages and generate types for local development
yarn build
```

## Online one-click setup

You can playaround with the code, work on issues and make PRs online using Gitpod
[Gitpod](https://www.gitpod.io/) (an Online Open Source VS Code-like IDE which is free for Open Source). With a single it will launch a workspace and automatically: 

- clone the `visx` repo.
- install the dependencies.
- run `yarn build`.

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/from-referrer/)

#### Rebuild one package

Upon modification of a single `package` you can run

```sh
# build the package as cjs version
yarn build-one --workspaces=@visx/package

# build the esm version (the @visx/demo next server sources these files)
yarn build-one --workspaces=@visx/package --esm

# generate d.ts(definition files) for a lib
yarn type-one --workspaces=@visx/package --esm
```

from the `visx` monorepo root to re-build the package with your changes.

#### Running demo pages

You can use the local [`next.js`](https://nextjs.org) dev server within `packages/visx-demo` to view
and iterate on your changes in the gallery. From the `packages/visx-demo` folder run `yarn dev` to
start the next server which (if correctly sym-linked) will also watch for changes you make to other
packages (upon re-building them).

#### Config generation

`visx` uses [`@airbnb/nimbus`](https://github.com/airbnb/nimbus) to generate build configuration for
`eslint`, `prettier`, `jest`, `babel`, and `typescript`.
