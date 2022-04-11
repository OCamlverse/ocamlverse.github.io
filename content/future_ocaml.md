# Future of OCaml

Some interesting news/developments coming up in OCaml's future:

## Medium-Term Plans

### Flambda 2.0

Flambda is the framework that currently optionally optimizes OCaml code.
Work is ongoing to create the next version at OCamlPro.
See [this post](https://www.ocamlpro.com/2019/08/30/ocamlpros-compiler-team-work-update/)
and [this development branch](https://github.com/mshinwell/ocaml/tree/flambda2.0).

### OCaml 5.0

Currently, OCaml has a global runtime lock,
with support for green threads (concurrency) via `lwt` and `Async`.
The plan is to allow OCaml to run in parallel threads (which are termed `domains`),
while also allowing for native green thread support via algebraic effects.

* [Multicore: what's coming in 2021 presentation](https://speakerdeck.com/kayceesrk/multicore-ocaml-whats-coming-in-2021)
* [Monthly updates](https://discuss.ocaml.org/tag/multicore-monthly)
* [Paper on retrofitting a parallel GC into OCaml](https://arxiv.org/abs/2004.11663)
* The [multicore OCaml github repo](https://github.com/ocamllabs/ocaml-multicore) and its [wiki](https://github.com/ocamllabs/ocaml-multicore/wiki).
* The [multicore roadmap](https://github.com/ocaml-multicore/ocaml-multicore/projects/3).
* [ICFP Presentation on advanced lock-free programming in multicore OCaml](https://www.youtube.com/watch?v=C0YkrerSNn0)
* [Discuss post on recent past and future of integrating multicore](https://discuss.ocaml.org/t/multicore-prerequisite-patches-appearing-in-released-ocaml-compilers-now/4408)
* [Update on status of multicore](https://discuss.ocaml.org/t/where-is-multicore-development-happening/4997/8)
* [Adjusting the stdlib for multicore](https://github.com/ocaml-multicore/ocaml-multicore/wiki/Safety-of-Stdlib-under-Multicore-OCaml)

### Typed Algebraic Effects

Part of the plan for multicore OCaml is to include non-monadic green threading into the runtime.
In order to allow for this, algebraic effects are being added to the language.
These are similar to exceptions but with a bookmark to the current position of the execution
(aka continuation) added to each "exception" (aka effect) thrown,
so one has the option to continue execution after handling the effect.

Initially, this was going to exist outside of the type system.
However, this introduces many issues, and we'd much rather have it be typed and handled by the
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
