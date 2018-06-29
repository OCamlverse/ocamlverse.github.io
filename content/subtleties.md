---
tags: [learning]
---

# OCaml subtleties
**Subtle points and items difficult to find via web search** (in progress)

Also see Pierre Weis's [Frequently asked Questions about Caml](http://caml.inria.fr/pub/old_caml_site/FAQ/FAQ_EXPERT-eng.html).

## Gotchas

* **Polymorphic compare**: TODO (bluddy will fill in.)

* **Semicolons and `if` statements with `let`**: 
When a `let` expression begins in the final branch of an `if` expression,
a semicolon will not terminate the `let`; instead the `let` expression will include 
the code that comes after the semicolon.  One might expect that the semicolon ends the
`if` expression, and that the code following it will execute *after* the entire `if` 
expression, but instead that code is part of the  `if` expression.  This can introduce
subtle bugs, although it is a consequence of the normal (and useful) scoping rule
for `let`.  To make the semicolon follow the entire `if` with the embedded `let`, wrap
the `let` expression in parentheses or `begin`/`end`.  For more, see
[if with semicolons](subtleties_if_semicolon.md).

* **Weak type variables**: What is "the value restriction"?
  Why do some of my type variables start with underscore?
  What is the difference between a function with (for example) type `'a -> 'b`,
  and one with type `'_weak1 -> '_weak2`?  Why am I getting a
  compiler error like these? (It worked when I tried it out in utop!)
  ```
  Values do not match:
    val foo : '_weak1 -> '_weak1
  is not included in
    val foo : 'a -> 'a
  ```
  This means that your function (or any other value that gets this type) is not really polymorphic, 
and the compiler doesn't have enough information to infer its concrete type, thus it represents the unknown
parts of the type with so called "weak type variables", the placeholders the need to be filled in by you.
(The compiler will do it itself, if possible, but when you see the weak type in the error produced by 
the compiler, it means that it wasn't possible, and your help is needed). 

  The [Weak Type Variables](weak_type_variables.md) article describes in detail why they exist in OCaml and
how to cope with them.   

## Bits of syntax

* **Printf directives**: Where can I find a list of `printf`, `sprintf`,
  etc. directives such as `%s`, `%b`, `%d`, `%f`, etc.?  
  
  See the [Printf
  module documentation](http://caml.inria.fr/pub/docs/manual-ocaml/libref/Printf.html)
  in the OCaml Manual.

* **Infix operators**: Where can I find documentation on standard infix
  operators such as `@@`?
  
  For general documentation on operators, see the OCaml manual: [Operators](https://caml.inria.fr/pub/docs/manual-ocaml/expr.html#sec151)
  in the Expressions section, [Index of values](http://caml.inria.fr/pub/docs/manual-ocaml/libref/index_values.html), or the 
  [Pervasives module documentation](http://caml.inria.fr/pub/docs/manual-ocaml/libref/Pervasives.html).  For the Pervasives document,
  you'll want to search the page for "operator" or for the specific operator you're interested in.
  
  For operator precedence and associativity, see the [Expressions](https://caml.inria.fr/pub/docs/manual-ocaml/expr.html)
  section of the manual, and scroll down past the BNF syntax specification or search for "Construction or operator".  The 
  Pervasives module also specifies precedence and associativity in the documentation for each operator.
  
  (Also possibly useful: [Built-in operators and functions](https://www2.lib.uchicago.edu/keith/ocaml-class/operators.html)
  at *OCaml for the Skeptical*.)

* **ppx**: What are these `[%% ...]`, `[@@ ...]` expressions that I
  see in people's code?  What does it mean when there's a percent sign in the 
  middle of a name, as in `let%lwt`? What are extension points?
  
  See [A Guide to PreProcessor eXtensions](ppx.md).

* **+'a, -'a**: Why are some type variables prefaced by "+" or "-",
  as in `type +'a t`?
  
  These are called "variance annotations".  They're used to constrain
  subtyping relations.  See [+'a and
  -'a](https://blog.janestreet.com/a-and-a) at the Jane Street Tech
  Blog.

* **open!**: What's the difference between `open My_module` and
  `open! My_module`?
  
  Both make the values and types in `My_module` available without having
  to write "My_module." in front of them.  `open My_module` will trigger
  a warning if `My_module` overrides existing definitions.  `open!` suppresses
  this warning.  See [Overriding in open statements](http://caml.inria.fr/pub/docs/manual-ocaml/extn.html#sec250)
  from [Chapter 8 Language extensions](http://caml.inria.fr/pub/docs/manual-ocaml/extn.html) in
  the OCaml manual.  
  
  At present `open!` also suppresses another warning as well.  This is a warning
  that no definition in the opened module is in fact used within
  `open!`'s scope.  There is some disagreement about whether this behavior
  is desirable.  Those who use `open!` for this purpose use it to open modules
  such as `Core`, `Batteries`, or `Containers` that shadow many built-in definitions, using such
  a module as a way of providing an alternative standard programming environment.
  See the discussion at this OCaml PR: [Fix PR6638: "unused open" warning was incorrectly suppressed
  by "open!"](https://github.com/ocaml/ocaml/pull/1110).
