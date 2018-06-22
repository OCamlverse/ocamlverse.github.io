---
tags: [learning, types]
---

# Weak Type Variables

## Polymorphism and type variables

All terms of a well-typed program must have a type. The type of a term
denotes in which context the term could be used. For example, a
program term `42` has type `int` and could be used anywhere, where
`int` is accepted. If a term could be used in several different typing
contexts (i.e., when the type of the term varies), then it is denoted
by a type variable in the term type. For example, `'a list` denotes a
term that fits into any place where some list is expected, e.g., `int
list`, `float list`, etc. We call such types _polymorphic_, as opposed
to _monomorphic_ types, that are sometimes called _ground_ types.

In OCaml a type of a term is inferred from its definition. OCaml tries
to find the most unrestrictive type, i.e., the most general type. For
example, a term `fun (x,y) -> (y,x)` has type `('a * 'b) -> ('b *
'a)`.  That is a term, that accepts a term that is a pair of any two
types, and swaps them.

## Why so weak?

The problems arise when we have to deal with mutable values. In pure
languages without mutability, we can treat values as pure mathematical
objects. This is nice, because all the properties of a mathematical
object are fully defined by its structure. So our knowledge is static
and there are no time variables involved. In not so pure languages,
i.e., in languages that support mutablility, a mutable value is
represented as a cell of memory, a placeholder. An assignment places a
real value into the cell (this real value could also be a cell by
itself, but let's not complicate things any further). We can't allow
the type of a value in the cell to change along the time, as in the
statically typed programming languages the type of a term is static,
i.e., it doesn't change in time. We can't say that this program is
well-formed _until_ someone puts a value of a wrong type into the
cell. Of course, OCaml is a statically typed language and it doesn't
allow a reference to change its type during the time, so after we put
a value of some type into a cell, the cell type is sealed. But what if
we put into the cell a value, that can have several types, i.e., a
value that has polymorphic type. Which type the compiler shall select?

For example let's consider the following simple program `let x = ref
None`. The `None` value is pure and has type `'a option`. The `ref`
value is also pure, and has type `'a -> 'a ref`. However, the `'a ref`
type has the following representation `type 'a ref = {mutable contents
: 'a}`. So which type the compiler should give to the value `x`. The
value put to the reference has type `'a option`, that denotes a whole
family of types, where no type is better than another. Since compiler
can't make any choice here, it denotes it by weakening the type
variable, and ascribing to `x` the following type `'_a option` (modern
versions of OCaml use `'_weak1` to make it more noticable and
explicit). Although `'_a` is named "weak type variable" it is not
actually a variable, but rather an _unknown_ type. What the compiler
is trying to say is: "this type is monomorphic, because it is mutable,
but I can't infer its type yet, because I didn't collect enough
information". Later usages of `x` may provide more insights to the
compiler, and the weak type variable will be transformed to a ground
type. E.g., `x := Some 42` will say to the compiler, that `'_a` is
actualy `int`. This gives us yet another insight on what the weak type
variable is - it is a delayed concrete type. However, the compiler may
not delay the decision infinitely, it must decide before the end of
file, aka compilation unit. Indeed, we do not want other files to
define what is the type of a variable defined in our file. So, if in
the scope of a file, the compiler didn't find enough evidences that
will reveal the true nature of the weak type variable, then an error
is signaled and we need to intervene and ascribe manually ground types
for all weak type variables. This is the rare case, when type
annotation is really required in OCaml.

## Why does my immutable value have a weak polymorphic type?

Now it is clear, why references and other mutable values can't have
polymoprhic type, and why weak variables arise in case if the compiler
can't infer the ground type for a mutable value. This is reasonable
limitation and a fair tradeoff - if you need a mutable cell, then type
it manually (as a courtesy, compiler may type it for you, if it
can). But unfortunately, this is only the start of the story, as
compiler may give weak types to terms that do not involve any mutable
values. Consider the following example. Suppose we have a function
`let const x y = y`. Why does `const ()` have type `'_a -> '_a`?

The problem is that `const ()` is a partial application. The result of
a function application is a runtime value called _closure_. Since this
value will be created only in runtime, the typechecker can't inspect
it, so it is left beyond its reach, so it should be very pessimistic
if not to say paranoid, and assume that the closure may create
arbitrary references and use them to breach the type
soundnessness. And in this case it is not over precautious, as we
indeed can breach it, as show below

```ocaml
let const _ =
  let cache = ref None in
  fun x -> match !cache with
    | Some cached when cached = x -> cached
    | _ -> cache := Some x; x
```

This function has the same type as the benign `const` function, `'a ->
'b -> 'b`, however its behavior is quite different. This function adds
a sort of hash-consing/memoization capability. It creates an identity
function, that reference to a storage, and if the last value is
structurally equal to the current value, the last value is
returned. Let's suppose that the typechecker would be more lax and
will give type `'a -> 'a` function `id` in `let id = const ()`. Then
this function could be applied as follows `id []; id None`. The first
application of `id` will cache the empty list, while the second
application will compare an empty list with `None`, that will breach
the type system. Even funnier, passing references to this function
will establish unsafe value aliasing, e.g., `let x = ref 0 and y = ref
3.14 in id x; id y := 0.0` will cause a segmentation fault.

Fortunately, nothing like this will happen in the real world, as OCaml
typechecker will give the weak polymorphic `'_a -> '_a` type to the
identity function created by the partial application to `const`. And
although `fun _ x -> x` is totally benign it has the same type as the
cached version of `const` so for the typechecker they are
indistinguishable. This basically puts partial applications in the
same group with references, arrays, hashtables, and other program
constructs that the type checker will suspect in impurity. In fact,
computer scientists decided instead to specify a class of program
terms that are always pure and require all other terms to have the
monomorphic type and weaken all type variables. They defined this
class syntactically and called it _values_. Hence the name _value
restriction_. The name _value_ here has nothing to do with the runtime
notion of a value, unfortunately this is an example when the locally
defined terminology leaks out of the context of its definition and
wreaks havoc around the world. In the context of the type systems, the
word "value" corresponds to a syntactic class of non-reducible terms,
in other words to syntactic constructs that are defined on the source
level, static constants. So the better name would be static
restriction, that allows only statically defined terms to have
polymoprhic type. But unfortunately the value restriction is the
historic name, so let's take it as granted.

## Relaxed Value Restriction

The value restriction was the first and rather pessimistic restriction
on value polymorphism, as it allowed only static constants to have a
polymorphic type. E.g., values such as `[]`, `None`, `fun x ->
x`. While all other values were considered as possibly impure. The
good news is thatin OCaml this restriction is relaxed, and besides
syntactic constants OCaml allows some other classes of expressions to
be generalized (i.e., to have the polymoprhic type).  First of all,
OCaml allows polymorphism for _non-expansive_ expressions, where an
expression is non-expansive if it doesn't have any observable
side-effects during the evaluation. That basically extends the notion
of constant from purely syntactic definition (something that looks
like a constant, is a constant) to semantic definition (something that
acts like a constant, is a constant). For example, this rule allows
the following expressions to have polymorphic type: `lazy None`, ` let
_ = ref None in 1`, and even `assert false`. However, the following
expression `(fun _ _ -> 0) ()`, will be given a non-polymorphic type
`'_a -> unit`, since the function `fun _ _ -> 0` can perform some
observable side-effect (it doesn't, but the typechecker doesn't look
into the body of a function).

## Subtyping???

Now is the most confusing part, the final bit of laxing the value
restriction is allowing the generalizaton of covariant type
variables. So how did this happen, that subtyping has any relation to
the value restriction?  Does OCaml objects break polymorphism and
complicates things even more? No, nothing like this. In fact, it has
nothing to do with the OCaml object system and with the way how
objects are typed in OCaml. Before we will delve into description we
need to build some intuition about the variance. Most of the articles
are of no help for us, as they focus on subtyping.  And it is really
hard to connect subtyping with value restriction. So let's forget
about subtyping and focus on functions.

In a function type, a type variable is _covariant_ if it occurs _only_
to the right of the arrow, if a variable occurs _only_ to the left of
the arrow, then it is _contravariant_. Otherwise, a variable is
_invariant_. That is all that we need to know about variance in to
build the right intuition to understand why it matters for the value
restriction.  In OCaml it is possible to specify variance of a type
variable: covariant variables are denoted with the prefix `+`, and
contravariant are denoted with the `-` prefix, e.g., `type (-'a,+'b)
fn = 'a -> 'b`. OCaml typechecker will infer the variance
automatically if the type definition is available. For example, for
the `'a -> 'b` type OCaml will know without any further ado that `'a`
is contravarint and `'b` is covariant. But if the type is abstract,
the the only way to preserve this information is to use the above type
annotations. It is also useful to play with variance annotations in
the toplevel, to get the intuition.

So, let's go back to the value restriction. The intuition behind the
covariant type, is that values of this type are never consumed, but
only produced (e.g., `unit -> 'a`, `int -> 'a`, etc). Thus if a
computation produced a value that is polymoprhic in some type `'a`
which is covariant, then it is guaranteed that values of this type was
never stored/captured or anyhow abused during the computation. Thus it
is safe to ascribe the polymoprhic type to this value.

Since OCaml has variance inference this usually works out of box,
e.g., given a function `val f : unit -> unit -> 'a` a partial
application `f ()` will have polymorphic type `unit -> 'a`. However,
if we will decide to abstact `unit -> 'a` as

```ocaml
module Thunk : sig
   type 'a t
   val create : unit -> 'a t
end = struct
   type 'a t = unit -> 'a
   let create () = fun () -> assert false
end
```

Then semantically the same code will suddenly get the weak type again:

```
Thunk.create ();;
- : '_a Thunk.t = <abstr>
```

The reason is that since we hide the type definition, OCaml can't
infer variance and pessimistically assume that `'a` is invariant in
`'a Thunk.t`. We can help the typechecker with the variance annotation
in module signature:

```ocaml
module Thunk : sig
   type +'a t
   val create : unit -> 'a t
end = struct
   type 'a t = unit -> 'a
   let create () = fun () -> assert false
end
```
and now everyone is happy:

```
# Thunk.create ();;
- : 'a Thunk.t = <abstr>
```

## Conclusion

The value restriction is a pessimistic assumption that compilers must
make in the face of the possible mutability, and it is a price that
must be payed even if mutability is not used. Weak type variables
alleviate the problem a little, by allowing us to omit type
annotations for values that don't have concrete or polymorphic
type. However, since types are analyzed on the compilation unit level
(the file level), weak type variables can't escape the scope of a
compilation unit (the scope of a file). So it is not possible to have
a weak type variable in the module interface (e.g., in the `mli`
file). The compiler will reject all toplevel definitions that have
weak types, unless they are either hidden from the module interface
(i.e., omitted in the interface - e.g., when the mli file is empty) or
given a concrete type.

If for some reason the compiler refuses to generalize your expression
and weak type variables occur in your type, then you can try the
following options to fix the situation:

- Convert your expression to a syntactic constant, by making it a
function, aka eta-expansion. E.g., `let x = ref None` could be made
polymorphic by making `x` a function, e.g., `let x () = ref None`
- If the problematic type is abstract, then the compiler can't perform
the variance analysis on it. You can expose that some type variables
of your abstract type are covariant, by making the variance
annotations, e.g., `type +'a t` in the  signature will tell the
compiler that values of that type could be safely given the
polymorphic type. (Of course, the definition should correspond to the
specification, that is checked by the compiler, for example, `type +'a
t = 'a list` would be accepted by the type checker, where `type +'a t
= 'a ref` will be rejected).
- If nothing else helps, then you need to manually annotate your value
with a concrete type and/or hide it from the interface (by adding an
mli file).

## Further reading
- [Side effects and weak polymorphism](https://realworldocaml.org/v1/en/html/imperative-programming-1.html#side-effects-and-weak-polymorphism) in *Real World OCaml*,
- [Section 5.1 Weak polymorphism and mutation](http://caml.inria.fr/pub/docs/manual-ocaml/polymorphism.html#sec51)
in the OCaml Manual,
- [Common Error Messages](http://ocaml.org/learn/tutorials/common_error_messages.html#The-type-of-this-expression-contains-type-variables-that-cannot-be-generalized) at ocaml.org,
- ["My function is not polymorphic (enough) ?"](http://caml.inria.fr/pub/old_caml_site/FAQ/FAQ_EXPERT-eng.html#eta_expansion) and subsequent sections in "Frequently asked Questions about Caml".
- [Relaxing the Value Restriction in OCaml](https://caml.inria.fr/pub/papers/garrigue-value_restriction-fiwflp04.pdf)
