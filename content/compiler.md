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

## Compiler Internals

* [hacking.adoc](https://github.com/ocaml/ocaml/blob/trunk/HACKING.adoc): a basic guide to the compiler's internals.

### Parser
#### ppx
### Typechecker
### Lambda
#### Pattern Matching

* [Compiling Pattern Matching to Good Decision Trees](http://moscova.inria.fr/~maranget/papers/ml05e-maranget.pdf)

### Flambda
### Clambda
### cmm
#### Register Coloring
### assembly
