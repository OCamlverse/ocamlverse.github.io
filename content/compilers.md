---
tags: [ecosystem]
---

# Compilers, Typecheckers, and Parsers

Because OCaml is one of the best tools for creating compilers, typecheckers, etc, you'll find a wide variety of projects made in OCaml.

# Languages and Compilers:

* [cDuce](http://www.cduce.org/)  - cDuce is a modern XML-oriented functional language with innovative features.
* [Compcert C Compiler](http://compcert.inria.fr/)  - It is a C Compiler supporting most of the ISO C90 and C99 / ANSI C  features.
* [Eff Programming Language](http://www.eff-lang.org/)  - Eff is a functional language with handlers of not only exceptions, but also of other computational effects such as state or I/O.
* [Hack Programming Language](http://hacklang.org/) 
* [Haxe Programming Language](http://haxe.org/) 
* [Neko Programming Language](http://nekovm.org)  - Originally the compiler was written in OCaml.
* [Mezzo Programming Language](http://protz.github.io/mezzo/)  - Mezzo is a programming language in the ML tradition, which places strong emphasis on the control of aliasing and access to mutable memory.
* [OCaml-Java](http://www.ocamljava.org)  - OCaml to Java bytecode compiler.
* [Opa Programming Language](http://opalang.org/) 
* [Rhine](https://github.com/artagnon/rhine-ml)  – A Lisp on LLVM written in OCaml.
* [Rust Programming Language](http://rust-lang.org)  - Originally written in OCaml before bootstrapping.
* [Quick C-- Target Language](http://www.cminusminus.org/)  - It is now a dead project. [https://github.com/nrnrnr/qc-- Github Repo]. [http://www.cs.tufts.edu/~nr/c--/qc--.html Alternative website].
* [tis-interpreter](https://github.com/TrustInSoft/tis-interpreter)  - An interpreter for finding subtle bugs in programs written in standard C
* [Reason](https://reasonml.github.io/)  - Friendly syntax & toolchain for OCaml by Facebook.
* [Others](http://caml.inria.fr/cgi-bin/hump.en.cgi?sort=0&browse=88)  - Some other compilers implemented in OCaml, quite a few dead now.

# Parser and Lexer Generators:

* [Opal](https://github.com/pyrocat101/opal)  – Self-contained monadic parser combinators for OCaml.
* [Sedlex](https://github.com/alainfrisch/sedlex)  is a modern, encoding-agnostic (read: Unicode-supporting) lexer generator (the ppx-based successor to [http://www.cduce.org/download.html#side ulex].)
* [Menhir](http://gallium.inria.fr/~fpottier/menhir)  – Menhir is a LR(1) parser generator for OCaml.
  * See [ocaml-parsing](https://github.com/smolkaj/ocaml-parsing)  for a clearer example of using Menhir and Sedlex to produce a useful parser,
  * [Obelisk](https://github.com/Lelio-Brun/Obelisk) , a neat project to produce readable LaTeX, HTML, or plain-text EBNF-style documentation for your grammar.
* [ocamllex/ocamlyacc](http://caml.inria.fr/pub/docs/manual-ocaml-4.01/lexyacc.html)  – lex and yacc implementation for OCaml.
* [Angstrom](https://github.com/inhabitedtype/angstrom)  - Parser combinators built for speed and memory efficiency

# Articles:

* [Kaleidoscope: Implementing a Language with LLVM in Objective Caml](http://llvm.org/docs/tutorial/OCamlLangImpl1.html) 
* [Getting started with OCaml bindings for LLVM](http://nopaniers.calepin.co/getting-started-with-ocaml-bindings-for-llvm.html) 
