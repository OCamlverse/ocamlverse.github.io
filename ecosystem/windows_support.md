# Windows Support

## Installation

Various projects exist for installing OCaml under windows. We recommend sticking to 
[OCaml for Windows][ocaml-win] as it is the most recent distribution.

* [OCaml for Windows][ocaml-win] - The most maintained version, which installs the Cygwin toolchain 
and OCaml on top of that. The OCaml versions lag slightly behind, but not as much as the other projects.
* [OCPWin][ocaml-ocpwin] - A self-contained binary distribution for Windows, supports MSVC. This distribution 
lags behind on OCaml versions 
* [Installing from source][ocaml-from-source] - Its possible to also install OCaml manually using the 
Cygwin toolcheck by following this README, published by the OCaml project.


## Limitations

The versions supported by the windows distributions seem to lag behind the versions 
supported on Unix. Many tools (`ocamlbuild`, `ocamlfind`, etc.) can't be used 
without cygwin or some other unix-like environment.  

There is work being put in by [OCaml Labs](http://ocamllabs.io/doc/windows.html) to improve
the windows situtation.

[ocaml-win]: https://fdopen.github.io/opam-repository-mingw/
[ocaml-ocpwin]: http://www.typerex.org/ocpwin.html
[ocaml-from-source]: https://github.com/ocaml/ocaml/blob/trunk/README.win32.adoc
