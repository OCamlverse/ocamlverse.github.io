---
tags: [learning]
---

# `if`, semicolon, and `let`

**tl;dr**: If a `let` expression in the final branch of an `if` expression is followed
by a semicolon, the `let` expression will include what's after the semicolon.
One might expect that the semicolon ends the `if` expression, and that the code
following it will execute *after* the entire `if` expression, but instead that
code is part of the  `if` expression.  This can introduce subtle bugs, which
may be difficult to see if indentation makes it look like the code after the
semicolon is not part of the `if` and `let` expressions.  To instead make the
semicolon follow the entire `if` with the embedded `let`, wrap the `let` expression
in parentheses or `begin`/`end`.

Suppose we have an `if` expression executed for the sake of
side effects.  This is a complete expression. A subsequent semicolon
will sequence the next expression so that it is always executed:
```ocaml
let foo n = 
  if n < 0 
  then print_string "low\n" 
  else print_string "high\n";
  print_string "done\n"
```
Let's try it out in `utop`:
```ocaml
# foo 42;;
high
done
- : unit = ()
# foo (-42);;
low
done
- : unit = ()
```
So far, so good.  Now we decide to introduce a `let` inside the first 
branch of the `if`, like this:
```ocaml
let bar x =
  if x < 0
  then let message = "low\n" in
    print_string message
  else print_string "high\n";
  print_string "done\n"
```
This behaves identically to the `foo` function defined above.  Great.

Next we define a function in which the let is in the second branch of
the `if`:
```ocaml
let buggy_baz x =
  if x < 0
  then print_string "low\n"
  else let message = "high\n" in
    print_string message;
  print_string "done\n"
```
Let's try it out in `utop`:
```ocaml
# buggy_baz 42;;
high
done
- : unit = ()
# buggy_baz (-42);;
low
- : unit = ()
```
What happened to the final "done" output in the second example?

The problem is that the `let` expression captured the final `print_string`.
OCaml interpreted the semicolon before `print_string "done\n"` as sequencing
it *within* the scope of the `let` expression, rather than after the entire 
`if`/`then`/`else`.  As a result, `print_string "done\n"` only runs when 
the `else` clause is executed.  Don't let the misleading indentation fool you.

We can fix the problem by explicitly delimiting the scope of `let` using
parentheses or `begin`/`end`:
```ocaml
let baz x =
  if x < 0
  then print_string "low\n"
  else (let message = "high\n" in
    print_string message);
  print_string "done\n"
```
Or:
```ocaml
let baz x =
  if x < 0
  then print_string "low\n"
  else begin 
    let message = "high\n" in
    print_string message
  end;
  print_string "done\n"
```
These functions will behave identically to the original `foo` function above.

Note that you have to include a semicolon after the closing `)` or `end`.
Otherwise you will get a potentially confusing error message such as this one:
```
Error: This expression has type unit
       This is not a function; it cannot be applied.
```

The semicolon problem also occurs with a single-branch `if`/`then` expression.
`let` will capture anything that's sequenced in whatever happens to be the last 
`if` clause.
