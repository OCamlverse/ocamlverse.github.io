# Future of OCaml

Some interesting developments coming up in OCaml's future:

## Immediate Plans
* [Post on plans for OCaml 4.08](https://blog.janestreet.com/plans-for-ocaml-408/)

## Medium-Term Plans

### Multicore OCaml

Currently, OCaml has a global runtime lock,
with support for green threads (concurrency) via `lwt` and `Async`.
The plan is to allow OCaml to run in parallel (which are termed `domains`),
while also allowing for native green thread support via algebraic effects.

See [this post](https://discuss.ocaml.org/t/ocaml-multicore-report-on-a-june-2018-development-meeting-in-paris/2202),
the [multicore ocaml github repo](https://github.com/ocamllabs/ocaml-multicore),
and its associated [wiki](https://github.com/ocamllabs/ocaml-multicore/wiki).
You can also look for things to help with on the [roadmap](https://github.com/ocaml-multicore/ocaml-multicore/projects/3).

A great explanation of algebraic effects can be found [here](https://github.com/ocamllabs/ocaml-effects-tutorial).

### Typed Algebraic Effects

Part of the plan for multicore OCaml is to include non-monadic green threading into the runtime.
In order to allow for this, algebraic effects are being added to the language.
These are similar to exceptions but with a bookmark to the current position of the execution
(aka continutation) added to each "exception" (aka effect) thrown,
so one has the option to continue execution after handling the effect.

Initially, this was going to exist outside of the type system.
However, this introduces many issues, and we'd much rather have it be typed and handled by the
type system.
Extending OCaml's type system with algebraic effects would make it similar to Haskell's,
but without requiring monads for effects.

See the tutorial above for an introduction to (untyped) algebraic effects.
Work on typed effects is ongoing [here](https://github.com/lpw25/ocaml-typed-effects).

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
