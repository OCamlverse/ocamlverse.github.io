---
tags: [ecosystem]
---

# Metaprogramming and PPX

## PPX Syntax Extensions

ppx is the syntax extension format supported currently by OCaml. It replaces older techniques such as Camlp4 by limiting the scope of language extensions and dedicating to them a specific syntax.

* [ppxlib](https://github.com/ocaml-ppx/ppxlib): The modern solution for writing PPX extensions. Without this library, writing PPX
extensions is fragile and breaks with OCaml version changes. `ppxlib` merges several older projects together to provide a complete
platform for writing efficient, resilient PPX extensions.

### Articles

* [A Guide to PreProcessor EXtensions](ppx.md)
* [A Guide to Extension Points in OCaml](http://whitequark.org/blog/2014/04/16/a-guide-to-extension-points-in-ocaml/)
* [Extension Points, or how OCaml is becoming more like Lisp](https://blogs.janestreet.com/extension-points-or-how-ocaml-is-becoming-more-like-lisp)
* [Syntax extensions without Camlp4: let's do it!](http://www.lexifi.com/blog/ocaml/syntax-extensions-without-camlp4-lets-do-it)

### PPX Extensions

* [ppx_deriving](https://github.com/ocaml-ppx/ppx_deriving):
Type-based framework for ppx extensions.
Contains built-in plugins for `show`, `eq`, `ord`, `enum`, `iter`, `map`, `fold`, and `make`.
* [ppx_visitors](https://gitlab.inria.fr/fpottier/visitors):
Automatically use the visitor object-oriented pattern on a data structure,
extending it with behaviors rather than needing to specify each variant's behavior.
* [ppx_import](https://github.com/whitequark/ppx_import):
Import is a syntax extension that allows to pull in types or signatures from other compiled interface files.
This can be handy when not wanting to repeat a type in both the `.ml` and `.mli` file, for example.
* [ppx_optcomp](https://github.com/janestreet/ppx_optcomp):
Conditional compilation like `#ifdef` for OCaml.
* [ppx_string_interpolate](https://github.com/sheijk/ppx_string_interpolate):
A simple ppx filter to support string interpolation like `[%str "value of foo is $(foo)"]`.
* [ppx_monad](https://github.com/rizo/ppx_monad):
Monad syntax extension for OCaml.
* [ppx_deriving_yojson](https://github.com/whitequark/ppx_deriving_yojson):
A Yojson codec generator for OCaml. See [Serialization](file_formats.md#Serialization).
* [yojson_ppx](https://github.com/NathanReb/ppx_yojson):
Another Yojson ppx generator.
* [ppx_regex](https://github.com/paurkedal/ppx_regexp):
Contains 2 ppx parsers to OCaml [regex](regular_expressions.md) libraries:
  * ppx_regexp: maps to use Re (untyped regex)
  * ppx_tyre: maps to use Tyre for typed regex.
* [ppx_expect](https://github.com/janestreet/ppx_expect):
Cram-like tests for OCaml. See [Testing](testing.md).
* [Bisect_ppx](https://github.com/rleonid/bisect_ppx):
Code coverage for OCaml. See [Code Tools](code_tools.md).
* [ppx_pgsql](https://github.com/tizoc/ppx_pgsql):
A syntax extension for embedded SQL queries using PG'OCaml. See [Databases](databases.md).
* [ppx_deriving_protobuf](https://github.com/ocaml-ppx/ppx_deriving_protobuf):
Derive Protobuf files from OCaml types. See [Protocols](protocols.md).

## Other

* [cppo](https://github.com/ocaml-community/cppo):
A simple C++-like preprocessor for OCaml files.
* [MetaOCaml](http://okmij.org/ftp/ML/MetaOCaml.html):
An OCaml dialect for multi-stage programming.
* [Fan](http://thinkinginmeta.com/Fan):
Fan is a compile-time metaprogramming system for OCaml, originally inspired from Camlp4.
It's a combination of OCaml and Lispy Macros.
It shares the same concrete syntax with OCaml.
* [camlp4](http://caml.inria.fr/pub/docs/manual-camlp4/manual002.html):
Camlp4 is an older way of modifying OCaml syntax and applying metaprogramming.
It is generally discouraged nowadays -- use ppx instead.
* [camlp5](http://camlp5.gforge.inria.fr/):
Another variant of metaprogramming that is discouraged nowadays.
