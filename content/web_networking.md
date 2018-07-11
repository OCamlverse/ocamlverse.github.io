---
tags: [ecosystem]
---

# Web and Networking

## Example Projects:

* [Cumulus](https://github.com/Cumulus/Cumulus) : Hackernews-like website with the OCaml framework Ocsigen (demo is currently down).
* [Prose](https://gitlab.com/adrien-n/prose/) : A Google-docs-like collaborative editing application written using Eliom/Ocsigen. See the demo [here](https://prose.yaxm.org/pads/foo-ocaml)

## HTTP Servers

* [cohttp](https://github.com/mirage/ocaml-cohttp) : A lightweight HTTP server using either Lwt or Async.
* [httpaf](https://github.com/inhabitedtype/httpaf) : A high performance web server written in OCaml. Written as a response to a scaling deficiency found in cohttp.
* [Opium](https://github.com/rgrinberg/opium)  – Sinatra like web toolkit for OCaml.

## Web Frameworks

* [Ocsigen Eliom](http://ocsigen.org/eliom/): a full-featured multi-tier framework,
for developing multi-platform Web and mobile apps as 100% OCaml distributed applications.
It can also be used for more traditional Web or mobile apps.
Eliom lets you write client and server code in OCaml, where both are typechecked against
each other, the client being compiled to JS and the backend to OCaml.
  * [Thesis on Eliom](https://www.irif.fr/~gradanne/papers/phdthesis.pdf)
* [webmachine](https://github.com/inhabitedtype/ocaml-webmachine)  – A REST toolkit for OCaml. OCaml webmachine is a layer on top of cohttp that implements a state-machine-based HTTP request processor. It's particularly well-suited for writing RESTful APIs. As the name suggests, this is an OCaml port of the webmachine project.
* [Ohm](http://ohm-framework.com/)  - Ohm was an open source web framework for the OCaml language which is now dead.

## Javascript Compiler

* [js_of_ocaml](http://ocsigen.org/js_of_ocaml)  compiles OCaml bytecode to Javascript. It makes it possible to run OCaml programs in a browser, while sticking to the OCaml paradigms and ecosystem.
  * [commonjs_of_ocaml](https://github.com/AngryLawyer/commonjs_of_ocaml) : Easily import and export CommonJS modules from a js_of_ocaml project.
* [BuckleScript](https://github.com/bloomberg/bucklescript)  compiles OCaml to Javascript directly, prioritizing readability. The code lives in the Javascript ecosystem and generally requires a Javascript toolchain. ReasonML is enabled by this compiler.

## Cloud Computing
* [aws-s3](https://github.com/andersfugmann/aws-s3): Access to Amazon's Simple Storage Solution (S3)

## Protocol Libraries

* [tyxml](http://ocsigen.org/tyxml) : build valid html using combinators. Leverages OCaml's type system.
* [ocurl](https://github.com/ygrek/ocurl) : OCaml bindings to libcurl.
* [ocaml-dns](https://github.com/mirage/ocaml-dns)  – A pure OCaml implementation of the DNS protocol.
* [udns](https://github.com/roburio/udns): An opinionated DNS server library written in pure OCaml.
* [fluent-logger](https://github.com/fluent/fluent-logger-ocaml) :  A fluentd logger for OCaml.
* [charrua-unix](https://github.com/haesbaert/charrua-unix)  - charrua-unix is a Unix DHCP daemon based on [charrua-core](https://github.com/haesbaert/charrua-core)
* [COW](https://github.com/mirage/ocaml-cow)  – Caml on the Web (COW) is a set of parsers and syntax extensions to let you manipulate HTML, CSS, XML, JSON and Markdown directly from OCaml code.
* [Ocamlnet](http://projects.camlcity.org/projects/ocamlnet.html) : has many relevant networking libraries:
  * [Nethtml](http://projects.camlcity.org/projects/dl/ocamlnet-4.0.4/doc/html-main/Nethtml.html)  html parser
  * [Netasn1](http://projects.camlcity.org/projects/dl/ocamlnet-4.0.4/doc/html-main/Netasn1.html)  ASN.1 parser
  * [Netencoding](http://projects.camlcity.org/projects/dl/ocamlnet-4.0.4/doc/html-main/Netencoding.html)  Base64, Quoted Printable, URL encoding and HTML escaping.
  * [Netmime](http://projects.camlcity.org/projects/dl/ocamlnet-4.0.4/doc/html-main/Netmime.html) : MIME processing.
  * Other [OCamlnet modules](http://projects.camlcity.org/projects/dl/ocamlnet-4.0.4/doc/html-main/index.html)
* [ocaml-uri](https://github.com/mirage/ocaml-uri)  – RFC3986 URI parsing library.
* [Goji](https://github.com/klakplok/goji)  – An OCaml bindings generator for JavaScript libraries.
* [Syndic](https://github.com/Cumulus/Syndic)  – RSS and Atom feed parsing
* [ocaml-mustache](https://github.com/rgrinberg/ocaml-mustache)  – mustache.js logic-less templates in OCaml.
* [atdjs](https://github.com/barko/atdjs)  – atd code generator for OCaml/js_of_ocaml.
* [jingoo](https://github.com/tategakibunko/jingoo)  – OCaml template engine almost compatible with jinja2.
* [dispatch](https://github.com/inhabitedtype/ocaml-dispatch)  – Path-based dispatching for client- and server-side applications.
* [Lambda Soup](https://github.com/aantron/lambda-soup)  - Functional HTML scraping and manipulation with CSS selectors, à la Python's Beautiful Soup.
* [Markup.ml](https://github.com/aantron/markup.ml)  - Error-recovering streaming HTML5 and XML parsers, serializers.
* [gen_js_api](https://github.com/LexiFi/gen_js_api)  - gen_js_api aims at simplifying the creation of OCaml bindings for Javascript libraries.
* [slacko](https://github.com/Leonidas-from-XIV/slacko) : command line interface to Slack.

### Low Level Protocols
* [mirage-tcpip](https://github.com/mirage/mirage-tcpip): Part of mirage OS -- a complete implementation of the TCP/IP stack in OCaml.

## ReasonML
* Reason uses Bucklescript to create Javascript code that lives in the npm-world but leverages OCaml's type system.
