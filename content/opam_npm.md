---
tags: [package management, quickstart]
---

# OPAM for npm/yarn users

Author: [Louis Khady (@khady)](https://github.com/Khady)

## Getting Started

[OPAM](https://opam.ocaml.org/) is the main package manager for OCaml.
This is the OCaml equivalent of [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/en/).
OPAM is a command line tool to manipulate packages that are defined in opam files.
Most [OPAM packages](https://opam.ocaml.org/packages/) are published on the main
 [OPAM repository](https://github.com/ocaml/opam-repository), which is the equivalent of the npm registry.

This document presents the corresponding opam commands, files and
configurations for the most common npm idioms.

OPAM 2.0 is available. If you're using an earlier version, you should upgrade.

There is a summary at the end of the page, containing all the most
common commands to know, and the the official [OPAM introduction](https://opam.ocaml.org/doc/2.0/Usage.html)
contains a lot of information.

## Initial configuration

### Installation

The first thing to do is to install OPAM, as one would install npm. There is an
[official documentation page](https://opam.ocaml.org/doc/2.0/Install.html) on installation.
Most of the time, we can simply get it from your package manager.
Otherwise, binaries are provided for every platform.

### Initialization

npm and yarn don't need any initialization after they are installed,
even if it is possible to customize a few settings.
For opam, however, there is a necessary first step:

```
opam init -a
```

Let's try to explain more in details what it does.
I am quoting the documentation of `opam init` itself here:

> The init command initialises a local "opam root" (by default,
> `~/.opam/`) that holds opam's data and packages. This is a necessary
> step for normal operation of opam. The initial software repositories
> are fetched, and an initial 'switch' can also be installed, according
> to the configuration and options. These can be afterwards configured
> using opam switch and opam repository.

> Additionally, this command allows to customise some aspects of opam's
> shell integration, when run initially (avoiding the interactive
> dialog), but also at any later time.

The interesting parts are:

- The opam root is at `~/.opam`
- opam uses shell integration to make our life easier
- opam uses the concept of a *switch*

A switch is the equivalent of the `node_modules` folder in npm's
world. It contains all the packages that are installed. One difference
from npm is that we can have multiple global switches, as if we could
have different `yarn global` projects. It can be handy sometimes, but
to avoid confusion I recommend avoiding global switches.

The default settings can be changed if the `-a` option is omitted while
calling `opam init`.

### Minimal package.json equivalent

The equivalent to `package.json` is an `app.opam` file, where `app` is the name of the package.
So, for example, `app.opam` could be `webpack.opam`.
It is possible to have multiple opam files in the same directory.

There is no opam command to manipulate the opam file.
Things like `npm init` or `yarn add` will have to be done by hand.

A minimal opam file looks like this:

```
opam-version: "2.0"
name: "my-app"
authors: "Louis"
homepage: "https://github.com/khady/example"
maintainer: "ex@ample.com"
dev-repo: "git+ssh://git@github.com:khady/example.git"
bug-reports: "https://github.com/khady/example/issues"
version: "0.1"
build: [
  [ "dune" "subst" ] {pinned}
  [ "dune" "build" "-p" name "-j" jobs ]
]
depends: [
  "dune" {build}
  "opam-lock" {dev}
]
```

`build:` tells opam that `dune` is needed only to build the project.
`dev:` is to mark dev dependencies.

## npm/yarn-equivalent commands

### npm install / yarn

`npm install` or `yarn` commands cover multiple opam commands,
depending on the context.

The first case is in the absence of a local switch in the current project.
This can be verified by looking for a `_opam` directory at the root of the
project, and it corresponds to an npm project without a `node_modules`
directory. In this first case, we need to initialize a local switch.

```
opam switch create . 4.07.0 --deps-only
```

The second case is in the presence of a local switch.

```
opam install . --deps-only
```

### npm install <pkg> / yarn add

To install a package with opam is easy:

```
opam install PACKAGE
```

But opam does not modify the `app.opam` file during the
installation -- it has to be done by hand.
This is as simple as adding
the name of the package in the `depends` field.

### npm link / yarn link

`npm link` in the opam world is `opam pin`.
Its usage is well described in
[the official documentation](https://opam.ocaml.org/doc/2.0/Usage.html#opam-pin
).

### npm upgrade / yarn upgrade

In this case, there is a direct equivalent for the command in opam, and it is easy to
remember.

```
opam upgrade PACKAGE
```

`opam upgrade` is also able to upgrade *all* the packages of the local
switch if no package name is given.

There is one big difference compared to npm though: opam stores a local copy
of the opam repository, like `apt-get` does in Debian.
So we often
want to update this copy before to request an upgrade:

```
opam update && opam upgrade PACKAGE
```

## Extra package.json concepts

### dev dependencies

There is no strict equivalent of the `dev-dependencies` field of
`package.json`, but it is possible to achieve the same thing in two
ways:

- By marking the package with `dev` in `depends`
- By using a `dev.opam` file.

### lock files

Lock files are also not common yet in the opam world, but it may be summarized as:

- Using `opam lock` to generate the lock file when needed (basically
  after each `opam install` or `opam upgrade`).
- Adding `--locked` to all the `opam install`, `--deps-only` and `opam
  switch create .` commands.

### Scripts

This aspect doesn't exist in the opam world. The closest we get is the
equivalent of `yarn exec`, which is `opam exec`.

Instead of writing a `package.json` with a script field like this:

```json
"scripts": {
  "release": "make release"
}
```

We run `opam exec` like this:

```
opam exec -- make release
```
