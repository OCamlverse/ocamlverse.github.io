# Data Structures and Algorithms

## Standard Library Data Structures

A major part of a standard library's role is providing basic
data structures and algorithms.
All the [standard libraries](standard_libraries.md)
(Containers, Base, Core and Batteries) provide these.

## Specialized Data Structures

* [OCamlGraph](https://github.com/backtracking/ocamlgraph) is a library for
graphs and graph algorithms.
* [ods](https://github.com/owainlewis/ods) is an algorithm/data structure library,
though it isn't as fully-featured as the standard libraries.
* [Discrete Interval Encoding Trees](https://github.com/djs55/ocaml-diet):
Useful for storing interval sets and testing membership efficiently.
* [Interval](https://github.com/Chris00/ocaml-interval):
An interval arithmetic library.
* [bitv](https://github.com/backtracking/bitv/):
A bit-vector library.

### Heterogeneous Maps

* [Containers](https://github.com/c-cube/ocaml-containers) (a standard library) contains the
[CCHet](https://c-cube.github.io/ocaml-containers/last/containers/CCHet/index.html) data structure, which
uses generative first-class modules on the inside to store values of different types.
* [hmap](https://github.com/dbuenzli/hmap):
Hmap is another variation of a heterogeneous map.
* [gmap](https://github.com/hannesm/gmap):
Allows for the creation of a heterogeneous map wrapped in a user-provided GADT.
As opposed to the above solution, the full closed universe of possible types to be stored
must be known by the user.
