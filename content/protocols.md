---
tags: [ecosystem]
---

# Protocols

* [obus](https://github.com/ocaml-community/obus):
Pure OCaml implementation of the [D-bus IPC protocol](https://en.wikipedia.org/wiki/D-Bus),
used by Freedesktop and Linux.
* [onanomsg](https://github.com/rgrinberg/onanomsg): nanomsg bindings for OCaml.
* [Kafka](https://github.com/didier-wenzek/ocaml-kafka): OCaml bindings for Apache Kafka.
* [AMQP](https://github.com/andersfugmann/amqp-client): AMQP client library for Async and Lwt.
* [MPI](https://github.com/xavierleroy/ocamlmpi): Message Passing Interface bindings for OCaml.
* [MQTT](https://github.com/j0sh/ocaml-mqtt): OCaml implementation of the MQTT pubsub protocol.
* [asn1-combinators](https://github.com/mirleft/ocaml-asn1-combinators):
Use the ASN.1 standard. See [introducing ASN.1](https://mirage.io/blog/introducing-asn1)
* [IMAP](https://github.com/nojb/ocaml-imap):
lwt-compatible implementation of IMAP4rev1.

## ZeroMQ
* [ocaml-zmq](https://github.com/issuu/ocaml-zmq): ZeroMQ bindings for OCaml.
* [async-zmq](https://github.com/rgrinberg/async-zmq): Async wrapper around ocaml-zmq.
* [lwt-zmq](https://github.com/hcarty/lwt-zmq): Lwt-friendly interface to ZeroMQ for OCaml.

## Protobuf
* [ocaml-protoc-plugin](https://github.com/issuu/ocaml-protoc-plugin/):
Full findings to Protobuf messages and types. Implements the full proto3 specification.
* [protoc](https://github.com/mransan/ocaml-protoc): Compiler from protobuf files to OCaml types.
* [ppx_deriving_protobuf](https://github.com/ocaml-ppx/ppx_deriving_protobuf): Derive Protobuf files from OCaml types.

## Capn-Proto
* [capnp-ocaml](https://github.com/capnproto/capnp-ocaml): Code generator for cap'n-proto.
* [capnp-rpc](https://github.com/mirage/capnp-rpc): RPC implemented over cap'n-proto.

# Security and Cryptography

* [ocaml-tls](https://github.com/mirleft/ocaml-tls): TLS in pure OCaml.
  * [Excellent series of articles](https://mirage.io/blog/introducing-ocaml-tls)
  on ocaml-tls and its design.
* [awa-ssh](https://github.com/haesbaert/awa-ssh) (WIP):
SSH implementation in OCaml, for `Mirage`.
* [Digestif](https://github.com/mirage/digestif): Hash algorithms (like SHA* or BLAKE2*) in OCaml and C.
* [cryptokit](https://github.com/xavierleroy/cryptokit): The Cryptokit library for OCaml provides a variety of cryptographic primitives that can be used to implement cryptographic protocols in security-sensitive applications.
* [nocrypto](https://github.com/mirleft/ocaml-nocrypto): A small cryptographic library behind the ocaml-tls project. It is built to be straightforward to use, adhere to functional programming principles and able to run in a Xen-based unikernel.
  * The differences between `nocrypto` and `cryptokit` cryptographic libraries are described in [this blog post](https://mirage.io/blog/introducing-nocrypto)
