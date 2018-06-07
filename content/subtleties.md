# OCaml subtleties
Subtle points and items that are difficult to find via web search

* **Polymorphic compare**: TODO

* **The semicolon problem in `if` statements**: TODO (I can fill this
  in unless someone else is inspired to do it first. -mars0i)

* **`+'a`, `-'a`**: Why are some type variables prefaced by "+" or "-",
  as in
  ```OCaml type +'a` t ``` ?  These are called *variance annotations*;
  they're used to constain subtyping relations.  See
  https://blog.janestreet.com/a-and-a/ .

* **`open!`**: What is the difference between `open My_module` and
  `open!  My_module`?  Both make the values and types in `My_module` available.
  `open My_module` will trigger a warning if `My_module` overrides
  existing definitions.  `open!` suppresses this warning.  See
  [Overriding in open
  statements](http://caml.inria.fr/pub/docs/manual-ocaml/extn.html#sec250)
  from [Chapter 8 Language
  extensions](http://caml.inria.fr/pub/docs/manual-ocaml/extn.html) of
  the OCaml manual.  (At present `open!` also suppresses a warning
  indicating that no definitions in the opened module are used within
  `open!`'s scope.  There is some disagreement about this behavior; see
  the discussion at [unused open" warning was incorrectly suppressed by
  "open!"](https://github.com/ocaml/ocaml/pull/1110).)

* **Printf directives**: Where can I find a list of `printf`, `sprintf`,
  etc. directives such as `%s`, `%b`, `%d`, `%f`, etc.?
  See [Printf module documentation](http://caml.inria.fr/pub/docs/manual-ocaml/libref/Printf.html).

* **Infix operators**: Where can I find documentation on standard infix
  operators such as `@@`?  See the [Pervasives module
  documentation](http://caml.inria.fr/pub/docs/manual-ocaml/libref/Pervasives.html)
  in the OCaml manual.

* **ppx**: What are these `[%% ...]` and `[@@ ...]` expressions I see
  in people's code?  See [A Guide to PreProcessor eXtensions](ppx.md).
