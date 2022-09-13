---
tags: [ecosystem]
---

# Systems Programming

## Number Types

* [ocplib-endian](https://github.com/OCamlPro/ocplib-endian):
Read and write all sizes of integers, both big and little endian, from [Bigarrays](bigarray.md), strings and bytes.
* [Bytes](https://v2.ocaml.org/api/Bytes.html):
The standard library has functions to read little endian and big endian numbers of different sizes,
both signed and unsigned, from bytes.
* [Integers](https://github.com/ocamllabs/ocaml-integers):
A library for support of unsigned and signed types of different sizes.
* [StdInt](https://github.com/andrenth/ocaml-stdint):
More comprehensive library for manipulation of unsigned and signed types of different sizes.
Includes the ability to read big endian and little endian numbers.

## Mirage OS

* [Mirage OS](https://github.com/mirage/mirage):
Unikernel-based operating system written in OCaml.
It serves as a programming framework for constructing secure,
high-performance network applications across a variety of cloud computing and mobile platforms.
  * [Arxiv paper on mirage](https://arxiv.org/pdf/1905.02529.pdf)
  * [mirage-skeleton](https://github.com/mirage/mirage-skeleton):
  Examples of simple Mirage apps.
  * [ICFP Presentation on Mirage and Irmin](https://www.youtube.com/watch?v=nUJYGFJDVVo)
* [mirage-tcpip](https://github.com/mirage/mirage-tcpip):
Pure OCaml TCPIP stack.
* [Irmin](https://github.com/mirage/irmin):
Git-like distributed database written in OCaml.
  * [Irmin](https://ani003.github.io/irmin/2020/08/13/irmin-containers-intro.html):
  Irmin containers.
* [ocaml-fat](https://github.com/mirage/ocaml-fat):
Read and write FAT format filesystems from OCaml.
* [ocaml-git](https://github.com/mirage/ocaml-git):
Pure OCaml low-level git bindings.
* [ocaml-vchan](https://github.com/mirage/ocaml-vchan):
Pure OCaml implementation of the "vchan" shared-memory communication protocol.

## Mirage OS Applications

* [Canopy](https://github.com/Engil/Canopy): A blogging MirageOS unikernel based on git.
Can be compiled to Unix as well.

## Embedded Programming

* [OMicroB](https://github.com/stevenvar/OMicroB):
OCaml virtual machine for devices with limited resources such as microcontrollers.
Based on [this paper](http://hal.upmc.fr/hal-01705825/document).
* [OCaPIC](https://github.com/bvaugon/ocapic):
OCaml for PIC microcontrollers.

## Lower-level OS Libraries

* [kqueue](https://github.com/anuragsoni/kqueue-ml/):
Bindings to the [kqueue](https://en.wikipedia.org/wiki/Kqueue) event notification interface in BSD-style systems.

## Articles
* [ocamlunix](https://ocaml.github.io/ocamlunix/ocamlunix.html):
Great introduction to systems programming in OCaml
