---
tags: [ecosystem]
---

# Definitions
* Unit Tests: tests involving specific functions.
The function is given a specific input, and the output is compared to the expected output.
This allows us to have guarantees about the behavior of code even after we refactor it,
or even before we write the code itself.
* Property Tests: tests which involve specifying the general behavior of a function -
given random input, what property should its output have -
rather than choosing specific input and output combinations, as we do in unit testing.
* Expect tests: a form of unit testing.
Rather than coming up with specific inputs and their respective outputs,
the programmer tries different inputs and gets the dumped state of the function output,
which is incorporated into the test itself.
This requires printers for every type involved,
but allows for exploration and regression testing.
See [this article](https://blog.janestreet.com/the-joy-of-expect-tests/).
* Cram Tests: a form of unit testing that involves using some shell,
such as the OCaml toplevel.
All input and output is included in the test itself,
and the test plays back the input and compares the output to what is expected.

# Unit Testing Frameworks

OCaml has many unit testing frameworks to choose from:

* [dune](build_systems.md#dune)
has a [useful page](https://dune.readthedocs.io/en/stable/tests.html)
explaining how to integrate all unit test options.
`dune` also supports its own simplified version of expect tests using `.expect` files,
which may be enough for many users.
`dune runtest` and `dune promote` are usually all that's needed to run and update expect tests (including `ppx_expect`).
`dune` also includes support for running Cram tests.
* [expect-test](https://github.com/janestreet/ppx_expect):
expect tests utilising the [ppx](ppx.md) system.
As discussed [here](https://blog.janestreet.com/the-joy-of-expect-tests/).
Tightly coupled with `dune`.
Tests can be in the same files as the code itself or placed separately.
* [ppx_inline_test](https://github.com/janestreet/ppx_inline_test):
Inline unit tests using the ppx system. Works well in concert with ppx_expect.
* [Alcotest](https://github.com/mirage/alcotest):
a lightweight, easy to use, and popular test framework.
Nice colored output for results.
* [OUnit](https://github.com/gildor478/ounit):
an older but still competitive unit test framework for OCaml.
* [QCheck](https://github.com/c-cube/qcheck):
a library that allows you to perform property tests.
Sub-libraries are provided to integrate with both `Alcotest` and `OUnit`
* [qtest](https://github.com/vincent-hugot/qtest):
write simple inline pragmas within your code to generate unit tests.
`qtest` can also integrate `QCheck` tests to have random testing, too.
* [mdx](https://github.com/realworldocaml/mdx):
Execute OCaml code blocks inside Markdown documentation files.
Also supports Cram tests.

## Less Popular Options
* [Kaputt](http://kaputt.x9c.fr): a comprehensive testing framework.
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

Fuzzing involves hitting your program with random or adversarially optimized input until you find ill-defined behavior.

[Fuzz Testing definition](https://en.wikipedia.org/wiki/Fuzzing#:~:text=Fuzzing%20or%20fuzz%20testing%20is,assertions%2C%20or%20potential%20memory%20leaks.)

* [Crowbar](https://github.com/stedolan/crowbar/):
Quickcheck tests + fuzzing courtesy of [afl-fuzz](http://lcamtuf.coredump.cx/afl/).
* [bun](https://github.com/yomimono/ocaml-bun/):
Integrate fuzzing into your CI.

* [Article about fuzzing with Crowbar, bun and afl-fuzz](https://tarides.com/blog/2019-09-04-an-introduction-to-fuzzing-ocaml-with-afl-crowbar-and-bun.html)
* [Monolith](https://gitlab.inria.fr/fpottier/monolith) can also be used for fuzzing.
