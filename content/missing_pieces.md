---
tags: [ecosystem]
---

# Missing Pieces
This page details the things most lacking in the current ecosystem -- the things we wish we had.
Hopefully this will direct some users to try create these things.


## Need Help
The following projects could really use some help and attention in some ways.

- GraphQL client. Having [ppx_graphql](https://github.com/andreas/ppx_graphql) support the full
[GraphQL spec](http://facebook.github.io/graphql/June2018/) opens up the possibility to interact
with many APIs that expose a GraphQL endpoint including Github. 

- Elasticsearch is the defacto search solution. 
[ocaml-elasticsearch](https://github.com/skydeck/ocaml-elasticsearch) is abandoned. 

## New Projects
The following projects need to be built from scratch.

- Bindings to GTK3

### Cloud APIs

[Google Cloud Platform](https://cloud.google.com/apis/) 


### Messaging 

- [gRPC](https://grpc.io/) OCaml does not have any support for gRPC. I opened an 
[issue](https://github.com/grpc/grpc/issues/14251) in the official project.
There is also a discussion on the 
[OCaml discourse](https://discuss.ocaml.org/t/grpc-implementation-in-ocaml/1624).

- [NATS/NATS Streaming](https://nats.io/) NATS is part of the 
[Cloud Native Foundation](https://www.cncf.io/) and gaining increased adoption. 
