---
tags: [learning]
---

# Learning

## Beginner

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

### Setting Up Your Editor for OCaml

OCaml can be edited conveniently with many different editors. See [Editor Support](editor_support.md).

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

## Intermediate

### The Format Module

The Stdlib has the [Format](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Format.html)
module for pretty printing.
It's a little tricky to get a hang of.
* [Tutorial](https://ocaml.org/learn/tutorials/format.html)
* [Blog post on Format](https://cedeela.fr/format-all-the-data-structures.html)
* [Paper](https://hal.archives-ouvertes.fr/hal-01503081/file/format-unraveled.pdf) on Format

### Tools
* [Fuzzing OCaml programs](https://tarides.com/blog/2019-09-04-an-introduction-to-fuzzing-ocaml-with-afl-crowbar-and-bun.html)
 
## Advanced

### Modules and Functors

* [A Very Basic Introduction to Functors](functors.md)

### Polymorphism

* [OCaml polymorphism examples](http://stackoverflow.com/questions/14440531/ocaml-polymorphism-example-other-than-template-function)
* [OCaml - polymorphic print and type erasure](http://stackoverflow.com/questions/7442449/ocaml-polymorphic-print-and-type-losing)
* [Weak Type Variables - when impurity breaks polymorphism](weak_type_variables.md)

### GADTs

* [Diff Lists](https://drup.github.io/2016/08/02/difflists/):
An application of GADTs to produce heterogenous lists.
* [Detecting use-cases for GADTs](https://mads-hartmann.com/ocaml/2015/01/05/gadt-ocaml.html)
* [Tradeoffs with GADTs](https://engineering.issuu.com/2015/09/17/gadt-practicalities)
* [Why GADTs matter for performance](https://blog.janestreet.com/why-gadts-matter-for-performance/)

### Phantom Types

* [Article from Jane Street](https://blog.janestreet.com/howto-static-access-control-using-phantom-types/)

### Iterators
* [Article](http://gallium.inria.fr/blog/generators-iterators-control-and-continuations/)

### PPX (PreProcessor eXtensions)

* [A Guide to PreProcessor eXtensions](ppx.md)
* [A PPX Tutorial](https://www.victor.darvariu.me/jekyll/update/2018/06/19/ppx-tutorial.html)

### FFI (Foreign Function Interface)

* See [FFI](ffi.md) for different options. `Ctypes` or `ppx_cstruct` is the recommended approach nowadays.
* [Article on wrapping C functions from OCaml by hand](http://www.linux-nantes.org/~fmonnier/OCaml/ocaml-wrapping-c.html):
If you want to get down and dirty, doing it yourself.
May be necessary for some library wrappers.

### Monads

* [Xavier Leroy's Monadic Programming Lecture Slides (pdf)](https://xavierleroy.org/mpri/2-4/monads.pdf) and [code](https://xavierleroy.org/mpri/2-4/monads.ml)
* [Cornell's CS 3110 Lecture about monads](https://www.cs.cornell.edu/courses/cs3110/2018sp/l/25-monads/lec.pdf), with [code](https://www.cs.cornell.edu/courses/cs3110/2018sp/l/25-monads/code.ml) and [recitation](https://www.cs.cornell.edu/courses/cs3110/2018sp/l/25-monads/lab.html)
* [A small monads tutorial from the Monads library](http://binaryanalysisplatform.github.io/bap/api/master/Monads.Std.html#intro)
* [Discussion on what you can do with Monads](https://discuss.ocaml.org/t/can-monads-help-me-my-refactor-code-for-an-enhanced-data-structure/1064/5?u=ivg) and what are [Monad Transformers](https://discuss.ocaml.org/t/ann-monads-the-missing-monad-transformers-library/830/6?u=ivg)
* [Monadic Error Handling](https://medium.com/@huund/monadic-error-handling-1e2ce66e3810)
* [More Typeclasses in OCaml](http://blog.shaynefletcher.org/2017/05/more-type-classes-in-ocaml.html)

### Category Theory

Category Theory is a branch of abstract mathematics that discusses concepts
that tend to pop up as patterns in functional programming.

* [First steps with Category Theory and OCaml](http://www.mseri.me/typeclass-ocaml/):
Focuses on Monoids and Applicatives.
* [Category Theory For Programmers](https://github.com/hmemcpy/milewski-ctfp-pdf):
Not OCaml-specific, but a good book to learn Category Theory from.
* [Category Theory For Programmers in Ocaml](https://github.com/ArulselvanMadhavan/ocaml-ctfp):
An ongoing work to translate CTFP's code from Haskell to OCaml.

### Writing Efficient Code
See [Optimizing OCaml Performance](optimizing_performance.md).

### Papers
See [Papers on OCaml](papers.md).

## Articles

* [Python to OCaml: retrospective](http://roscidus.com/blog/blog/2014/06/06/python-to-ocaml-retrospective/)
* [Xen – OCaml Coding Considerations](http://wiki.xen.org/wiki/OCaml_Coding_Considerations)
* [A blog about game development in OCaml](http://cranialburnout.blogspot.ca/)
* [(Functional) Alternatives to inheritance](http://ocamltutorials.blogspot.se/2013/06/alternatives-to-subtyping.html)
* [Higher-Rank Polymorphism in OCaml](http://devmusings.legiasoft.com/blog/2008/05/23/higher-rank_polymorphism_in_ocaml)
* [mikmatch](https://github.com/mjambon/mikmatch)  – OCaml pattern-matching extended with regexps
* [Inlined records in constructors](http://www.lexifi.com/blog/ocaml/inlined-records-constructors)
* [Algebraic Data Types](https://espertech.wordpress.com/2014/07/30/algebraic-data-types/)
* [A safe but strange way of modifying OCaml compiler](https://bitbucket.org/camlspotter/compiler-libs-hack)
* [Fiddling with the OCaml Type System](http://technotroph.wordpress.com/2013/10/25/fiddling-with-the-ocaml-type-system/)
* [Quick and Dirty Guide to Monadic Parsers and Angstrom](monadic-parsers-angstrom.md)

## Projects

A list of projects that can be used as examples or for inspiration.

See [Projects](projects.md)

## Exercises

* [99 problems](http://ocaml.org/learn/tutorials/99problems.html): classic 99 problems, with solutions.
* [Rosetta Code](http://rosettacode.org/wiki/Category:OCaml)
* [OCaml at Exercism](http://exercism.io/languages/ocaml)  – Exercism is your place to engage in thoughtful conversations about code. Explore simplicity, idiomatic language features, and expressive readable code.
  [Solutions](https://github.com/exercism/xocaml).

## Books

* [Real World OCaml](https://dev.realworldocaml.org/)  by Y. Minsky, A. Madhavapeddy and J. Hickey - Functional programming for the masses. The latest, and arguably the most readable book on OCaml. Note that the book uses only Jane Street libraries, but the material can be applied to other libraries.
  * [RWO-lwt](https://github.com/dkim/rwo-lwt) : translating the Async code examples from Real World OCaml to lwt.
* [Free Cornell OCaml Textbook](http://www.cs.cornell.edu/courses/cs3110/2019sp/textbook/):
Great free online book, covering both beginner and advanced topics.
* [More OCaml: Algorithms, Methods, and Diversions](http://www.amazon.com/More-OCaml-Algorithms-Methods-Diversions/dp/0957671113/)  – In More OCaml John Whitington takes a meandering tour of functional programming with OCaml, introducing various language features and describing some classic algorithms. The book ends with a large worked example dealing with the production of PDF files. There are questions for each chapter together with worked answers and hints.
* [How to Think Like a (Functional) Programmer](http://www.greenteapress.com/thinkocaml/index.html)  by Allen Downey and Nicholas Monje – How to Think Like a Computer Scientist is an introductory programming textbook based on the OCaml language. It is a modified version of Think Python by Allen Downey. It is intended for newcomers to programming and also those who know some programming but want to learn programming in the function-oriented paradigm, or those who simply want to learn OCaml.
* [OCaml from the Very Beginning](http://ocaml-book.com/)  by J. Whitington - OCaml from the Very Beginning will appeal both to new programmers, and experienced programmers eager to explore functional languages such as OCaml.
* [Pearls of Functional Algorithm Design](http://www.amazon.co.uk/Pearls-Functional-Algorithm-Design-Richard/dp/0521513383)  by Richard Bird - It summaries 30 hard algorithm problems in function programming world. Although it is for Haskell, the algorithm problems are very interesting and trying to solve them in OCaml also helps the thinking of functional programming. Partial solutions in OCaml are [https://github.com/MassD/pearls here].
* [Unix System Programming in OCaml](http://ocamlunix.forge.ocamlcore.org/)  by X. Leroy and D. Rémy – Introduction to Unix system programming, with an emphasis on communications between processes.
* [Using, Understanding, and Unraveling OCaml](http://caml.inria.fr/pub/docs/u3-ocaml)  – This book describes both the OCaml language and the theoretical grounds behind its powerful type system.
* [Purely Functional Data Structures](http://www.amazon.co.uk/Purely-Functional-Structures-Chris-Okasaki/dp/0521631246/ref=sr_1_1?ie=UTF8&qid=1406279836&sr=8-1&keywords=functional+data+structures) : A classic book focusing on various data structures in the functional programming world. Can be very useful for understanding functional data structures, though OCaml obviously supports imperative data structures as well.
* [OCaml for Scientists](http://www.ffconsultancy.com/products/ocaml_for_scientists/)  - by Jon Harrop.
* [Types and Programming Languages](https://www.cis.upenn.edu/~bcpierce/tapl) by Benjamin C. Pierce - A friendly
but serious book on types, type checking, etc.  Much of what's covered is relevant to OCaml.  Several chapters present
OCaml implementations of the concepts covered in preceding chapters, and the examples in the book have been typechecked
using OCaml programs that are available at the author's site. (As of mid-2018, the Kindle version can be difficult to read on small
devices because the pages are images of the hardcover's pages.  The iBook version is a standard e-book with resizable fonts,
though.)
* [Advanced Topics in Types and Programming Languages](https://www.cis.upenn.edu/~bcpierce/attapl/index.html) is an anthology edited by Benjamine C. Pierce.  It includes some articles that are relevant to OCaml.

## Online Courses

* [Introduction to Functional Programming in OCaml](https://www.fun-mooc.fr/courses/parisdiderot/56002S02/session02/about) .
* [Cornell University – Data Structures and Functional Programming](http://www.cs.cornell.edu/Courses/cs3110/2014fa/course_info.php) .
* [Princeton University - Functional programming in OCaml](http://www.cs.princeton.edu/~dpw/courses/cos326-12/) .
* [University of Illinois](https://courses.engr.illinois.edu/cs421/fa2014/)  - Course that uses OCaml to teach functional programming and programming language design
