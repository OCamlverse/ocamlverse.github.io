---
tags: [learning]
---

# An if, semicolon, and let gotcha

## tl;dr

When a `let` expression begins in the final branch of an `if` expression,
a semicolon will not terminate the `let`; instead the `let` expression will include
the code that comes after the semicolon.  One might expect that the semicolon ends the
`if` expression, and that the code following it will execute *after* the entire `if` expression,
but instead that code is part of the  `if` expression.  This can introduce subtle bugs because
the code may behave as expected when the final branch of the `if` executes, but not when it
doesn't.  Indentation that suggests that the code after the semicolon is not part of the `if`
and `let` can also make the bug difficult to see.  To make the semicolon follow the entire `if`
with the embedded `let`, wrap the `let` expression in parentheses or `begin`/`end`.
(The apparent problem is a consequence of the normal, useful behavior of `let` interacting
user expectations for how `if` works.)

## The problem

Suppose we have an `if` expression executed for the sake of
side effects.  This is a complete expression. A subsequent semicolon
will sequence the next expression so that it is always executed:

```ocaml
let foo n =
  if n < 0
  then print_string "low\n"
  else print_string "high\n";
  print_string "ok\n"
```

Let's try it out in `utop`:

```ocaml
# foo 42;;
high
ok
- : unit = ()
# foo (-42);;
low
ok
- : unit = ()
```

So far, so good.  Now we decide to introduce a `let` inside the first,
`then` branch of the `if`, like this:

```ocaml
let bar x =
  if x < 0
  then let message = "low\n" in
    print_string message
  else print_string "high\n";
  print_string "ok\n"
```

This behaves identically to the `foo` function defined above.  Great.

Next we define a function in which the let is in the second, `else`,
branch of the `if`:

```ocaml
let buggy_baz x =
  if x < 0
  then print_string "low\n"
  else let message = "high\n" in
    print_string message;
  print_string "ok\n"
```

Let's try it out in `utop`:

```ocaml
# buggy_baz 42;;
high
ok
- : unit = ()
# buggy_baz (-42);;
low
- : unit = ()
```

Why is the final "ok" output missing in the second example?  This isn't
what we intended.

This problem will also occur with a single-branch `if`/`then` expression
and a `let` in the `then` branch.

## Why does the problem occur?

The problem is that the `let` expression captured the final `print_string`.
OCaml interpreted the semicolon before `print_string "ok\n"` as sequencing
it *within* the scope of the `let` expression, rather than after the entire
`if`/`then`/`else`.  As a result, `print_string "ok\n"` only runs when
the `else` clause is executed.

Misleading indentation, as in the example above, can make it difficult to see
the problem.  `print_string "ok\n"` should be indented in the same way as the
line above it.

This behavior is really just a consequence of the normal (and useful) scoping
rule for `let`.  Here's an example in `utop`:

```ocaml
# let x = 3 in
print_int x;
print_string ",";
print_int x;
print_string "\n";;
3,3
- : unit = ()
```

`let` is designed have a scope that extends past semicolons. (How far? That's a
bigger question about OCaml syntax more generally.)  The problem is that
when the `let` is in the last branch of the `if`, it can be natural for us to
think that the semicolon ends the `if` expression, as it would if the `let` wasn't
part of the branch.  However, for `if`, `let` and semicolon to behave *that* way would
require `let` to have a different behavior when it was placed inside an `if` expression.

## The solution

Misleading indentation can be avoided by using an in-editor code formatting tool
such as `ocp-indent`.  See [Editor Tools](https://ocamlverse.github.io/content/code_tools.html#editor-tools)
on the Code Tools page.

We can make the code after the semicolon execute *after* the `if` and `let` expressions
by explicitly delimiting the scope of the inner `let` using parentheses or `begin`/`end`:

```ocaml
let baz x =
  if x < 0
  then print_string "low\n"
  else (let message = "high\n" in
        print_string message);
  print_string "ok\n"
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
  print_string "ok\n"
```

These functions will behave identically to the original `foo` function above.
Another solution is to wrap the entire `if` expression in parentheses
or `begin`/`end`.

Note that you have to include a semicolon after the closing `)` or `end`.
Otherwise you will get a potentially confusing error message such as this one:

```
Error: This expression has type unit
       This is not a function; it cannot be applied.
```

## Summary

The general rule is that `let` will capture anything that's sequenced in whatever happens
to be the last `if` clause.  This is because the scope of `let` always extends
as far as it can into subsequent semicolon-delimited expressions.  You can prevent
this behavior by explicitly delimiting the `let` or the `if` using parentheses
or `begin`/`end`.
