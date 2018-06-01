# Basic Libraries

## Standard Libraries

OCaml comes with its own [Standard Library](https://caml.inria.fr/pub/docs/manual-ocaml/libref/). Most OCamlers, however, agree that the built-in standard library is problematic: it's not comprehensive enough, and it uses outmoded patterns, such as using exceptions rather than error types. The community has had trouble expanding the library due to namespacing issues.

*Note, however, that since OCaml 4.07, the namespace issue has mostly been fixed, and the standard library is being expanded to cover more missing use-cases. Additionally, many functions that threw exceptions now have no-exception counterparts.*

In the absence of a comprehensive standard library, several competitors developed. Due to OCaml's support for modularity, each can be swapped out for the other wholesale.

* The [standard library](https://caml.inria.fr/pub/docs/manual-ocaml/libref/) offers a selection of functional data structures (List, Map) and imperative data structures (Array, Queue, Stack). Many of the functions throw an exception rather than returning an option type. The library also includes the Unix module, which, despite its name, has many functions that work on Windows. The Unix module is a catch-all for many IO-processing functions. Also included is the Format module for pretty printing and the Str module for regular expression matching, among other useful modules.
* [Base](https://github.com/janestreet/base)  is Jane Street Capital's internally developed, battle-tested standard library implementation. It's library covered by the 2nd edition of Real World OCaml. The library doesn't try to extend the basic standard library, but instead chooses its own design. To the users, the most obvious difference compared to the other standard library options will be the choice of having labels in function arguments, similar to the ListLabels, ArrayLabels, etc modules in the standard library. Additionally, Base does not use polymorphic comparison anywhere in its API.
* [Containers](https://github.com/c-cube/ocaml-containers)  is a lightweight and modern-style standard library which extends the standard library with additional functionality while applying more modern design concepts. As of version 2.0, Containers does not use polymorphic comparison anywhere.
* [Core](https://github.com/janestreet/core)  is Jane Street's expanded standard library, sitting on top of Base. Core is more comprehensive than Base.
* [Batteries Included](https://github.com/ocaml-batteries-team/batteries-included)  is a mature, full-featured standard library, taking the approach of extending the standard library with additional functionality rather than replacing it wholesale. It includes many data structures and algorithms. Note that Containers came about as a split-off from Batteries.

### Recommendations
Several non-compatible modern alternatives are recommended:

* Containers + stdlib: Containers is a modern extension of the stdlib, and extends it in powerful ways. For OS interaction, BOS (see below) is a great fit.
* Base + Core: The Jane Street standard libraries eschew the conventions of the stdlib, and present an alternative, powerful combination that works particularly well with other Jane Street libraries.

## Data Structures and Common Algorithms

* In effect, a standard library's primary role is providing basic data structures and algorithms. All the standard libraries (Containers, Base, Core and Batteries) provide both.
* [OCamlGraph](https://github.com/backtracking/ocamlgraph) is a library for graphs and graph algorithms.
* [ods](https://github.com/owainlewis/ods) is an algorithm/data structure, though it isn't as fully-featured as the standard libraries.

## Command Line Arguments

* The standard library contains the [Arg](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Arg.html) module, which has a simple syntax for defining command line arguments. However, it uses mutable state for arguments, and doesn't have a built-in way to handle things such as sub-arguments, or argument aliases (long and short) for the same command, though these things can be done.
* [https://github.com/dbuenzli/cmdliner Cmdliner] is a declarative approach to laying out command-line arguments. The library uses combinators to build up the desired arguments.
* [BOS - Basic OS Interaction](https://github.com/dbuenzli/bos) is a general OS abstraction library which also contains a command line argument module (BOS.OS.Arg).
* Jane Street's Core standard library contains the Command module, which takes a similar approach to Cmdliner.
* [Minicli](https://github.com/UnixJunkie/minicli)  is a self-described minimalist library for command line parsing.

## String Manipulation

* The standard library's String module is somewhat limited currently.
* Containers has an expanded String module, with iteration functions etc.
* [AString](https://github.com/dbuenzli/astring): an alternative implementation of expanded string functionality, with less regard for standard library compatibility
* [Bigstring](https://github.com/c-cube/ocaml-bigstring): allows handling C-style strings of any size as if they were OCaml strings.
  Built on top of BigArray, and supports memory-mapping.

## Regular Expressions

* [Re](https://github.com/ocaml/ocaml-re)  – a pure OCaml regular expressions library with combinators, supporting several formats (glob, posix, str...)
* [ocaml-pcre](https://github.com/mmottl/pcre-ocaml)  – bindings to the PCRE library (perl-compatible regular expressions)
* [Humane-re](https://github.com/rgrinberg/humane-re)  – Humane-re attempts to provide an easy interface for 90% of your regex needs. It is a binding on top of ocaml-re.
* [Tyre](https://github.com/Drup/tyre)  - Tyre is a set of combinators to build type-safe regular expressions, allowing automatic extraction and modification of matched groups.
* The standard library contains the [Str](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Str.html) module. This module is __not__ recommended, but its availability in the standard library makes it useful when you don't have access to anything better.

## File Path

## IO
* [BOS - Basic OS Interaction](https://github.com/dbuenzli/bos) is an OS interaction layer containing many elements, including file manipulation, command line argument parsing, etc.

## Pretty printing

* [easy-format](https://github.com/mjambon/easy-format)  – Pretty-printing library for OCaml.


## Logging

* [dolog](https://github.com/UnixJunkie/dolog) : simple OCaml logger.
* [Volt](https://github.com/codinuum/volt) : a variant of Bolt OCaml logging tool.
* [Logs](http://erratique.ch/software/logs) : provides a logging infrastructure for OCaml.

## Time and Date

* [ptime](http://erratique.ch/software/ptime) 
* [ISO8601](https://github.com/sagotch/ISO8601.ml/) 
* [calendar](http://calendar.forge.ocamlcore.org/) 
* [odate](https://github.com/hhugo/odate) 
