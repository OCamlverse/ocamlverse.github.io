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
* [Introduction to the PPX Ecosystem](https://tarides.com/blog/2019-05-09-an-introduction-to-ocaml-ppx-ecosystem.html):
Nice and thorough introduction to writing PPXs using `ppxlib`.
* [A Guide to Extension Points in OCaml](http://whitequark.org/blog/2014/04/16/a-guide-to-extension-points-in-ocaml/)
* [Extension Points, or how OCaml is becoming more like Lisp](https://blogs.janestreet.com/extension-points-or-how-ocaml-is-becoming-more-like-lisp)
* [A guide to writing PPX Deriving plugins](http://rgrinberg.com/posts/deriving-slowly/)
* [Am I missing some comprehensive ppxlib resource somewhere?](https://discuss.ocaml.org/t/am-i-missing-some-comprehensive-ppxlib-resource-somewhere/9277):
A discuss post which turned into an important resource about aspects of PPX writing such as `Ast_pattern`.
* [ppxlib as the new standard](https://discuss.ocaml.org/t/ppx-omp-2-0-0-and-next-steps/6231)
* Older: [The Future of PPX: post on discuss](https://discuss.ocaml.org/t/the-future-of-ppx/3766)

### PPX Extensions

* [ppx_enum](https://github.com/cryptosense/ppx_enum):
A nice, simple ppx using `ppxlib` that serves as a good example for potential ppx writers.
* [ppx_deriving](https://github.com/ocaml-ppx/ppx_deriving):
Type-based framework for ppx extensions.
Contains built-in plugins for `show`, `eq`, `ord`, `enum`, `iter`, `map`, `fold`, and `make`.
  * NOTE: `ppx_deriving` currently doesn't make use of `ppxlib`, making it hard to update for future
      OCaml releases.
      As powerful as `ppx_deriving` is, we recommend trying to find a `ppxlib`-based extension instead,
      which will then be a lot more robust going forward.
* [ppx_show](https://gitlab.inria.fr/tmartine/ppx_show/):
A `show` deriver, creating functions for printing out values.
Uses `ppxlib`, which makes it forward-compatible.
* [ppx_visitors](https://gitlab.inria.fr/fpottier/visitors):
Automatically use the visitor object-oriented pattern on a data structure,
extending it with behaviors rather than needing to specify each variant's behavior.
* [ppx_import](https://github.com/ocaml-ppx/ppx_import):
Import is a syntax extension that allows to pull in types or signatures from other compiled interface files.
This can be handy when not wanting to repeat a type in both the `.ml` and `.mli` file, for example.
* [ppx_override](https://gitlab.inria.fr/tmartine/override):
Override allows you to import a module or its types, and then easily change and modify aspects, such as
using `ppx_deriving` on that module's types.
* [ppx_optcomp](https://github.com/janestreet/ppx_optcomp):
Conditional compilation like `#ifdef` for OCaml.
* [ppx_string_interpolate](https://github.com/sheijk/ppx_string_interpolate):
A simple ppx filter to support string interpolation like `[%str "value of foo is $(foo)"]`.
* [ppx_monad](https://github.com/rizo/ppx_monad):
Monadic syntax extension.
* [ppx_let](https://github.com/janestreet/ppx_let):
A monadic syntax extension from Jane Street.
* [ocaml-monadic](https://github.com/zepalmer/ocaml-monadic):
Another monadic syntax extension.
* [ppx_regex](https://github.com/paurkedal/ppx_regexp):
Contains 2 ppx parsers to OCaml [regex](regular_expressions.md) libraries:
  * ppx_regexp: maps to use Re (untyped regex)
  * ppx_tyre: maps to use Tyre for typed regex.
* [ppx_expect](https://github.com/janestreet/ppx_expect):
Cram-like tests for OCaml. See [Testing](testing.md).
* [Bisect_ppx](https://github.com/aantron/bisect_ppx):
Code coverage for OCaml. See [Code Tools](code_tools.md).
* [ppx_pgsql](https://github.com/tizoc/ppx_pgsql):
A syntax extension for embedded SQL queries using PG'OCaml. See [Databases](databases.md).
* [ppx_cstubs](https://github.com/fdopen/ppx_cstubs):
Write C functions directly in your OCaml code. See [FFI](ffi.md).
* [ppx-tyxml](https://ocsigen.org/tyxml/4.3.0/manual/ppx):
Convert html/xml syntax to `tyxml` function calls.

#### Protocol-related

* [ppx_deriving_yojson](https://github.com/whitequark/ppx_deriving_yojson):
A Yojson codec generator for OCaml. See [Serialization](file_formats.md#Serialization).
* [ppx_yojson_conv](https://github.com/janestreet/ppx_yojson_conv):
Alternative to `ppx_deriving_yojson` from Jane Street.
* [ppx_yojson](https://github.com/NathanReb/ppx_yojson):
Convert JSON expressions to `yojson` AST, allowing your code to be cleaner.
* [ppx_deriving_protobuf](https://github.com/ocaml-ppx/ppx_deriving_protobuf):
Derive Protobuf files from OCaml types. See [Protocols](protocols.md).
* [ppx_sexp_conv](https://github.com/janestreet/ppx_sexp_conv):
Derive converters to s-expressions.
* [ppx_protocol_conv](https://github.com/andersfugmann/ppx_protocol_conv):
Framework for multiple serializers for different protocols.

## Other

* [cppo](https://github.com/ocaml-community/cppo):
A simple C++-like preprocessor for OCaml files.
* [MetaOCaml](http://okmij.org/ftp/ML/MetaOCaml.html):
An OCaml dialect for multi-stage programming.
* [metapp](https://github.com/thierry-martinez/metapp):
A ppx extension that provides metaquoting facilities similar to `MetaOCaml`.
* [about_macros](https://oliviernicole.github.io/about_macros.html):
Blog post describing an experimental system of typed macros in OCaml.
* [Fan](http://thinkinginmeta.com/Fan):
Fan is a compile-time metaprogramming system for OCaml, originally inspired from Camlp4.
It's a combination of OCaml and Lispy Macros.
It shares the same concrete syntax with OCaml.
* [camlp4](http://caml.inria.fr/pub/docs/manual-camlp4/manual002.html):
Camlp4 is an older way of modifying OCaml syntax and applying metaprogramming.
It is generally discouraged nowadays -- use ppx instead.
* [camlp5](http://camlp5.gforge.inria.fr/):
Another variant of metaprogramming that is discouraged nowadays.
