---
tags: [ecosystem]
---

# Foreign Function Interface

Interop with C/C++ is the most natural option for OCaml, since the runtime is partially written in C.

## Miscellaneous

* [optint](https://github.com/mirage/optint):
OCaml's built-in `int` is 63-bits on 64-bit platforms and 31-bits on 32-bit platforms.
`optint` allows 64-bit platforms to use the native `int` type for 32-bit values,
while boxing on those platforms that need it (32-bit).
This is extremely useful for high-performance interop with other languages, network protocols etc.

## C FFI

* [ctypes](https://github.com/ocamllabs/ocaml-ctypes): Modern library for binding to C libraries using pure OCaml.
You should always try to bind to C code using ctypes before trying the older method.
* [ppx_cstubs](https://github.com/fdopen/ppx_cstubs):
Possibly the easiest solution for FFI with C, allowing you to place C code in your OCaml files.
Everything else is taken care of for you.
* [cstruct](https://github.com/mirage/ocaml-cstruct): Library to access C-style structures from OCaml.
It comes with a ppx preprocessor and variants for lwt and async.
* The older way of binding to C code is to create stubs in C which call functions in the OCaml runtime.
This method is error prone, and you're advised to stay away from it unless it's absolutely necessary.
* [ocaml-main-program-in-c](https://github.com/johnwhitington/ocaml-main-program-in-c) – Example build system for making mixed C/Ocaml binaries where the main program is in C.

## Python FFI

* [pyml](https://github.com/thierry-martinez/pyml):
Library for interacting with python. Uses C stubs.
* [pyml_bindgen](https://github.com/mooreryan/ocaml_python_bindgen):
Automatically create bindings to python libraries with minimal boilerplate utilizing `pyml`.
* [OCaml-in-Python](https://github.com/thierry-martinez/ocaml-in-python):
Easily call OCaml code from Python.
* [Py](https://github.com/zshipko/ocaml-py):
Library for interacting with Python 3.5 using Ctypes.
* [lymp](https://github.com/dbousque/lymp):
Another library for interacting with Python, this one using a Python process.

## Rust FFI

* [rust-ocaml-derive](https://github.com/ahrefs/rust-ocaml-derive): provides an FFI with Rust.
Works on both the OCaml-to-Rust and Rust-to-OCaml directions.
  * [ICFP Presentation: Safely mixing OCaml and Rust](https://www.youtube.com/watch?v=UXfcENNM_ts)

## Others

* [OCaml-R](https://github.com/pveber/ocaml-r):
FFI to the [R statistical language](https://www.r-project.org/about.html).
[Docs](http://pveber.github.io/ocaml-r/index.html).

## Articles

* The OCaml manual's chapter on [interfacing C with OCaml](https://v2.ocaml.org/manual/intfc.html)
* Real World OCaml's [foreign function interface](https://dev.realworldocaml.org/foreign-function-interface.html) chapter
* [Modular foreign function bindings](https://mirage.io/blog/modular-foreign-function-bindings) with [ctypes](https://github.com/ocamllabs/ocaml-ctypes).
