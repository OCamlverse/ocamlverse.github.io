---
layout: page
tags: [ecosystem]
---

# Monads

Monads in OCaml are generally used in a slightly different way than in other languages.
Rather than using `>>=` for monadic binds, values are generally bound using a ppx
with a syntax such as `let%bind x = ...`.

Additionally, as of OCaml 4.08, the langauge itself contains syntax for calling
monadic functions.
See [this blog post](https://jobjo.github.io/2019/04/24/ocaml-has-some-new-shiny-syntax.html)
and the [OCaml manual on this](https://caml.inria.fr/pub/docs/manual-ocaml-4.08/manual046.html).

## Monadic Synax Extensions

* [ppx_monad](https://github.com/rizo/ppx_monad):
Monadic syntax extension.
* [ppx_let](https://github.com/janestreet/ppx_let):
A monadic syntax extension from Jane Street.
* [ocaml-monadic](https://github.com/zepalmer/ocaml-monadic):
Another monadic syntax extension.

## Classic Monads

* [BAP Monads](http://binaryanalysisplatform.github.io/bap/api/master/Monads.Std.html):
BAP (Binary Analysis Platform) has an independent and comprehensive monad library.
Rather than using a `ppx`, BAP makes use of Functors to create expressive monad hierarchies.
