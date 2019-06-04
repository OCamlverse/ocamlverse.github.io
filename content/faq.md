---
tags: [learning]
---

# Frequently asked questions

Also see the [ocaml.org FAQ](http://ocaml.org/learn/faq.html)
and Pierre Weis's [Frequently asked Questions about Caml](http://caml.inria.fr/pub/old_caml_site/FAQ/FAQ_EXPERT-eng.html).

## General

* What is a "toplevel"?

  A/the "toplevel" is an OCaml term for a program that provides a prompt
  at which you can enter OCaml expressions and see what happens when they
  are evaluated.  In some languages this is known as a "REPL", a
  Read-Eval-Print loop. (It Reads what you enter, Evaluates it, and
  then Prints the result.)  Many people who use an OCaml toplevel use the
  `utop` toplevel.  It's more full-featured than the `ocaml` toplevel that
  comes with an OCaml compiler. You can also evaluate OCaml expressions in an
  editor or IDE, for example.  See the 
  [Code tools](https://github.com/OCamlverse/ocamlverse.github.io/blob/master/content/code_tools.md)
  page.

* Why are compound types such as `float list` and `int option` written with the "enclosing", polymorphic type last?

  There's no real reason, except that this is how it's always been done in OCaml.
  It might be a bad idea to change the syntax of types in a language that puts so much emphasis on
  types.  (Standard ML uses the same convention.  Since it and OCaml both developed from an earlier
  ML, it's likely that the convention predates OCaml.)
  
  However, the type syntax kind of makes sense if you think about English syntax:  A "passenger
  ship" is a ship that carries passengers.  An `int list` is a list that contains `int`s.
  (You could also write "list of integers" in English, but then you need to add the "of".)

* Why do OCaml's constructors not work like Haskell's, i.e. they can't be curried?

  Originally, there was thought of doing them that way. The implementation was more complicated though,
  and OCaml's module system makes it hard to deal with them. See the full answer
  [here](http://caml-list.inria.narkive.com/WUIPH06Z/why-can-t-i-use-constructors-as-functions).

* What does `+'a` and `-'a` mean?

  They indicate variance. See [this blog post](https://blog.janestreet.com/a-and-a/).

## OCaml Gotchas

* **Polymorphic compare**:
    OCaml's comparison functions - `=`, `<`, `>` etc. use structural comparison by default.
    This means that while they work on any type, they don't understand the meaning of the data,
    but instead rely on the layout of the data in memory.
    This is a problem, and most standard library replacements have disabled this feature by
    making standard polymorphic comparison work only on integers.

    To understand why this is a problem, let's think about how a `Map.t` is organized.
    `Map.t` uses a tree of variants to store its data.
    Suppose I store `1, 2, 3 and 4` in map `a`, in that order.
    Now suppose I store `4, 3, 2, 1` in map `b`, in that order.
    Content-wise, the maps are the same. But do their backing trees look the same? No.
    The semantic meaning of the maps don't match their structure, and in fact each logical
    `Map.t` can be backed by many possible structures in memory.
    This is a problem when comparing maps using the default comparisons.

    It's an even worse problem when you have a higher-order function, such as `find`.
    `find` will work fine on a list of integers, because integers can only have one
    possible structural representation each.
    But it will often fail if you pass it a list of maps.
    Even worse, if you pass it a list of hashtables, which are backed by arrays mixed
    with buckets of lists, the arrays will match, but once in a while, the lists will not,
    causing subtle, quite horrible bugs.

    This is why polymorphic comparison should never be used except in places where you know
    the code will not be changed (which is hard to predict).
    Even if you know what you're doing with your code today, someone will come and modify
    it someday and use your polymorphic comparison on a data structure that doesn't support it.

* **Semicolons and `if` statements with `let`**: 
When a `let` expression begins in the final branch of an `if` expression,
a semicolon will not terminate the `let`; instead the `let` expression will include 
the code that comes after the semicolon.  One might expect that the semicolon ends the
`if` expression, and that the code following it will execute *after* the entire `if` 
expression, but instead that code is part of the  `if` expression.  This can introduce
subtle bugs, although it is a consequence of the normal (and useful) scoping rule
for `let`.  To make the semicolon follow the entire `if` with the embedded `let`, wrap
the `let` expression in parentheses or `begin`/`end`.  For more, see
[if with semicolons](faq_if_semicolon.md).

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

## Syntax

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
  
  See [A Guide to PreProcessor eXtensions](ppx.md) or [A Tutorial to OCaml -ppx Language Extensions](https://www.victor.darvariu.me/jekyll/update/2018/06/19/ppx-tutorial.html).

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

