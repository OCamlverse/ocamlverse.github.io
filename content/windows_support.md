---
tags: [learning]
---

# Windows Support

Many projects, including the OCaml compiler itself, rely on the Unix shell and its various utilities.
Windows doesn't include these utilities or any of their substitutes (or even a built-in compiler),
making it much harder to support a complex library on Windows.

Nevertheless, OCaml is gradually making a transition towards full Windows support.

For newcomers the simplest option is to download and run the latest DkML [`Windows 64-bit Native Installer`](https://gitlab.com/dkml/distributions/dkml/-/releases/permalink/latest/downloads/setup64nu.exe).

## Options

* [DkML]:
A distribution of OCaml that uses [MSYS2] for Unix utilities and [Microsoft Visual Studio 2019](https://visualstudio.microsoft.com/vs/)
for 100% Windows library compatibility, and has a traditional `setup.exe` to install. The distribution transparently uses Unix utilities so that Windows users do not need to learn Unix.

  The disadvantages of DkML are:
    * Visual Studio 2019, even though it is automatically installed, is a multi-gigabyte program that requires Administrator permissions to install
    * Only OCaml 4.14.0 is officially supported. OCaml 5.x does not yet support Visual Studio.

* OCaml on [WSL (Windows Subsystem for Linux)](https://docs.microsoft.com/en-us/windows/wsl/install-win10) - 
  Windows 10 supports Ubuntu or any other Linux distribution *natively*.

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
However, the binaries produced can be run in Windows proper without cygwin,
if they're built with the right compiler (mingw).
    * [sys2cyg](https://github.com/mnxn/sys2cyg) is a tool that allows you to install up-to-date packages
    from `MSYS2` (a lightweight fork of cygwin).
    `MSYS2` by itself is incapable of building OCaml packages,
    but has better-maintained libraries,
    which could be useful for building OCaml libraries.
 
* [esy](https://esy.sh/):
a build tool similar to npm and OPAM created by the [Reason] community.
`esy` operates on top of [cygwin] but hides it away, making OCaml feel completely native to windows.
It therefore also inherits `cygwin`'s slow compilation speed.
Not all OPAM packages are available yet, but support is rapidly growing.

OPAM is being extended to support a Windows environment.
See [this post](https://discuss.ocaml.org/t/ann-opam-2-0-5-release/4081/7) for details.

[DkML]: https://diskuv.com/dkmlbook/
[ocaml-win]: https://fdopen.github.io/opam-repository-mingw/
[opam-cross-windows]: https://github.com/ocaml-cross/opam-cross-windows
[Reason]: https://reasonml.github.io/
[cygwin]: https://www.cygwin.com
[MSYS2]: https://www.msys2.org/
[ocamlearlybird]: https://github.com/hackwaly/ocamlearlybird#readme

## Resources

* [Video on getting OCaml to Windows](https://www.youtube.com/watch?v=1DAuSSljLFI).
