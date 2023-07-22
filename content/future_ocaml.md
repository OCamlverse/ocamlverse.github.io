# Future of OCaml

Some interesting news/developments coming up in OCaml's future:

## Medium-Term Plans

### Flambda 2.0

Flambda is the framework that currently optionally optimizes OCaml code.
Work is ongoing to create the next version at OCamlPro.
See [this post](https://www.ocamlpro.com/2019/08/30/ocamlpros-compiler-team-work-update/)
and [the Flambda backend development tree](https://github.com/ocaml-flambda/flambda-backend).

## Long-Term Plans

### Modular Implicits

Haskell's type classes, Scala's implicits, and Rust's traits are
solutions to the expression problem, a well-known problem of programming
language design formulated by Philip Wadler in 1998.
Modular implicits were introduced as OCaml's solution to the expression
problem in 2014.

As clarified in [the original paper on modular implicits], adding type
classes to OCaml is difficult due to its adherence to type abstraction.
In short, you can have functors or type classes, but not both, and
OCaml already has functors.
While the community eagerly awaits this solution, its implementation,
unfortunately, appears to be years away.

* [Modular implicits] (video) (ML/OCaml 2014) demonstrates how modular
  implicits would interact with the rest of OCaml's type system. The
  proceeding paper is available at <https://arxiv.org/abs/1512.01895>.
* [Leo White's response on implementing modular implicits]
* Attempts to implement modular implicits:
  * <https://github.com/lpw25/implicits-module-system>
  * <https://github.com/ocamllabs/ocaml-modular-implicits>

[the original paper of modular implicits]: https://arxiv.org/abs/1512.01895
[Modular implicits]: https://www.youtube.com/watch?v=3wVUXTd4WNc
[Leo White's response on implementing modular implicits]: https://discuss.ocaml.org/t/modular-implicits/144/18

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
