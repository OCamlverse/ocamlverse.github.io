# Iterators

Functional languages tend to use immutable data structures and transform them with functions.
This makes reasoning about the code easier, but it has the unfortunate side-effect of
creating many allocations, and allocations are expensive.
In general, if you're coding something that needs to be fast, you'll get a huge performance
boost from *not* tranforming into a full data structure until you need your data to
use certain properties only available in that data structure
(e.g. looking up a value using a key with Map).
Until that point, you want to use iterators instead.
The classic example is something like

```ocaml
let l1 = [1; 2; 3] |>
  List.map (fun x -> x + 1) |>
  List.map (fun x -> x * 3)
```

In this example, each stage of the computation needs to be materialized, causing allocation.
Instead, we can do

```ocaml
let l1 = List.to_seq [1; 2; 3] |>
  Seq.map (fun x -> x + 1) |>
  Seq.map (fun x -> x * 3) |>
  List.of_seq
```

This version will not allocate the intermediate steps.

There are several possible types of iterators.
If you want to understand the differences between them,
[this article](http://gallium.inria.fr/blog/generators-iterators-control-and-continuations/)
does a good job of differentiating them.

* As of 4.07, OCaml has a built-in
[Seq](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Seq.html)
type, which every Stdlib data structure can convert to and from.
Making use of this iterator type will greatly increase performance when doing
whole-datastructure operations such as maps.
* Additionally, the [Standard Libraries](standard_libraries.ml) have their own iterator types which
act similarly.
* For example, Containers has 2 different iterator types, `gen` and `sequence`, each of which
works slightly differently.
