Suppose we have an `if` expression executed for the sake of
side effects.  With the `else` clause, this is a complete expression. 
A subsequent semicolon will sequence the next expression so that it
is always executed:
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
This behaves identically to the `foo` function defined above.

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
Now let's try it out in `utop`:
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

This problem also occurs with a single-branch `if`/`then` expression.
`let` will capture anything that's sequenced in whatever happens to be the last 
`if` clause.
