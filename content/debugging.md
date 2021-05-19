---
tags: [ecosystem]
---

# Debugging
* OCaml comes with a built-in debugger for the bytecode compiler.
You invoke it with the `ocamldebug` command.
See [the manual](https://caml.inria.fr/pub/docs/manual-ocaml/debugger.html) for more details.
* The easiest way to debug OCaml code, other than inserting print statements,
is choosing bytecode as your compilation target, and using teh OCaml debugger.
* Additionally, one can use `gdb` to debug native code.
* [ocamlearlybird](https://github.com/hackwaly/ocamlearlybird):
[Debug Adapter Protocol](https://microsoft.github.io/debug-adapter-protocol/)
implementation for OCaml.
Allows integrating the OCaml debugger with an IDE.
* [ocaml-dap](https://github.com/hackwaly/ocaml-dap):
Generic [Debug Adapter Protocol](https://microsoft.github.io/debug-adapter-protocol/)
implementation in OCaml.

## Profiling
* [ocaml-tracy](https://github.com/AestheticIntegration/ocaml-tracy):
Bindings to the amazing [tracy](https://github.com/wolfpld/tracy) profiler.
