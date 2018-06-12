---
tags: [learning]
---

# OCaml subtleties
**Subtle points and items difficult to find via web search** (in progress)

Also see Pierre Weis's [Frequently asked Questions about Caml](http://caml.inria.fr/pub/old_caml_site/FAQ/FAQ_EXPERT-eng.html).

## Gotchas

* **Polymorphic compare**: TODO (bluddy will fill in.)

* **Semicolons and `if` statements**: TODO (I can fill this
  in later unless someone else is inspired to do it first. -mars0i)

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

  Part of the answer is that `'_weak1`, `'_weak2`, etc., which are called "weak type variables", are roughly speaking, only *temporarily* [polymorphic](http://ocaml.org/learn/tutorials/basics.html#Polymorphic-functions) types (unlike `'a`, etc.).  If an expression type includes a weak type variable, the compiler will permanently substitute the variable with a regular concrete (i.e., monorphic) type (e.g. `float list`) the first time that it sees an application of the function.
  
  In OCaml and other ML-style languages that support mutability, only _values_ can have polymorphic types, hence the name -- "value restriction". The underlying reason, is that if an expression is mutable (an since we don't know its type, we must assume that it is mutable), then it could be assigned multiple times, each time with a value of a different type, thus we can't guarantee that the type of a value would be preserved. That will eventually break the type soundness. 
  
  Originally, values were defined as syntatic constants. I.e., something that is a static constant on the source level, is considered a value, e.g., `1`, `"hello"`, `None`, `fun x -> x`. However, in OCaml this restriction is relaxed, and besides syntactic constants OCaml allows some other classes of expressions to be generalized (i.e., to have the polymoprhic type). First of all, OCaml allows polymorphism for _non-expansive_ expressions, where an expression is non-expansive if it doesn't have any observable side-effects during the evaluation. That basically extends the notion of constant from purely syntactic definition (something that looks like a constant, is a constant) to semantic definition (something that acts like a constant, is a constant). For example, this restiction allows the following expressions to have polymorphic type: `lazy None`, ` let _ = ref None in 1`, `assert false`. But that's not all, OCaml is able to prove that it is safe to generalize certain type variables, by performing their variance analysis. It was [observed]((https://caml.inria.fr/pub/papers/garrigue-value_restriction-fiwflp04.pdf)) that there is a nice interaction between subtyping, variance, and value restriction. If a value occurs only in covariant positions, then it can be safely generalized and given the polymorphic type. With this rule, it is possible to give the polymorphic type to the following expressions: `fun () -> []`, `fun () -> ref None`. 
  
  The value restriction is a pessimistic assumption that a compiler must make in the face of the possible mutability, and is a price that must be payed even if mutability is not used. Weak type variables alleviate the problem a little, by allowing us to omit type annotations for values that don't have concrete or polymorphic type. However, since types are analyzed on the compilation unit level (the file level), weak type variables can't escape the scope of a compilation unit (the scope of a file). So it is not possible to have a weak type variable in the module interface (e.g., in the `mli` file). Compiler will reject all toplevel definitions that have weak types, unless they are either hidden from the module interface (i.e., omitted in the interface - e.g., when the mli file is empty) or given a concrete type. 

  If for some reason compiler refuses to generalize your expression and weak type variables occur in your type, then you can try the following options to fix the situation:
  - Convert your expression to a syntactic constant, by making it a function, aka eta-expansion. E.g., `let x = ref None` could be made polymorphic by making `x` a function, e.g., `let x () = ref None` 
  - If the problematic type is abstract, then a compiler can't perform the variance analysis on it. You can expose, that some type variables of your abstract type are covariant, by making the variance annotations, e.g., `type +'a t` in the signature will tell the compiler that values of that type could be safely given the polymorphic type. (Of course, the definition should correspond to the specification, that is checked by the compiler, for example, `type +'a t = 'a list` would be accepted by the type checker, where `type +'a t = 'a ref` will be rejected). 
  - If nothing else helps, then you need to manually annotate your value with a ground type or hide from the interface. 

  **Further reading**:
  - [Side effects and weak polymorphism](https://realworldocaml.org/v1/en/html/imperative-programming-1.html#side-effects-and-weak-polymorphism) in *Real World OCaml*,
  - [Section 5.1 Weak polymorphism and mutation](http://caml.inria.fr/pub/docs/manual-ocaml/polymorphism.html#sec51) 
  in the OCaml Manual, 
  - [Common Error Messages](http://ocaml.org/learn/tutorials/common_error_messages.html#The-type-of-this-expression-contains-type-variables-that-cannot-be-generalized) at ocaml.org,
  - ["My function is not polymorphic (enough) ?"](http://caml.inria.fr/pub/old_caml_site/FAQ/FAQ_EXPERT-eng.html#eta_expansion) and subsequent sections in "Frequently asked Questions about Caml".
  
  

## Bits of syntax

* **Printf directives**: Where can I find a list of `printf`, `sprintf`,
  etc. directives such as `%s`, `%b`, `%d`, `%f`, etc.?  
  
  See the [Printf
  module documentation](http://caml.inria.fr/pub/docs/manual-ocaml/libref/Printf.html)
  in the OCaml Manual.

* **Infix operators**: Where can I find documentation on standard infix
  operators such as `@@`?
  
  See the [Index of values](http://caml.inria.fr/pub/docs/manual-ocaml/libref/index_values.html) or the [Pervasives module
  documentation](http://caml.inria.fr/pub/docs/manual-ocaml/libref/Pervasives.html)
  in the OCaml Manual.  For the Pervasives module docs, you'll want to search the page for "operator" 
  or for the specific operator you're interested in.
  
  (Also possibly useful: [Built-in operators and functions](https://www2.lib.uchicago.edu/keith/ocaml-class/operators.html)
  at *OCaml for the Skeptical*, and (very old) [Infix symbols](https://caml.inria.fr/pub/docs/manual-caml-light/node4.9.html) in the old CAML light manual.)

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
