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
