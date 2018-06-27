# Design Principles For Stdlib 2.0

## Design Goals
* Create a more user-friendly, modern interface for OCaml's stdlib.
* Keep data structure compatibility.
* Lay out good principles for API design.
* Keep the underlying machinery for OS interaction stable.
* Controversial: avoid polymorphic comparison.

## Hypothetical Module List

This is a hypothetical list of modules that would be included in the V2 stdlib:

### Data Structures

* List
* Array
* BigArray
* String
* Bytes
* Buffer
* BigString?
* Map
* Hashtbl
* Hashtrie?
* Stack
* Queue
* FQueue (functional queue)?
* FStack (functional stack)?
* Vector
* WeakArray? (from Weak)
* WeakHash? (from Weak)

### Data Types

* Int/32/64/NativeInt
* Float
* Bool
* Char?
* Uchar (expanded)
* Option
* Result
* Lazy

### OS

* Path
* File
* Dir
* IO? (needs to be fleshed out, some from Unix)
* Process
* Mutex
* Thread
* Socket (from Unix)
* Time (from Unix & Sys)

### Utilities

* Arg
* Marshal
* Printf (unify with Format?)
* Random
* Regex (incorporate ocamlre)
* Terminal? (from Unix)
