# scheme-interpreter
scheme interpreter written in python 

> **Note:** This repository is a technical overview and documentation only. To comply with UC Berkeley academic policy, the source code is kept in a private repository.

A fully functional interpreter for a subset of the Scheme programming language, built using Python. This project covers lexical and dynamic scoping, and functional programming paradigms taught in cs61a at Berkeley.

## Features
- **Evaluator:** Implemented a recursive `scheme_eval` and `scheme_apply` loop.
- **Lexical Scoping:** Standard Scheme behavior, where environments are linked to where the procedure was defined.
- **Dynamic Scoping:** Implemented a custom `mu` special form where environments link to where the procedure is called instead of defined.
- **Special Forms:** Built-in support for `define`, `lambda`, `if`, `and`, `or`, and `cond`.
- **Logic Handling:** Supports short-circuiting logical operators and tail-call optimization.

## Challenge: The Eval-Apply Cycle
The most complex part of this project in my opinion was the mutual recursion between **Evaluation** and **Application**. 

- **Eval:** Processes expressions. If it encounters a call expression, it calls Apply.
- **Apply:** Takes a procedure and arguments. To execute the body of a user-defined procedure, it calls Eval again.

Breaking this cycle during debugging required me to understand how `Frame` instances (environments) track variable bindings and parent-child relationships.

## Implementation Details
- **Frame Management:** I implemented a `Frame` class to handle symbol lookup. The `lookup` method searches parent frames recursively, basically just like the scope chain.
- **Data Representation:** Used cs61a's `Link` class (linked lists) to represent Scheme expressions to convert them into Python-readable formats for built-in functions.

## Lessons That I Learned
This project helped strengthen my understanding of how high-level code is parsed and executed. It taught me the importance of environment management, and how misplaced parent pointers in a Frame can lead to "undefined variable" errors or wrong scope leaks.
