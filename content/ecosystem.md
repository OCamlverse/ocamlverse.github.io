---
tags: [ecosystem]
---

# Ecosystem

This page describes the current state of the OCaml ecosystem.

* [check.ocamllabs.io](http://check.ocamllabs.io):
View current build status of the entire OPAM ecosystem.
* [The OCaml Platform](ocaml_platform.md): a community endeavor to standardize the
infrastructure in the OCaml world.
* [Community poll on OCaml](https://docs.google.com/forms/d/1OZV7WCprDnouU-rIEuw-1lDTeXrH_naVlJ77ziXQJfg/viewanalytics?gxids=7628):
How the community views the language and ecosystem.

## Help Needed
For a list of things currently missing in OCaml's ecosystem,
see [Help Needed](help_needed.md)

## Standard Libraries
For an overview of the different standard library options and recommendations,
see [Standard Libraries](standard_libraries.md).

## Data Structures and Algorithms
See [Data Structures and Algorithms](data_struct.md)

## Audio
See [Audio](audio.md)

## Build System/Package Management
See [Build System and Package Management](build_systems.md)

## Cloud Computing

* [aws-s3](https://github.com/andersfugmann/aws-s3): Access to Amazon's Simple Storage Solution (S3)
* [Google Drive OCamlFuse](https://github.com/astrada/google-drive-ocamlfuse):
A User file system for Google Drive. Also one of the few ways to sync Google Drive from Linux.
* [aws-lambda](https://github.com/anmonteiro/aws-lambda-ocaml-runtime):
OCaml runtime for AWS Lambda.

## Code Tools
See [Code Tools](code_tools.md)

## Command Line Arguments

* The standard library contains the 
[Arg](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Arg.html) module,
which has a simple syntax for defining command line arguments.
However, it uses mutable state for arguments,
and doesn't have a built-in way to handle things such as sub-arguments,
or argument aliases (long and short) for the same command, though these things can be done.
* [Cmdliner](https://github.com/dbuenzli/cmdliner) is a declarative approach to
laying out command-line arguments.
The library uses combinators to build up the desired arguments.
* [BOS - Basic OS Interaction](https://github.com/dbuenzli/bos) is a general OS abstraction
library which also contains a command line argument module
([BOS.OS.Arg](http://erratique.ch/software/bos/doc/Bos.OS.Arg.html)).
* Jane Street's Core standard library contains the Command module,
which takes a similar approach to Cmdliner.
* [Minicli](https://github.com/UnixJunkie/minicli)  is a self-described minimalist library
for command line parsing.

## Compilers
For compilation tools made in OCaml, see [Compilers](compilers.md)

## Concurrency, Parallelism, Distributed Computing
See [Concurrency, Parallelism and Distributed Computing](parallelism.md)

## Cryptography
See [Security and Cryptography](security.md)

## Databases
See [Databases](databases.md)

## Debugging
* OCaml comes with a built-in debugger for the bytecode compiler.
You invoke it with the `ocamldebug` command.
See [the manual](https://caml.inria.fr/pub/docs/manual-ocaml/debugger.html) for more details.
* The easiest way to debug OCaml code, other than inserting print statements,
is choosing bytecode as your compilation target, and using teh OCaml debugger.
* Additionally, one can use `gdb` to debug native code.

## Formal Software Verification
See [Formal Software Verification](software_verification.md)

## File Formats
For manipulating different file formats from OCaml, see [File Formats](file_formats.md)

## File Manipulation
See [File Manipulation](file_manip.md).

## Foreign Function Interface
For integrating with C, C++, Python etc., see [Foreign Function Interface](ffi.md).

## Functional Reactive Programming
See [Functional Reactive Programming](frp.md).

## Game Development
See [Games](games.md)

## Graphics
For graphic libraries, see [Graphics](graphics.md).

## Hardware Design
For usage of OCaml in hardware design, see [Hardware Design](hardware_design.md)

## Iterators
See [Iterators](iterators.md)

## Lens
[Accessors](https://github.com/janestreet/accessor):
a Lens library (easy access/functional updates to records).

## Logging
* [dolog](https://github.com/UnixJunkie/dolog):
a simple OCaml logger.
* [Volt](https://github.com/codinuum/volt):
a variant of Bolt OCaml logging tool.
* [Logs](http://erratique.ch/software/logs):
provides a logging infrastructure for OCaml.
* [easy-logging](https://github.com/sapristi/easy_logging):
An object-based simple logging module.

## Machine Learning, Data Science, Scientific Computing
For machine learning, data science and scientific computing,
see [Scientific Computing](scientific.md)

## Metaprogramming and PPX
For metaprogramming facilities such as PPX, camlp4 and MetaOCaml,
see [Metaprogramming](metaprogramming.md).

## Mobile
For compilation of OCaml to mobile platforms, see [Mobile](mobile.md).

## Monads
See [Monads](monads.md).

## Pretty printing
See [Pretty Printing](pretty_printing.md).

## Process Management
See [Process Management](process_management.md).

## Protocols
For support of protocols, see [Protocols](protocols.md)

## Profiling
See [Profiling](profiling.md).

## Regular Expressions
See [Regular Rxpressions](regular_expressions.md)

## RPC
See [RPC](rpc.md)

## Searching
For search-related libraries, see [Searching](searching.md)

## Security
See [Security and Cryptography](security.md)

## Static Analysis
For static analysis using OCaml, see [Static Analysis](static_analysis.md)

## String Manipulation
* The standard library's String module is somewhat lacking in terms of functionality.
* [Containers](https://github.com/c-cube/ocaml-containers) has an expanded String module,
with iteration functions and so on.
Containers strives to be backwards-compatible with the Stdlib.
* [AString](https://github.com/dbuenzli/astring):
another implementation of expanded string functionality,
with less regard for standard library compatibility
* [Bigstring](https://github.com/c-cube/ocaml-bigstring):
On 32-bit platforms, OCaml strings are constrained to 20MB sizes.
This library allows one to handle strings of any sizes, and also
to handle C-style strings as if they were OCaml strings.
Built on top of BigArray, and supports memory-mapping.
* [Bigstring/af](https://github.com/inhabitedtype/bigstringaf):
another implementation of a string overlay on top of BigArray, with similar benefits.
Emphasizes speed.

## Systems Programming
For low-level systems programming, see [Systems Programming](systems_programming.md)

## Testing Frameworks
For testing frameworks in OCaml, see [Testing](testing.md)

## Time and Date
* For short-term timing requirements,
[Sys.time](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Sys.html) can do the job.
* [mtime](https://github.com/dbuenzli/mtime): wall-clock monotonic time,
and the best choice for longer-running timing requirements.
* [ptime](http://erratique.ch/software/ptime): POSIX time.
* [ISO8601](https://github.com/sagotch/ISO8601.ml/) 
* [calendar](http://calendar.forge.ocamlcore.org/) 
* [odate](https://github.com/hhugo/odate) 

## Unicode Support
See [Unicode](unicode.md)

## User Interface
For GUIs and TUIs (Terminal User Interfaces), see [User Interface](ui.md)

## Web and Networking
For libraries related to web development and networking,
see [Web and Networking](web_networking.md)



