---
layout: page
tags: [ecosystem]
---

# Lenses

Lenses are a modular, functional method to update and read immutable record fields.
They were developed originally by the Haskell community but have now been ported to other languages,
including OCaml.
If you're writing a functional application with deeply-nested immutable records,
Lenses are very helpful.

* [Lens](https://github.com/pdonadeo/ocaml-lens):
A lens implementation in OCaml.
Includes a PPX rewriter for boilerplate lens accessors.
* [Accessor](https://github.com/janestreet/accessor):
Jane Street's version of Lenses.
Compiles against either `Base`, `Core` or `Async`.
Also includes a PPX rewriter.
