---
tags: [package_management, ecosystem]
---

# Package Management

* [OPAM](http://opam.ocaml.org/)  is the modern package manager for OCaml. If you want to publish a library
in OCaml, OPAM is your friend, taking care of package dependency and invoking the build system as needed.
    * [OPAM command tutorial with comparison to npm](opam_npm.md)
    * [opam-ci](https://github.com/ocaml/infrastructure/wiki/Using-the-opam-ci-tool), a plugin for OPAM,
    provides access to full continuous integration information about every package in OPAM.
    You can see which packages compile and which are broken from the command line.
* [opam-check-all](http://check.ocamllabs.io/): shows you all OPAM packages and their build status
on multiple versions of the compiler.
Provides filtering for specific package versions, build errors, and package authors.
* [OPAM for Windows](https://fdopen.github.io/opam-repository-mingw)  - opam repository and experimental
native build for Windows.
* [esy](https://esy.sh/)
is a tool that is fully compatible with OPAM on the client side, while also allowing for the installation of
ReasonML packages.
Currently it is installed either via `npm` (the node.js package manager) or your operating system's package manager.
What `esy` brings to the table that OPAM lacks is the ability to cache all installed packages,
allowing for reuse of binaries, and for the effortless creation of sandboxed environments for each of your projects.

## Package Release System

* [dune-release](https://github.com/samoht/dune-release): a tool for managing and releasing a package easily
on OPAM.
Built only for projects that use Dune as a build system.
This is the tool you should use for easily updating your OPAM projects.
* [topkg](https://github.com/dbuenzli/topkg):
an alternative, older tool that allows you to easily release and maintain
many OCaml packages at once.
A little bit of extra metadata in your repo gives you the ability to use the
topkg command line tools and manage your authored packages.

## OCaml Build System

* [dune](https://github.com/ocaml/dune)  (formerly jbuilder) is a fast, easy to use build system for OCaml
projects, and is seen as the main choice for new projects in OCaml. Dune can handle both OCaml (.ml) and
Reason (.re) files.

  * [dune-starter](https://github.com/mjambon/dune-starter):
  a sample project indicating ideal code layout for an OCaml project.
  * [dune-configurator](https://github.com/ocaml/dune/blob/master/doc/configurator.rst):
  a tool similar to configure scripts that can query the state of a given system at the library level
  and produce configuration files to build differently based on said configuration.
  * By default, Dune treats warnings as errors when building in the dev mode (ie. a local build).
  To change this, use [this tip](https://dune.readthedocs.io/en/latest/faq.html#how-to-make-warnings-non-fatal).

* [ocamlscript](https://github.com/mjambon/ocamlscript):
Allows you to run OCaml files as if they were scripts.
Pre-compiles and runs them on the spot.

* [ocamlfind](http://projects.camlcity.org/projects/findlib.html)  is a utility similar to //pkg-config//
that allows local libraries to find each other on your system. You don't need to have much awareness of 
ocamlfind nowadays because Dune and OPAM (see below) will do all the work, but it's good to know about
ocamlfind's existence.

## ReasonML Build System/Package Management

* Reason lives in the Javascript ecosystem, and as such, its build tool of choice is Bucklescript, and its
package management solution is `npm`

### Legacy OCaml build systems

You may find some other build systems used by various OCaml projects. The general recommendation though is to
stick with Dune whenever possible.

* [ocamlbuild](http://ocaml.org/learn/tutorials/ocamlbuild/) : the option most used as a build tool before Dune
came about.
* [Oasis](http://oasis.forge.ocamlcore.org/) : An older tool to integrate a configure, build and install system
in your OCaml project.  Before OPAM and Dune, this was a relatively easy way to create your project.
* [oasis2opam](https://github.com/ocaml/oasis2opam) : Tool to convert OASIS metadata to OPAM package descriptions.
* [jenga](https://github.com/janestreet/jenga) : A monadic build system from Jane Street. Much of the underlying
system used by Dune is composed of code from Jenga.
* [ocaml-makefile](https://github.com/mmottl/ocaml-makefile) : Easy to use Makefile for small to medium-sized
OCaml-projects.
* [obuild](https://github.com/ocaml-obuild/obuild) : Simple package build system for ocaml.
