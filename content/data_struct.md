---
tags: [ecosystem]
---

# Data Structures and Algorithms

## Standard Library Data Structures

A major part of a standard library's role is providing basic
data structures and algorithms.
All the [standard libraries](standard_libraries.md) provide these:
* The [standard library](https://v2.ocaml.org/api/) contains basic data structures:
  List, Array, Immutable Map, Hashtable, Mutable Queue, Mutable Stack.
* [Base](https://github.com/janestreet/base) contains many additional data structures.
* [Containers](https://github.com/c-cube/ocaml-containers) is a data structure-oriented extension of the standard library.
* [Batteries Included](https://github.com/ocaml-batteries-team/batteries-included)
  is an older extension of the standard library with many data structures.
* [Vocal](https://github.com/vocal-project/vocal):
  A data structure library for OCaml, verified in Coq. See [here](http://www-verimag.imag.fr/VOCaL.html).

## Specific Data Structure Libraries

* [Ropes](https://github.com/Chris00/ocaml-rope):
Persistent, functional views on top of strings.
* [Patricia Trees](https://github.com/codex-semantics-library/patricia-tree):
implementation of high performance functional map.
* [Persistent Vectors](https://github.com/dbuenzli/pvec):
Data structures that behave similar to vectors but using immutable trees (of arrays).
* [baby](https://cambium.inria.fr/~fpottier/baby/doc/baby/):
Immutable sets and maps that perform better than the standard library's.
* [OCamlGraph](https://github.com/backtracking/ocamlgraph) is a library for
graphs and graph algorithms.
* [bimap](https://github.com/pat227/bimap):
Bi-directional map, from key to value and value-to-key.
* [ods](https://github.com/owainlewis/ods) is an algorithm/data structure library,
though it isn't as fully-featured as the standard libraries.
* [Discrete Interval Encoding Trees](https://github.com/djs55/ocaml-diet):
Useful for storing interval sets and testing membership efficiently.
* [Interval](https://github.com/Chris00/ocaml-interval):
An interval arithmetic library.
* [bitv](https://github.com/backtracking/bitv/):
A bit-vector library.
* [psq](https://github.com/pqwy/psq):
Functional priority search queues library.
* [bloomf](https://github.com/mirage/bloomf):
Fast [Bloom filter](https://en.wikipedia.org/wiki/Bloom_filter) library.
* [skip-list](https://github.com/UnixJunkie/slist):
Pure skip lists. Seems incomplete.
* [art](https://github.com/dinosaure/art):
Adaptive Radix Trees: speed of hashtables but based on an order.
* [bitmasks](https://github.com/metastack/bitmasks):
Use bitmasks as sets.

### Heterogeneous Maps

* [Containers](https://github.com/c-cube/ocaml-containers) (a standard library) contains the
[CCHet](https://c-cube.github.io/ocaml-containers/last/containers-data/CCHet/index.html) data structure, which
uses generative first-class modules on the inside to store values of different types.
* [hmap](https://github.com/dbuenzli/hmap):
Hmap is another variation of a heterogeneous map.
* [gmap](https://github.com/hannesm/gmap):
Allows for the creation of a heterogeneous map wrapped in a user-provided GADT.
As opposed to the above solution, the full closed universe of possible types to be stored
must be known by the user.
