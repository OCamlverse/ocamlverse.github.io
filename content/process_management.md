# Process Management and Shell Scripting

* The standard library contains the [Unix](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Unix.html) module,
which allows for low-level process management.
This is fairly brittle due to the fact that it's mostly (but not entirely) tailored towards Unix.
* [shexp](https://github.com/janestreet/shexp):
A library for type-safe command line programming.
This includes process manipulation and piping.
In fact, this is one of the few libraries that supports piping properly.
* [feather](https://github.com/charlesetc/feather):
Lightweight shell scripting and process management.
[docs](https://github.com/charlesetc/feather/blob/master/README.md).
* [lwt](https://github.com/ocsigen/lwt) has the 
[lwt_process](https://ocsigen.org/lwt/3.2.1/api/Lwt_process) module,
which has cross-platform process manipulation functions.
