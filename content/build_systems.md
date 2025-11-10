---
tags: [package management, ecosystem]
---

# Package Management

We'll suggest the easiest tools to use first, and then explain the details.

## End-to-End Project Management Tools

* [drom](https://github.com/ocamlpro/drom):
A full project management tool similar to Rust's `cargo`,
aiming for the easiest possible user experience.
Calls `opam`, `dune` and `odoc` behind the scenes.
`drom` knows how to talk to github, is configured with `toml` files, and can produce `Sphinx` and `odoc` documentation.
* [spin](https://github.com/tmattio/spin):
For easy project initialization, you may want to try `spin`.
It has all sorts of templates for different kinds of project (more than `drom` does),
but unlike `drom` it doesn't manage the various OCaml tools.
* [pesy](https://github.com/esy/pesy):
On the other side of the package management divide,
we have `pesy`, which uses `esy` as its package management backend.


## Package Management

Currently, package management and building involves 2 tools: `dune` for building the code
and `opam` for packaging it and installing dependencies.
This may change as there is an ongoing effort to make `dune` do both jobs.

* [OPAM](http://opam.ocaml.org/) is the modern package manager for OCaml.
If you want to publish a library
in OCaml, OPAM is your friend, taking care of package dependency and invoking the build system as needed.
OPAM supports lockfiles and sandboxing (local switch creation),
but the features aren't as well-integrated as they are in `esy`.

    * [OPAM command tutorial with comparison to npm](opam_npm.md)
    * [opam-ci](https://github.com/ocaml/infrastructure/wiki/Using-the-opam-ci-tool), a plugin for OPAM,
    provides access to full continuous integration information about every package in OPAM.
    You can see which packages compile and which are broken from the command line.
    * [OPAM 2.0 tips](https://opam.ocaml.org/blog/opam-20-tips/):
    Local opam installs, pinning, and lock files.
    * [opam-check-all](http://check.ocamllabs.io/): shows you all OPAM packages and their build status
    on multiple versions of the compiler.
    Provides filtering for specific package versions, build errors, and package authors.
    * [OPAM for Windows](https://fdopen.github.io/opam-repository-mingw):
    OPAM repository modified for native Windows usage (deprecated).

* [esy](https://esy.sh/):
    **NOTE**: as of 2025, it's not clear how well `esy` is maintained or will continue being maintained.
    An alternative tool for package management that draws on lessons learned from the JavaScript ecosystem.
    Its main advantages over OPAM are

    * Immutable packages managed in a git-like system.
    * All packages have been made relocatable.
    * lockfiles specifying precise package versions by default.

    What this means is that sandboxed, isolated environments with a global binary cache are easier to create than in OPAM,
    as is a lockfile-based development approach.
    However, `esy`'s method suffers from the fact that even the slightest upgrade creates new binary artifacts,
   causing garbage to pile up.
   A periodic garbage collection is therefore recommended.
   Currently `esy` is installed using `npm` (the node.js package manager),
   but this is done purely for ease of distribution.

## OCaml Build System

* [dune](https://github.com/ocaml/dune)  is a fast, easy to use build system for OCaml
projects. Dune can handle both OCaml (`.ml`) and
Reason (`.re`) files.

  * [mkocaml](https://github.com/chrisnevers/mkocaml):
  tool for creating a new OCaml project using dune.
  * [dune-starter](https://github.com/mjambon/dune-starter):
  a sample project indicating ideal code layout for an OCaml project.
  * By default, Dune treats warnings as errors when building in the dev mode (ie. a local build).
  To change this, use [this tip](https://dune.readthedocs.io/en/latest/faq.html#how-to-make-warnings-non-fatal).
  * [dune-deps](https://github.com/mjambon/dune-deps):
  Allows you to view your dependencies in graph form.
  * Caching: Dune now includes an opt-in feature that shares build artifacts. See [here](https://dune.readthedocs.io/en/stable/caching.html).
  * [Article outlining dune's history](https://blog.janestreet.com/how-we-accidentally-built-a-better-build-system-for-ocaml-index/)

## Package Release System

Managing packages can take some effort, and there are some tools available for automating this process.

* [dune-release](https://github.com/samoht/dune-release): a tool for managing and releasing a package easily
on OPAM.
Built only for projects that use Dune as a build system.
This is the tool you should use for easily updating your OPAM projects.
* [topkg](https://github.com/dbuenzli/topkg):
an alternative, older tool that allows you to easily release and maintain
many OCaml packages at once.
A little bit of extra metadata in your repo gives you the ability to use the
topkg command line tools and manage your authored packages.

## Other Tooling

* [ocamlscript](https://github.com/mjambon/ocamlscript):
Allows you to run OCaml files as if they were scripts.
Pre-compiles and runs them on the spot.

* [ocamlfind](http://projects.camlcity.org/projects/findlib.html)  is a utility similar to `pkg-config`
that allows local libraries to find each other on your system. You don't need to have much awareness of
ocamlfind nowadays because Dune and OPAM (see below) will do all the work, but it's good to know about
ocamlfind's existence.

## Continuous Integration

* [setup-ocaml]:
Easy-to-use [GitHub Actions] for running your code on Linux, Mac and Windows machines.
* [setup-dkml](https://github.com/diskuv/dkml-workflows#dkml-workflows): Slightly higher initial setup than setup-ocaml,
but you get [GitHub Actions], [GitLab CI/CD](https://docs.gitlab.com/ee/ci/) and troubleshooting directly on your Linux/macOS/Windows desktop.
The narrow design goal of setup-dkml is to distribute native code, so it has many other advantages and disadvantages compared
to [setup-ocaml]. There is a comprehensive comparison chart available at [setup-dkml].

[setup-ocaml]: https://github.com/ocaml/setup-ocaml
[setup-dkml]: https://github.com/diskuv/dkml-workflows#dkml-workflows
[GitHub Actions]: https://github.com/features/actions

## Legacy OCaml build systems

You may find some other build systems used by various OCaml projects.
The general recommendation is to avoid these legacy tools.

* [ocamlbuild](https://github.com/ocaml/ocamlbuild/blob/master/manual/manual.adoc) : the option most used as a build tool before Dune
came about.
* [Oasis](http://oasis.forge.ocamlcore.org/) : An older tool to integrate a configure, build and install system
in your OCaml project.  Before OPAM and Dune, this was a relatively easy way to create your project.
* [oasis2opam](https://github.com/ocaml/oasis2opam) : Tool to convert OASIS metadata to OPAM package descriptions.
* [jenga](https://github.com/janestreet/jenga) : A monadic build system from Jane Street. Much of the underlying
system used by Dune is composed of code from Jenga.
* [ocaml-makefile](https://github.com/mmottl/ocaml-makefile) : Easy to use Makefile for small to medium-sized
OCaml-projects.
* [obuild](https://github.com/ocaml-obuild/obuild) : Simple package build system for ocaml.
