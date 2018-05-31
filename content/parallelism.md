# Concurrency, Parallelism, and Distributed Systems

Concurrency refers to running multiple computations more-or-less simultaneously, whereas parallelism refers to using multiple cores or OS-level threads to coordinate computation. We now know that the former is relatively safe and easy to reason about, whereas the latter is extremely difficult and causes many subtle bugs. OCaml currently supports concurrency elegantly, but parallelism support is not built in to the runtime.

## Concurrency

* [lwt](https://github.com/ocsigen/lwt) : a monadic concurrency library. Concurrent code uses monads to express the higher-level abstractions of control flow.
* [Async](https://github.com/janestreet/async) : another monadic concurrency library developed by Jane Street. This library is covered in Real World OCaml. While the concept is very similar to lwt, small discrepancies make compatibility between the libraries difficult.
* [RWO-lwt](https://github.com/dkim/rwo-lwt) : Real World OCaml code examples translated from Async to lwt.

### Articles

* [The blog post that introduced Async](https://blog.janestreet.com/announcing-async/)
* [A user gives up on Async](http://rgrinberg.com/posts/abandoning-async/)
* [Cooperative Concurrency in OCaml: A Core.Std.Async Example](http://philtomson.github.io/blog/2014/07/09/core-dot-async-example/) .

## Process Management

* The [standard library] contains the Unix module, which allows for low-level process management. This is fairly brittle due to the fact that it's mostly (but not entirely) tailored towards Unix.
* [lwt]](https://github.com/ocsigen/lwt) has the [lwt_process](https://ocsigen.org/lwt/3.2.1/api/Lwt_process) module, which has cross-platform process manipulation functions.

## Parallelism

As mentioned above, OCaml doesn't natively support multiple OS-level OCaml threads running simultaneously. A global lock prevents multiple OCaml threads from running simultaneously.

* The most hopeful and powerful way to use multicore is with the new [https://github.com/ocamllabs/ocaml-multicore OCaml multicore] branch. This branch uses a parallel garbage collector, which means that OCaml will eventually be able to run on multiple cores in the same process. Note that this branch is not yet ready for real work, but it's rapidly advancing.
* By interfacing with external C code through the FFI, OCaml can pass off long-running computations to C threads running at the same time as the OCaml code. This is made easier nowadays due to CTypes (see [ffi](ffi.md))
* [Parmap](http://rdicosmo.github.io/parmap/)  provides easy-to-use parallel map and fold functions. The library makes use of forking to create short-lived child processes, and memory mapping to feed the data back to the parent process.
* [ForkWork](https://github.com/mlin/forkwork)  is a simple library for forking child processes to perform work on multiple cores.
* [Functory](http://functory.lri.fr/About.html)  is a distributed computing library which facilitates distributed execution of parallelizable computations in a seamless fashion.
* [Ocamlnet](http://projects.camlcity.org/projects/ocamlnet.html)  is an enhanced system platform library. It contains the /netmulticore/ library to compute tasks on as many cores of the machine as needed. This is probably the most advanced implementation currently available, as it is capable of creating a shared memory region, and running a custom-made garbage collector on said region, thus solving the problem of sharing memory with tracing garbage collectors.
* [Nproc](https://github.com/MyLifeLabs/nproc)  is a process pool implementation for OCaml.
* [Parany](https://github.com/UnixJunkie/parany)  is another parallel computation library.
* [Sklml](http://sklml.inria.fr)  is a functional parallel skeleton compiler and programming system for OCaml programs.

### Articles

* [What is the state of OCaml's parallelization abilities?](http://stackoverflow.com/questions/6588500/what-is-the-state-of-ocamls-parallelization-abilities) : Note that this article is quite a bit out-of-date.

## Distributed Computing

* [Rpc.Parallel](https://github.com/janestreet/rpc_parallel)  is a library for spawning processes on a cluster of machines, and passing typed messages between them.
* [MPI](https://github.com/xavierleroy/ocamlmpi)  – Message Passing Interface bindings for OCaml.
* [ocaml-rpc](https://github.com/mirage/ocaml-rpc)  – Light library to deal with RPCs in OCaml.
