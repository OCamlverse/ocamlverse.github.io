---
tags: [ecosystem]
---

# Missing Pieces in the OCaml Ecosystem

This page details the things most lacking in the current ecosystem.
If you're looking to contribute to OCaml but not sure where to focus
your attention, this page should give you some ideas of where the community
thinks work is needed.

## Documentation
- [odoc](https://github.com/ocaml/odoc/tree/master/src/odoc) (needs help):
the new standard documentation tool for OCaml.
Unfortunately, it still needs some love -- check out the issues.
This is a great place to contribute since a little effort on the documentation
front can go a long way.

## Web and Networking

- HTTP2 (*high priority*): no bindings.
There are issues to provide HTTP2 support for both
[Cohttp](https://github.com/mirage/ocaml-cohttp/issues/272) and
[HTTP/AF](https://github.com/inhabitedtype/httpaf/issues/51).
This is very important as it's currently a barrier to OCaml being used as
a server language.

- [gRPC](https://grpc.io/): no support. Requires HTTP2.
There is an [issue](https://github.com/grpc/grpc/issues/14251) in the official
project.
There is also a discussion on the [OCaml
discourse](https://discuss.ocaml.org/t/grpc-implementation-in-ocaml/1624).

- Elasticsearch (needs help): the defacto standard search solution.
[ocaml-elasticsearch](https://github.com/skydeck/ocaml-elasticsearch) is
abandoned.

- GraphQL client (needs help):
Having [ppx_graphql](https://github.com/andreas/ppx_graphql)
support the full [GraphQL spec](http://facebook.github.io/graphql/June2018/)
opens up the possibility to interact with many APIs that expose a GraphQL
endpoint including Github.

## GUI

- GTK3: no bindings.

## Machine Learning

- [OWL](https://github.com/owlbarn/owl) (needs help):
OCaml's equivalent to Numpy and Pytorch.
Currently, the project doesn't support GPUs, which hurts its adoption by
machine learning professionals.

## Cloud Technology

- [Google Cloud Platform](https://cloud.google.com/apis/): no bindings.
- [NATS/NATS Streaming](https://nats.io/): no bindings.
Part of the [Cloud Native Foundation](https://www.cncf.io/) and gaining increased adoption. 
