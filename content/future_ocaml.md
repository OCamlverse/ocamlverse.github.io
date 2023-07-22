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

Algebraic effects and handlers are a way to model various computational
effects in a composable manner.
They can express assignments, I/O operations, exceptions, iterators,
asynchronous computations, non-deterministic computations, etc.

The experimental support for algebraic effects was introduced in OCaml
5.0.
However, the type system does not provide dedicated functionalities to
track effects.
In other words, algebraic effects in OCaml 5.0 are untyped.
It introduces various problems, and it would be better to have algebraic
effects typed and handled by the type system instead.
By extending OCaml's type system with algebraic effects, it would become
more similar to Haskell's but without the need for monads for effects.

* [Concurrent Programming with Effect Handlers] is an excellent tutorial
  on algebraic effects in OCaml.
* [Experiences with Effects in OCaml] (video) (OCaml 2021) presents case
  studies of applying algebraic effects to Angstrom and Httpaf. The
  proceeding paper is available at
  <https://kcsrk.info/papers/ocaml2021b.pdf>.
* [Effectively Tackling the Awkward Squad] (video) (ML 2017)
  demonstrates practical examples of algebraic effects. The proceeding
  paper is available at
  <https://dhil.net/research/papers/awkward_effects-ml17.pdf>.
* [Eff directly in OCaml] (video) (ML 2016) introduces an implementation
  of typed algebraic effects on OCaml. The proceeding paper is available
  at <https://arxiv.org/abs/1812.11664>.
* [Effects bibliography] is a collaborative bibliography of work
  related to the theory and practice of computational effects.
* [An attempt to implement OCaml with typed algebraic effects]

[Concurrent Programming with Effect Handlers]: https://github.com/ocaml-multicore/ocaml-effects-tutorial
[Experiences with Effects in OCaml]: https://watch.ocaml.org/videos/watch/74ece0a8-380f-4e2a-bef5-c6bb9092be89
[Effectively Tackling the Awkward Squad]: https://www.youtube.com/watch?v=DNp3ifNpgPM
[Eff directly in OCaml]: https://www.youtube.com/watch?v=0dAafhi-IuE
[Effects bibliography]: https://github.com/yallop/effects-bibliography
[An attempt to implement OCaml with typed algebraic effects]: https://github.com/lpw25/ocaml-typed-effects
