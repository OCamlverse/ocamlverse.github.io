---
tags: [ecosystem]
---

# Concurrency, Parallelism, and Distributed Systems

Concurrency refers to running multiple computations more-or-less simultaneously,
whereas parallelism refers to using multiple cores or OS-level threads to coordinate computation.
We now know that the former is relatively safe and easy to reason about,
whereas the latter is extremely difficult and causes many subtle bugs.
OCaml currently supports concurrency elegantly,
but parallelism support is not built in to the runtime.

## Concurrency

* [lwt](https://github.com/ocsigen/lwt): a monadic concurrency library.
Concurrent code uses monads to express the higher-level abstractions of control flow.
    * [lwt-pipe](https://github.com/c-cube/lwt-pipe):
    Stream/queue for lwt.
* [Async](https://github.com/janestreet/async):
another monadic concurrency library developed by Jane Street.
This library is covered in Real World OCaml.
While the concept is very similar to lwt,
small discrepancies make compatibility between the libraries difficult.
* [RWO-lwt](https://github.com/dkim/rwo-lwt):
Real World OCaml code examples translated from Async to lwt.

### Articles

* [The blog post that introduced Async](https://blog.janestreet.com/announcing-async/)
* [A user gives up on Async](http://rgrinberg.com/posts/abandoning-async/)
* [Cooperative Concurrency in OCaml][cooperative concurrency]: Using Async

[cooperative concurrency]: http://philtomson.github.io/blog/2014/07/09/core-dot-async-example/


## Process Management

* The standard library contains the [Unix](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Unix.html) module,
which allows for low-level process management.
This is fairly brittle due to the fact that it's mostly (but not entirely) tailored towards Unix.
* [lwt](https://github.com/ocsigen/lwt) has the 
[lwt_process](https://ocsigen.org/lwt/dev/api/Lwt_process) module,
which has cross-platform process manipulation functions.

## Parallelism

As mentioned above, OCaml currently doesn't natively support multiple OS-level OCaml
threads running simultaneously.
A global lock prevents multiple OCaml threads from running simultaneously.

* The most promising and powerful way to use multicore is with the new 
[multicore](https://github.com/ocamllabs/ocaml-multicore) branch.
This branch uses a parallel garbage collector,
which means that OCaml will eventually be able to run on multiple cores in the same process.
Note that this branch is not yet ready for real work, but it's rapidly advancing.
For more information, consult the [Multicore Wiki](https://github.com/ocamllabs/ocaml-multicore/wiki).
* By interfacing with external C code through the FFI,
OCaml can pass off long-running computations to C threads running at the
same time as OCaml code.
This is made easier nowadays due to CTypes (see [ffi](ffi.md))
* [Parmap](http://rdicosmo.github.io/parmap/): provides easy-to-use parallel map and fold functions.
The library makes use of forking to create short-lived child processes,
and memory mapping to feed the data back to the parent process.
* [parallel](https://github.com/ivg/parallel):
Distributed computing with lwt support.
* [ForkWork](https://github.com/mlin/forkwork): a simple library for forking child processes
to perform work on multiple cores.
* [Functory](http://functory.lri.fr/About.html):
a distributed computing library which facilitates distributed execution of
parallelizable computations in a seamless fashion.
* [Ocamlnet](http://projects.camlcity.org/projects/ocamlnet.html): an enhanced system platform library.
It contains the /netmulticore/ library to compute tasks on as many cores of the machine as needed.
This is probably the most sophisticated implementation currently available,
as it is capable of creating a shared memory region,
and running a custom-made garbage collector on said region,
thus solving the problem of sharing memory with tracing garbage collectors.
* [Nproc](https://github.com/MyLifeLabs/nproc): a process pool implementation for OCaml.
* [Parany](https://github.com/UnixJunkie/parany): another parallel computation library.
* [Sklml](http://sklml.inria.fr):
a functional parallel skeleton compiler and programming system for OCaml programs.

## Distributed Computing

* [Rpc.Parallel](https://github.com/janestreet/rpc_parallel):
a library for spawning processes on a cluster of machines, and passing typed messages between them.
* [MPI](https://github.com/xavierleroy/ocamlmpi): message Passing Interface bindings for OCaml.
* [ocaml-rpc](https://github.com/mirage/ocaml-rpc): light library to deal with RPCs in OCaml.
* [distributed](https://github.com/essdotteedot/distributed):
Library for distributed computation in OCaml.
Similar to Erlang's model and inspired by Cloud Haskell.
