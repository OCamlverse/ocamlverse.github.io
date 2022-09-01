---
tags: [learning, best practices]
---

# OCaml Documentation Guidelines

{% raw %}

This document aims to be the community-driven one-stop reference of how to write
good documentation for OCaml libraries.

## Background

When we want to publish a library for the public to use, the presence of a
documentation is a must. In fact, it can be the sole deciding factor of
whether a potential user will end up choosing to use the library in their
project.

As a small illustration, in an undocumented system, every user loses time
understanding the system (lost time is [O(n)][bigo]). On the other hand,
in a well-documented system, one person "lost" time documenting the system
but it saves time for all the other users (lost time is O(1)). That is a
rather good investment.

However, what makes a good documentation? How good is "good enough"? These
questions can be a rather confusing obstacle, particularly for the
less-experienced devs publishing their library for the first time and
still unfamiliar with OCaml documentation tools. But it shouldn't be that
way!

Writing documentation should be fun, easy, and rewarding. It should not be
an afterthought; instead, it should be included in the development phase,
because as we write docs we can gain useful feedback on how good our
library's design is from a user's perspective.

These things considered, it would be nice to have a guideline on how to
write good, effective documentation in the OCaml ecosystem. This document
aims to tackle that problem.

[bigo]: https://en.wikipedia.org/wiki/Big_O_notation

## Purpose

The purpose of this guideline is to provide a standard that can be referred
to by library authors to (ask contributors to) produce good docs.

This guideline is expected to evolve with the latest discovered practices,
language features, tooling features, and feedback from community. This document
maintain a changelog to track these changes.

# 1. Writing documentation

## Documentation <> Comments

The first thing that needs to be established is the difference between
documentation and comments. Elixir's [Writing Documentation][exdocs] guide
has a nice section explaining about this:

> Documentation is for users of your Application Programming Interface (API),
> be it your co-worker or your future self. Modules and functions must always
> be documented if they are part of your API.
>
> Code comments are for developers reading the code. They are useful to mark
> improvements, leave notes for developers reading the code (for example, you
> decided not to call a function due to a bug in a library) and so forth.
>
> In other words: documentation is required, code comments are optional.

[exdocs]: https://hexdocs.pm/elixir/master/writing-documentation.html

## Basic documentation syntax

OCaml documentation is written in the **OCamldoc** syntax. This is different
from the usual markdown that many other languages use. OCamldoc is much more
powerful than markdown, with distinguishing features such as cross-references
and target-specific formatting (e.g. for LaTeX).

Documentations are written as special comments wrapped in `(**` and `*)`. The
content is free-form text much like markdown but with different set of
formatting constructs.

The [OCamldoc manual][ocamldocman] includes the formal explanation of the
syntax, and we recommend familiarizing yourself with it.

Here is the table that maps common markdown syntax to the OCamldoc counterpart:

| Description             | Markdown         | OCamldoc         |
| ----------------------- | ---------------- | ---------------- |
| Section header          | `# text`         | `{0 text}`       |
|                         | `## text`        | `{1 text}`       |
|                         | `### text`       | `{2 text}`       |
|                         |                  | etc.             |
| Section header with labels (for cross-referencing) | _N/A_ | `{0:mylabel text}` |
| Bold text               | `**text**`       | `{b text}`       |
| Italic text             | `*text*`         | `{i text}`       |
| Link                    | `[text](url)`    | `{{: url} text}` |
| Inline code             | \`code\`         | `[code]`         |
| Code block              | \`\`\`code\`\`\` | `{[code]}`       |
| Target-specific content | _N/A_            | `{%latex: text %}` |
| Cross-reference         | _N/A_            | `{!name}`, `{!module:name}`, `{!type:name}`, `{!section:name}`, etc.
| Unordered lists         | - foo<br/>- bar<br />- baz | - foo<br/>- bar<br />- baz |
| Ordered lists           | 1. foo<br/>2. bar<br />3. baz | + foo<br/>+ bar<br />+ baz |
| Raw HTML                | _Directly_       | `{%html: ... %}` |
| Images                  | `![alt text](url)` | `{%html: <img src=.../> %}`}


Note that OCamldoc _the syntax_ is a different from OCamldoc _the tool_. The
latter is a documentation generation tool that understands OCamldoc syntax. We
are going to touch about documentation generation on the later section of this
document.

[ocamldocman]: https://caml.inria.fr/pub/docs/manual-ocaml/ocamldoc.html#sec349

## Recommendations

This section introduces several recommendations that should be followed on
writing library documentation.

### Write documentation in .mli files

This item recommends putting documentation in `.mli` files.

OCaml encourages people to separate the interface of a module from its
implementation. Interface go to files with `.mli` extension, while
implementation go to `.ml` files. Documentation is part of the interface
of a module, hence it is logical to put it on `.mli`s, unburdened by
implementation details.

This approach also has the benefit of organizability: as OCaml is a strict
language where order of declarations are important, putting docs in `.ml`
files means you will have less flexibility in organizing your doc comments.
`.mli` files do not have that restriction, and you may reorder at will.

Note that this does _not_ mean you should not have comments on `.ml` files.
Utilize comments on `.ml` files for implementation notes to help contributors.
See the "Documentation <> Comments" section above.

Example:

```ocaml
(* ----- BAD ----- *)
(* math.ml         *)

let add a b = a + b
(** [add a b] returns the result of a + b *)


(* ----- GOOD ----- *)
(* math.ml          *)

let add a b = a + b

(* math.mli         *)

val add : int -> int -> int
(** [add a b] returns the result of a + b *)
```

### Write introductory documentation for the toplevel module

This item recommends to utilize the special first comment of the module, which
is not attached to anything, to give introductory material for the module.

Keep the first paragraph of the documentation concise and simple, typically
one-line. Documentation tools such as [odig] may use the first line to generate
a summary of the module.

Unless the module is really trivial (which is not true for most of the time),
the next paragraph(s) should explain in greater detail:

1. what capabilities the module provides,
2. why/when we should use it,
3. usage examples, and
4. links/reference to sections in the documentation.

Example (taken from Daniel Bünzli's [Vg library][vg]&mdash;formatting
removed):

```ocaml
(** Declarative 2D vector graphics.

    Vg is a declarative 2D vector graphics library. In Vg, images are values
    that denote functions mapping points of the cartesian plane to colors.
    The library provides combinators to define and compose them. Renderers
    for PDF, SVG and the HTML canvas are distributed with the library. An
    API allows to implement new renderers.

    Consult the {{!basics}basics}, the {{!semantics}semantics} and
     {{!examples}examples}.

    Open the module to use it, this defines only modules and types in
    your scope and a single composition operator. *)
```

For usage examples, you may keep it on the introductory documentation or
introduce a new section linked from it. See "Write usage examples".

[odig]: https://github.com/dbuenzli/odig
[vg]: https://github.com/dbuenzli/vg/blob/master/src/vg.mli

### Organize signatures into logical sections

This item recommends to use sections liberally, particularly for modules with
many exported modules, types, and values. By grouping them into sections, we
gain the benefit of cohesive documentation elements being close to one another,
bringing better clarity of how things are organized.

The `.mli` file is basically a document much like a book, so feel free to
organize the contents to be as coherent as possible without caring about the
order of values in the implementation file.

An example would be Simon Cruanes' [iter] documentation, where the elements
are neatly organized into sections, such as "Build a sequence", "Consume a
sequence", etc. Another example is Daniel Bünzli's [Fmt][fmt] documentation.

Note that you can also add paragraphs after every section headers should you
deem it necessary.

[iter]: http://c-cube.github.io/iter/1.2/iter/Iter/index.html
[fmt]: https://erratique.ch/software/fmt/doc/Fmt/index.html

### Document all your signatures

This item recommends that all signatures (modules, types, functions, etc.)
should have a documentation attached to it. At the minimum, it should provide
a one-liner that explains what the function does. A better effort would be to
also add minimal usage examples for interesting functions.

The rationale of this recommendation is that undocumented values tend to give
the feeling of unfinished work and may prevent users from adopting the library.

Example (inspired by the [Jane Street Style Guide][jststyle]):

```ocaml
(* ----- BAD ----- *)

val compare : string -> string -> int

(* ----- BETTER ----- *)

val compare : string -> string -> int
(** Compares two strings *)

(* ----- GOOD ----- *)

val compare : string -> string -> int
(** [compare x y] compares the strings [x] and [y] lexicographically. *)
```

The above example also shows that it is recommended to start a function
documentation with a call to the function and naming the arguments (the
`[compare x y]` part). This gives you the benefit of being able to refer to
the variables in the doc text afterwards, especially when the function does
not accept labeled args.

The Jane Street Style Guide also has a reasonable point for writing docs for
trivial functions:

> If you really can’t find anything useful to add with a comment, it’s
> acceptable to have a comment that is redundant with the type and name.

The point is, we don't have to spend time to ask ourselves whether a
signature item warrants a documentation string or not. Just do it, even
if it feels entirely pointless and redundant it has to become a reflex.

We might find the semantics of a signature item obvious based solely on
its name, but that's just because _we_ implemented it. A reader not
familliar with the implementation may not find it so obvious.

[jststyle]: https://opensource.janestreet.com/standards/

### Put documentation comments after signature elements

This item recommends attaching documentation comments after the signature
item they represent, as shown in the previous examples.

OCaml supports putting documentation before or after signature elements.
Note that this might be foreign to some users of other languages that are
used to putting documentation _before_ the element they refer, but putting
it after the element has several benefits:

1. When you scan `.mli`s your eyes anchor on type, val, etc. keywords.
   Once you spotted the one of interest, the documentation then follows
   in the scanning direction, rather than having to switch directions.

2. That's the way they end up being presented by documentation generators
   (OCamldoc, odoc, explained later in this document), so there will be
   less cognitive dissonance when you switch from one to the other. A
   documentation generator output will then just be a prettified view of
   your `.mli`.

An exception to this rule is for the first toplevel documentation and for
inner-modules documentation. For the latter, documentation should go
before the module declaration.

This rule has the unfortunate caveat for variants: if you don't document
every case of the variant, then at least the last case would require to
have an empty comment block `(** *)` so that the following block will
be attached correctly to the whole variant.

Example (taken from [Alcotest] documentation):

```ocaml
type speed_level = [`Quick | `Slow]
(** Speed level for a test. *)

type 'a test_case = string * speed_level * ('a -> unit)
(** A test case is an UTF-8 encoded documentation string, a speed
    level and a function to execute. *)

val test_case: string -> speed_level -> ('a -> unit) -> 'a test_case
(** [test_case n s f] is the test case [n] running at speed [s] using
    the function [f]. *)

type 'a test = string * 'a test_case list
(** A test is an US-ASCII encoded name and a list of test cases. *)

exception Test_error
(** The exception return by {!run} in case of errors. *)
```

[alcotest]: https://github.com/mirage/alcotest

### Write usage examples

This item recommends that usage examples should be made required, especially
on non-trivial modules and functions.

Usage examples tend to give more clarity of how things work instead of relying
users to stitch ideas together from the disconnected API reference.

There are several ways to introduce usage examples in a module documentation:

1. Put it in the introductory toplevel documentation. This is preferable if the
   example is short enough and encompasses the usage of the whole module.

2. Put it in a different section (e.g. "Basics", "Examples", etc.), usually
   after the API reference, for longer examples and/or explanations. Requires
   to be linked from first toplevel documentation.

3. Put it in a function's documentation if the usage example is specific for
   a function.

4. Put it in separate manual (`.mld`) files if the usage examples span multiple
   toplevel modules.

When introducing example code blocks, use the `{[...]}` construct.

Small, runnable examples are good, but non-runnable illustrative examples are
better than none.

### Properly document deprecations

This item recommends properly documenting value deprecations. This includes:

- Annotating the docs with `@deprecated` tag
- Making note of what should be used instead (utilize cross-reference)
- (Optional) Making note of why it is deprecated

Deprecations are useful for moving the API forward, and annotating them can
make it easier for users to actually migrate out of the deprecated values.

Avoid adding `@deprecated` tag without providing alternative(s).

### Have meaningful README

This item recommends putting informative material in project READMEs.

Most libraries are hosted on public services such as GitHub, which by default
display the README on the main page. Such pages are often the first entry point
for users looking for a library to use. Hence, READMEs should be treated as
such, and should contain information that help such users decide whether they
should use a library.

At the very least, READMEs should include:

- The name of the library
- A short-ish description of the library (preferably not only a one-liner)
- Instruction to install the library
- Link to manual, usage examples, and online API documentation

It is good to have a (probably common) usage example written out on the README
to give visitors illustrative idea of how the library work. In fact, if you have
the resource, investing in making the README thorough is preferable, although
that would mean extra effort of keeping the README and API documentation in
sync.

# 2. Generating documentation

_This section is meant for library authors trying to preview their library's
documentation, but the same methods can be used by library users._

There are several tools related to generating documentation, and we're going to
give a quick look on how they interact together.

## OCamldoc

OCamldoc is a tool to generate documentation from source files. The official
user manual page [on documentation generator][ocamldoc] shows how to use it.

Note that the use of OCamldoc the tool is a bit discouraged at the moment due
to its deficiencies on handling some parts of the OCaml language, particularly
in regards to linking and references between modules and libraries.

[ocamldoc]: https://caml.inria.fr/pub/docs/manual-ocaml/ocamldoc.html

## odoc

[odoc] is also a documentation generator that aims to address the aforementioned
limitations of OCamldoc, and should be the go-to tool for documentation
generation.

That said, odoc is a low-level tool, and casual end-users should not need to
call it directly. Instead, we rely on higher-level tools that knows how to use
odoc to stitch together documentations, such as Dune, odig, and Topkg.

Even so, you will need to install odoc on your switch. You can install odoc
via opam:

```
opam install odoc
```

[odoc]: https://github.com/ocaml/odoc

## Dune (Jbuilder)

[Dune] (formerly Jbuilder) is a build system by Jane Street. It supports
generating documentations out of the box. To be able to generate documentation
for your Dune-powered projects (usually notable by the presence of `dune` or
`dune-workspace` files), you need to:

- make sure that `dune` and `odoc` are installed, and
- make sure that a `<package>.opam` file exists.

If you haven't already, install Dune and odoc:

```
opam install dune odoc
```

To generate the documentation, run this command:

```
dune build @doc
```

The documentation will then be available at
`_build/default/_doc/_html/index.html`. You may open it with your favorite web
browser.

For more on Dune, consult the [official docs][dunedocs].

[dune]: https://github.com/ocaml/dune
[dunedocs]: https://dune.readthedocs.io/en/latest/

## odig

[odig] is a documentation mining tool. Basically what it does is it scans the
installed packages on your current opam switch and tries to build their
documentations. What makes odig powerful is that, while Dune is good for
generating documentation for a single package, odig can actually cross-reference
modules and dependencies on the generated docs.

To start using odig, install the required packages:

```
opam install odig odoc ocaml-manual
```

Then, tell odig to generate the documentation for *all* installed libraries
using odoc.

```
odig odoc
```

Note that the above operation may take a while in switches with many packages!
It may also trigger warnings when trying to generate documentation for some
packages, but it can be safely ignored (for now).

Next step, open the documentation in your browser via:

```
odig doc
```

You will be presented with the index of installed libraries that you can browse
to get their API documentations.

Note that odig also supports generating and showing docs for a specific
library, by specifying the package name after the commands, e.g. to generate
and show docs only for the `lwt` library:

```
odig odoc lwt
odig doc lwt
```

Consult the [README page][odig] for more info.

## Topkg

[Topkg] is a packager for distributing OCaml software. Among other neat
features, it also supports generating documentation.

On a Topkg-powered projects (notable by the presence of `pkg/pkg.ml` file),
make sure that you have `topkg-care` (the Topkg CLI tool) installed:

```
opam install topkg-care
```

You can then invoke:

```
topkg doc
```

It will generate the documentation in the `_build/doc/api.docdir/` directory.

Consult the [basics][topkgbasics] section of the Topkg API documentation for
more info.

[topkg]: https://github.com/dbuenzli/topkg
[topkgbasics]: https://erratique.ch/software/topkg/doc/Topkg/index.html#basics

# 3. Putting documentation online

While generating docs locally may be beneficial in some cases, the requirement
of having the libraries installed or the source available (and dev environment
set up) to get the docs is not ideal. Consider users that are looking for a
library that do X, having to build and install multiple packages that provides
X-like capability.

Hence, **putting documentation online should be required for all libraries that
expect public use**.

One way to achieve that, if your library project is hosted on GitHub, is to
utilize the free [GitHub Pages][ghpages] feature. GitHub Pages support
multiple publishing source, such as the `master` branch, `gh-pages` branch,
and a `docs/` folder on `master` branch. Since `master` branch are reserved
for library code, feel free to choose one of the latter two. Consult the
[GitHub Pages documentation][ghpagesdocs] for more info.

After you chose a publishing source, you can put the generated documentation
achieved from the previous section there and push it. The docs should then be
online in no time.

If your project uses Topkg as a packager, the `topkg-care` tool also provides
the capability of doing those menial tasks of setting up the branch and copying
the files for you. It is as simple as invoking:

```
topkg distrib
topkg publish doc
```

It's also worth noting that works are in progress to bring forth a centralized
online documentation site (docs.ocaml.org, currently not available) for OCaml
libraries, which will make browsing docs significantly easier.

[ghpages]: https://pages.github.com/
[ghpagesdocs]: https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/

# Useful links

A collection of useful links, many of which are mentioned above.

- odoc [manual](https://ocaml.github.io/odoc/index.html)
- odoc's [advice for library authors](https://ocaml.github.io/odoc/odoc_for_authors.html)
- Dune [manual page](https://dune.readthedocs.io/en/stable/documentation.html) on generating documentation
- [odig](https://github.com/dbuenzli/odig) for generating local docs
- OCaml manual's chapter on [documentation comments](https://v2.ocaml.org/manual/doccomments.html)
- OCaml manual's chapter describing [ocamldoc](https://v2.ocaml.org/manual/ocamldoc.html)
- Section on comments from Jane Street's [style guide](https://opensource.janestreet.com/standards/#comments)
- Elixir's [writing documentation][https://hexdocs.pm/elixir/master/writing-documentation.html] guide


## Examples of good docs

These libraries illustrate many of the recommendations discussed above.

- [brr](https://erratique.ch/software/brr/doc/): in addition to each module having a clearly organized API, also provides a few [manuals](https://erratique.ch/software/brr/doc/#manuals) to help new users understand and get started with the library
- [Dream](https://aantron.github.io/dream/): includes introductory material and rationale, many examples, and logical organization of the API.  Also includes an extensive [tutorial](https://github.com/aantron/dream/tree/master/example#readme).
- [iter](https://c-cube.github.io/iter/1.4/iter/Iter/index.html): includes a nice introduction to the main module and `mli` files organized into logical sections
- [Vg](https://erratique.ch/software/vg/doc/Vg/index.html): combines high-level introductory material, examples, and detailed API docs

# Final words

Hopefully this guide can help improve the documentation of the whole OCaml
ecosystem. Great tools alone don't make good documentations&mdash;humans do.

Keep calm and write docs!

- Originally taken from
[Bobby Priambodo's document](https://github.com/bobbypriambodo/ocaml-documentation-guideline/blob/master/README.md)

{% endraw %}
