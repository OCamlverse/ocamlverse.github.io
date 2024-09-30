---
tags: [ecosystem]
---

# Web, Networking and Cloud Computing

## Articles

* [Full stack development in OCaml](https://ceramichacker.com/blog/26-1x-full-stack-webdev-in-ocaml-intro):
  Uses `Dream`, `Bonsai` and `GraphQL`.
* [ICFP presentation on improving the OCaml web stack](https://www.youtube.com/watch?v=tTqqu4xh4UY&t=1156s)
* [Building an OCaml webapp using Opium](https://shonfeder.gitlab.io/ocaml_webapp/)

## HTTP Servers

* [dream](https://github.com/aantron/dream):
Tidy, feature complete web framework. Supports http and http2.
* [Opium](https://github.com/rgrinberg/opium):
Sinatra like micro-framework web toolkit for OCaml.
    * [Tutorial: Building an OCaml WebApp](https://shonfeder.gitlab.io/ocaml_webapp/)
* [ocamlapi](https://github.com/nosman/Ocamlapi):
Routing with ppx support. Uses cohttp and Core.
* [http_async](https://github.com/anuragsoni/http_async):
Fast HTTP/1.1 server implementation for Async.
Supports both regular async TCP connections and encrypted connections via async_ssl.
* [tiny httpd](https://github.com/c-cube/tiny_httpd):
Simple HTTP server like python's SimpleHTTPServer, for serving files.
* [routes](https://github.com/anuragsoni/routes):
Typed bidirectional routing utility with combinators.
Could be useful as part of creating a server.

## Web Frameworks

* [dream](https://github.com/aantron/dream):
Tidy, feature complete web framework. Supports http and http2.
* [nightmare](https://github.com/funkywork/nightmare):
Set of useful components to use with `Dream`.
* [hc](https://erratique.ch/software/hc):
Lightweight framework for web applications using server processing and the `fetch` interface.
* [Ocsigen Eliom](http://ocsigen.org/eliom/): a full-featured multi-tier framework,
for developing multi-platform Web and mobile apps as 100% OCaml distributed applications.
It can also be used for more traditional Web or mobile apps.
Eliom lets you write client and server code in OCaml, where both are typechecked against
each other, the client being compiled to JS and the backend to OCaml.
  * [Oscigen Tutorial](https://ocsigen.org/eliom/latest/manual/clientserver-applications)
  * [Thesis on Eliom](https://www.irif.fr/~gradanne/papers/phdthesis.pdf)
* [Sihl](https://github.com/oxidizing/sihl):
A modular web framework.
* [Morph](https://github.com/reason-native-web/morph):
Lightweight web framework for OCaml and Reason. [docs](https://reason-native-web.github.io/morph/).
* [re-web](https://github.com/yawaramin/re-web):
*experimental*.
A type-safe web framework.
Currently requires `esy` to build.
* [webmachine](https://github.com/inhabitedtype/ocaml-webmachine):
A REST toolkit for OCaml.
Implements a state-machine-based HTTP request processor that is well-suited for writing RESTful APIs.
Uses co-http.
* [OCaml-graphql-server](https://github.com/andreas/ocaml-graphql-server):
A GraphQL server library. GraphQL is a regimented approach to data management in web apps.
* [ppx_graphql](https://github.com/andreas/ppx_graphql):
Generate type-safe code for graphql queries from GraphQL schema and queries.
* [OCaml On Ice](https://github.com/roddyyaga/ocoi):
A web framework in the style of Ruby on Rails, built on top of Opium. It is designed for building REST APIs.
* [Finch](https://github.com/roddyyaga/finch):
Static site generator using markdown, with a server-side renderer.
* [Naboris](https://github.com/shawn-mcginty/naboris):
An light OCaml/Reason-based web framework.
* [sopault](https://soupault.app/): a static website generator that exploits the fact that well-formed HTML is machine readable and transformable.
* [Brr](https://github.com/dbuenzli/brr):
A toolkit for interfacing `js_of_ocaml` with common browser APIs.
Also includes experimental [FRP](frp.md) support via `Note`.

## Web Apps

* [Muhokama](https://github.com/xvw/muhokama):
Forum software written on top of `Dream`.
* [Cumulus](https://github.com/Cumulus/Cumulus):
Hackernews-like website with the OCaml framework Ocsigen (demo is currently down).
* [Prose](https://gitlab.com/adrien-n/prose/):
A Google-docs-like collaborative editing application written using Eliom/Ocsigen.
* [Canopy](https://github.com/Engil/Canopy):
A blogging MirageOS unikernel based on git.
Can be compiled to Unix as well.

## Low-Level HTTP Protocol

* [h2](https://github.com/anmonteiro/ocaml-h2):
High performance http2 implementation.
* [httpaf](https://github.com/inhabitedtype/httpaf):
A high performance HTTP implementation written in OCaml. Compatible with Async and Lwt.
* [cohttp](https://github.com/mirage/ocaml-cohttp):
Older, slower implementation of HTTP supporting only HTTP/1.x.

## HTTP Clients

* [piaf](https://github.com/anmonteiro/piaf):
An HTTP client that supports both HTTP/1.x and HTTP/2, and with better cross-platform support for SSL.
* [http-lwt-client](https://github.com/roburio/http-lwt-client):
A simple HTTP client with emphasis on minimal dependencies.
* [cohttp](https://github.com/mirage/ocaml-cohttp):
A mature, lightweight HTTP server and client that currently only supports HTTP/1.x.
* [fetch](https://github.com/lessp/fetch):
*Experimental*.
Aims to provide a common interface, following the fetch specification,
over different HTTP and Promise implementations. Currently only supports `piaf` and `lwt`,
but also plans to support BuckleScript in the near future.
* [Curly](https://github.com/rgrinberg/curly): Wrapper around the `curl` command for applications that want to create simple HTTP requests

## Ocaml to Javascript

* [js_of_ocaml](http://ocsigen.org/js_of_ocaml):
Compiles OCaml bytecode to Javascript.
This makes it possible to run OCaml programs in a browser, while sticking to the OCaml paradigms and ecosystem.
  * [commonjs_of_ocaml](https://github.com/AngryLawyer/commonjs_of_ocaml) : Easily import and export CommonJS modules from a js_of_ocaml project.
* [ReScript](https://rescript-lang.org/):
A fork of an older version of the OCaml compiler with its own opinionated syntax that compiles to JavaScript directly,
prioritizing readability of JavaScript and compatibiltiy with the NPM/JavaScript ecosystem over compatibility with the OCaml ecosystem.
* [Melange](https://github.com/melange-re/melange):
A fork of the ReScript compiler with the aim to integrate better with the OCaml ecosystem, in particular dune and opam,
and keep up-to-date with new releases of the OCaml compiler.

## Virtual DOM

The browser's Document Object Model is very expensive to manipulate,
and some frameworks work on making DOM manipulation more efficient.

* [ocaml-vdom](https://github.com/LexiFi/ocaml-vdom):
A version of virtual DOM manipulation that goes well with Ocsigen.
* [incr_dom](https://github.com/janestreet/incr_dom):
Jane Street's version of virtual DOM,
backed by the very powerful [Incremental](https://github.com/janestreet/incremental) library.

## Protocol Libraries

* [tyxml](http://ocsigen.org/tyxml):
build valid html using combinators.
Leverages OCaml's type system.
  * [tyxml-ppx](https://ocsigen.org/tyxml/4.3.0/manual/ppx):
  PPX syntax extension to translate html/xml syntax into `tyxml` function calls.
* [omd](https://github.com/ocaml/omd):
convert Markdown to html.
* [ocurl](https://github.com/ygrek/ocurl):
OCaml bindings to libcurl.
* [ocaml-dns](https://github.com/mirage/ocaml-dns):
A pure OCaml implementation of the DNS protocol. Part of `Mirage`.
* [udns](https://github.com/roburio/udns):
An opinionated DNS server library written in pure OCaml.
* [oidc](https://github.com/ulrikstrid/ocaml-oidc):
Library for [OpenID Connect](https://openid.net/connect/faq/).
* [fluent-logger](https://github.com/fluent/fluent-logger-ocaml):
A fluentd logger for OCaml.
* [charrua-unix](https://github.com/haesbaert/charrua-unix):
A Unix DHCP daemon based on [charrua-core](https://github.com/haesbaert/charrua-core)
* [COW](https://github.com/mirage/ocaml-cow):
Caml on the Web (COW) is a set of parsers and syntax extensions to manipulate
HTML, CSS, XML, JSON and Markdown directly from OCaml code.
* [JOSE](https://github.com/ulrikstrid/reason-jose):
Library for [JOSE](https://jose.readthedocs.io/en/latest/) (JSON Object Signing and Encryption) support.
* [Cookie](https://github.com/ulrikstrid/ocaml-cookie):
Library for working with web cookies.
* [Ocamlnet](http://projects.camlcity.org/projects/ocamlnet.html):
An older, but battle-tested suite of advanced networking libraries.
Includes many components, such as ones allowing for shared-memory multi-processing,
as well as
  * [Nethtml](http://projects.camlcity.org/projects/dl/ocamlnet-4.0.4/doc/html-main/Nethtml.html):
  HTML parser
  * [Netasn1](http://projects.camlcity.org/projects/dl/ocamlnet-4.0.4/doc/html-main/Netasn1.html):
  ASN.1 parser
  * [Netencoding](http://projects.camlcity.org/projects/dl/ocamlnet-4.0.4/doc/html-main/Netencoding.html):
  Base64, Quoted Printable, URL encoding and HTML escaping.
  * [Netmime](http://projects.camlcity.org/projects/dl/ocamlnet-4.0.4/doc/html-main/Netmime.html):
  MIME processing.
  * Other [OCamlnet modules](http://projects.camlcity.org/projects/dl/ocamlnet-4.0.4/doc/html-main/index.html)
* [letters](https://github.com/oxidizing/letters):
High-level library for creating and writing emails. Uses `mrmime` and `lwt`.
* [mrmime](https://github.com/mirage/mrmime):
  High performance email parsing/generation library.
  * [Announcement](https://discuss.ocaml.org/t/ann-first-release-of-mrmime-parser-and-generator-of-emails/4436)
  * [Talk](https://www.youtube.com/watch?v=kQkRsNEo25k) about mrmime.
* [ocaml-uri](https://github.com/mirage/ocaml-uri):
RFC3986 URI parsing library.
* [Goji](https://github.com/klakplok/goji):
An OCaml bindings generator for JavaScript libraries.
* [Syndic](https://github.com/Cumulus/Syndic):
RSS and Atom feed parsing
* [ocaml-mustache](https://github.com/rgrinberg/ocaml-mustache):
mustache.js logic-less templates in OCaml.
* [atdjs](https://github.com/barko/atdjs):
atd code generator for OCaml or `js_of_ocaml`.
* [jingoo](https://github.com/tategakibunko/jingoo):
OCaml template engine almost compatible with jinja2.
* [dispatch](https://github.com/inhabitedtype/ocaml-dispatch):
Path-based dispatching for client and server-side applications.
* [Lambda Soup](https://github.com/aantron/lambda-soup):
Functional HTML scraping and manipulation with CSS selectors, similar to Python's Beautiful Soup.
* [Markup.ml](https://github.com/aantron/markup.ml):
Error-recovering streaming HTML5 and XML parsers, serializers.
* [gen_js_api](https://github.com/LexiFi/gen_js_api):
Helps simplify the creation of OCaml bindings for Javascript libraries in `js_of_ocaml`.
* [AMQP-client](https://github.com/andersfugmann/amqp-client):
[AMQP](https://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol) client library written in OCaml.
Supports [RabbitMQ](https://www.rabbitmq.com/),
and both `lwt` and `Async`.

### Chat Protocols

* [slacko](https://github.com/Leonidas-from-XIV/slacko):
command line interface to Slack.
* [dis.ml](https://gitlab.com/Mishio595/disml):
API for Discord servers. Uses Async and Core.
* [irc-client](https://github.com/johnelse/ocaml-irc-client):
Client and API for IRC.
* [ocaml-orc](https://github.com/pymander/ocaml-irc):
IRC library.
* [proofchat](https://github.com/CharlesAverill/proofchat):
A multithreaded TCP client/server chat application written in Coq and extracted to OCaml

### Low Level Protocols

* [mirage-tcpip](https://github.com/mirage/mirage-tcpip):
Part of `Mirage`.
A complete implementation of the TCP/IP stack in OCaml.
* [ocaml-xsk](https://github.com/suttonshire/ocaml-xsk):
Bindings to `AF_XDP` of `libbpf`.
These provide high-performance packet management on Linux, bypassing the kernel.
    * [AF_XDP docs](https://github.com/torvalds/linux/blob/master/Documentation/networking/af_xdp.rst)
    * [Tutorial](https://github.com/xdp-project/xdp-tutorial/tree/master/advanced03-AF_XDP)
