# Iterators And Streams

## Available Options

* As of 4.07, OCaml has a built-in
[Seq](https://v2.ocaml.org/api/Seq.html)
type, which every Stdlib data structure can convert to and from.
Technically, this is a generator.
Making use of this type will increase performance when running
multiple-stage operations on data.
However, this iterator still requires allocation for every data member.
One of the more efficient options below is therefore recommended instead.
* [OSeq](https://github.com/c-cube/oseq/blob/master/src/OSeq.mli):
Expanded functionality for the stdlib's `seq` type.
For example, creation of a sequence using a range of numbers,
and then folding over that sequence.
* [Iter](https://github.com/c-cube/iter):
A lighter alternative to `seq`, using iterators rather than generators.
Since `iter` doesn't allocate anything except a closure,
with `flambda` on, `iter`'s performance can match that of a `for` loop.
`iter` works best with the [Containers](https://github.com/c-cube/ocaml-containers) standard library,
made by the same author.
* The other alternative [Standard Libraries](standard_libraries.md) have their own iterator types.
* [Streaming](https://github.com/odis-labs/streaming):
An iterator library that has fast abstractions (especially `Streaming.Stream`),
but unlike `iter`, doesn't require mutable state internally,
and has resource cleanup built-in at the cost of some additional complexity.
[docs](https://odis-labs.github.io/streaming/streaming/index.html).


## Explanation

Functional languages tend to use immutable data structures and transform them with functions.
This makes reasoning about the code easier, but it has the unfortunate side-effect of
creating many allocations, and allocations are expensive.
In general, if you're coding something that needs to be fast, you'll get a huge performance
boost from *not* tranforming into a full data structure until you need your data to
use certain properties only available in that data structure
(e.g. looking up a value using a key with Map).
Until you reach that point though, you want to use iterators instead.

The classic example is something like the following:

```ocaml
(* version A: pure lists *)
let l1 = [1; 2; 3]
  |> List.map (fun x -> x + 1) (* step 1 *)
  |> List.map (fun x -> x * 3) (* step 2 *)
```

In this example, each stage of the computation needs to be materialized fully,
causing a lot of simultaneous allocation.
Instead, we can use

```ocaml
(* version B: Seq *)
let l = List.to_seq [1; 2; 3]
  |> Seq.map (fun x -> x + 1) (* step 1 *)
  |> Seq.map (fun x -> x * 3) (* step 2 *)
  |> List.of_seq
```

Note that this version will *still* allocate in the intermediate steps 1 and 2,
but total memory consumption in the intermediate steps will remain lower than in version A above.
If we want to remove intermediate allocations altogether, we can use the
[Iter](https://github.com/c-cube/iter) library:

```ocaml
(* version C: Iter *)
let l = Iter.of_list [1; 2; 3]
  |> Iter.map (fun x -> x + 1) (* step 1 *)
  |> Iter.map (fun x -> x * 3) (* step 2 *)
  |> Iter.to_list
```

Note that `Iter` is less flexible than `Seq`, but is much faster due to its lack of allocations.

## Iterator vs Generator Internals

There are 2 main types of iterators for functional languages: iterators and generators.
[This article](http://gallium.inria.fr/blog/generators-iterators-control-and-continuations/)
does a good job of explaining the differences in how they're built.

## Comparison of Iterators

Two choices currently exist for iterators: `Iter` and `Streaming.Stream`.
Performance-wise, both libraries are quite similar (and close to optimal), making either one a good choice.
`Iter` benefits from extra simplicity, including, since it's a structural, non-abstract type -- there's no need
to actually import the `Iter` library for a data structure to use it.
`Streaming.Stream` avoids inner mutable types, but they're essentially hidden from the user at the `Iter` level.
`Streaming.Stream` also has resource cleanup as part of its design,
for example when streaming from a file or socket.
For `Iter`, resource cleanup is not built in, and
usage of a `with_resource` function is required for resource cleanup.

## Recommendations

Since iterators are chosen for performance,
the best performing iterators are `Iter` and `Streaming`,
particularly with flambda turned on (`-O3`).
If either one of these fits your application, it's the optimal choice.
If your usage prevents you from using these iterators, the stdlib's `Seq` may be used,
preferably using `OSeq`'s expanded functionality.
