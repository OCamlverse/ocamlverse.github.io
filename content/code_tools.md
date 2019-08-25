---
tags: [ecosystem]
---

# Code Tools

## Editor Tools

For an OCaml beginner, the recommended editor of choice is Visual Studio code with the ReasonML plugin.

* [VSCode-Reason](https://github.com/reasonml-editor/vscode-reasonml):
the Reason/OCaml plugin for Visual Studio code.
It allows for all the advantages provided by Merlin with the convenience of the VSCode IDE.
* [merlin](https://github.com/ocaml/merlin):
the main tool used to provide information to editors about OCaml codebases.
Note that to provide information, the code must first be compiled.
Dune is able to automatically create /.merlin/ files, which are needed to help merlin find the compiled files.
* [tuareg](https://github.com/ocaml/tuareg):
OCaml mode for Emacs that can run the toplevel and the debugger within Emacs.
* [Sublime better ocaml](https://github.com/whitequark/sublime-better-ocaml):
better OCaml mode for Sublime Text.
  * [Sublime text package](https://github.com/def-lkb/sublime-text-merlin)
* [ocp-index](http://www.typerex.org/ocp-index.html):
Easy access to the interface information of installed OCaml libraries.
Contains a few standalone tools:
  * [ocp-browser](http://www.typerex.org/ocp-index.html#ocp-browser):
  Excellent, easily accessible ncurses-based API and documentation browser.
  Available independently on OPAM.
  * [ocp-index-top](https://github.com/reynir/ocp-index-top):
  toplevel directive for looking up documentation using ocp-index.
* [ocp-indent](http://www.typerex.org/ocp-indent.html):
indentation tool for OCaml, to be used from editors like Emacs and Vim.
  * [Vim plugin](https://github.com/def-lkb/ocp-indent-vim)

* [user-setup](https://github.com/OCamlPro/opam-user-setup):
automatically configures several editors to use merlin, ocp-indent, and ocp-index if they are installed.
Run `opam install user-setup` to install it, and then follow the instructions,
which tell you to run `opam user-setup install`.

## Developer Tools

* [utop](https://github.com/diml/utop):
Very powerful toplevel for OCaml, that is far better than the default one.
A must-install for every OCaml programmer.
* [sketch.sh](https://sketch.sh/ml):
Online tool for playing around with OCaml (most up-to-date version).
* [odoc](https://github.com/ocaml/odoc):
An automatic documentation generator for OCaml that creates beautiful html.
* [Try OCaml](http://try.ocamlpro.com/):
Try OCaml in your web browser.
* [codingground](https://www.tutorialspoint.com/compile_ocaml_online.php):
Compile and execute OCaml code online.
* [mdx](https://github.com/realworldocaml/mdx):
Tool for executing code or shell snippets inside markdown files.
* [iocaml](https://github.com/andrewray/iocaml):
An OCaml kernel for the IPython notebook.
* [ocamlbrowser](http://caml.inria.fr/pub/docs/manual-ocaml/browser.html):
A source and compiled interface browser, written using LablTk and included with it.
* [ghim](https://github.com/samoht/ghim):
A command-line tool to manage Github Issues.
* [OCaml Yeoman Generator](https://github.com/mabrasil/generator-ocaml):
Yeoman generator to scaffold OCaml modules.
* [Dead Code Analyzer](https://github.com/LexiFi/dead_code_analyzer):
OCaml dead code analysis.

### Code Coverage

* [Bisect_ppx](https://github.com/aantron/bisect_ppx):
A coverage tool for OCaml.
