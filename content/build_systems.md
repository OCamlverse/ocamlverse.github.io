---
tags: [ecosystem]
---

# OCaml Package Management

* [OPAM](http://opam.ocaml.org/)  is the modern package manager for OCaml. If you want to publish a library
in OCaml, OPAM is your best and only option, taking care of package dependency and invoking the build system as needed.
    * [opam-ci](https://github.com/ocaml/infrastructure/wiki/Using-the-opam-ci-tool), a plugin for OPAM,
    provides access to full continuous integration information about every package in OPAM.
    You can see which packages compile and which are broken from the command line.
* [opam-check-all](http://check.ocamllabs.io/): shows you all OPAM packages and their build status
on multiple versions of the compiler.
Provides filtering for specific package versions, build errors, and package authors.
* [OPAM for Windows](https://fdopen.github.io/opam-repository-mingw)  - opam repository and experimental
native build for Windows.
* [makorel](https://github.com/sagotch/makorel)  – Release OPAM packages easily. (edit: Is this maintained?)
* [topkg](https://github.com/dbuenzli/topkg)  is a tool that allows you to easily release and maintain
many OCaml packages at once. A little bit of extra metadata in your repo gives you the ability to use the
topkg command line tools and manage your authored packages.
* [dune-release](https://github.com/samoht/dune-release): a tool for managing and releasing a package easily
on OPAM. Built only for projects that use Dune as a build system.

## OCaml Build System

* [Dune](https://github.com/ocaml/dune)  (formerly jbuilder) is a fast, easy to use build system for OCaml
projects, and is seen as the main choice for new projects in OCaml. Dune can handle both OCaml (.ml) and
Reason (.re) files.

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
