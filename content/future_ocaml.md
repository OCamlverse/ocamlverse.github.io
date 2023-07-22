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

### Certifiable OCaml Type Inference

OCaml's type checker is complex and fragile, as noted in
`ocaml/typing/TODO.md` in the compiler codebase.
While refactoring the type checker for lower maintenance costs is a
priority, it is tough for less experienced developers to participate.
The type system has many features, so the underlying algorithm is hard
to comprehend.
Additionally, the implementation could be better structured.

The Certifiable OCaml Type Inference (COCTI) project aims to develop the
foundation for a "robust, modular, and verifiable" type system
implementation for OCaml.
In addition to the cleanup and refactoring of the existing code base,
COCTI develops a compiler backend targeting Gallina, Coq's programming
language, and proofs of soundness of the type system, among others.

Most code on COCTI is available at <https://github.com/COCTI/ocaml>.

* [Validating OCaml soundness by translation into Coq] (TYPES 2022)
  introduces [Coqgen], "a backend for OCaml that generates well-typed
  and executable Coq code".
  The slides are available at
  <https://types22.inria.fr/files/2022/06/TYPES_2022_slides_15.pdf>.
* [Interpreting OCaml GADTs into Coq] (video) (ML 2022) shows how to
  map GADTs in OCaml to Coq and open problems toward translating them
  automatically.
  The proceeding paper is available at
  <https://www.math.nagoya-u.ac.jp/~garrigue/papers/ml2022.pdf>.
  The slides are available at
  <https://www.math.nagoya-u.ac.jp/~garrigue/papers/coqgen-slides-ml2022.pdf>.

[Validating OCaml soundness by translation into Coq]: https://types22.inria.fr/files/2022/06/TYPES_2022_paper_15.pdf
[Coqgen]: https://www.math.nagoya-u.ac.jp/~garrigue/cocti/coqgen/
[Interpreting OCaml GADTs into Coq]: https://www.youtube.com/watch?v=8VPygk6NHB8
