# Future of OCaml

Some interesting news/developments coming up in OCaml's future:

## Medium-Term Plans

### Flambda 2.0

Flambda is the framework that currently optionally optimizes OCaml code.
Work is ongoing to create the next version at OCamlPro.
See [this post](https://www.ocamlpro.com/2019/08/30/ocamlpros-compiler-team-work-update/)
and [the Flambda backend development tree](https://github.com/ocaml-flambda/flambda-backend).

### WebAssembly

WebAssembly, or Wasm, is a portable binary instruction format that can
be used with any programming language. It runs in a secure environment
embedded within web browsers.

Porting OCaml to Wasm has excellent potential.
While we already have OCaml to JavaScript compilers, the compiled code
is more or less inefficient as JavaScript is not designed as a
low-level target language.
Wasm will fill the gap and lead to high-performance client-side web
applications written in OCaml.

* [OCaml to Wasm - an overview] is a collection of materials on
  compiling OCaml to Wasm.
* [A world to win: WebAssembly for the rest of us] (video) (BOB 2023)
  explains the difficulties of compiling programming languages with
  garbage collection to Wasm and upcoming features to address them.
  While the presentation talks about Scheme, most points also apply to
  OCaml. The transcript is available at
  <https://wingolog.org/archives/2023/03/20/a-world-to-win-webassembly-for-the-rest-of-us>.
* [WebAssembly/Wasm and OCaml] (2022) introduces OCamlPro's activities
  on Wasm.

[OCaml to Wasm - an overview]: https://github.com/sabine/ocaml-to-wasm-overview
[A world to win: WebAssembly for the rest of us]: https://media.ccc.de/v/bob2023-web-assembly-for-the-rest-of-us-wingo
[WebAssembly/Wasm and OCaml]: https://ocamlpro.com/blog/2022_12_14_wasm_and_ocaml/

## Long-Term Plans

### Modular Implicits

A type-based dispatch similar to Haskell's typeclasses.

See a video demonstration [here](https://www.youtube.com/watch?v=3wVUXTd4WNc).
As [this paper](https://arxiv.org/pdf/1512.01895.pdf) clarifies,
creating typeclasses in OCaml is difficult due to its adherence to
type abstraction.
Put simply, you can have functors or type classes, but not both, and OCaml already has functors.
While the community eagerly awaits this solution, its implementation unfortunately appears to be years away.

To see how complicated the solution is, see [this response](https://discuss.ocaml.org/t/modular-implicits/144/18).
You can follow some of the work that is taking place [here](https://github.com/lpw25/implicits-module-system)
and [here](https://github.com/ocamllabs/ocaml-modular-implicits).

### Typed Algebraic Effects

OCaml 5.0 introduces algebraic effects.
They are similar to exceptions but with a bookmark to the current position of the execution
(aka continuation) added to each "exception" (aka effect) thrown,
so one has the option to continue execution after handling the effect.

Algebraic effects introduced in OCaml 5.0 are untyped,
i.e. they exist outside of the type system.
However, it introduces many issues, and we'd much rather have it be typed and handled by the
type system.
Extending OCaml's type system with algebraic effects would make it similar to Haskell's,
but without requiring monads for effects.

See the tutorial above for an introduction to (untyped) algebraic effects.
Work on typed effects is ongoing [here](https://github.com/lpw25/ocaml-typed-effects).

* A great explanation of algebraic effects can be found [here](https://github.com/ocamllabs/ocaml-effects-tutorial).
* [Presentation on effects in OCaml 21](https://watch.ocaml.org/videos/watch/74ece0a8-380f-4e2a-bef5-c6bb9092be89)
* [Presentation on algebraic effects at ICFP](https://www.youtube.com/watch?v=DNp3ifNpgPM)
* [Presentation on typed effects in OCaml](https://www.youtube.com/watch?v=0dAafhi-IuE)
* [Complete bibilography of literature on effects](https://github.com/yallop/effects-bibliography)
