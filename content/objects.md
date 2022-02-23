---
tags: [compiler]
---

# Object-Oriented Programming in OCaml

## Implementation of Objects

(from [here](https://discuss.ocaml.org/t/actual-performance-costs-of-oop-objects/9400/11))
Each object comes with its own map from method labels to closures. The map is implemented using an array of two-word cells,
one word for the key and one word for the values. Keys are ordered, so looking up a given method from the associated label is a dichotomic search.
For each method call in the generated code, a global cache entry is generated that will hold the last index found by dichotomic search at this particular call.
So the next dichotomic search can be skipped if the index from the cache points to the correct label.
This happens fairly often if you don’t have too many different classes/raw objects implementing the same signature.
But that’s also all the cache saves you: a few iterations of a short loop.
