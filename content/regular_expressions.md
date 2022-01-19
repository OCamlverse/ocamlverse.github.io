# Regular Expressions

* [Re](https://github.com/ocaml/ocaml-re): a pure OCaml regular expressions library
with combinators, supporting several formats (glob, posix, str...)
* [Tyre](https://github.com/Drup/tyre): Tyre is a set of combinators to build
type-safe regular expressions, allowing automatic extraction and modification of
matched groups.
* [ppx_regex](https://github.com/paurkedal/ppx_regexp): Contains 2 ppx parsers:
  * ppx_regexp: maps to use Re (untyped regex)
  * ppx_tyre: maps to use Tyre for typed regex.
* [ocaml-pcre](https://github.com/mmottl/pcre-ocaml): bindings to the PCRE library
(perl-compatible regular expressions)
* [Humane-re](https://github.com/rgrinberg/humane-re): attempts to provide an easy
interface for 90% of your regex needs.
This is a binding on top of Re.
* OCaml comes with the
[Str](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Str.html) module.
This module is __not__ recommended because it is not part of the standard library,
it uses global states and is not particularly fast, but its availability makes it
useful when you don't have access to anything better.  It is partially implemented
in C and thus not available in `js_of_ocaml`.
