# Bigarray

[Bigarray](https://caml.inria.fr/pub/docs/manual-ocaml/libref/Bigarray.html)
serves as a way to bypass some of the limitations with OCaml's built-in array data structures.

For example:

* Interop with external C or Fortran applications requires copying array data from the OCaml heap
to the outside world, which is inefficient.
* On 32-bit platforms, arrays, strings and bytes are limited in size to roughly 4MB.
This limitation does not exist on 64-bit platforms.
* While strings and bytes aren't scanned internally by the OCaml garbage collector,
OCaml arrays *are*.
This means that large arrays on the OCaml heap will need to be scanned during a major GC event,
and matrices (arrays of arrays) require the GC to scan every array-of-array.
(Note that OCaml float arrays are currently treated as a special case, but this is
temporary.)
* OCaml arrays (but not bytes or Buffers) have write barriers to keep them GC-safe,
making it so writing into an array cell requires additional time.

Bigarrays are based on pointers outside of the OCaml heap.
They support multiple, possible smaller views of the same memory without copying it.
Thanks to compiler primitives, manipulation of values inside Bigarrays is fast,
and via [ocplib-endian](https://github.com/OCamlPro/ocplib-endian),
one can read/write values in an endian-neutral way, which is ideal for network protocols.

Bigarrays are not size-limited, and because Bigarray memory resides outside of the OCaml heap,
they are never scanned internally by the GC.
For the same reason, they also don't require a write barrier.

All of this makes Bigarrays ideal for network IO, as well as for FFI (foreign function interface)
in applications that require manipulation of large amounts of data,
such as [Owl] for data science and
and bitmap surfaces for [tSDL](https://github.com/dbuenzli/tsdl).
Bigarrays are therefore very similar to python's `numpy` library,
though the more advanced operations for data manipulation are found in a library like [Owl],
which wraps Bigarray in its own [ndarray](https://www.cl.cam.ac.uk/~lw525/owl/chapter/ndarray.html)
structure.

On the downside,
small Bigarrays do not benefit from OCaml's rapid minor heap allocation,
unlike native data structures.
Allocation costs are always similar to major heap allocation.
Additionally,
substring operations, which are useful for IO,
are also slow.
[cstruct](https://github.com/mirage/ocaml-cstruct) attempts to solve this issue
by allocating [small OCaml records](https://github.com/mirage/ocaml-cstruct/blob/master/lib/cstruct.mli#L143)
(on the minor heap) as views into an underlying
Bigarray.

[Owl]: https://ocaml.xyz/ "Owl"
