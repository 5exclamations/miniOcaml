# MiniOCaml (lexer + parser + type checker + evaluator)

This project is a small “MiniOCaml”-style interpreter for a tiny functional language.

It includes:
- A **lexer** that converts an input string into tokens (keywords like `if/then/else`, `let/in/rec`, symbols like `+ - * <= ->`, parentheses, commas, etc.).
- A **parser** that builds an AST (expressions such as variables, integer/boolean constants, arithmetic/`<=`, function application, `if`, lambdas, `let`, `let rec`, and pairs).
- A **type checker** for a simple type system with:
  - `int`, `bool`
  - function types `t1 -> t2`
  - pair types `t1 * t2`
- An **evaluator** that evaluates expressions using an environment and supports closures (including recursive closures) and pairs.

The main “user-facing” entry points are:
- `checkStr : string -> ty` (type-check only)
- `evalStr : string -> value` (evaluate only)
- `interpretStr : string -> string` (type-check + evaluate, returns `"type : value"` as a string)

## Requirements
- OCaml installed (any recent version should work).

## How to run (REPL / easiest)
1. Start the OCaml toplevel:
   ```bash
   ocaml

    Load the file:

    ocaml
    #use "submission.ml";;

    Test with interpretStr:

    ocaml
    interpretStr "1 + 2";;
    interpretStr "if true then 1 else 2";;
    interpretStr "let x = 10 in x * 2";;
    interpretStr "((1, 2))";;              (* pair example *)

If you want to test pieces separately:
```
  ocaml
    checkStr "let x = 1 in x + 2";;
    evalStr  "let x = 1 in x + 2";;
```
How to run (script mode)

If your file contains only definitions, script mode won’t print anything by itself, but it’s still useful to confirm it loads without errors:
```bash
    ocaml submission.ml
```
How to compile (optional)

You can also compile it to check there are no syntax/type errors in the implementation:
```bash
      ocamlc -o miniocaml submission.ml
```
Running ./miniocaml will only do something if you add a main (printing / reading input), because the current code is primarily a library of functions.
Testing notes

    All tests are strings passed to interpretStr / evalStr / checkStr.

    If a test is invalid (lexing/parsing/type error), the code raises Failure with a message (e.g., missing parentheses, unexpected token, wrong types, etc.).

Suggested test cases

Try these to cover the features:
```
ocaml
  interpretStr "1 + 2 * 3";;
  interpretStr "1 <= 2";;
  interpretStr "if 1 <= 2 then 10 else 20";;
  interpretStr "let x = 5 in let y = 6 in x * y";;
  interpretStr "(1, 2)";;
  interpretStr "let (a, b) = (1, 2) in a + b";;
```
