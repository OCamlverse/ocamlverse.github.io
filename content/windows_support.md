---
tags: [learning]
---

# Windows Support

Historically, OCaml has lived in the Unix and Linux ecosystems.
However, OCaml has recently obtained relatively good Windows support, with several good options available.
Windows has truly become a viable platform for OCaml development.

For newcomers, there are 2 easy options:
* Install [opam] either from [winget] or using [the script found here](https://opam.ocaml.org/doc/Install.html).
* Alternatively, download and run the latest DkML
  [`Windows 64-bit Native Installer`](https://gitlab.com/dkml/distributions/dkml/-/releases/permalink/latest/downloads/setup64nu.exe).

## Options

* OPAM for Windows:
[opam], OCaml's package manager, now supports Windows natively, and can be installed most easily
by invoking `winget install OCaml.opam` at the Windows Command Prompt.
Behind the scenes, OPAM's challenge is supporting the actual OCaml compiler, which relies on some Unix-based plumbing.
[opam] can install `cygwin` behind the scenes as a compatibility layer so you don't have to worry about that.
    * Note that for certain OCaml packages that require system-level libraries (e.g. `SDL`), it may be easier to install the system library via [vcpkg]
      than to use the mechanism currently provided via cygwin.

* [DkML]:
A distribution of OCaml that uses [MSYS2] for Unix utilities and [Microsoft Visual Studio 2019](https://visualstudio.microsoft.com/vs/)
for 100% Windows library compatibility, and has a traditional `setup.exe` to install.
The distribution transparently uses Unix utilities so that Windows users do not need to learn Unix.

    Disadvantages are:
    * Visual Studio, while automatically downloaded, is a multi-gigabyte download that requires Administrator permissions to install.
    * Only OCaml 4.14.0 is officially supported. OCaml 5.x does not yet support Visual Studio.

* [WSL] (Windows Subsystem for Linux). 
  Windows supports Ubuntu or any other Linux distribution *natively*.
  This is a very clean way to program OCaml.
      By default, you'll be creating Linux binaries, which can only be run on Linux or on another
      Windows machine that has WSL activated. However, this can be mitigated by using [opam-cross-windows],
      which can cross-compile OCaml Windows programs from Linux.

* Linux proper, with cross-compilation to Windows using [opam-cross-windows].

## Other Alternatives

* [esy](https://esy.sh/):
a build tool similar to npm and OPAM created by the [Reason] community.
`esy` operates on top of [cygwin] but hides it away, making OCaml feel completely native to windows.
It therefore also inherits `cygwin`'s slow compilation speed.
Not all OPAM packages are available yet.


[DkML]: https://diskuv.com/dkmlbook/
[ocaml-win]: https://fdopen.github.io/opam-repository-mingw/
[opam-cross-windows]: https://github.com/ocaml-cross/opam-cross-windows
[Reason]: https://reasonml.github.io/
[cygwin]: https://www.cygwin.com
[MSYS2]: https://www.msys2.org/
[ocamlearlybird]: https://github.com/hackwaly/ocamlearlybird#readme
[winget]: https://learn.microsoft.com/en-us/windows/package-manager/winget/
[opam]: https://opam.ocaml.org/
[vcpkg]: https://github.com/microsoft/vcpkg
[WSL]: https://learn.microsoft.com/en-us/windows/wsl/install

## Resources

* [Video on getting OCaml to Windows](https://www.youtube.com/watch?v=1DAuSSljLFI).
