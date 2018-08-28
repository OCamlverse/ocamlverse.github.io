---
tags: [learning, best practices]
---
# Optimizing OCaml Performance

OCaml benefits from having a very lean runtime representation for a GC-based language.
Other languages that use a tracing GC generally need to allocate a lot more memory to do the same operations.
This often results in a serious speed boost, since modern architectures are dominated by caching.
However, this in itself is not always enough:

* Functional code writing patterns tend to allocate a lot of memory, which is expensive.
* Functional data structures are tree-based and immutable, and in most cases mutable data
structures are faster, but not fully compatible with functional paradigms.
* OCaml's default data format is good for certain cases such as symbolic computation,
but the fact that floats, for example, are allocated on the heap, means that some programs will be slower
than in other languages.

Due to these reasons, it's good to know how to optimize OCaml for performance when you need it.

## Tools

* [Flambda](https://caml.inria.fr/pub/docs/manual-ocaml/flambda.html)
is OCaml's built-in optimizer.
By default, OCaml will compile without Flambda since it takes longer to do so.
Compiling without Flambda is recommended when running code that isn't performance-sensitive.
To switch to a compiler with flambda, use opam's `opam switch X.YY+flambda` command,
where `X.YY` refers to a compiler version.
Flambda will try to inline and then optimize code where possible.
* [Spacetime](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Spacetime.html)
is an allocation profiler included with OCaml.
Since memory dominates performance nowadays, Spacetime can tell you where your program allocates
memory so that you can try and reduce memory usage, and thus increase speed.
* [perf](https://en.wikipedia.org/wiki/Perf_(Linux))
is a Linux performance tool that works with OCaml.
* Flame graph tools like [speedscope](https://github.com/jlfwong/speedscope) give a great view of
where your program spends its time.
Very useful for optimization.

## Writing Efficient Code

* Use [iterators](iterators.md) instead of allocating data structures where possible.
Every standard library now has them, and they reduce the weight of functional data structure allocations.
* [asm-ocaml](https://www.ocamlpro.com/2016/04/01/asm-ocaml/): A tongue-in-cheek approach to heavily optimizing OCaml.
Note the date of the post: for our American friends, remember that European dates reverse the month and day :)
The post starts with the extreme premise of trying to remove all allocation and proceeding from there.
We don't recommend following this advice, but it's useful for understanding how to write efficient code without Flambda.
* [GADTs and performance](https://blog.janestreet.com/why-gadts-matter-for-performance/)
* [How OCaml exceptions are implemented](https://stackoverflow.com/questions/8564025/ocaml-internals-exceptions):
Good to know to work efficiently with exceptions.
