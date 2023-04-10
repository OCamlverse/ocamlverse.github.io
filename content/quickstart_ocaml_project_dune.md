---
tags: [learning, quickstart]
---

# Quickstart an OCaml app project using Dune

*Updated June 2022*

Once you're done playing with OCaml snippets online, you'll want to build an actual OCaml project.
Let's go through the process of doing so.

## Requirements

To be able to follow this tutorial, you need to have `opam`, the OCaml package manager, installed.
Follow the basic instructions [here](https://ocaml.org/docs/up-and-running) to install `opam`.

You can verify your opam installation with the following command:

```
$ opam --version
2.1.2
```

Your version of `opam` may be greater, and that should be fine.
This tutorial generally assumes a MacOS or Linux environment.
For Windows, you can use `WSL` or see [Windows Support](windows_support.md) for more information.

## Editor setup

See [Editor Setup](editor_setup.md) for tips on setting up your environment to work with OCaml.

## Initial dune project

`dune` is a sophisticated tool. We can use it to create our project for us:

```
dune init proj project_name
```

where `project_name` is whatever you want to call your project.
Dune will create a directory named `project_name`, containing the following subdirectories and files:

```
bin/ (the place for executable code)
bin/dune (a basic dune file specifying how to build the main executable)
bin/main.ml (our main executable code)
lib/ (the place for library code)
lib/dune (a basic dune file specifying how to build the library)
test/ (the place for test code)
test/project_name.ml (a dummy test file)
test/dune (a dune file specifying how to build our tests)
dune-project (a configuration file for the entire project)
project_name.opam (an opam file that's created automatically by dune)
```

Let's try to get `dune` to build the dummy code it wrote for us:

```
$ dune build
```

`dune` will now build the dummy code.

Note that `dune` has now added the `_build` directory.
This directory contains all of the artifacts which were used to build our project.

We can now use `dune` to run our code:

```
$ dune exec ./bin/main.exe
Hello, World!
```

The dummy code in `./bin/main.ml` writes 'Hello World!' to the screen,
and when we execute it we see the result.

## Using dune

Every directory where we compile something needs a `dune` file.
The `dune` file format uses `sexp`; much like the languages `lisp` and `clojure`.
It's a little counter-intuitive, but not too complicated once you get used to it.

Let's take a look at the file `./bin/dune`, which compiles our main application:

```
(executable
 (public_name project_name)
 (name main)
 (libraries project_name))
```

The parentheses may make things look confusing, but consider that every parenthesis pair indicates a sentence or command.
First we have the `executable` command.
This indicates that within the parenteses, we'll have information about building the executable.
`public_name` is the command indicating the external name of the project.
`name` indicates the name of the main file of the executable.
`libraries` introduces a list of the libraries we'll be using in this project,
which in this case is just the dummy library `dune` created for us under `./lib/`.

How do we add more stuff for `dune` to compile?
Most of the time, we'll just need to list the libraries we need to use under `libraries`.
This can include other OCaml libraries from `opam`.

## dune_project file

Now let's take a look at the `dune_project` file `dune` created for us:

```
(lang dune 3.2)

(name project_name) ; The name of our project

(generate_opam_files true) ; Always keep this true

(source
 (github username/reponame)) ; Once you have a github repo, place it here

(authors "Author Name") ; Your name

(maintainers "Maintainer Name")

(license LICENSE)

(documentation https://url/to/documentation)

(package
 (name project_name)
 (synopsis "A short synopsis")
 (description "A longer description")
 (depends ocaml dune) ; Add your opam dependencies here
 (tags
  (topics "to describe" your project)))

; See the complete stanza docs at https://dune.readthedocs.io/en/stable/dune-files.html#dune-project
```

Here we see a lot of fields to fill in once we know more about our project.
For a play project, we can leave these fields as they are,
but if we want to get serious about our project, we want to fill them in.
Most importantly, we want to make sure we fill in the `package`/`depends` field to have all the `opam` libraries we're using.
Running `dune build` after updating our `dune_project` file will transfer this information to the `project_name.opam` file so
`opam` knows how to handle our project.
Do not update `project_name.opam` manually! Let `dune` do it for you.

## OPAM switch

We're now going to invoke `opam`.
If `dune` manages building your individual project,
`opam` (the OCaml Package Manager) handles downloading all the other necessary OCaml packages.
`dune` speaks in terms of OCaml executables and libraries -- the products of OCaml `.ml` files.
`opam` speaks in terms of OCaml packages -- other packaged bits of OCaml code that depend on each other.
Fortunately, we don't need to write any complex configuration file for `opam` - `dune` handles it for us!

Next up, we are going to create an `opam` switch. Opam install packages globally, and switches makes it easy
to have a isolated environment in which you can install packages that will not be shared between switches,
and therefore reduce the chance of dependencies conflict. You can think of it as an analog to Python’s
virtualenv.

An `opam` switch contains a whole bunch of installed packages that are specified as compatible with each other.
However, it can only have one installed version of each package!
We're going to create an entirely new `opam` switch at our main directory.
This switch will include an OCaml compiler, our project dependencies, as well as the project itself.
We do all of this by making sure we're in our main directory and typing

`opam switch create .`

`opam` will respond with

```
Package project_main does not exist, create as a NEW package? [Y/n]
```

Answer with yes (y) to create a new local package for our project.

`opam` will now pin our project and install a whole bunch of stuff needed for our dependencies.
Finally, `opam` tells us to

```
Run eval $(opam env) to update the current shell environment
```

Do as it asks by running `eval $(opam env)`:
We need to update our shell to know about the current `opam` switch.

## Locking dependencies

Nowadays it's become quite popular to 'lock' projects to specific dependency versions.
This allows us to recreate the exact same environment on other installations.
There are two ways to restrict versions:

1. We can specify the exact versions of our dependencies in the `dune_project` file under `depends`.
   For example, we could specify
   
   ```
   (depends ocaml=4.14)
   ```
   or
   ```
   (depends ocaml>=4.14)
   ```
   if we want to specify a minimal version.
 
 2. Alternatively, we can have `opam` automatically specify the exact versions of our dependencies using the command
   ```
   opam lock .
   ```
   `opam` will create a new file for us, `project_name.opam.locked`,
   which will have these exact dependencies listed.

## Using git

At this point we have a bunch of files and directories.
What do we include in git?
Obviously, we want to place the `bin`, `lib` and `test` directories and their contents in git versioning.
We also need to include the `dune_project` and opam files.
In fact, the only things we *don't* want to include are the `_build` and `_opam` directories.
It's a good idea to add a `.gitignore` file containing

```
_build/
_opam/
```
and then to add that to our git repository as well.

## Expanding our dummy application

`dune` created a nice little skeleton application for us.
All we have to do is expand it!


* If we're writing a regular application, use `./bin/main.ml` as the starting point.
Add subdirectories and additional `.ml` files as needed.


## Libraries

Structuring your code in a modular way is one of software engineering best practices.
In OCaml and Dune, such structure can be achieved through the use of libraries.
While there may be a formal definition of it, I like to think of a library as a collection of modules
that can be depended on.

In this section, I am going to show you how to create a library with Dune.
In many open source OCaml libraries I encounter, it would seem that a flat directory structure is
preferred, so we are going with that in this tutorial.
Note that while this might be okay in most cases, you might want to create multiple libraries
if your codebase is “big enough”.

So let’s get to it! Let’s create another dune file inside the lib directory as follows:

```
(library
  (name lib))
```

Observe that instead of executable, we now use the library stanza.
It also has the field name just like an executable.
The value you put in the name field will be the identifier that you can use to refer to this library
from other executables or libraries.

To illustrate the use of libraries, we are going to add a Math module to this library,
which exposes two functions, add and sub. With your editor, create a math.ml file inside the lib directory:

```ocaml
let add x y = x + y

let sub x y = x - y
```

Nothing too hard here, we only defined the two functions. Now, let’s make our main executable
depends on this library.
Open bin/dune file on your editor and add lib (the name of your library) to the libraries
field of your executable:

```
(executable
  (name main)
  (libraries lib))
```

Great!
Then, let’s first rebuild the project so our editor can pick up and resolve the new
dependency that we just add:

```
$ dune build bin/main.exe
```

(The above step is not really necessary, but if we don’t do it we will see errors on
our editor if we try to refer any modules and functions from the new library we just
add until we rebuild the project.)

Now, open up `bin/main.ml` and replace the contents with the following:

```ocaml
open Lib

let () =
  let result = Math.add 2 3 in
  print_endline (string_of_int result);
  let result = Math.sub 3 1 in
  print_endline (string_of_int result)
```

At the first line, we open Lib so that all the modules under it (currently only Math)
is available in scope.
We then use functions from the new Math module and print out the results.

Let’s try it:

```
$ dune exec bin/main.exe
5
2
```

If I remember my elementary school math subject correctly, our program now prints
the correct result of the functions from our library!

## Interface files

One thing you may (or may not) observe from the above steps is that anything you write
on math.ml module will be automatically visible from the client module (in this case, main.ml).
This is how OCaml works; by default all identifiers are exposed from a module.

Sometimes — well, most of the times, in fact — this is not what you want.
You may have several internal small helper functions to do your job,
but you don’t want other modules to use those functions directly.
There is a way to do that, which is by using interface files.

While `.ml` files contain implementations, interfaces are put into files with .mli extensions.
An interface file is also the place where developers put API doc comments.

Suppose that for some reason, we design our Math module to only expose add function,
and leave sub unexposed for now.
We can do it by defining the following math.mli file inside lib directory:

```ocaml
val add : int -> int -> int
(** [add x y] returns the result of x + y. *)
```

In this instance, you might consider the comment redundant,
but I am a fan of always putting documentations for public facing APIs
It gives me that sense of safety: “hey, it’s documented, so it should be safe to use.”

Now, what happens if you leave main.ml as it is and you try to build the project?

```
$ dune exec bin/main.exe
(...some output...)
File "bin/main.ml", line 6, characters 15-23:
Error: Unbound value Math.sub
(...some output...)
File "lib/math.ml", line 3, characters 4-7:
Error (warning 32): unused value sub.
```

Whoops, the build fails because Math.sub is no longer found!
That is expected, because with our interface as it is we only allow add to be visible
to the client modules.
You can see how we can limit the public interface of our modules with this technique,
and keep internal implementation details, um, internal.

Okay, so how could we change the interface file to solve this build failure?
You would add a declaration of sub! Here’s what you might end up with:

```ocaml
val add : int -> int -> int
(** [add x y] returns the result of x + y. *)

val sub : int -> int -> int
(** [sub x y] returns the result of x - y. *)
```

You can try to build and run it with `dune exec` like we did before,
and it will run correctly.

## Trying out libraries interactively via utop

Another benefit of having the libraries in a separate directory from the executables
is that you can use utop REPL to play around with your functions.
The REPL will evaluate the files given,
so if any of it produces a side-effect on evaluation time
(e.g. printing, starting a web server) like what typically executables entry point do,
it will be run on starting the REPL, which may not be what you want.

Let’s have a look on how to use the REPL.
With Dune and utop installed, let’s invoke `dune utop lib`.

The command `dune utop <dir>` is a convenient way to invoke utop while having the
source inside `<dir>` (in this case, lib) automatically built and loaded.

Let’s try out our library (I will only be showing the prompt and result, and not the
extra graphics that you might actually see):

```
utop # open Lib;;
utop # #show Math.add;;              (* 1 *)
val add : int -> int -> int
utop # Math.add 1 2;;                (* 2 *)
- : int = 3
utop # let add2 = Math.add 2;;       (* 3 *)
val add2 : int -> int = <fun>
utop # add2 5;;                      (* 4 *)
- : int = 7
```

Note the double semicolon!
It’s necessary to tell utop that we want to evaluate the expression.

In this snippet, we tried opening the Lib, and:

1. Querying a type of a function;
2. Actually invoking a function;
3. Partially applying a function; and
4. Invoking the partially-applied function with the remaining arguments.

I personally find utop to be a helpful tool when I want to interactively try the
functions I defined.
It can give fast feedback on the behavior and the API of the modules,
so that I can quickly tweak things if I find something to be unsatisfactory.
If I made changes to the code and want to reload it in utop,
I usually just exit the session and spawn another one, since it’s quite fast.

To exit the utop session, you can use `CTRL+D` or use `#quit;;`.

That concludes our exploration on Dune to build our OCaml app project.
I have by no means exhausted the capabilities that Dune have, but what I demonstrated
here is sufficient to get you up and running with your own app.
