---
tags: [ecosystem]
---

# Compilers, Typecheckers, and Parsers

Because OCaml is one of the best tools for creating compilers, typecheckers, etc, you'll find a wide variety of projects made in OCaml.

## Languages and Compilers:

* [Reason](https://reasonml.github.io/):
Friendly syntax & toolchain for OCaml allowing both compilation to javascript and native executables.
* [Morbig](https://github.com/colis-anr/morbig):
Parser for a POSIX-compliant shell.
* [cDuce](http://www.cduce.org/):
a modern XML-oriented functional language with innovative features.
* [Compcert C Compiler](http://compcert.inria.fr/):
C Compiler supporting most of the ISO C90 and C99 / ANSI C  features.
* [Eff Programming Language](http://www.eff-lang.org/):
functional language with typed handlers for exceptions as well as other computational effects such as state or I/O.
* [Hack Programming Language](http://hacklang.org/) 
* [Haxe Programming Language](http://haxe.org/) 
* [Mezzo Programming Language](http://protz.github.io/mezzo/):
a programming language in the ML tradition,
which places strong emphasis on the control of aliasing and access to mutable memory.
* [OCaml-Java](http://www.ocamljava.org):
OCaml to Java bytecode compiler.
* [Opa Programming Language](http://opalang.org/) 
* [Rhine](https://github.com/artagnon/rhine-ml):
A Lisp on LLVM written in OCaml.
* [tis-interpreter](https://github.com/TrustInSoft/tis-interpreter):
An interpreter for finding subtle bugs in programs written in standard C

## Parsers and Lexers

* [Angstrom](https://github.com/inhabitedtype/angstrom):
Parser combinators targetted at fast protocols, built for speed and memory efficiency
* [Sedlex](https://github.com/alainfrisch/sedlex):
a modern, encoding-agnostic (read: Unicode-supporting) lexer generator.
* [Menhir](http://gallium.inria.fr/~fpottier/menhir):
An LR(1) parser generator for OCaml.
* [Nice Parser](https://github.com/smolkaj/nice-parser):
Remove boilerplate from OCaml parser generators using `Menhir` and `Sedlex`.
* [ocamllex/ocamlyacc](https://caml.inria.fr/pub/docs/manual-ocaml/lexyacc.html):
lex and yacc C-based implementation for OCaml. Were the go-to solution for many years.
* [Opal](https://github.com/pyrocat101/opal):
Self-contained monadic parser combinators for OCaml.
* [Obelisk](https://github.com/Lelio-Brun/Obelisk):
produce readable LaTeX, HTML, or plain-text EBNF-style documentation for your grammar.

## Type Checkers

* [Flow](https://github.com/facebook/flow):
A typechecker for Javascript written by Facebook.
* [Pyre](https://github.com/facebook/pyre-check):
A typechecker for Python written by Facebook.

## Systems

* [mpst](https://github.com/keigoi/ocaml-mpst):
Multiparty Session Types. A communication library guaranteeing important properties.

# Miscellaneous
* [pp-loc](https://github.com/Armael/pp_loc):
[PPX](ppx.md) processor that generates nice error messages, just like the OCaml compiler.

## Articles:

* [Kaleidoscope: Implementing a Language with LLVM in Objective Caml](https://releases.llvm.org/12.0.0/docs/tutorial/OCamlLangImpl1.html) (Since 13.0.0, LLVM started using C as the tutorial language)

