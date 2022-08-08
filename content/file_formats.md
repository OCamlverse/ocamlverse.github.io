---
tags: [ecosystem]
---

# File Formats

## Serialization

### JSON

* [yojson](https://github.com/mjambon/yojson):
an optimized parsing and printing library for the JSON format.
    * [ppx_yojson_conv](https://github.com/janestreet/ppx_yojson_conv):
    A solid `ppx_deriving` solution for automatically deriving JSON serializers from types.
    Other solutions are not recommended.
    * [yojson_ppx](https://github.com/NathanReb/ppx_yojson):
    Write `yojson`-oriented code more easily and concisely.
* [jsonm](http://erratique.ch/software/jsonm):
non-blocking streaming JSON codec for OCaml.
* [ezjsonm](https://github.com/mirage/ezjsonm):
library to simplify usage of `jsonm`.
* [jsonxy](https://github.com/stevebleazard/ocaml-jsonxt):
RFC-compliant JSON library. [docs](https://stevebleazard.github.io/ocaml-jsonxt/jsonxt/index.html).
* [data-encoding](https://gitlab.com/nomadic-labs/data-encoding):
A library for JSON and binary encoding of values.

### TOML

* [otoml](https://github.com/dmbaturin/otoml):  TOML parsing, manipulation, and pretty-printing library for OCaml (fully 1.0.0-compliant)
* [To.ml](https://github.com/ocaml-toml/To.ml): an OCaml library for reading and writing TOML files

### XML

* [Markup](https://github.com/aantron/markup.ml):
streaming, lazy parser for XML and HTML5.
* [xmlm](http://erratique.ch/software/xmlm):
a streaming codec to decode and encode the XML data format.
* [easyxmlm](https://github.com/mirage/ezxmlm):
easy to use wrapper over `xmlm`.

### YAML

* [ocaml-yaml](https://github.com/avsm/ocaml-yaml):
Parse and generate yaml 1.1 files.

### Others

* [sexplib](https://github.com/janestreet/sexplib):
a S-expression parser and printer
* [biniou](https://github.com/mjambon/biniou):
extensible binary data format, like JSON but faster.
* [ocaml-protoc](https://github.com/mransan/ocaml-protoc) pure OCaml implementation of
  [Protobuf](https://developers.google.com/protocol-buffers/) with binary, Yojson and BuckleScript JSON support.
* [bin_prot](https://github.com/janestreet/bin_prot) efficient, type-safe binary protocol specific to OCaml.
* [camlon](https://gitlab.com/camlspotter/camlon):
configuration and serialization format similar to JSON but with an OCaml feel.
* [ocaml-decoders](https://github.com/mattjbray/ocaml-decoders): Elm-inspired decoders for OCaml

## Data Science Files

* [npy](https://github.com/LaurentMazare/npy-ocaml):
read and write the numpy file format.
* [hdf5-OCaml](https://github.com/vbrankov/hdf5-ocaml):
OCaml implementation of hdf5 reader/writer.
Mostly used in data science.

## Miscellaneous

* [camlPDF](https://github.com/johnwhitington/camlpdf):
OCaml library for reading, writing and modifying PDF files.
* [bencode](https://github.com/rgrinberg/bencode):
Bencode (.torrent file format) reader/writer.
* [Decompress](https://github.com/oklm-wsh/Decompress):
a pure OCaml implementation of `Zlib`.
* [Easy-xslx](https://github.com/brendanlong/ocaml-ooxml):
read Microsoft Office Open XML files.
* [hevea](https://github.com/maranget/hevea):
library to convert LaTex to html.
Used for the [OCaml manual](http://caml.inria.fr/pub/docs/manual-ocaml/)
* [ocaml-pandoc](https://github.com/smimram/ocaml-pandoc):
Interface to [pandoc](https://pandoc.org/MANUAL.html), a universal markup converter.
