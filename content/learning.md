---
tags: [learning]
---

# Learning

## Beginner Topics

Some motivations for using OCaml can be found [here](http://spyder.wordpress.com/2014/03/16/why-ocaml-why-now/),
[here](http://web.archive.org/web/20140713005224/http://www.mimisbrunnr.net/~munin/blog/why-ocaml.html),
[here](http://queue.acm.org/detail.cfm?id=2038036) and
[here](https://espertech.wordpress.com/2014/07/15/why-we-use-ocaml/).

* The [quickstart](quickstart.md) page to get you up and running as fast as possible.
* [OCaml cheat sheet](https://github.com/alhassy/OCamlCheatSheet/blob/master/CheatSheet.pdf)
* Play around with OCaml online using [sketch.sh](https://sketch.sh/ml).
* [The Beginner's Guide to OCaml Beginner's guides](http://blog.nullspace.io/beginners-guide-to-ocaml-beginners-guides.html)
* [Learn X in Y minutes](https://learnxinyminutes.com/docs/ocaml/) where X=OCaml.
* [Functional Programming with OCaml](https://haifengl.wordpress.com/2014/06/17/ocaml-introduction/)
* [OCaml file types and filename extensions](https://ocaml.org/learn/tutorials/filenames.html)
* [The faq](faq.md): a good place to find answers to questions about OCaml.
* [Real World OCaml](https://dev.realworldocaml.org/):
A free online book, and a great introduction to OCaml.
* [Links to OCaml Q&A around the web](qna_links.md).
* [Using the OCaml toplevel/REPL](toplevel.md)
* [Article on algebraic data types](https://espertech.wordpress.com/2014/07/30/algebraic-data-types/)
* [Python to OCaml: a retrospective](http://roscidus.com/blog/blog/2014/06/06/python-to-ocaml-retrospective/):
Blog entries about rewriting 0Install in OCaml instead of python.
* [Functional Alternatives to Inheritance](http://ocamltutorials.blogspot.se/2013/06/alternatives-to-subtyping.html):
Beginner-friendly look at alternatives to OOP inheritance.


### Setting Up Your Editor for OCaml

OCaml can be edited conveniently with many different editors.
See [editor setup](editor_setup.md) and [code tools](code_tools.md).

### Using the OCaml Build Tools

* [Quick Start an OCaml project with Dune](quickstart_ocaml_project_dune.md)
* [Project showing how to use OPAM with/without dune](https://github.com/jserot/opam-howto)
* [Project showing how to use Dune in different configurations](https://github.com/jserot/dune-howto)
* [OPAM for npm/yarn users](opam_npm.md)
* [A sample Dune project](https://github.com/mjambon/dune-starter)
* [OPAM 2.0 tips](https://opam.ocaml.org/blog/opam-20-tips/):
Local opam installs, pinning, and lock files.

### Best Practices

Several guidelines for best practices have been established by the community.
See [Best Practices](best_practices.md).

### Beginner Books

* [Real World OCaml](https://dev.realworldocaml.org/) by Y. Minsky, A. Madhavapeddy and J. Hickey (free online):
Functional programming for the masses.
The latest, most up-to-date, and arguably the most readable book on OCaml.
Note that the book uses only Jane Street libraries, but the material can be applied to other libraries.
  * [RWO-lwt](https://github.com/dkim/rwo-lwt):
  translation of the `Async` code examples in the book to use `lwt`.
* [Cornell OCaml Textbook](https://www.cs.cornell.edu/courses/cs3110/2020fa/textbook/) (free online):
Excellent free online book, covering both beginner and advanced topics.
* [How to Think Like a (Functional) Programmer](http://www.greenteapress.com/thinkocaml/index.html) by Allen Downey and Nicholas Monje (free online):
An introductory programming textbook using OCaml.
It is a modified version of Think Python by Allen Downey.
This book is intended for newcomers to programming and also those who know some programming but
want to learn programming in the function-oriented paradigm,
or those who simply want to learn OCaml.
* [OCaml from the Very Beginning](http://ocaml-book.com/) by J. Whitington:
A book for both new programmers and experienced programmers eager to explore functional languages such as OCaml.

### Online Exercises for Beginners

* [99 problems](http://ocaml.org/learn/tutorials/99problems.html):
The classic 99 problems, with solutions in OCaml.
* [Rosetta Code](http://rosettacode.org/wiki/Category:OCaml)
* [OCaml at Exercism](http://exercism.io/languages/ocaml):
  * [Solutions](https://github.com/exercism/xocaml)

### Beginner Online Courses

* [Introduction to Functional Programming in OCaml](https://www.fun-mooc.fr/courses/parisdiderot/56002S02/session02/about)
* [Cornell University: Data Structures and Functional Programming](http://www.cs.cornell.edu/Courses/cs3110/2014fa/course_info.php)
* [Princeton University: Functional programming in OCaml](http://www.cs.princeton.edu/~dpw/courses/cos326-12/)
* [University of Illinois Course on OCaml and Functional Programming](https://courses.engr.illinois.edu/cs421/fa2014/)

## Intermediate Topics

* [BigArray](bigarray.md):
A high-performance array for interacting with non-OCaml programs.
* [ocamlunix](https://ocaml.github.io/ocamlunix/ocamlunix.html):
Great introduction to systems programming in OCaml
* [Higher-Rank Polymorphism in OCaml](http://devmusings.legiasoft.com/blog/2008/05/23/higher-rank_polymorphism_in_ocaml):
How to activate higher-rank polymorphism in OCaml. Old, but still relevant.

### Deploying Apps

* [Building an OCaml webapp using Opium](https://shonfeder.gitlab.io/ocaml_webapp/)

### The Format Module

The Stdlib has the [Format](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Format.html)
module for pretty printing.
It's a little tricky to get a hang of.
* [Tutorial](https://ocaml.org/learn/tutorials/format.html)
* [Blog post on Format](https://blag.cedeela.fr/format-all-the-data-structures/)
* [Paper](https://hal.archives-ouvertes.fr/hal-01503081/file/format-unraveled.pdf) on Format

### Tools

* [Fuzzing OCaml programs](https://tarides.com/blog/2019-09-04-an-introduction-to-fuzzing-ocaml-with-afl-crowbar-and-bun.html)

### Functional Data Structures

* [Purely Functional Data Structures](http://www.amazon.co.uk/Purely-Functional-Structures-Chris-Okasaki/dp/0521631246/ref=sr_1_1?ie=UTF8&qid=1406279836&sr=8-1&keywords=functional+data+structures):
A classic book focusing on various data structures in the functional programming world.
Can be very useful for understanding functional data structures,
though OCaml obviously supports imperative data structures as well.

### Writing Efficient Code

See [Optimizing OCaml Performance](optimizing_performance.md).

### Intermediate Level Books

* [More OCaml: Algorithms, Methods, and Diversions](http://www.amazon.com/More-OCaml-Algorithms-Methods-Diversions/dp/0957671113/)
by John Whitington:
A meandering tour of functional programming with OCaml, introducing various language features and describing some classic algorithms.
The book ends with a large worked example dealing with the production of PDF files.
There are questions for each chapter together with worked answers and hints.
* [Pearls of Functional Algorithm Design](http://www.amazon.co.uk/Pearls-Functional-Algorithm-Design-Richard/dp/0521513383) by Richard Bird:
Tackles 30 hard algorithm problems using function programming.
Although it is writtern for Haskell, trying to solve the problems in OCaml also helps develop functional programming.
  * Partial solutions in OCaml are [available here](https://github.com/MassD/pearls).
* [Scientific Computing in OCaml and Owl](https://ocaml.xyz/book/) (free):
Covers OCaml and using the [Owl](https://ocaml.xyz) library,
which is a heavy-duty library for scientific and numerical computation as well as machine learning.
* [Unix System Programming in OCaml](http://ocamlunix.forge.ocamlcore.org/) by X. Leroy and D. Rémy (free):
Introduction to Unix system programming, with an emphasis on communications between processes.
* [OCaml for Scientists](http://www.ffconsultancy.com/products/ocaml_for_scientists/) by Jon Harrop

### Large Source Code Examples in the Wild

Below are some examples of larger applications and libraries, which you can use to build up an understanding of how
people structure larger ocaml projects. The list below tries to avoid code that needs to be particularly complex or hairy, 
which is sometimes needed in lower level libraries.

* [Dark](https://github.com/darklang/dark): "combined language, editor, and infrastructure to make it easy to build backends". See the libshared, client and backend directories.

## Advanced Topics

* [Quick and Dirty Guide to Monadic Parsers and Angstrom](monadic-parsers-angstrom.md)

### Modules and Functors

* [Introduction to Functors](functors_intro.md)
* [Functors](functors.md)

### Polymorphism

* [OCaml polymorphism examples](http://stackoverflow.com/questions/14440531/ocaml-polymorphism-example-other-than-template-function)
* [OCaml - polymorphic print and type erasure](http://stackoverflow.com/questions/7442449/ocaml-polymorphic-print-and-type-losing)
* [Weak Type Variables - when impurity breaks polymorphism](weak_type_variables.md)

### Existential Types

* [Existential types In CS242](http://cs242.stanford.edu/f17/assets/slides/04.2-polymorphism-existential.pdf)
* [Application: universal hashtable for GC roots](https://discuss.ocaml.org/t/ctypes-whats-the-most-idiomatic-way-to-anchor-an-ocaml-value-so-that-its-not-garbage-collected/6258/2)

### GADTs

* [GADTs in the OCaml manual](https://caml.inria.fr/pub/docs/manual-ocaml/gadts.html)
* [Diff Lists](https://drup.github.io/2016/08/02/difflists/):
An application of GADTs to produce heterogenous lists.
* [Detecting use-cases for GADTs](https://mads-hartmann.com/ocaml/2015/01/05/gadt-ocaml.html)
* [Tradeoffs with GADTs](https://engineering.issuu.com/2015/09/17/gadt-practicalities)
* [Why GADTs matter for performance](https://blog.janestreet.com/why-gadts-matter-for-performance/)
* [Cambridge University lecture: Programming with GADTs](https://www.cl.cam.ac.uk/teaching/1415/L28/gadts.pdf)

### Phantom Types

* [Static Access Control Using Phantom Types](https://blog.janestreet.com/howto-static-access-control-using-phantom-types/)

### Iterators

* [Generators Iterators Control and Continuations](http://gallium.inria.fr/blog/generators-iterators-control-and-continuations/)

### PPX (PreProcessor eXtensions)

See [Metaprogramming](metaprogramming.md) for both libraries and articles.

### FFI (Foreign Function Interface)

* See [FFI](ffi.md).

### Monads

* [Xavier Leroy's Monadic Programming Lecture Slides (pdf)](https://xavierleroy.org/mpri/2-4/monads.pdf) and [code](https://xavierleroy.org/mpri/2-4/monads.ml)
* [Cornell's CS 3110 Lecture about monads](https://www.cs.cornell.edu/courses/cs3110/2018sp/l/25-monads/lec.pdf), with [code](https://www.cs.cornell.edu/courses/cs3110/2018sp/l/25-monads/code.ml) and [recitation](https://www.cs.cornell.edu/courses/cs3110/2018sp/l/25-monads/lab.html)
* [A small monads tutorial from the Monads library](http://binaryanalysisplatform.github.io/bap/api/master/monads/Monads/Std/index.html)
* [Discussion on what you can do with Monads](https://discuss.ocaml.org/t/can-monads-help-me-my-refactor-code-for-an-enhanced-data-structure/1064/5?u=ivg) and what are [Monad Transformers](https://discuss.ocaml.org/t/ann-monads-the-missing-monad-transformers-library/830/6?u=ivg)
* [Monadic Error Handling](https://medium.com/@huund/monadic-error-handling-1e2ce66e3810)
* [More Typeclasses in OCaml](http://blog.shaynefletcher.org/2017/05/more-type-classes-in-ocaml.html)

### Concurrency

* [lwt tutorial](https://raphael-proust.github.io/code/lwt-part-1.html)

### Multicore

* [Parallel programming in Multicore OCaml](https://github.com/prismlab/parallel-programming-in-multicore-ocaml/tree/draft)

### Type Theory

* [Using, Understanding, and Unraveling the OCaml Language](http://caml.inria.fr/pub/docs/u3-ocaml/ocaml.pdf) by Didier Remy:
Covers both practical and type-theoretical aspects of OCaml.
* [Types and Programming Languages](https://www.cis.upenn.edu/~bcpierce/tapl) by Benjamin C. Pierce:
A friendly but serious book on type theory.
Much of what's covered is relevant to OCaml.
OCaml implementations of typechecking are presented in the book.
* [Advanced Topics in Types and Programming Languages](https://www.cis.upenn.edu/~bcpierce/attapl/index.html):
A more advanced anthology on type theory edited by Benjamin C. Pierce.
Includes some articles that are relevant to OCaml.

### Category Theory

Category Theory is a branch of abstract mathematics that discusses concepts
that tend to pop up as patterns in functional programming.

* [First steps with Category Theory and OCaml](http://www.mseri.me/typeclass-ocaml/):
Focuses on Monoids and Applicatives.
* [Category Theory For Programmers](https://github.com/hmemcpy/milewski-ctfp-pdf):
Not OCaml-specific, but a good book to learn Category Theory from.
* [Category Theory For Programmers in Ocaml](https://github.com/ArulselvanMadhavan/ocaml-ctfp):
An ongoing work to translate CTFP's code from Haskell to OCaml.

### Academic Papers

See [academic papers relevant to OCaml](papers.md).

