# OCaml Runtime

The runtime part of OCaml dovetails with the compiled code,
providing the major services needed for an OCaml program to function,
such as memory allocation and garbage collection.
The runtime is not generated anew for each compiled program --
it's mostly written in C code that is compiled to run together with
the generated code (in the case of native compilation),
or to additionally run the OCaml bytecode (in the case of bytecode compilation).

### Heap Data Scheme

In order to facilitate garbage collection (GC),
all data allocated in the OCaml heap must have an appropriate header.
The GC is a 'dumb' piece of code that does not know
the specifics of a compiled program: it must be able to look at data in memory and
'scan' it correctly.

The header is specified in the
[/runtime/caml/mlvalues.h](https://github.com/ocaml/ocaml/blob/trunk/runtime/caml/mlvalues.h)
file.
2 formats of the header exist: one for 32-bit programs
and one for 64-bit programs.

The 32-bit header is as follows:

| word-size | color | tag |
| --- | --- | --- |
| 22 bits | 2 bits | 8 bits |

While the 64-bit header is:

| word-size | color | tag |
| --- | --- | --- |
| 54 bits | 2 bits | 8 bits |

Where `word-size` is the number of machine words (32-bits on 32-bit architectures, 64-bits on 64-bit architectures),
`color` is used by the GC algorithm, and `tag` categorizes the data. 
