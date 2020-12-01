---
layout: page
tags: [ecosystem]
---

# String Manipulation

* The standard library's [String](https://caml.inria.fr/pub/docs/manual-ocaml/libref/String.html)
module is somewhat lacking in terms of functionality.
* [Containers](https://github.com/c-cube/ocaml-containers) has an expanded String module,
with iteration functions and so on.
Containers strives to be backwards-compatible with the Stdlib.
* [AString](https://github.com/dbuenzli/astring):
another implementation of expanded string functionality,
with less regard for standard library compatibility
* [Bigstring](https://github.com/c-cube/ocaml-bigstring):
On 32-bit platforms, OCaml strings are constrained to 20MB sizes.
This library allows one to handle strings of any sizes, and also
to handle C-style strings as if they were OCaml strings.
Built on top of BigArray, and supports memory-mapping.
* [Bigstring/af](https://github.com/inhabitedtype/bigstringaf):
another implementation of a string overlay on top of BigArray, with similar benefits.
Emphasizes speed.
* [ez_subst](https://ocamlpro.github.io/ez_subst/):
Library to perform substitution on strings.
