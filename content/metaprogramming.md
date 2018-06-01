# Metaprogramming

## PPX Syntax Extensions

ppx is the syntax extension format supported currently by OCaml. It replaces older techniques such as Camlp4 by limiting the scope of language extensions and dedicating to them a specific syntax.

* [ppxlib](https://github.com/ocaml-ppx/ppxlib): The modern solution for writing PPX extensions. Without this library, writing PPX
extensions is fragile and breaks with OCaml version changes. `ppxlib` merges several older projects together to provide a complete
platform for writing efficient, resilient PPX extensions.

### Articles

* [A Guide to Extension Points in OCaml](http://whitequark.org/blog/2014/04/16/a-guide-to-extension-points-in-ocaml/)
* [Extension Points, or how OCaml is becoming more like Lisp](https://blogs.janestreet.com/extension-points-or-how-ocaml-is-becoming-more-like-lisp)
* [Syntax extensions without Camlp4: let's do it!](http://www.lexifi.com/blog/syntax-extensions-without-camlp4-lets-do-it)

### Extensions

* [ppx_import](https://github.com/whitequark/ppx_import)  – Import is a syntax extension that allows to pull in types or signatures from other compiled interface files.
* [ppx_string_interpolate](https://github.com/sheijk/ppx_string_interpolate)  – A simple ppx filter to support string interpolation like `[%str "value of foo is $(foo)"]`.
* [ppx_monad](https://github.com/rizo/ppx_monad)  – Monad syntax extension for OCaml.
* [ppx_deriving_yojson](https://github.com/whitequark/ppx_deriving_yojson)  – A Yojson codec generator for OCaml.

## Other

* [MetaOCaml](http://okmij.org/ftp/ML/MetaOCaml.html)  – an OCaml dialect for multi-stage programming.
* [Fan](http://thinkinginmeta.com/Fan)  – Fan is a compile-time metaprogramming system for OCaml, originally inspired from Camlp4. It's a combination of OCaml and Lispy Macros. It shares the same concrete syntax with OCaml.
* [camlp5](http://camlp5.gforge.inria.fr/)  - Camlp5 is a preprocessor-pretty-printer of OCaml.
* [camlp4](http://caml.inria.fr/pub/docs/manual-camlp4/manual002.html)  - Camlp4 is part of the standard OCaml distribution and is different from Camlp5.
