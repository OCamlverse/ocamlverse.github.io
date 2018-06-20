---
tags: [learning, best practices]
---
# Optimizing OCaml Performance

## Writing Efficient Code
* [asm-ocaml](https://www.ocamlpro.com/2016/04/01/asm-ocaml/): A tongue-in-cheek approach to heavily optimizing OCaml.
Note the date of the post: for our American friends, remember that European dates reverse the month and day :)
The post starts with the extreme premise of trying to remove all allocation and proceeding from there.
We don't recommend following this advice, but it's useful for understanding how to write efficient code without Flambda.
* [GADTs and performance](https://blog.janestreet.com/why-gadts-matter-for-performance/)
* [Jane Street on performant OCaml](https://janestreet.github.io/ocaml-perf-notes.html)

## Exception Efficiency
* [How OCaml exceptions are implemented](https://stackoverflow.com/questions/8564025/ocaml-internals-exceptions)
