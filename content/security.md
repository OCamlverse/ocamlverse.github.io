---
tags: [ecosystem]
---

# Security and Cryptography

* [ocaml-tls](https://github.com/mirleft/ocaml-tls): TLS in pure OCaml.
  * [Excellent series of articles](https://mirage.io/blog/introducing-ocaml-tls)
  on ocaml-tls and its design.
* [awa-ssh](https://github.com/haesbaert/awa-ssh) (WIP):
SSH implementation in OCaml, for `Mirage`.
* [ocaml-libssh](https://github.com/fxfactorial/ocaml-libssh):
Bindings to libssh.
* [Digestif](https://github.com/mirage/digestif): Hash algorithms (like SHA* or BLAKE2*) in OCaml and C.
* [cryptokit](https://github.com/xavierleroy/cryptokit): The Cryptokit library for OCaml provides a variety of cryptographic primitives that can be used to implement cryptographic protocols in security-sensitive applications.
* [nocrypto](https://github.com/mirleft/ocaml-nocrypto): A small cryptographic library behind the ocaml-tls project. It is built to be straightforward to use, adhere to functional programming principles and able to run in a Xen-based unikernel.
  * The differences between `nocrypto` and `cryptokit` cryptographic libraries are described in [this blog post](https://mirage.io/blog/introducing-nocrypto)
* [u2f](https://github.com/roburio/u2f):
The server protocol for [U2F](https://fidoalliance.org/specs/fido-u2f-v1.2-ps-20170411/),
two-factor authentication using specialized devices.
[docs](https://roburio.github.io/u2f/doc)
