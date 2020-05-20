---
tags: [compiler]
---

# Compiler

The OCaml compiler is a complicated software artifact. Below is an attempt to document information that could not fit easily into the codebase, including relevant papers. Feel free to break this up into pages as the need arises.

## Articles

* [Presentation on OCaml Internals (pdf)](/assets/pdf/ocaml_internals.pdf):
excellent presentation on how OCaml is built on the inside.
* [Exception handling in OCaml](https://stackoverflow.com/questions/8564025/ocaml-internals-exceptions):
a StackOverflow answer detailing how exceptions work in OCaml.

## Interesting Branches of the Compiler

* [Multicore OCaml](https://github.com/ocamllabs/ocaml-multicore) and its associated
[wiki](https://github.com/ocamllabs/ocaml-multicore/wiki)
* [WASM backend](https://github.com/SanderSpies/ocaml/tree/wasm-backend)
* [Typed Algebraic Effects](https://github.com/lpw25/ocaml-typed-effects)

## Commands

* `ocamlc -config`:
show all configuration parameters for the compiler. Very useful.

## Compiler Internals

* [hacking.adoc](https://github.com/ocaml/ocaml/blob/trunk/HACKING.adoc): a basic guide to the compiler's internals.

### Driver

The compiler driver, residing in the [/driver](https://github.com/ocaml/ocaml/tree/trunk/driver) directory,
runs the entire compilation process from start to finish.
The 2 entry points into the system are [optmain.ml](https://github.com/ocaml/ocaml/blob/trunk/driver/optmain.ml)
for the native compiler and [main.ml](https://github.com/ocaml/ocaml/blob/trunk/driver/main.ml)
for the bytecode compiler,
setting up 2 separate execution paths through the code.

Both paths go through the [pparse.ml](https://github.com/ocaml/ocaml/blob/trunk/driver/pparse.ml) file,
which handles PPX rewriters.
This file dumps the current parsed AST, calls a given PPX executable,
and reloads the resulting AST.

The two compilation files are [compile.ml](https://github.com/ocaml/ocaml/blob/trunk/driver/compile.ml)
for bytecode, and [optcompile.ml](https://github.com/ocaml/ocaml/blob/trunk/driver/optcompile.ml) for native.
Both files pipe the different kinds of data through all the compilation stages.
While native compilation has options for
either `clambda` (naive) or `flambda` (optimized) compilation, bytecode compilation currently has only
one mode, which is equivalent to `clambda` compilation.

### Parser
#### ppx
### Typechecker
### Lambda
* [ICFP Presentation on Semantics of Lambda](https://www.youtube.com/watch?v=R3Uk9gt90Tk)
#### Pattern Matching

* [Compiling Pattern Matching to Good Decision Trees](http://moscova.inria.fr/~maranget/papers/ml05e-maranget.pdf)

### Flambda
### Clambda
### cmm
#### Register Coloring
### assembly

## Runtime

* [Description of allocator schemes](http://gallium.inria.fr/~scherer/doc/chameau-sur-le-plateau/2019-10-08-damien-doligez-major-allocator.org)
* [Low-latency garbage collection](https://blog.janestreet.com/building-a-lower-latency-gc/)

