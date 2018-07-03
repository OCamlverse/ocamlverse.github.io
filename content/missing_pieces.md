---
tags: [ecosystem]
---

# Missing Pieces

This page details the things most lacking in the current ecosystem -- the
things we wish we had.  Hopefully this will direct some users to try create
these things.


## Need Help

The following projects could really use some help and attention:

- GraphQL client. Having [ppx_graphql](https://github.com/andreas/ppx_graphql)
  support the full [GraphQL spec](http://facebook.github.io/graphql/June2018/)
  opens up the possibility to interact with many APIs that expose a GraphQL
  endpoint including Github. 

- Elasticsearch is the defacto standard search solution.
  [ocaml-elasticsearch](https://github.com/skydeck/ocaml-elasticsearch) is
  abandoned.


## New Projects

The following projects need to be built to allow the ecosystem to grow:

- HTTP2 Implementation: there is an issue to provide HTTP2 support for both
  [Cohttp](https://github.com/mirage/ocaml-cohttp/issues/272) and
  [HTTP/AF](https://github.com/inhabitedtype/httpaf/issues/51).
- Bindings to GTK3


### Cloud Technology

- [Google Cloud Platform](https://cloud.google.com/apis/) 
- [gRPC](https://grpc.io/) OCaml does not have any support for gRPC. I opened
  an [issue](https://github.com/grpc/grpc/issues/14251) in the official
  project. There is also a discussion on the [OCaml
  discourse](https://discuss.ocaml.org/t/grpc-implementation-in-ocaml/1624).


### Messaging 

- [NATS/NATS Streaming](https://nats.io/) NATS is part of the [Cloud Native
  Foundation](https://www.cncf.io/) and gaining increased adoption. 
