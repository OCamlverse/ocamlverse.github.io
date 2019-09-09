# OCaml REPL (Toplevel)

OCaml has a very powerful REPL, which can be used to explore your code during development.

* [utop](https://github.com/ocaml-community/utop)
is an alternative, advanced REPL with support for tab completion and other features.
It's highly recommended to use `utop` instead of the standard REPL.
* The regular REPL is started simply with `ocaml`.
* To make OCaml packages available to ocaml, we need to use the topfind utility,
which is installed as a part of the ocamlfind package.
If you're using `ocaml`, your first command should be

```
#use "topfind";;
```
Note the `#` symbol that precedes all directives to the REPL (ie. not ocaml calls).

* The `~.ocamlinit` file is executed as soon as you start up the toplevel.
For regular `ocaml`, you want to insert the `#use "topfind;;"` line in there.

* Note also the `;;` that follows every phrase in the toplevel.
Since OCaml uses `;` for statements and lists, we need some way to tell it when to process our commands.
That's what `;;` is for.

* View all possible directives with `#help;;`

* You can now list all available libraries with

```
#list;;
```

* And easily load a library with

```
#require "library";;
```

Note how we use a string for the library name.

#require "core_kernel";;

## Printers.

While OCaml will try its best to print everything, it doesn't know about custom data structures.
You can install your own printers for different types.
You can have many different printers for your data, to give you different views on what is going on,
so that you can switch between one and another.

The `#install_printer` directive enables custom printers for your data, which is very useful during development and debugging.
It takes a function, which should have the type

```
Format.formatter -> t -> unit
```
where t is the type of your data, e.g.,

```
type t = Student of int

let pp_name ppf (Student id) = 
   Format.fprintf ppf "%s" (Hashtbl.find_exn names id)
```

and now we can install it,

```
#install_printer pp_name
```

## Tracing

OCaml toplevels also provide a nice feature called tracing,
which shows how your functions are invoked and what they return..
This is especially powerful with custom printers.

To trace a function use the `#trace` directive, e.g.,

```
#trace find_best_student;;
```

To stop tracing use `#untrace`

## Developing Large Applications

* REPL driven development best fits the bottom-up style of development.
If you keep your modules small and independent, you can minimize the context needed to debug with the REPL.
You can debug each piece of an application independently, and then load the piece using `#require`.

* Dune contains utop integration which will allow you to run your project.

* Another trick is to stub a needed library with a dummy interface:

```
(* let's stub some complex external library which is developed 
    by some other guy, and is still not yet ready *)
module Database  : Database.S = struct 
   type t = string
   
   let connect str = printf "connect %s" str; 
   let select conn query = 
     printf "%s> %s" conn query;
     []
end

(* here comes our code that needs the database, which is not yet ready,
    but it doesn't stop us anymore *)

let start_driviving env = 
   let db = Database.connect env.main_host in
   let waypoints = Database.select db waypoints_query in
   drive_through waypoints
```
