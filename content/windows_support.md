---
tags: [learning]
---

# Windows Support

Many projects, including the OCaml compiler itself, rely on the Unix shell and its various utilities.
Windows doesn't include these utilities or any of their substitutes (or even a built-in compiler),
making it much harder to support a complex library on Windows.

Nevertheless, OCaml is gradually making a transition towards increased Windows support.

## Options

* OCaml on [WSL (Windows Subsystem for Linux)](https://docs.microsoft.com/en-us/windows/wsl/install-win10) - 
Windows 10 supports Ubuntu or any other Linux distribution *natively*. This is by far the easiest option
for using OCaml on Windows, and the one that support OCaml most fully.
The one disadvantage is that you'll be creating Linux binaries, which can only be run on Linux or on another
Windows 10 machine that has WSL activated. GUI support is also limited to running via an X server (such as [Xming](https://sourceforge.net/projects/xming/)) on the Windows side.

* Several other projects exist for installing OCaml under windows. We recommend sticking to 
[OCaml for Windows][ocaml-win] as it is the most recent distribution.
 
  * [OCaml for Windows][ocaml-win]:
  The most maintained version, which installs the Cygwin toolchain 
  and OCaml on top of that. The OCaml versions lag slightly behind, but not as much as the other projects.
  * [OCPWin][ocaml-ocpwin]:
  A self-contained binary distribution for Windows, supports MSVC. This distribution 
  lags behind on OCaml versions 
  * [Installing from source][ocaml-from-source]:
  Its possible to also install OCaml manually using the 
  Cygwin toolchain by following this README, published by the OCaml project.

* Another obvious option is to run OCaml in a Linux virtual machine. If you have Windows 10 though, this is suboptimal,
as WSL is much less resource-intensive than running a virtual machine.

* Yet another option (in development) is to use the growing Reason ecosystem, which supports OCaml syntax as well.
[esy](https://github.com/esy/esy) is a tool similar to OPAM that can install full OCaml binaries.
It has some OPAM support, though not all OPAM packages will be available.

## Limitations

Using OCaml on WSL is virtually the same as using it on Linux. Otherwise, the versions supported by the
windows distributions seem to lag behind the versions 
supported on Unix.
Many tools (`ocamlbuild`, `ocamlfind`, etc.) can't be used 
without cygwin or some other unix-like environment.  

There is work being put in by [OCaml Labs](http://ocamllabs.io/doc/windows.html) to improve
the windows situtation.

[ocaml-win]: https://fdopen.github.io/opam-repository-mingw/
[ocaml-ocpwin]: http://www.typerex.org/ocpwin.html
[ocaml-from-source]: https://github.com/ocaml/ocaml/blob/trunk/README.win32.adoc
