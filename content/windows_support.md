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
  Windows 10 supports Ubuntu or any other Linux distribution *natively*. This is by far the easiest and fastest option
  for using OCaml on Windows, and the one that support OCaml most fully.

  The disadvantages of this approach are:
    * By default, you'll be creating Linux binaries, which can only be run on Linux or on another
      Windows 10 machine that has WSL activated. However, this can be mitigated by using and following the instructions
      at [opam-cross-windows], which can create Windows OCaml programs
      from Linux.
    * WSL on Windows has no direct graphical support. It thus requires communication via the X protocol, using an X server
      such as [Xming](https://sourceforge.net/projects/xming/)) on the Windows side.
      Again, by using [opam-cross-windows], this barrier can be eliminated.

* Similar to WSL above, you can create OCaml programs on Linux proper,
and cross-compile them so they work on Windows using [opam-cross-windows].

* [OCaml for Windows][ocaml-win]:
A [cygwin]-based Ocaml distribution, with `opam` support. 
Keep in mind that [cygwin] is a translation layer for unix commands, and thus slows down compilation performance.
However, the binaries produced can be run in Windows proper without cygwin.
 
* [esy](https://esy.sh/):
a build tool similar to npm and OPAM created by the [Reason] community.
It operates on top of [cygwin] but hides it away, making OCaml feel completely native to windows.
It also inherits `cygwin`'s slow compilation speed.
Not all OPAM packages are available yet, but support is rapidly growing.

There is work being put in by [OCaml Labs](http://ocamllabs.io/doc/windows.html) to improve
the Windows situtation further.
Additionally, OPAM is being extended to support a Windows environment.
See [this post](https://discuss.ocaml.org/t/ann-opam-2-0-5-release/4081/7) for details.

[ocaml-win]: https://fdopen.github.io/opam-repository-mingw/
[opam-cross-windows]: https://github.com/ocaml-cross/opam-cross-windows
[Reason]: https://reasonml.github.io/
[cygwin]: https://www.cygwin.com

## Resources

* [Video on getting OCaml to Windows](https://www.youtube.com/watch?v=1DAuSSljLFI).

## Older

* [OCPWin](http://www.typerex.org/ocpwin.html): *obsolete*
  A self-contained binary distribution for Windows that supports MSVC.
  *This cannot be considered as an option anymore -- the latest OCaml provided is 4.01.*
