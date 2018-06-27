---
tags: [learning, quickstart]
---

# Quickstart an OCaml app project using Dune

(adapted from @bobbypriambodo's post [here](https://medium.com/@bobbypriambodo/starting-an-ocaml-app-project-using-dune-d4f74e291de8))

Let's explore how to start building an OCaml project. The project we will be building is a To-Do List app,
which connects to a PostgreSQL database as its datastore.
However, this post will only cover initializing and bootstrapping the project.
Specifically, we will be setting up Dune (formerly named Jbuilder) to build our app.

Dune, formerly Jbuilder, is the state-of-the-art build system that is currently overtaking OASIS
as the de facto build system for new projects.
The overview and strengths sections of Dune’s readme explain why so: it’s fast, has no system dependencies,
supports parallel builds, generates configuration and install files easily, and has first-class Windows support.
If it’s not enough, Dune also supports cross-compilation, builtin testing, and ReasonML syntax out-of-the-box!

## Requirements
To be able to follow this tutorial, you would need to have opam, the OCaml package manager, installed.
Consult the official docs on how to install it on your machine. I recommend using your OS package manager,
but if you’re downloading the binary, don’t forget to also download an external solver beforehand.

You can verify your opam installation with the following command:

```
$ opam --version
1.2.2
```

This tutorial assumes MacOS or Linux environment, but theoretically it should also work on Windows.

## Editor setup
You will also need to setup your editor to handle OCaml files. I highly recommend Microsoft’s VSCode
with the vscode-reasonml extension as it works great out of the box (seriously, it rocks!).

Another path that is also easy to setup is Spacemacs with OCaml layer. If those two are not to your liking,
Merlin’s wiki also has pointers to setup an IDE experience for other editors. If you’re using Emacs or Vim,
opam-user-setup can help putting the right things to your dotfiles.
Or, if you’re already using a Language Server Protocol plugin, there’s an LSP implementation for OCaml which
you can integrate to your editor.

Note that after you get these plugins or extensions installed there are some extra tools to be installed to
give you that smooth IDE experience, which will be addressed in the next section.

## Initial setup
Let’s create a new directory for our awesome project! As naming is one of the hardest problems in Computer Science,
we will choose to be uninspired and pick the most perfect name for our project: todolist.

```
$ mkdir todolist
$ cd todolist
```

Next up, we are going to create an opam switch. Opam install packages globally, and switches makes it easy
to have a isolated environment in which you can install packages that will not be shared between switches,
and therefore reduce the chance of dependencies conflict. You can think of it as an analog to Python’s
virtualenv. For more on switches, have a look at the “Switching OCaml version” section of my previous article.

We are going to name the switch todolist, the same as our project name, for consistency.
We will be using OCaml version 4.05.0 as the base compiler. To create the switch, use this command:

```
$ opam switch todolist --alias-of 4.05.0
```

If you’re on opam v2, use this instead to create a local switch:

```
opam switch create . ocaml-base-compiler.4.05.0.
```

Local switches are self-contained only in the current directory instead of an ~/.opam/<switch-name> directory.

Creating a switch will involve downloading and building the compiler.
Depending on your machine and internet connection, this could take a while!

After that, run this command to make sure our environment is properly synced:

```
$ eval $(opam config env)
```

Or, for opam 2:

```
$ eval $(opam env)
```

Neat! This will, among others, make sure that opam-installed libraries are available on our PATH.
Next up, we’re going to install some tools via opam:

```
$ opam install merlin ocp-indent jbuilder utop
```

Using this command, we install:

- `merlin`, available via the `ocamlmerlin` command, is the tool providing OCaml IDE experience that can
be integrated to your editor. Its features include context-sensitive auto-completion, error-reporting,
querying type information and documentation, and jumping to definition. Merlin will most likely be used
by your editor plugins and not you directly.
- `ocp-indent`, a simple, customizable tool to indent your OCaml source code. As with Merlin, most editor
plugins also make use of this to indent your code automatically. If you want a more opinionated solution,
there is also ocamlformat, but it’s still in active development and might not be stable yet.
You might still want to try it, though.
- `jbuilder`, the installable library of Dune. The command-line tool is still named after Jbuilder
currently, but there is plan in motion to adapt it to the new name, which probably will happen soon.
At the point of this writing, Dune’s latest version is 1.0+beta19.1.
- `utop`, an improved REPL (toplevel) for OCaml. It is based on lambda-term and supports auto-completion.
In general, I favor utop as our REPL instead of the builtin ocaml, since the former have better UX.

Wait for the install to finish, and our initial setup is done!

## Dune basics
In this section, we’re going to create a new Dune project.

### Executables
The first concept that we’re going to explore is an executable. An executable is, as the name implies,
a program that can be executed. This is contrast to a library, which we will explore in the later section.

Let’s get started! First, we need to create a `jbuild` configuration file.
Make sure you’re in the todolist directory, and create the file with the following contents on your editor:

```
(jbuild_version 1)

(executable
  ((name main)
    (libraries ()))
```
    
The file should pretty much be self-explanatory. jbuild files are written using S-expressions
(those lisp-y parentheses).
In this particular file, we note that we’re using version 1 of jbuild specification.
Each of the top-level elements are called stanzas, and currently we have two stanzas.

In the executable stanza, the value of name field denotes the module (file) name that contains the
entry point of the program.
In this case, we set it to main, meaning that Dune will look for a main.ml file on the
directory. We also have the libraries field — that is now currently empty — which will be the place
to list the libraries our executable depends on (more on that in a moment).

We’re now still missing the required main.ml file, so let’s create one:

```ocaml
let () =
  print_endline "Hello, world!"
```

This is a simple OCaml program that is going to print a hello world to the console.
Let’s try to build it via Dune:

```
$ jbuilder build main.exe
```

The build should be instant! This command will create a new directory `_build` containing
the build artifacts.
If you noticed, we used main.exe in the name there — this is a convention used by Dune to
refer to executables.
It is not to be confused with Windows-specific executables, you must also use the .exe
extension on MacOS and Linux.

After it is built, we can ask Dune to run it:

```
$ jbuilder exec main.exe
Hello, world!
```

Great! The program is working correctly. Note that since Dune 1.0+beta18, exec command also
implies build, so going forward we will mostly only use exec to build and run our program.

You might notice that currently, our created files reside at the root of the project directory.
In most cases, this is not desirable since the project root is reserved for project metadata
such as a readme, change log, license, and other project configurations.
To keep things tidy, let’s move the program to a subdirectory. We will name the directory bin,
a convention I use as a place to put entry point modules for executables:

```
$ mkdir bin
$ mv jbuild main.ml bin/
```

Let’s make sure that it’s all working correctly by cleaning and rebuilding the program:

```
$ jbuilder clean
$ jbuilder exec bin/main.exe
Hello, world!
```

Still working as expected.
Next up, we’re going to look at putting reusable code as library modules to be used from the executable.

### Libraries
Structuring your code in a modular way is one of software engineering best practices.
In OCaml and Dune, such structure can be achieved through the use of libraries.
While there may be a formal definition of it, I like to think of a library as a collection of modules
that can be depended on.

In this section, I am going to show you how to create a library with Dune.
In many open source OCaml libraries I encounter, it would seem that a flat directory structure is
preferred, so we are going with that in this tutorial.
Note that while this might be okay in most cases, you might want to create multiple libraries
if your codebase is “big enough”.

So let’s get to it! Let’s create a library directory called lib that will be the place to put
our library code:

```
$ mkdir lib
```

After that, we’ll create another jbuild file inside the lib directory as follows:

```
(jbuild_version 1)

(library
  ((name lib)
   (libraries ())))
```

Observe that instead of executable, we now use the library stanza.
It also has the field name and libraries just like an executable.
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
Open bin/jbuild file on your editor and add lib (the name of your library) to the libraries
field of your executable:

```
(jbuild_version 1)

(executable
 ((name main)
  (libraries (lib))))
```

Great!
Then, let’s first rebuild the project so our editor can pick up and resolve the new
dependency that we just add:

```
$ jbuilder build bin/main.exe
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
$ jbuilder exec bin/main.exe
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
(** [add x y] returns the result of x + y. *)
val add : int -> int -> int
```

In this instance, you might consider the comment redundant,
but I am a fan of always putting documentations for public facing APIs
It gives me that sense of safety: “hey, it’s documented, so it should be safe to use.”

Now, what happens if you leave main.ml as it is and you try to build the project?

```
$ jbuilder exec bin/main.exe
(...some output...)
File "bin/main.ml", line 6, characters 15-23:
Error: Unbound value Math.sub
```

Whoops, the build fails because Math.sub is no longer found!
That is expected, because with our interface as it is we only allow add to be visible
to the client modules.
You can see how we can limit the public interface of our modules with this technique,
and keep internal implementation details, um, internal.

Okay, so how could we change the interface file to solve this build failure?
You would add a declaration of sub! Here’s what you might end up with:

```ocaml
(** [add x y] returns the result of x + y. *)
val add : int -> int -> int

(** [sub x y] returns the result of x - y. *)
val sub : int -> int -> int
```

You can try to build and run it with jbuilder exec like we did before,
and it will run correctly.

## Trying out libraries interactively via utop

Another benefit of having the libraries in a separate directory from the executables
is that you can use utop REPL to play around with your functions.
The REPL will evaluate the files given,
so if any of it produces a side-effect on evaluation time
(e.g. printing, starting a web server) like what typically executables entry point do,
it will be run on starting the REPL, which may not be what you want.

Let’s have a look on how to use the REPL.
With Dune and utop installed, let’s invoke jbuilder utop lib.

The command `jbuilder utop <dir>` is a convenient way to invoke utop while having the
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
in this article is sufficient to get you up and running with your own app.
