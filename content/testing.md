---
tags: [ecosystem]
---

# Testing

* [ppx_expect](https://github.com/janestreet/ppx_expect):
a Cram-like framework for OCaml, enabled by PPX metaprogramming.
Write some code that creates output, and then create expectation tests that match
the output against a canonical version you write.
* [mdx](https://github.com/realworldocaml/mdx):
ensure correctness of example code blocks in Markdown files
(Cram-like testing for the output of shell scripts and OCaml toplevel code).
* [Alcotest](https://github.com/mirage/alcotest):
a lightweight and colourful test framework.
* [OUnit](http://ounit.forge.ocamlcore.org/):
a unit test framework for OCaml based on HUnit,
a unit testing framework for Haskell.
It allows one to easily create unit-tests for OCaml code.
* [QCheck](https://github.com/c-cube/qcheck):
a property testing library inspired by Haskell's QuickCheck.
* [iTeML](https://github.com/vincent-hugot/iTeML): formerly known as
[qtest](http://batteries.vhugot.com/qtest/), it supports inline pragmas to generate tests.
* [Kaputt](http://kaputt.x9c.fr): a comprehensive testing framework.
* [Pa_test](https://ocaml.janestreet.com/ocaml-core/111.28.00/doc/pa_test):
general inline testing macros.
* [TestSimple](https://github.com/hcarty/ocaml-testsimple):
a lightweight unit testing framework
compatible with the [Test Anything Protocol](https://testanything.org/).
* [Cucumber.ml](https://github.com/cucumber/cucumber.ml):
Behavior Driven Development using Cucumber.
* [qcstm](https://github.com/jmid/qcstm):
State machine framework for testing imperative code.
Built on `QCheck`.
[Paper](https://icfp20.sigplan.org/details/ocaml-2020-papers/2/A-Simple-State-Machine-Framework-for-Property-Based-Testing-in-OCaml)
[Video](https://www.youtube.com/watch?v=uuL9RYuaZV4)
* [Monolith](https://gitlab.inria.fr/fpottier/monolith):
Specify the behavior of a program and perform random or fuzz testing on it automatically.
[Paper](http://cambium.inria.fr/~fpottier/publis/pottier-monolith-2021.pdf)


## Fuzzing

[Fuzz Testing definition](https://en.wikipedia.org/wiki/Fuzzing#:~:text=Fuzzing%20or%20fuzz%20testing%20is,assertions%2C%20or%20potential%20memory%20leaks.)

* [Crowbar](https://github.com/stedolan/crowbar/):
Quickcheck tests + fuzzing courtesy of [afl-fuzz](http://lcamtuf.coredump.cx/afl/).
* [bun](https://github.com/yomimono/ocaml-bun/):
Integrate fuzzing into your CI.
* [Article about fuzzing with Crowbar, bun and afl-fuzz](https://tarides.com/blog/2019-09-04-an-introduction-to-fuzzing-ocaml-with-afl-crowbar-and-bun.html)
* [Monolith](https://gitlab.inria.fr/fpottier/monolith) can also be used for fuzzing.
