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
    * [RWO-lwt](https://github.com/dkim/rwo-lwt):
    Real World OCaml code examples translated from Async to lwt.
    * [lwt tutorial](https://raphael-proust.github.io/code/lwt-part-1.html)
    [part 2](https://raphael-proust.github.io/code/lwt-part-2.html)
    [part 3](https://raphael-proust.github.io/code/lwt-part-3.html)
* [Async](https://github.com/janestreet/async):
another monadic concurrency library developed by Jane Street.
This library is covered in Real World OCaml.
While the concept is very similar to lwt,
small discrepancies make compatibility between the libraries difficult.
* [LUV](https://github.com/aantron/luv):
Bindings to [libuv](https://github.com/libuv/libuv),
an event loop-based system that runs `node.io`.
This is also a replacement for the `Unix` module,
allowing for full process control in a system-independent manner.

### Articles

* [The blog post that introduced Async](https://blog.janestreet.com/announcing-async/)
* [A user gives up on Async](http://rgrinberg.com/posts/abandoning-async/)
* [Cooperative Concurrency in OCaml][cooperative concurrency]: Using Async

[cooperative concurrency]: http://philtomson.github.io/blog/2014/07/09/core-dot-async-example/

## Parallelism

As mentioned above, OCaml currently doesn't natively support multiple OS-level OCaml
threads running simultaneously.
A global lock prevents multiple OCaml threads from running simultaneously.

Since we currently don't have thread-level parallelism, process-level is used instead.

* [Parmap](http://rdicosmo.github.io/parmap/):
Provides easy-to-use parallel map and fold functions.
The library makes use of forking to create short-lived child processes,
and memory mapping to feed the data back to the parent process.
* [Parany](https://github.com/UnixJunkie/parany):
Generalized map reduce for multicore computers (unfold, map in parallel, fold).
Parany can process in parallel an "infinite" stream of elements (too big to fit in memory).
Any Parmap functionality can be reimplemented using parany.
* [hack-parallel](https://github.com/rvantonder/hack-parallel/):
Parallel processing library using shared memory. Used by Facebook's Hack.
* [lwt-parallel](https://github.com/ivg/parallel):
Lower level mechanism to create child processes in lwt and have it communicate with the parent via socket.
* [ForkWork](https://github.com/mlin/forkwork):
Similar to Parmap above.
* By interfacing with external C code through the FFI,
OCaml can pass off long-running computations to C threads running at the
same time as OCaml code.
This is made easier nowadays due to CTypes (see [ffi](ffi.md))
* [Nproc](https://github.com/MyLifeLabs/nproc):
A process pool implementation for OCaml using lwt.
Rather than creating or forking processes as needed, preallocates them
and sends them units of work as required.
* [Ocamlnet](http://projects.camlcity.org/projects/ocamlnet.html):
An enhanced system platform library.
It contains the **netmulticore** library to compute tasks on as many cores of the machine as needed.
This is the most powerful implementation of parellelism currently available for OCaml,
as it is capable of creating a shared memory region,
and running a *custom-made garbage collector* on said region.
* [Sklml](http://sklml.inria.fr):
A functional parallel skeleton compiler and programming system for OCaml programs.

### Multicore OCaml 5.0

The most promising and powerful way to use multicore is with the new
[multicore](https://github.com/ocamllabs/ocaml-multicore) branch,
has recently been incorporated into OCaml 5.0.
OCaml 5.0 will use a parallel garbage collector,
which means that it will eventually be able to run on multiple cores in the same process.
Note that this branch is not yet ready for real work, but it's rapidly advancing.
For more information, consult the [Multicore Wiki](https://github.com/ocamllabs/ocaml-multicore/wiki).

* [Parallel Programming in Multicore OCaml](https://github.com/ocaml-multicore/parallel-programming-in-multicore-ocaml):
great article on using the Multicore OCaml branch.

### Distributed Computing

Distributed computing is similar to process-based parallelism, except that the child
processes may or may not be on remote machines.
Therefore, distributed computing libraries generally also perform parallelism on the same machine as well.

* [Rpc.Parallel](https://github.com/janestreet/rpc_parallel):
a library for spawning processes on a cluster of machines, and passing typed messages between them.
* [Functory](http://functory.lri.fr/About.html):
a distributed computing library which facilitates distributed execution of
parallelizable computations in a seamless fashion.
* [MPI](https://github.com/xavierleroy/ocamlmpi):
message Passing Interface bindings for OCaml.
* [ocaml-rpc](https://github.com/mirage/ocaml-rpc):
light library to deal with RPCs in OCaml.
* [distributed](https://github.com/essdotteedot/distributed):
Library for distributed computation in OCaml.
Similar to Erlang's model and inspired by Cloud Haskell.
* [reactor](https://github.com/ostera/reactor) (alpha):
Actor model for OCaml, similar to Erlang Elixir.
