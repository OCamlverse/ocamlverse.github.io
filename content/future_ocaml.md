# Future of OCaml

Some interesting news/developments coming up in OCaml's future:

## Ongoing

### Concurrency and Parallelism with OCaml

OCaml 5.0 has integrated Multicore OCaml, which provides building blocks
for concurrent and parallel programming.
It includes algebraic effect handlers that can express computational
effects, including resumable exceptions, delimited continuations, and
asynchronous computations.
Additionally, domains, abstractions of native threads, can run
simultaneously on shared-memory multiprocessor systems.

The OCaml community has taken advantage of these new features by
developing several libraries, and the ecosystem has evolved to gain full
potential from today's hardware.
For more information, visit the
[Concurrency, Parallelism, and Distributed Systems] page.

* [The Journey to OCaml Multicore: Bringing Big Ideas to Life] (2023)
  summarizes the history and challenges of the Multicore OCaml project
  that started in 2013.
* [Retrofitting Concurrency – Lessons from the Engine Room] (video)
  (ICFP 2022) retrospects how OCaml 5.0 has enabled multi-threaded OCaml
  programs without sacrificing the efficiency of existing
  single-threaded programs. The slides are available at
  <https://speakerdeck.com/kayceesrk/retrofitting-concurrency-lessons-from-the-engine-room>.
* [Retrofitting Parallelism onto OCaml] (video) (ICFP 2020) presents
  the garbage collection algorithm in OCaml 5.0. The proceeding paper
  is available at <https://dl.acm.org/doi/10.1145/3408995>.

[Concurrency, Parallelism, and Distributed Systems]: /content/parallelism.html
[The Journey to OCaml Multicore: Bringing Big Ideas to Life]: https://tarides.com/blog/2023-03-02-the-journey-to-ocaml-multicore-bringing-big-ideas-to-life/
[Retrofitting Concurrency – Lessons from the Engine Room]: https://www.youtube.com/watch?v=zJ4G0TKwzVc
[Retrofitting Parallelism onto OCaml]: https://www.youtube.com/watch?v=9ClMPz7QaIs

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
