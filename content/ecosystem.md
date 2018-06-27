---
tags: [ecosystem]
---

# Ecosystem

This page describes the current state of the OCaml ecosystem. Please help keep it up to date.

* [The OCaml Platform](ocaml_platform.md): a community endeavor to standardize the infrastructure in the OCaml world.

## Missing Pieces
For a list of things currently missing in OCaml's ecosystem, see [Missing Pieces](missing_pieces.md)

## Standard Libraries
For an overview of the different standard library options and recommendations, see [Standard Libraries](standard_libraries.md).

## Data Structures and Common Algorithms

* In effect, a standard library's primary role is providing basic data structures and algorithms. All the [standard libraries](standard_libraries.md) (Containers, Base, Core and Batteries) provide both.
* [OCamlGraph](https://github.com/backtracking/ocamlgraph) is a library for graphs and graph algorithms.
* [ods](https://github.com/owainlewis/ods) is an algorithm/data structure, though it isn't as fully-featured as the standard libraries.

## Audio
See [Audio](audio.md)

## Build System/Package Management
See [Build System and Package Management](build_systems.md)

## Code Tools
See [Code Tools](code_tools.md)

## Command Line Arguments

* The standard library contains the [Arg](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Arg.html) module, which has a simple syntax for defining command line arguments. However, it uses mutable state for arguments, and doesn't have a built-in way to handle things such as sub-arguments, or argument aliases (long and short) for the same command, though these things can be done.
* [Cmdliner](https://github.com/dbuenzli/cmdliner) is a declarative approach to laying out command-line arguments. The library uses combinators to build up the desired arguments.
* [BOS - Basic OS Interaction](https://github.com/dbuenzli/bos) is a general OS abstraction library which also contains a command line argument module ([BOS.OS.Arg](http://erratique.ch/software/bos/doc/Bos.OS.Arg.html)).
* Jane Street's Core standard library contains the Command module, which takes a similar approach to Cmdliner.
* [Minicli](https://github.com/UnixJunkie/minicli)  is a self-described minimalist library for command line parsing.

## Compilers
For compilation tools made in OCaml, see [Compilers](compilers.md)

## Concurrency, Parallelism, Distributed Computing
See [Concurrency, Parallelism and Distributed Computing](parallelism.md)

## Databases
See [Databases](databases.md)

## Debugging

* OCaml comes with a built-in debugger for the bytecode compiler. You invoke it with the `ocamldebug` command. See [the manual](https://caml.inria.fr/pub/docs/manual-ocaml/debugger.html) for more details.
* The easiest way to debug OCaml code, other than inserting print statements, is choosing bytecode as your compilation target, and using teh OCaml debugger.
* Additionally, one can use `gdb` to debug native code.

## Editor Support
See [Editor Support](editor_support.md)

## Formal Software Verification
See [Formal Software Verification](software_verification.md)

## File Formats
For manipulating different file formats from OCaml, see [File Formats](file_formats.md)

## File Path Manipulation
* [Fpath](https://github.com/dbuenzli/fpath): Cross-platform path manipulation library.

## Foreign Function Interce
For integrating with C, C++, Python etc., see [Foreign Function Interface](ffi.md)

## Functional Reactive Programming
See [Functional Reactive Programming](frp.md)

## Graphics
For graphic libraries, see [Graphics](graphics.md)

## Hardware Design
For usage of OCaml in hardware design, see [Hardware Design](hardware_design.md)

## Logging

* [dolog](https://github.com/UnixJunkie/dolog) : simple OCaml logger.
* [Volt](https://github.com/codinuum/volt) : a variant of Bolt OCaml logging tool.
* [Logs](http://erratique.ch/software/logs) : provides a logging infrastructure for OCaml.

## Mobile
For compilation of OCaml to mobile platforms, see [Mobile](mobile.md)

## Metaprogramming
For metaprogramming facilities such as PPX, see [Metaprogramming](metaprogramming.md)

## Pretty printing
* [easy-format](https://github.com/mjambon/easy-format)  – Pretty-printing library for OCaml.

## Protocols
For support of protocols, see [Protocols](protocols.md)

## Profiling

* [SpaceTime](https://caml.inria.fr/pub/docs/manual-ocaml/spacetime.html) is integrated into the compiler
and allows profiling of memory allocation.
* [landmarks](https://github.com/LexiFi/landmarks): a profiling library for OCaml, taking into account both
memory allocation and CPU time.
* Standard tools such as [gprof](https://sourceware.org/binutils/docs/gprof/) can also be used to debug OCaml
programs.

## Regular Expressions

* [Re](https://github.com/ocaml/ocaml-re)  – a pure OCaml regular expressions library with combinators, supporting several formats (glob, posix, str...)
* [ocaml-pcre](https://github.com/mmottl/pcre-ocaml)  – bindings to the PCRE library (perl-compatible regular expressions)
* [Humane-re](https://github.com/rgrinberg/humane-re)  – Humane-re attempts to provide an easy interface for 90% of your regex needs. It is a binding on top of ocaml-re.
* [Tyre](https://github.com/Drup/tyre)  - Tyre is a set of combinators to build type-safe regular expressions, allowing automatic extraction and modification of matched groups.
* The standard library contains the [Str](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Str.html) module. This module is __not__ recommended, but its availability in the standard library makes it useful when you don't have access to anything better.

## Scientific Computing and Machine Learning
For machine learning, data science and scientific computing, see [Scientific Computing](scientific.md)

## Static Analysis
For static analysis using OCaml, see [Static Analysis](static_analysis.md)

## Searching
For libraries related to search, see [Searching](searching.md)

## String Manipulation

* The standard library's String module is somewhat limited currently.
* Containers has an expanded String module, with iteration functions etc.
* [AString](https://github.com/dbuenzli/astring): an alternative implementation of expanded string functionality, with less regard for standard library compatibility
* [Bigstring](https://github.com/c-cube/ocaml-bigstring): allows handling C-style strings of any size as if they were OCaml strings.
  Built on top of BigArray, and supports memory-mapping.

## Systems Programming
For low-level systems programming, see [Systems Programming](systems_programming.md)

## Testing Frameworks
For testing frameworks in OCaml, see [Testing](testing.md)

## Time and Date

* [mtime](https://github.com/dbuenzli/mtime): Monotonic time.
* [ptime](http://erratique.ch/software/ptime): POSIX time.
* [ISO8601](https://github.com/sagotch/ISO8601.ml/) 
* [calendar](http://calendar.forge.ocamlcore.org/) 
* [odate](https://github.com/hhugo/odate) 

## User Interface
For GUIs, TUIs, see [User Interface](ui.md)

## Web and Networking
For libraries related to web development and networking, see [Web and Networking](web_networking.md)



