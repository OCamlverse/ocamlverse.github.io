---
tags: [ecosystem]
---

# Testing

OCaml has many testing frameworks to choose from:

* [expect-test](https://github.com/janestreet/ppx_expect):
a Cram framework for OCaml, enabled by PPX metaprogramming.
Write some code that creates textual output, then create expectation tests that test against
said output.
Usage of PPX means you need to write a minimal amount of code,
and the simplicity means you don't need to look up much.
* [Alcotest](https://github.com/mirage/alcotest):
a lightweight test framework. Nice terminal UI with color for results.
`Alcotest` can compare many different kinds of outputs, but requires a bit more boilerplate
than `expect-test`, as well as looking up different kinds of tests.
* [OUnit](https://github.com/gildor478/ounit):
an older but still competitive unit test framework for OCaml.
Tests are done via `assert_equal` statements.
A little bit of boilerplate is needed.
* [QCheck](https://github.com/c-cube/qcheck):
a library that allows you to create unit tests based on random input.
* [qtest](https://github.com/vincent-hugot/qtest):
write simple inline pragmas within your code to generate unit tests.
`qtest` can integrate `QCheck` tests to have random testing, too.
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
* [mdx](https://github.com/realworldocaml/mdx):
Execute OCaml code blocks inside Markdown files.
Also supports Cram tests.


## Fuzzing

[Fuzz Testing definition](https://en.wikipedia.org/wiki/Fuzzing#:~:text=Fuzzing%20or%20fuzz%20testing%20is,assertions%2C%20or%20potential%20memory%20leaks.)

* [Crowbar](https://github.com/stedolan/crowbar/):
Quickcheck tests + fuzzing courtesy of [afl-fuzz](http://lcamtuf.coredump.cx/afl/).
* [bun](https://github.com/yomimono/ocaml-bun/):
Integrate fuzzing into your CI.
* [Article about fuzzing with Crowbar, bun and afl-fuzz](https://tarides.com/blog/2019-09-04-an-introduction-to-fuzzing-ocaml-with-afl-crowbar-and-bun.html)
* [Monolith](https://gitlab.inria.fr/fpottier/monolith) can also be used for fuzzing.
