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

## Notable Ideas

### Modes

OCaml's generational garbage collector efficiently handles short-lived
small values OCaml programs often produce.
While it works well, one can improve the performance even more if such
ephemeral values are allocated to a stack, like local variables in C.

However, we must ensure that stack-allocated values are not referenced
from heap-allocated long-lived values to prevent use-after-free bugs.
A similar problem is also in values shared between multiple threads.
Rust's type system has the concept of lifetime and ownership to manage
such values safely at the cost of complexity.

Modes provide a proper subset of Rust's lifetime and ownership separate
from the type system.
A prototype of modes-enabled OCaml is being developed at
<https://github.com/ocaml-flambda/ocaml-jst>.

* The "Oxidizing OCaml" series (2023) on Jane Street Tech Blog:
  * [Part 1: Locality] introduces a limited form of lifetime named
    locality mode.
  * [Part 2: Rust-style Ownership] shows how ownership in Rust can be
    expressed with modes.
* [Stack allocation for OCaml] (video) (OCaml 2022) is a clear and
  concise introduction to modes. The slides are available at
  <https://stedolan.net/talks/ocaml22/>.

[Part 1: Locality]: https://blog.janestreet.com/oxidizing-ocaml-locality/
[Part 2: Rust-style Ownership]: https://blog.janestreet.com/oxidizing-ocaml-ownership/
[Stack allocation for OCaml]: https://watch.ocaml.org/w/6c86b050-334b-4a11-bb04-c347a6e57215
