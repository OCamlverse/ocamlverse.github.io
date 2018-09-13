# A Very Basic Introduction to Functors

Originally written by "Kantian" on
[Discuss](https://discuss.ocaml.org/t/help-me-to-understand-functors/)

Good documentation on the module system and functors is given here:

- [The module system](http://caml.inria.fr/pub/docs/manual-ocaml/moduleexamples.html)
- [Destructive substitution](http://caml.inria.fr/pub/docs/manual-ocaml/extn.html#sec249)

We'll explain how modules and functors work with a simple example.

## Modules

Imagine that you want to define the notion of sets of `int` with one
predefined value and two functions on it:

- the `empty` set
- `is_element` to test if an `int` belongs to a given set
- `add` to add an int in a set (but only if it is not already present).

We can represent a set of int as a list of int, so we define this module:

```ocaml
module Int_Set = struct
  type elt = int (* an alias to `int` for the elements of the set *)
  type t = elt list (* an alias for the type of sets *)

  let (empty : t) = []

  let rec is_element i (set : t) =
    match set with
    | [] -> false
    | x :: xs -> if x = i then true else is_element i xs

  let add i set = if is_element i set then set else i :: set
end
```

We can play around a bit with this module:


```ocaml
let s = Int_Set.(add 1 (add 2 empty));;
val s : Int_Set.t = [1; 2]

Int_Set.is_element 2 s;;
- : bool = true

Int_Set.is_element 3 s;;
- : bool = false
```

We can also `add` elements and verify that  the invariant
that an element already present isn't added again is maintained:

```ocaml
Int_Set.add 3 s;;
- : Int_Set.t = [3; 1; 2]

Int_Set.add 2 s;; (* the invariant is satisfied *)
- : Int_Set.t = [1; 2]
```

But there is a problem: since the concrete representation of the type
of sets is known (they are just lists), we can *break* the invariant:

```ocaml
Int_Set.add 3 (2 :: s);;
- : Int_Set.t = [3; 2; 1; 2]
```

The solution is to use what is called an *abstract* type.

## Signatures

When you define a module, the compiler automatically infers its type
or its *signature*. For the module defined above, the toplevel
returns:

```ocaml
module Int_Set :
  sig
    type elt = int
    type t = elt list
    val empty : t
    val is_element : elt -> t -> bool
    val add : elt -> t -> t
  end
```

What we can do is to define a less precise signature to
*hide* the fact that sets are implemented using lists:

```ocaml
module type S = sig
  type elt = int
  type t
  val empty : t
  val is_element : elt -> t -> bool
  val add : elt -> t -> t
end
```

Here, since we want to add `int`s to our sets, we don't hide the fact
that elements are `int`.

We can now restrict the interface of our module and the invariant
can't be broken anymore:

```ocaml
module Abstract_Int_Set = (Int_Set : S)

let s1 = Abstract_Int_Set.(add 1 (add 2 empty));;
val s1 : Abstract_Int_Set.t = <abstr>

1 :: s1;;
Error: This expression has type Abstract_Int_Set.t
       but an expression was expected of type int list
```

So far so good. We have a simple notion of sets of int and we can
preserve an invariant, but what do we do if we want to *generalize*
this notion to have sets over other types without repeating ourselves?
That's where *functors* come into play.

## Functors

In the same way that functions are used to *construct* new values
given other values as parameters, functors are used to *construct* new
modules given other modules as parameters.

First, as in our `int` case, to define sets for a given type we need
to know when two values are equal. So we define this signature:

```ocaml
module type EQ = sig
  type t
  val eq : t -> t -> bool
end
```

Then we define the general signature for a set module:

```ocaml
module type SET = sig
  type elt
  type t
  val empty
  val is_element : elt -> t -> bool
  val add : elt -> t -> t
end
```

Finally we write code to explain how to construct a set module for a
specific type when we are given a function to test equality between its
values:

```ocaml
module Make_Set (Elt : EQ) : SET with type elt = Elt.t = struct
  type elt = Elt.t
  type t = elt list

  let empty = []

  let rec is_element i set =
    match set with
    | [] -> false
    | x :: xs -> if Elt.eq x i then true else is_element i xs

  let add i set = if is_element i set then set else i :: set
end
```

The code is mostly the same as before, except in the function
`is_element` where to test for equality we now use the function `Elt.eq`
given by the parameter of the functor.

Now, with this *generic* way to construct module of sets, we can
easily redefine our previous module:

```ocaml
module Abstract_Int_Set = Make_Set (struct type t = int let eq = (=) end)

let s2 = Abstract_Int_Set.(add 1 (add 2 empty));;
val s2 : Abstract_Int_Set.t = <abstr>

Abstract_Int_Set.is_element 2 s2;;
- : bool = true

Abstract_Int_Set.is_element 3 s2;;
- : bool = false
```

But now we can also use it to define sets of `string`s:

```ocaml
module String_Set = Make_Set (struct type t = string let eq = (=) end)

let s = String_Set.(add "hello" (add "world" empty));;
val s : String_Set.t = <abstr>

String_Set.is_element "hello" s;;
- : bool = true

String_Set.is_element "foo" s;;
- : bool = false
```

I hope that you can now see what functors are, how to define them, and
how to use them.
