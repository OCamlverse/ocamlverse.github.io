---
tags: [ecosystem]
---

# Functional Reactive Programming

Functional Reactive Programming is a model for programming that tries to adapt state-heavy programming such as UIs or games to the functional programming world. For example, the normal mode of operation for asynchronous event-driven programming is to use callbacks everywhere. However, this requires mutating state, since the user's code is not driving the program but is being 'driven' via events. This model is common in GUIs and in Javascript.

The FRP approach is to transform state mutation over time into 'signals', and to describe what happens with those signals. This approach can be used in GUI programming, web interfaces, and many other domains. There is only one known OCaml library that performs FRP:

* [React](http://erratique.ch/software/react) : an OCaml library for functional reactive programming (FRP). It provides support to program with time varying values. Used by, among others, the Eliom web framework.

* [Incremental](https://opensource.janestreet.com/incremental/):
A more opinionated FRP library.
While React is computation-agnostic, Incremental is built to maintain the computation graph efficiently.
