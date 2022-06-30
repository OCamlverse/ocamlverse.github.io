# Profiling

* [SpaceTime](https://v2.ocaml.org/releases/4.07/htmlman/spacetime.html)
is integrated into the compiler and allows profiling of memory allocation. (Removed since [4.12.0](https://ocaml.org/releases/4.12.0))
  * [ICFP Presentation: Profiling Memory](https://www.youtube.com/watch?v=wX4m8yqbuqE)
* [landmarks](https://github.com/LexiFi/landmarks): a profiling library for OCaml,
taking into account both
memory allocation and CPU time.
* Standard tools such as [gprof](https://sourceware.org/binutils/docs/gprof/)
can also be used to debug OCaml programs.
* [ocaml-tracy](https://github.com/AestheticIntegration/ocaml-tracy):
Bindings to the amazing [tracy](https://github.com/wolfpld/tracy) profiler.
* [gdbprofiler](https://github.com/copy/gdbprofiler):
Profile OCaml programs by connecting to `gdb`. Very impressive output.
