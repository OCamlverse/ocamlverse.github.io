---
tags: [ecosystem]
---

# Databases

## Bindings

* [Caqti](https://github.com/paurkedal/ocaml-caqti): monadic, asynchronous common interface to relational databases.
Currently supports MariahDB, PostgreSQL and SQLite3.
* [Mongo](https://massd.github.io/mongo/): OCaml driver for Mongodb
* [OCaml-mariahdb](https://github.com/andrenth/ocaml-mariadb): OCaml bindings to MariahDB interface.
* [PG'OCaml](http://pgocaml.forge.ocamlcore.org/): a type-safe interface to PostgreSQL in pure OCaml.
*NOTE:* uses camlp4, which is deprecated.
* [ppx_pgsql](https://github.com/tizoc/ppx_pgsql): a syntax extension for embedded SQL queries using PG'OCaml.
* [PostgreSQL-OCaml](https://mmottl.github.io/postgresql-ocaml/): a low-level interface to PostgreSQL through the C API (`libpq`).
* [ezpostgresql](https://github.com/bobbypriambodo/ezpostgresql): simple, non-type-safe interface to PostgreSQL.
Prioritizes simplicity. Wraps around PostgreSQL-OCaml.
* [SQLite3-OCaml](https://github.com/mmottl/sqlite3-ocaml/): OCaml bindings to the SQLite3 database.
* [Sqlite3EZ](https://mlin.github.io/ocaml-sqlite3EZ/): thin wrapper for SQLite3 with a simplified interface.
* [ocaml-redis](https://github.com/0xffea/ocaml-redis): Redis bindings for OCaml.
* [mysql](http://ocaml-mysql.forge.ocamlcore.org/): bindings to libmysqlclient for interacting with MySQL databases.
* [mysql_protocol](https://github.com/slegrand45/mysql_protocol): implementation of MySQL Protocol with the Bitstring library.
* [Dbm](https://forge.ocamlcore.org/projects/camldbm/): a binding to the NDBM/GDBM Unix "databases".
* [camltc](https://github.com/toolslive/camltc): OCaml bindings to [Tokyo Cabinet](https://github.com/Incubaid/tokyocabinet).
* [orocksdb](https://github.com/domsj/orocksdb): OCaml RocksDB bindings using ctypes.

## OCaml Clients

* [PGX](https://github.com/arenadotio/pgx): a pure-OCaml PostgreSQL client library, supporting Async, LWT, or synchronous operations.

## Ocaml Databases

* [Irmin](https://github.com/mirage/irmin): a distributed database that follows the same design principles as Git.
  * A fairly through tutorial for Irmin can be found [here](https://zshipko.github.io/irmin-tutorial/Introduction.html).
* [Obigstore](http://obigstore.forge.ocamlcore.org/): a database with BigTable-like data model atop LevelDB.
* [RunOrg](https://github.com/RunOrg/RunOrg): a WIP database server written in OCaml.
* [Arakoon](https://github.com/openvstorage/arakoon): a consistent distributed key-value store built on top of Tokyo Cabinet.

## Overlays

* [Macaque](https://github.com/ocsigen/macaque): Macaque is a library for safe and flexible database queries using comprehensions on top of PG'OCaml.
* [ORM](https://github.com/mirage/orm/): ORM for SQLite.

## Articles

* [Implementing the Binary Memcached Protocol with Ocaml and Bitstring](http://andreas.github.io/2014/08/22/implementing-the-binary-memcached-protocol-with-ocaml-and-bitstring/)
* [Interfacing OCaml and PostgreSQL with Caqti](https://medium.com/@bobbypriambodo/interfacing-ocaml-and-postgresql-with-caqti-a92515bdaa11)
