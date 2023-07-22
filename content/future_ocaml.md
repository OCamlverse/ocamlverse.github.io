# Future of OCaml

Some interesting news/developments coming up in OCaml's future:

## Medium-Term Plans

### Flambda2

Flambda is an optimization framework introduced in OCaml 4.03.
It allows for conveniently inlining small code snippets, resulting in a
faster binary.
However, the trade-off is a longer compilation time.
It should be noted that Flambda is currently an opt-in feature of the
compiler.

Flambda2 is the successor to Flambda and is currently being developed at
<https://github.com/ocaml-flambda/flambda-backend>.

* Read the [Optimization with Flambda] chapter in the OCaml manual for
  the details of Flambda.
* The progress of Flambda2 development is reported in
  [OCamlPro's compiler team work update] (2019).
* [A better inliner for OCaml, and why it matters] (2016) offers an
  insightful introduction to Flambda.
* [Optimizations you shouldn't do] (2013) shows how the OCaml compiler's
  classic inliner works.

[Optimization with Flambda]: https://v2.ocaml.org/manual/flambda.html
[OCamlPro's compiler team work update]: https://ocamlpro.com/blog/2019_08_30_ocamlpros_compiler_team_work_update/
[A better inliner for OCaml, and why it matters]: https://blog.janestreet.com/flambda/
[Optimizations you shouldn't do]: https://ocamlpro.com/blog/2013_05_24_optimisations_you_shouldnt_do/

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
