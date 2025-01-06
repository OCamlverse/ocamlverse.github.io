---
layout: page
tags: [ecosystem]
---

# Command Line Arguments

* The standard library contains the
[Arg](https://v2.ocaml.org/api/Arg.html) module,
which has a simple syntax for defining command line arguments.
However, it uses mutable state for arguments,
and doesn't have a built-in way to handle things such as sub-arguments,
or argument aliases (long and short) for the same command, though these things can be done.
* [Cmdliner](https://github.com/dbuenzli/cmdliner) is a declarative approach to
laying out command-line arguments.
The library uses combinators to build up the desired arguments.
  * [Cmdliner cheat sheet](https://github.com/mjambon/cmdliner-cheatsheet)
* [ez_cmdliner](https://ocamlpro.github.io/ez_cmdliner/):
Simpler interface on top of `Cmdliner`.
* [BOS - Basic OS Interaction](https://github.com/dbuenzli/bos) is a general OS abstraction
library which also contains a command line argument module
([BOS.OS.Arg](https://erratique.ch/software/bos/doc/Bos/index.html)).
* Jane Street's Core standard library contains the Command module,
which takes a similar approach to Cmdliner.
* [Minicli](https://github.com/UnixJunkie/minicli)  is a self-described minimalist library
for command line parsing.
* [Quick-and-dirty pure command-line arguments in OCaml](https://dev.to/yawaramin/quick-and-dirty-pure-command-line-arguments-in-ocaml-3hcg) (using the standard Library's Arg module)
* [Climate](https://github.com/gridbugs/climate) A declarative command-line parser with (quite) intuitive direct-style arguments parsers.
