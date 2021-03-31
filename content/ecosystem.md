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
See [Command Line Arguments](command_line.md)

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
* [ocamlearlybird](https://github.com/hackwaly/ocamlearlybird):
[Debug Adapter Protocol](https://microsoft.github.io/debug-adapter-protocol/)
implementation for OCaml.
Allows integrating the OCaml debugger with an IDE.
* [ocaml-dap](https://github.com/hackwaly/ocaml-dap):
Generic [Debug Adapter Protocol](https://microsoft.github.io/debug-adapter-protocol/)
implementation in OCaml.

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
See [Logging](logging.md).

## Machine Learning, Data Science, Scientific Computing
See [Scientific Computing](scientific.md)

## Metaprogramming and PPX
See [Metaprogramming](metaprogramming.md) for metaprogramming facilities such as PPX, camlp4 and MetaOCaml.

## Mobile
See [Mobile](mobile.md) for compilation of OCaml to mobile platforms.

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
See [String Manipulation](string_manipulation.md)

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
* [Timere](https://github.com/daypack-dev/timere): date time handling and reasoning.
* [Timere-parse](https://github.com/daypack-dev/timere): natural language parsing of date, time and duration.

## Unicode Support
See [Unicode](unicode.md)

## User Interface
For GUIs and TUIs (Terminal User Interfaces), see [User Interface](ui.md)

## Web and Networking
For libraries related to web development and networking,
see [Web and Networking](web_networking.md)



