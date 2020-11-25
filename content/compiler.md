---
tags: [compiler]
---

# Compiler

The OCaml compiler is a complicated piece of software. Below is an attempt to document information that could not fit easily into the codebase, including relevant papers. Feel free to break this up into pages as the need arises.

## Articles

* [Runtime memory layout from the Real World OCaml book](https://dev.realworldocaml.org/runtime-memory-layout.html)
* [Presentation on OCaml Internals (pdf)](/assets/pdf/ocaml_internals.pdf):
excellent presentation on how OCaml is built on the inside.
* [Exception handling in OCaml](https://stackoverflow.com/questions/8564025/ocaml-internals-exceptions):
a StackOverflow answer detailing how exceptions work in OCaml.
* [The OCaml compiler pipeline](https://sookocheff.com/post/ocaml/the-ocaml-compiler-pipeline/)

## Interesting Branches of the Compiler

* [Multicore OCaml](https://github.com/ocamllabs/ocaml-multicore) and its associated
[wiki](https://github.com/ocamllabs/ocaml-multicore/wiki)
* [WASM backend](https://github.com/SanderSpies/ocaml/tree/wasm-backend)
* [Typed Algebraic Effects](https://github.com/lpw25/ocaml-typed-effects)

## Commands

* `ocamlc -config`:
show all configuration parameters for the compiler. Very useful.

## Runtime

* [Runtime memory layout from the Real World OCaml book](https://dev.realworldocaml.org/runtime-memory-layout.html)

[See also Runtime](runtime.md)

### Articles

* [Description of allocator schemes](http://gallium.inria.fr/~scherer/doc/chameau-sur-le-plateau/2019-10-08-damien-doligez-major-allocator.org)
* [Low-latency garbage collection](https://blog.janestreet.com/building-a-lower-latency-gc/)


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

The parser converts OCaml syntax to an abstract sytnax tree (AST) representation
([parsing/parsetree.mli](https://github.com/ocaml/ocaml/blob/trunk/parsing/parsetree.mli)).

#### ppx

PPX rewriters are separate executables that parse binary AST,
modify certain parts as needed,
and spit out binary AST for the compiler to reload.

### Typechecker

The typechecker transforms the plain AST to typechecked AST
([typing/typedtree.mli](https://github.com/ocaml/ocaml/blob/trunk/typing/typedtree.mli)).

### Lambda

After typechecking, if a program isn't rejected,
types are mostly erased from the AST except information relevant to optimizations.
The resulting AST 
([lambda/lambda.mli](https://github.com/ocaml/ocaml/blob/trunk/lambda/lambda.mli))
is leaner and easier to manipulate than the typed AST.

* [ICFP Presentation on Semantics of Lambda](https://www.youtube.com/watch?v=R3Uk9gt90Tk)

#### Pattern Matching

Pattern matching uses a fairly complex algorithm
([lambda/matching.mli](https://github.com/ocaml/ocaml/blob/trunk/lambda/matching.ml))
to convert potentially complex patterns into simpler, efficient AST.

* [Compiling Pattern Matching to Good Decision Trees](http://moscova.inria.fr/~maranget/papers/ml05e-maranget.pdf)

### Flambda

Flambda is an optional, additional layer of optimization,
residing in [/middle_end](https://github.com/ocaml/ocaml/tree/trunk/middle_end).

### Clambda
### cmm
#### Register Coloring
### assembly


