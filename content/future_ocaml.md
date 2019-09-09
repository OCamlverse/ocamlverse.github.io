# Future of OCaml

Some interesting news/developments coming up in OCaml's future:

## Recently Introduced

* [Post on plans for OCaml 4.08](https://blog.janestreet.com/plans-for-ocaml-408/):
Pre-4.08 blog post.
* [A Look at OCaml 4.08](https://blog.janestreet.com/a-look-at-ocaml-4.08/):
Looking at what 4.08 included.

## Interesting Pull Requests

* [Array data types](https://github.com/ocaml/ocaml/pull/616):
Right now, OCaml has multiple array types (string, float array, array) that are treated differently.
This PR is an attempt to combine these into one type, while allowing for future optimization.

## Medium-Term Plans

### Flambda 2.0

Flambda is the framework that currently optionally optimizes OCaml code.
Work is ongoing to create the next version at OCamlPro.
See [this post](https://www.ocamlpro.com/2019/08/30/ocamlpros-compiler-team-work-update/)
and [this development branch](https://github.com/mshinwell/ocaml/tree/flambda2.0).

### Multicore OCaml

Currently, OCaml has a global runtime lock,
with support for green threads (concurrency) via `lwt` and `Async`.
The plan is to allow OCaml to run in parallel (which are termed `domains`),
while also allowing for native green thread support via algebraic effects.

See [this post](https://discuss.ocaml.org/t/ocaml-multicore-report-on-a-june-2018-development-meeting-in-paris/2202),
the [multicore ocaml github repo](https://github.com/ocamllabs/ocaml-multicore),
and its associated [wiki](https://github.com/ocamllabs/ocaml-multicore/wiki).
You can also look for things to help with on the [roadmap](https://github.com/ocaml-multicore/ocaml-multicore/projects/3).

* [ICFP Presentation on advanced lock-free programming in multicore OCaml](https://www.youtube.com/watch?v=C0YkrerSNn0)


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

* A great explanation of algebraic effects can be found [here](https://github.com/ocamllabs/ocaml-effects-tutorial).
* [Presentation on algebraic effects at ICFP](https://www.youtube.com/watch?v=DNp3ifNpgPM)
* [Presentation on typed effects in OCaml](https://www.youtube.com/watch?v=0dAafhi-IuE)

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
