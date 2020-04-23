# Iterators

## Available Options

* As of 4.07, OCaml has a built-in
[Seq](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Seq.html)
type, which every Stdlib data structure can convert to and from.
Technically, this is a generator.
Making use of this type will increase performance when running
multiple-stage operations on data.
* [OSeq](https://github.com/c-cube/oseq/blob/master/src/OSeq.mli):
Expanded functionality for the stdlib's `seq` type.
For example, creation of a sequence using a range of numbers,
and then folding over that sequence.
* [iter](https://github.com/c-cube/iter):
A lighter alternative to `seq`, using iterators rather than generators.
Since `iter` doesn't allocate anything except a closure,
with `flambda` on, `iter`'s performance matches that of a `for` loop.
* The alternative [Standard Libraries](standard_libraries.md) have their own iterator types.

## Explanation

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
let l1 = [1; 2; 3]
  |> List.map (fun x -> x + 1)
  |> List.map (fun x -> x * 3)
```

In this example, each stage of the computation needs to be materialized, causing allocation.
Instead, we can do

```ocaml
let l1 = List.to_seq [1; 2; 3]
  |> Seq.map (fun x -> x + 1)
  |> Seq.map (fun x -> x * 3)
  |> List.of_seq
```

This version will not allocate the intermediate steps.

There are 2 main types of iterators: iterators and generators.
If you want to understand the differences between them,
[this article](http://gallium.inria.fr/blog/generators-iterators-control-and-continuations/)
does a good job of differentiating them.
