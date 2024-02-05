---
tags: [ecosystem]
---

# Concurrency, Parallelism, and Distributed Systems

Concurrency refers to running multiple computations and switching from one to the other rapidly (green threads),
whereas parallelism refers to using multiple OS-level threads to coordinate computation.
Since OCaml 5.0, OCaml supports concurrency with the Effect system and parallelism with Domains.

## Concurrency

* [eio](https://github.com/ocaml-multicore/eio):
A concurrency library using the OCaml effect system.
Unlike the other concurrency libraries, `eio` doesn't require the usage of monads.
This makes it easier to code using 'plain` OCaml code.
    * [video presentation](https://watch.ocaml.org/w/02a7accc-2a2c-44d5-889e-d75e1489946e) on `eio`. 
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
* [Riot](https://github.com/leostera/riot):
Riot is an in-development library to support actor-based processing (similar to Erlang)
on OCaml 5.0.
* [LUV](https://github.com/aantron/luv):
Bindings to [libuv](https://github.com/libuv/libuv),
an event loop-based system that runs `node.io`.
This is also a replacement for the `Unix` module,
allowing for full process control in a system-independent manner.
* [miou](https://github.com/robur-coop/miou)
Miou is a simple scheduler (in beta) for OCaml 5 to run concurrent and/or parallel tasks.

### Articles

* [The blog post that introduced Async](https://blog.janestreet.com/announcing-async/)
* [A user gives up on Async](http://rgrinberg.com/posts/abandoning-async/)
* [Cooperative Concurrency in OCaml][cooperative concurrency]: Using Async
* [The core of Miou](https://blog.osau.re/articles/miou.html) & [Rules of Miou](https://blog.osau.re/articles/miou_rules.html)

[cooperative concurrency]: https://philtomson.github.io/blog/2014-07-09-cooperative-concurrency-in-ocaml-a-core.std.async-example/

## Parallelism

### Domain (thread)-based Parallelism

OCaml 5.0 introduced `domains`, which roughly map to the number of cores in a CPU.
They allow for true parallelism in OCaml.

* [Parallel Programming in Multicore OCaml](https://github.com/ocaml-multicore/parallel-programming-in-multicore-ocaml):
great article on using the OCaml's multicore capabilities.
* [kCAS](https://github.com/ocaml-multicore/kcas): Software-Transactional Memory (STM) in OCaml.
STM allows for programming across threads (domains) via lockless data structures and interfaces that make the difficult work
of parallelism easier for average programmers.
* [MoonPool](https://github.com/c-cube/moonpool):
Thread pools with work-stealing for domains.

### Process-Level Parallelism

Pre-5.0, OCaml supported parallelism only by running multiple processes.
This option still exists and is supported by many libraries.

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

## Distributed Computing

Distributed computing is similar to process-based parallelism, except that the child
processes may or may not be on remote machines.
Therefore, distributed computing libraries generally also perform parallelism on the same machine as well.

* [Rpc.Parallel](https://github.com/janestreet/rpc_parallel):
a library for spawning processes on a cluster of machines, and passing typed messages between them.
* [zmq](https://github.com/issuu/ocaml-zmq): ZeroMQ
an open-source universal messaging library.
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
