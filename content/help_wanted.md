---
tags: [ecosystem]
---

# Help Wanted

Are you looking to help the OCaml ecosystem, but not sure where to start?
This page should give you some ideas of where the community
thinks work is needed.

It's worth keeping in mind that making the ecosystem just a little more usable,
especially at critical points, can have massive implications downstream.

## Databases

Both [Sequoia](https://github.com/andrenth/sequoia) and [ocaml-mysql](https://github.com/ygrek/ocaml-mysql) are out of date and need to be updated to the latest versions of OCaml, to use dune etc.

## Windows Support

- [Diskuv Box](https://github.com/diskuv/diskuvbox):
Adding native Windows support requires getting rid of the usage of small bash utilities.
`Diskuv Box` is a file utility working on replacing bash utilities with a cross-platform program
so that OCaml can easily work on Windows.

## Web and Networking

- [gRPC](https://grpc.io/): no support.
There is an [issue](https://github.com/grpc/grpc/issues/14251) in the official
project.
There is also a discussion on the [OCaml discourse](https://discuss.ocaml.org/t/grpc-implementation-in-ocaml/1624).

- Elasticsearch (needs help): the de facto standard search solution.
[ocaml-elasticsearch](https://github.com/skydeck/ocaml-elasticsearch) is
abandoned.

- GraphQL client (needs help):
Having [ppx_graphql](https://github.com/andreas/ppx_graphql)
support the full [GraphQL spec](http://spec.graphql.org/)
opens up the possibility to interact with many APIs that expose a GraphQL
endpoint including Github.

## GUI

- [LablGTK3](https://github.com/garrigue/lablgtk) (needs help): not yet feature
complete as GTK2 state, see `lablgtk3` branch.

## Machine Learning

* [OWL](https://github.com/owlbarn/owl) (needs help):
OCaml's equivalent to numpy, scipy and Pytorch/Tensorflow.
  * [OWL proposed project page](https://ocaml.xyz/project/proposal.html):
  List of proposed projects for people interested in helping develop `OWL`.
  
## Cloud Technology

- [Google Cloud Platform](https://cloud.google.com/apis/): no bindings.
- [NATS/NATS Streaming](https://nats.io/): no bindings.
Part of the [Cloud Native Foundation](https://www.cncf.io/) and gaining increased adoption.
