---
tags: [learning]
---

# Frequently asked questions

Also see [OCaml subtleties](subtleties.md), the [FAQ](http://ocaml.org/learn/faq.html) at ocaml.org, and Pierre Weis's [Frequently asked Questions about Caml](http://caml.inria.fr/pub/old_caml_site/FAQ/FAQ_EXPERT-eng.html).

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

* Why do OCaml's constructors not work like haskell's ie. they can't be curried?

  Originally, there was thought of doing them that way. The implementation was more complicated though,
  and OCaml's module system makes it hard to deal with them. See the full answer
  [here](http://caml-list.inria.narkive.com/WUIPH06Z/why-can-t-i-use-constructors-as-functions).
