# A Guide to PreProcessor eXtensions

Author: Perry Metzger @pmetzger

> This is a _very very_ rough work in progress. Please help the author
  improving it.

OCaml provides a _syntactic extension facility_ known as
PreProcessor eXtensions, or PPXs. They allow to add
entirely new syntax and features to
the OCaml language that would otherwise be impossible.
For example, the [`ppx_regexp`][ppx_regexp] package adds a **match**-like
construct that matches strings with regular expressions, like:

```ocaml
match%pcre somestring with
  | "^foo"       -> some_expression1
  | "(bar){2,3}" -> some_expression2
  | _            -> some_default
```

PPX extensions are implemented as OCaml programs which are plugged into the
compiler. The extensions look for small syntactic "hooks" that signal
that an extension should do its work. These syntactic signals that
extensions look for are defined by the OCaml language specification,
but mean nothing to the compiler itself without the plugin.

This document is presented in three parts. The first part gives a
brief informal explanation of how PPX extensions are used. The second
part gives some detail on how PPX works and the syntactic hooks OCaml
provides for use by PPX extensions.  The third section provides some
detail on how you can write new PPX extensions, and gives pointers to
other documentation that may be of interest to extension writers.

## How PPX extensions are used

We have already seen an example of the `ppx_regexp` extension, which
creates a version of the `match` construct that checks strings for
regular expression matches.

Another typical PPX extension is `ppx_deriving`, a family of
extensions that automatically generate code from OCaml data
structures. For example, if you add the annotation:

```ocaml
[@@deriving show]
```

to a data type, as in:

```ocaml
type point3d = float * float * float
[@@deriving show]
```

the `deriving show` plugin to `ppx_deriving` will construct a `show`
function for the `point3d` type that will pretty print it.

The standard OCaml compiler knows nothing about the `ppx_deriving`
extension, of course. The extension exists as a plug-in for the
compiler, and the compiler must be invoked in such a way as to run
that extension over your code.

The documentation for an extension will typically explain how to tell
the compiler how to invoke the plugin. (For example, for
`ppx_deriving` and its `show` component, one usually adds the flags
`-package ppx_deriving.show` when invoking `ocamlfind`.)

## How does a PPX extension work behind the scenes?

The OCaml compiler operates in several steps. When it reads your
program, the first thing it does is convert the OCaml code into an
internal data structure called an "Abstract Syntax Tree", or "AST."

When you add

```ocaml
[@@deriving show]
```

or syntax from the `lwt` extension

```ocaml
let%lwt foo = ...
```

or the like to your code, the OCaml compiler records the presence of
the `@@` or `%` or similar constructs in your code in the AST.

PPX syntactic extensions then walk the Abstract Syntax Tree looking
for constructs they are intended to respond to. (For example, the
`ppx_deriving` framework will look for attribute nodes labeled with
`@@deriving`, and the `ppx_regexp` extension will look for extension
nodes with the name `%pcre`.)

When they find such a construct, the extension can take fairly
arbitrary actions in response, though typically the extension will
rewrite a section of the the OCaml AST. (For example, `ppx_deriving`'s
`show` plugin will examine the AST of the type that has been annotated
`[@@deriving show]` and will then insert an appropriate `show`
function customized for the type into the AST.)

### Syntactic hooks for PPX extensions

Among other "hooks" are:

1. Operator names starting with a `#` character and containing more than
   one `#` character are reserved for extensions.
2. Int and float literals followed by an one-letter identifier in the
   range `[g..z|G..Z]` are reserved for extensions.
3. _Attributes_ [Insert explanation of attributes]
4. _Extension nodes_ [Insert explanation of extension nodes]

In addition, "Quoted" strings of the form `{|string|}` or
`{foo|string|foo}` are not per se reserved for extensions, but are
often of use in them because they allow for strings containing
unescaped `"` and similar characters.

## Writing PPX Extensions

_This section is woefully incomplete. Please help me turn
it into something useful! Send me specific suggestions for things it
should say._

A PPX is implemented as an executable that reads a binary serialized
form of the OCaml AST and writes out a transformed binary serialized
AST.

The OCaml compiler simply runs each of the PPX executables it has
been asked to invoke, feeding each one the serialized AST and getting
it back again.

Thus, a PPX simply manipulates the OCaml AST, nothing more and nothing
less, but it can manipulate the AST in quite arbitrary ways.

The OCaml AST is quite complicated, so the use of libraries intended
to aid the writing PPX extensions easy is nearly mandatory.

Another serious problem is that the OCaml AST format is not guaranteed
to remain the same between versions of the compiler. Indeed, the OCaml
AST does, in practice, change significantly enough between compiler
versions that without the use of tools, PPX extensions would break
with every compiler update.

It is therefore necessary to understand a bit both about the OCaml AST
and about the available PPX-writing libraries in order to successfully
write a PPX.

_Insert some explanation of suggested tools here, potentially focusing
on [ppxlib](https://github.com/ocaml-ppx/ppxlib)._


[ppxregexp]: https://github.com/paurkedal/ppx_regexp
