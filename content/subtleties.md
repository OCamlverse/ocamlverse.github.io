---
tags: [learning]
---

# OCaml subtleties
**Subtle points and items difficult to find via web search** (in progress)

## Gotchas

* **Polymorphic compare**: TODO (bluddy will fill in.)

* **Semicolons and `if` statements**: TODO (I can fill this
  in later unless someone else is inspired to do it first. -mars0i)

* **Weak types**: What is "the value restriction"?
  Why do some of my type variables start with underscore?
  What is the difference between a function with (for example) type `'a -> 'b`,
  and one with type `'_weak1 -> '_weak2`?  Why am I getting a
  compiler error like these? (It worked when I tried it out in utop!)
  ```
  Values do not match:
    val foo : int -> int
  is not included in
    val foo : 'a -> 'a
  
  Values do not match:
    val foo : '_weak1 -> '_weak1
  is not included in
    val foo : 'a -> 'a
  ```

  Part of the answer is that `'_weak1`, `'_weak2`, etc., which are called
  "weak types" or "weakly polymorphic types", are roughly speaking, only *temporarily*
  polymorphic types (unlike `'a`, etc.).  If a function's type includes a weak type,
  the compiler will permanently replace the weak type with a regular concrete type
  (e.g. `float list`) the first time that it sees an application of the function.
  The errors above say that the type `'a -> 'a` specified by a signature is too general.
  The signature says that the function will work with any type, but the compiler
  thinks that your function might only work with a single input and output type
  (`int`, in the first error).  The value restriction is the name of the heuristic
  that the compiler uses to make this decision.  For more information see the section on
  [Side effects and weak polymorphism](https://realworldocaml.org/v1/en/html/imperative-programming-1.html#side-effects-and-weak-polymorphism)
  in *Real World OCaml*, or
  [Section 5.1 Weak polymorphism and mutation](http://caml.inria.fr/pub/docs/manual-ocaml/polymorphism.html#sec51) 
  in the OCaml Manual.

## Bits of syntax

* **Printf directives**: Where can I find a list of `printf`, `sprintf`,
  etc. directives such as `%s`, `%b`, `%d`, `%f`, etc.?  
  
  See the [Printf
  module documentation](http://caml.inria.fr/pub/docs/manual-ocaml/libref/Printf.html)
  in the OCaml Manual.

* **Infix operators**: Where can I find documentation on standard infix
  operators such as `@@`?
  
  See the [Pervasives module
  documentation](http://caml.inria.fr/pub/docs/manual-ocaml/libref/Pervasives.html)
  in the OCaml Manual.

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
  such as `Core` or `Batteries` that shadow many built-in definitions, using such
  a module as a way of providing an alternative standard programming environment.
  See the discussion at this OCaml PR: [Fix PR6638: "unused open" warning was incorrectly suppressed
  by "open!"](https://github.com/ocaml/ocaml/pull/1110).
