# Design Principles For Stdlib 2.0

## Data Structures

* To maintain compatibility with previous versions of the stdlib, we will, in all likelihood,
need to keep datastructure types identical.

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

Note: we may want to use libuv for cross-platform support here.

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
