---
tags: [ecosystem]
---

# Databases

## Bindings

* [camltc](https://github.com/toolslive/camltc): OCaml bindings to [Tokyo Cabinet](https://github.com/Incubaid/tokyocabinet).
* [Caqti](https://github.com/paurkedal/ocaml-caqti): monadic, asynchronous common interface to relational databases. Currently supports MariaDB, PostgreSQL and SQLite3.
* [Dbm](https://forge.ocamlcore.org/projects/camldbm/): a binding to the NDBM/GDBM Unix "databases".
* [ezpostgresql](https://github.com/bobbypriambodo/ezpostgresql): simple, non-type-safe interface to PostgreSQL. Prioritizes simplicity. Wraps around PostgreSQL-OCaml.
* [Mongo](https://massd.github.io/mongo/): OCaml driver for Mongodb
* [mysql8](https://github.com/chrisnevers/mysql8): Bindings to the latest version of the mysql database. [docs](https://chrisnevers.github.io/mysql8/mysql8/index.html)
* [mysql_protocol](https://github.com/slegrand45/mysql_protocol): implementation of MySQL Protocol with the Bitstring library.
* [OCaml-mariahdb](https://github.com/andrenth/ocaml-mariadb): OCaml bindings to MariahDB interface.
* [ocaml-redis](https://github.com/0xffea/ocaml-redis): Redis bindings for OCaml.
* [ocaml-sql-query](https://github.com/yawaramin/ocaml_sql_query): Experimental functional wrapper over SQL queries.
* [orocksdb](https://github.com/domsj/orocksdb): OCaml RocksDB bindings using ctypes.
* [Petrol](https://github.com/gopiandcode/petrol): Provides a high-level, type-safe API that allows defining SQL tables and queries directly in OCaml rather than writing SQL code.
* [PG'OCaml](https://github.com/darioteixeira/pgocaml): PostgreSQL client in pure OCaml. Includes a `PPX` that provides compile-time checking of SQL syntax and types.
* [PGX](https://github.com/arenadotio/pgx): a pure-OCaml PostgreSQL client library, supporting Async, LWT, or synchronous operations.
* [PostgreSQL-OCaml](https://mmottl.github.io/postgresql-ocaml/): a low-level interface to PostgreSQL through the C API (`libpq`).
* [ppx_mysql](https://github.com/issuu/ppx_mysql): Syntax extension for mysql bindings. [Blog post](https://engineering.issuu.com/2019/05/06/announcing-ppx-mysql).
* [ppx_pgsql](https://github.com/tizoc/ppx_pgsql): a syntax extension for embedded SQL queries using PG'OCaml.
* [ppx_rapper](https://github.com/roddyyaga/ppx_rapper): a syntax extension for PostgreSQL using Caqti
* [SQLite3-OCaml](https://github.com/mmottl/sqlite3-ocaml/): OCaml bindings to the SQLite3 database.
* [Sqlite3EZ](https://mlin.github.io/ocaml-sqlite3EZ/): thin wrapper for SQLite3 with a simplified interface.

### Out of Date

* [mysql](http://ocaml-mysql.forge.ocamlcore.org/): (Older version of mysql) mysql library.
* [Sequoia](https://github.com/andrenth/sequoia): (Needs update to latest OCaml) Create type-safe queries. Currently with bindings to MySQL/MariaDB and SQLite.

## OCaml Databases

* [Arakoon](https://github.com/openvstorage/arakoon): a consistent distributed key-value store built on top of Tokyo Cabinet.
* [Irmin](https://github.com/mirage/irmin): a distributed database that follows the same design principles as Git.
  * A fairly through tutorial for Irmin can be found [here](https://irmin.io/tutorial/introduction).
* [Obigstore](http://obigstore.forge.ocamlcore.org/): a database with BigTable-like data model atop LevelDB.
* [RunOrg](https://github.com/RunOrg/RunOrg): a WIP database server written in OCaml.

## Overlays

* [Macaque](https://github.com/ocsigen/macaque): Macaque is a library for safe and flexible database queries using comprehensions on top of PG'OCaml.
* [ORM](https://github.com/mirage/orm/): ORM for SQLite.

## Articles

* [Implementing the Binary Memcached Protocol with Ocaml and Bitstring](http://andreas.github.io/2014/08/22/implementing-the-binary-memcached-protocol-with-ocaml-and-bitstring/)
* [Interfacing OCaml and PostgreSQL with Caqti](https://medium.com/@bobbypriambodo/interfacing-ocaml-and-postgresql-with-caqti-a92515bdaa11)
* [Petrol: embedding a type-safe SQL API in OCaml using GADTs](https://gopiandcode.uk/logs/log-ways-of-sql-in-ocaml.html)
