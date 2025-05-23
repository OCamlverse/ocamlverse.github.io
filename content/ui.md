---
tags: [ecosystem]
---

# User Interface

## GUI

* [lablgtk](https://github.com/garrigue/lablgtk):
GTK2/3 bindings for OCaml with various higher-level facilities to define GUIs.
* [lablqml](https://github.com/Kakadu/lablqml):
QML Qt5 bindings for OCaml.
* [labltk](https://github.com/garrigue/labltk):
Interface to the Tcl/Tk GUI framework.
* [bogue](https://github.com/sanette/bogue):
A new, SDL-based GUI. Ideal for integration in games. [demo video](https://youtu.be/isFLxnDooL8)
* [Revery](https://github.com/revery-ui/revery) **WIP**:
A brand-new (and exciting) OCaml/ReasonML-based GUI.
Revery stands as a native, cross-platform alternative to Electron.
* [Brisk](https://github.com/briskml/brisk) **WIP**:
Rather than taking Revery's approach of having a uniform interface,
Brisk aims to use native platform APIs do draw OS-based GUI elements.
* [Stk](https://zoggy.frama.io/ocaml-stk/): An SDL-based GUI toolkit
* [owme](https://github.com/CharlesAverill/owme): A window manager **emulator** for faking graphical desktop applications

### Recommendations
Any of GTK, QML and Tcl/Tk can produce solid cross-platform UIs.
If you want to be more adventurous, you might want to try `bogue`.

## TUI (Terminals)
* [Lambda-Term](https://github.com/ocaml-community/lambda-term):
Lambda-Term is a cross-platform library for manipulating the terminal.
It provides an abstraction for keys, mouse events, colors, as well as a set of widgets to write curses-like applications.
* [Lwd](https://github.com/let-def/lwd):
Reactive interfaces in the terminal.
  * [Article on using Lwd and Nottui](https://tarides.com/blog/2020-09-24-building-portable-user-interfaces-with-nottui-and-lwd)
* [Notty](https://github.com/pqwy/notty):
Notty is a declarative terminal library for OCaml, structured around a notion of composable images.
* [Nottui](https://github.com/let-def/lwd/tree/master/lib/nottui):
Higher level DSL on top of `Notty`. Used together with `lwd`.
* [Progress](https://github.com/CraigFe/progress/):
Beautiful user-definable progress bars. Highly recommended.
