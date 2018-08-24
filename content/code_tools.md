---
tags: [ecosystem]
---

# Code Tools

## Editor Tools

For an OCaml beginner, the recommended editor of choice is Visual Studio code with the ReasonML plugin.

* [VSCode-Reason](https://github.com/reasonml-editor/vscode-reasonml)  is the Reason/OCaml plugin for Visual Studio code. It allows for all the advantages provided by Merlin with the convenience of the VSCode IDE.

* [merlin](https://github.com/ocaml/merlin)  is the main tool used to provide information to editors about OCaml codebases. Note that to provide information, the code must first be compiled. Dune is able to automatically create /.merlin/ files, which are needed to help merlin find the compiled files.
* [tuareg](https://github.com/ocaml/tuareg)  - OCaml mode for Emacs that can run the toplevel and the debugger within Emacs.
* [Sublime better ocaml](https://github.com/whitequark/sublime-better-ocaml)  – Better OCaml mode for Sublime Text.
  * [Sublime text package](https://github.com/def-lkb/sublime-text-merlin)
* [ocp-index](http://www.typerex.org/ocp-index.html)  – Easy access to the interface information of installed OCaml libraries. a few standalone tools:
  * [ocp-browser](http://www.typerex.org/ocp-index.html#ocp-browser)  – Small ncurses-based API and documentation browser.
  * [ocp-index-top](https://github.com/reynir/ocp-index-top)  – Toplevel directive for looking up documentation using ocp-index.
  * [Sublime text package](https://sublime.wbond.net/packages/OCaml%20Autocompletion)
* [ocp-indent](http://www.typerex.org/ocp-indent.html)  – Indentation tool for OCaml, to be used from editors like Emacs and Vim.
  * [Vim plugin](https://github.com/def-lkb/ocp-indent-vim) .
  
* [user-setup](https://github.com/OCamlPro/opam-user-setup) - Automatically configures several editors to use merlin,
ocp-indent, and ocp-index if they are installed.  (Politely works to avoid messing up your existing configuration, but can occasionally come into conflict with something you already have set up.)  Run `opam install user-setup` to install it, and then follow the instructions, which tell you to run `opam user-setup install`. (Note different order of terms.)

## Developer Tools

* [utop](https://github.com/diml/utop)  – Universal toplevel for OCaml with support of multiline edition, history, real-time and context sensitive completion, colors, and more. This is a must-install for every OCaml programmer.
* [sketch.sh](https://sketch.sh/ml): Online tool for playing around with OCaml (most up-to-date version).
* [Try OCaml](http://try.ocamlpro.com/)  – Try OCaml in your web browser.
* [codingground](https://www.tutorialspoint.com/compile_ocaml_online.php)  – Compile and execute OCaml code online.
* [iocaml](https://github.com/andrewray/iocaml)  – An OCaml kernel for the IPython notebook.
* [ocamlbrowser](http://caml.inria.fr/pub/docs/manual-ocaml/browser.html)  – A source and compiled interface browser, written using LablTk. Included in the standard distribution for ocaml <= 4.01 and with labltk for ocaml >= 4.02.
* [ghim](https://github.com/samoht/ghim)  – A command-line tool to manage Github Issues.
* [OCaml Yeoman Generator](https://github.com/mabrasil/generator-ocaml)  – Yeoman generator to scaffold OCaml modules.

## Code Coverage

* [Bisect](http://bisect.x9c.fr/)
* [Bisect_ppx](https://github.com/rleonid/bisect_ppx)  a more recent fork of the previous tool, using ppx processing.
