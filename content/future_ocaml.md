# Future of OCaml

Some interesting developments coming up in OCaml's future:

## Immediate Plans
* [Post on plans for OCaml 4.08](https://blog.janestreet.com/plans-for-ocaml-408/)

## Medium-Term Plans

### Multicore OCaml

Currently, OCaml has a global runtime lock,
with support for green threads (concurrency) via `lwt` and `Async`.
The plan is to allow OCaml to run in parallel (which are termed `domains`),
while also allowing for native green thread support.

See [this post](https://discuss.ocaml.org/t/ocaml-multicore-report-on-a-june-2018-development-meeting-in-paris/2202),
the [multicore ocaml github repo](https://github.com/ocamllabs/ocaml-multicore),
and its associated [wiki](https://github.com/ocamllabs/ocaml-multicore/wiki).

## Long-Term Plans

### Modular Implicits
A type-based dispatch similar to Haskell's typeclasses.
As [this paper](https://arxiv.org/pdf/1512.01895.pdf) clarifies, creating typeclasses in OCaml is harder due to the way
it preserves type abstraction.
Put simply, you can have functors or type classes, but not both, and OCaml already has functors.
While the community eagerly awaits this solution, its implementation appears to be years away.
To see how complicated the solution is, see [this response](https://discuss.ocaml.org/t/modular-implicits/144/18).
You can follow some of the work that is taking place [here](https://github.com/lpw25/implicits-module-system).
