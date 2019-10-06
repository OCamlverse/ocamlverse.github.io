---
tags: [learning, ecosystem]
---

# Quick and Dirty Guide to Monadic Parsers and Angstrom

Author: Metin Akat [@loxs](https://github.com/loxs)

Review: Ivan Gotovchits [@ivg](https://github.com/ivg)

## Abstract
This tutorial aims to give you abilities to write parsers quickly for your daily tasks. It's not a formal or academic explanation of parsers, grammars, monads etc. On the contrary, it aims to be as informal as possible and to have as little requirements for previous knowledge as possible.

## Requirements
You need to be a moderately accomplished programmer to read this. Also, basic knowledge of OCaml and functional programming is required. Probably reading (and understanding) the [first chapter of Real World Ocaml](https://dev.realworldocaml.org/guided-tour.html) is enough.
We will not replicate the documentation of every individual [Angstrom](https://github.com/inhabitedtype/angstrom) parser and combinator. They are documented [here](https://github.com/inhabitedtype/angstrom/blob/master/lib/angstrom.mli). So although we will explain the usage, go consult the formal definition if you need it.
Also, there are formal documents describing monads and parser combinators (and Angstrom mostly adheres to the conventions defined there) but they are **not** preconditions for reading this tutorial.

## Terminology
Monadic parsers are called so, because they use monads to allow you to represent the convoluted logic of covering all the possible cases when writing a grammar. Monads allow you to do things like "only proceed if this condition is met", which is really valuable when writing a parser.
Another term you will come upon is "**parser combinator**" and in order to understand that, you need to know what is a "parser". In the case of monadic parser combinators, a parser is any function that does a "piece of parsing" and the "parser combinator" is a monadic operator provided by the library (in our case Angstrom) with the aim of letting you combine your parsers in such a way that allows you to write parsers without too many `if` or `match` expressions.

## A word on infix operators
OCaml has this feature which is somewhat obscure and not always (or very briefly) mentioned in books and tutorials. Depending on the first character of a function, it can behave as an infix operator.
This is a core feature of OCaml and Angstrom (and lots of other monadic interfaces) exploit it in order to achieve their goals. Explained [here](http://caml.inria.fr/pub/docs/manual-ocaml/expr.html) and [here](http://caml.inria.fr/pub/docs/manual-ocaml/lex.html#sec82).

So anyone can define such a function like this:

```ocaml
let ( *> ) param1 param2 =
    calc_something param1 param2
```

Which can later be used like `param1 *> param2`

Try to make sense of this concept before proceeding, as otherwise you will have a very hard time.

## A basic explanation of monads and parsers
Lets see what the `*>` combinator of Angstrom is used for.
Presuming we have the following two parsers (which we'll define later in this tutorial): `integer` and `whitespace`, we can write a combinator expression like this:
```ocaml
whitespace *> integer
```
In pure English, this means: Parse whitespace, then discard it, then parse integer and return it". There is a corresponding combinator - `<*` which does "the opposite", so we can even write this:
```ocaml
let int_without_whitespace =
   whitespace *> integer <* whitespace
```
which means: 1) parse whitespace and (if successful) discard it 2) parse integer and (if successful) retain it 3) parse whitespace and (if successful) discard it, while returning the result of the previous step. So overall evalutation of the whole expression returns the integer. This is really powerful, as otherwise we would have to write lots of functions like this:
```ocaml
let discard_first parser1 parser2 input =
    match run_parser parser1 input with
    | Result.Ok _result1 remainder -> run_parser parser2 remainder
    | Result.Error e -> Error e
```
Of course, the [actual implementation](https://github.com/inhabitedtype/angstrom/blob/c914dbc91188e258027b56d91cc42edc40bbe3f7/lib/parser.ml#L110) is a bit more complex and relying on previous definitions, but in essence it does exactly what our naive function does.

In the same way we could define `discard_second` and combine them like this:
```ocaml
discard_second (discard_first whitespace integer) whitespace
```

This is a a lot less straightforward and less readable. And the situation becomes even worse if you tried writing more complex logic. And that's probably the main reason for the invention of the parser monad, as it hides this complexity. So here is another amateur attempt at defining what the parser monad is (at least for our context). You can think of the parser monad like a device that links your parsers in a chain (using the combinators), and runs them using a function that has roughly the following definition:
```ocaml
let rec run state remainder_of_input =
  match check_state_for_errors state with
  | Error e ->
    generate_error state
  | Ok result ->
    let new_state = evaluate_next_combinator_with_result state in
    run new_state new_state.next_parser
```

And when you write your parsers and combinators, they get evaluated in order by the state monad, which treats the combinators as special conditions in order to decide what to do with your state and results. Of course, the above definition is very naive and implementing the state monad is quite a lot harder, but that (again) is the essence of it.

## A Hello World Example
So let's proceed with actually defining our most basic (and functioning) parser.
Consider this:

```ocaml
open Angstrom

let is_whitespace = function
  | '\x20' | '\x0a' | '\x0d' | '\x09' -> true
  | _ -> false

let whitespace = take_while is_whitespace
```

Start utop and have Angstrom available there ([here is a good tutorial on doing that](quickstart_ocaml_project_dune.md)), then paste the above definitions, and we'll get something like this evaluated:

```ocaml
val is_whitespace : char -> bool = <fun>
val whitespace : string t = <abstr>
```

Angstrom (like other parsers) works on chars. It provides you with tools to compare chars and act on the results. Our first function `is_whitespace` provides just the comparison of whether a char is any of the chars considered to constitute whitespace (at least for our needs right now). The second function `whitespace` is the actual parser which is of the proper type to be considered by Angstrom to be a "parser".

We already use a predefined (in Angstrom) parser which is called `take_while`. You can consult the angstrom docs, and it's also quite self explanatory, but it takes chars while our predicate (`is_whitespace`) returns true.

We can then try it:
```ocaml
utop # Angstrom.parse_string whitespace "    ";;
- : (string, string) result = Result.Ok "    "


utop # Angstrom.parse_string whitespace " 1 ";;
- : (string, string) result = Result.Ok " "
```

Something interesting happened in the second example... Although we provided a string that contains more than only whitespace, the parser is perfectly happy to return only the whitespace that it was able to parse (Just a single space). This is probably not what we want, and we need to account for that in our program. But that's how we have written our parser - we haven't instructed it to fail if it finds other things after what we wanted. We can do that now:

```ocaml
let only_whitespace =
  whitespace
  >>= fun parsed_whitespace ->
  peek_char
  >>= function
  | None -> return parsed_whitespace
  | Some c -> fail (Format.sprintf "Unexpected char %c" c)
```

And when we run it, we get:
```ocaml
utop # Angstrom.parse_string only_whitespace " 1 ";;
- : (string, string) result = Result.Error ": Unexpected char 1"
```

Here we make use of the `>>=` combinator which means "If the previous parser is successful, take the result of it and feed it to the next parser".

Another built in parser is `peek_char` which looks ahead a character, whithout moving the current position of parser state forward in the input string.

Also, note the usage of `return` and `fail`. If you come from imperative languages, `return` is not the same as what you are used to. Here `return` is just a function that packs what we give it into a structure recognized by the state monad as a "successful parsed result". `fail` is the opposite - it packs the result in a structure, that tells the state monad that we have failed and we want it to treat this as an "unsuccessful parser result". Both success and "not success" can be interpreted by higher level parsers the way we want (by using the appropriate combinators). Of course, if a failure reaches the "top layer" of the parser, Angstrom will just return it, as it did above.

Lets look at another important concept when writing grammars:

```ocaml
utop # Angstrom.parse_string whitespace "";;
- : (string, string) result = Result.Ok ""
```

Here we feeded our parser with an empty string and we still got a successful result. That's because `take_while` won't fail if it doesn't encounter the chars which we are looking for. But if we wanted it to, we could use its sibling, which in Angstrom is called `take_while1`. If we rewrite our whitespace function with it, it will fail unless it encounters at least one successful evaluation of the predicate.
This is an important decision when writing your parsers. When working with whitespace, it is often reasonable to use `take_while`, if you want your whitespace to be optional in the language you are defining/parsing.

But next, lets define a parser wich actually does make use of `take_while1`, so that we are able to parse integers:

```ocaml
let is_digit = function '0'..'9' -> true | _ -> false

let integer =
    take_while1 is_digit
```

And let's test it:

```ocaml
utop # Angstrom.parse_string integer "1";;
- : (string, string) result = Result.Ok "1"

utop # Angstrom.parse_string integer " ";;
- : (string, string) result = Result.Error ": count_while1"

utop # Angstrom.parse_string integer " 1";;
- : (string, string) result = Result.Error ": count_while1"
```

Do you see where is this going?

```ocaml
utop # Angstrom.parse_string (whitespace *> integer <* whitespace ) " 1 ";;
- : (string, string) result = Result.Ok "1"
```

So here is your monadic parsers "hello world" example :-)


## More Advanced Parsers

Taking on from where we left, let's see what are the problems we have with our current state of affairs:

```ocaml
utop # Angstrom.parse_string (whitespace *> integer <* whitespace ) " -1234";;
- : (string, string) result = Result.Error ": count_while1"
utop # Angstrom.parse_string (whitespace *> integer <* whitespace ) " 1234.35";;
- : (string, string) result = Result.Ok "1234"
```

We are not able to parse negative integers and neither are we able to parse floats. Lets give it a go:

```ocaml
let sign =
  peek_char
  >>= function
    | Some '-' -> advance 1 >>| fun () -> "-"
    | Some '+' -> advance 1 >>| fun () -> "+"
    | Some c  when (is_digit c) -> return "+"
    | _ -> fail "Sign or digit expected"

let dot =
  peek_char
  >>= function
  | Some '.' -> advance 1 >>| fun () -> true
  | _ -> return false

let number =
  sign
  >>= fun sign ->
  take_while1 is_digit
  >>= fun whole ->
  dot
  >>= function
  | false ->
     return (float_of_string (sign ^ whole))
  | true ->
     take_while1 is_digit >>= fun part ->
     return (float_of_string (sign ^ whole ^ "." ^ part))
```

This shouldn't really be that more complex than before.
One interesting concept here is employing `advance 1` where we peeked one char (which doesn't advance the position of the parser) and then acting accordingly.
Another new combinator is `>>|` which is quite like `>>=` but doesn't require us to use `return`, but instead packs the result of the function for us.

```ocaml
utop # Angstrom.parse_string number "-10.45";;
- : (float, string) result = Result.Ok (-10.45)

utop # Angstrom.parse_string number "10.45";;
- : (float, string) result = Result.Ok 10.45

utop # Angstrom.parse_string number "something_else 10.45";;
- : (float, string) result = Result.Error ": Sign or digit expected"
```

By this point (and after consulting the [.mli docs](https://github.com/inhabitedtype/angstrom/blob/master/lib/angstrom.mli)) you should be quite comfortable with understanding the example given in the Angstrom [README](https://github.com/inhabitedtype/angstrom/blob/master/README.md)

But still, here is some explanation of some of the concepts used there...

* `<|>` combinator is like a logical `or`. If the left parser returns a failure, the right one is evaluated (with the same input, so this means backtracking)
* `lift1`, `lift2`, etc - here is some [explanation](https://discuss.ocaml.org/t/angstrom-parser-optimization/1754) on how to use these. They are (a little convoluted) way to tell the parser monad to run several parsers in sequence while retaining everything they return
* `fix` is the way to impose recursion on the parser monad


## Abstract Syntax Tree

Let's revisit our number parser from above and try to combine it to work with another parser. Imagine that we have a file with key/value pairs where the key is a word and the value is a number:

```ocaml
let key = take_while1 (function 'a'..'z' -> true | _ -> false)

let key_value =
  key <* whitespace
  >>= fun k -> number >>= fun v -> return (k, v)

```

```ocaml
utop # Angstrom.parse_string key_value "apples -23.48";;
- : (string * float, string) result = Result.Ok ("apples", -23.48)
```

For this very simple example, returning a tuple is OK, but it gets ugly very fast if you try to parse more complex things. That's the reason you need to have more complex types which can coexist with each other in a tree, the so called "abstract syntax tree".

That's what they are doing here in the Angstrom JSON parser [example](https://github.com/inhabitedtype/angstrom/blob/c914dbc91188e258027b56d91cc42edc40bbe3f7/examples/rFC7159.ml#L3)

If you are new to OCaml, by this point you should read about Variants and Records and start using them to represent your ASTs

## Epilogue

If you reached this point of the tutorial, you should be able to write pretty complex parsers with this knowledge.

Here are some gotchas which might make your life easier/harder:

* Try to use the `list` and `choice` combinators as little as possible. Read [here](https://discuss.ocaml.org/t/angstrom-parser-optimization/1754) why. Instead, write more functions by using the `>>=` combinator as we did in the `number` parser. Also, you can use look ahead in order to decide what to do next.

* Try to separate (into two steps) lexical and semantic analysis. It's much less bug prone if you have two separate codebases where one only cares about identifying parts of your grammar and the next verifies logical dependencies like "is this number negative" etc. This usually means doing a second (or even third) pass over the AST where you do the needed transformations (or build a completely separate structures out of the AST).

* Trust the compiler and the editor tools (like Merlin). Do not waste huge amounts of time while trying to have a working version all the time. You don't need to constantly check (via utop) how things work. If they typecheck, they most probably will work in the end.
