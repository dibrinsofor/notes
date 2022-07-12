# writing an INTERPRETER in go

> Interpreters vs Compilers: they are pretty much the same thing. They both take a bunch of seemingly useless characters (source code) and return something meaningful (that can be executed later on), but the Interpreter does this line by line while the Compiler does it all at once

> There are a plethora of Compiler/Interpreter architectural styles -- tiny ones that do not bother parsing the code (or offload it to some 3rd party) all the way to more elaborate ones with advanced parsing and evaluation techniques (Think just-in-time (JIT) interpreters). The implementation in this book strikes a solid balance between both extremes by parsing the source code, building an abstract syntax tree out of it and then evaluating the tree. This style is commonly called the tree-walking interpreter.

<details open>
<summary> Chapter 1: Lexing</summary>

Lexing or Lexical Analysis is the process of turning source code to Tokens using a Lexer/Tokenizer/Scanner.
> A token is source code broken into its lowest-level syntax. Consider this bit of code:
> `var jack = 10`. The tokens present in this tiny chunk could be represented as:
> - VAR -> keyword,
> - INDENTIFIER("jack"),
> - EQUAL_SIGN,
> - INTEGER(10)

When defining tokens, we also want to consider how and what special characters or delimiters (`[, {, ;, +, =, ( ...`) and keywords our compiler should understand.

The lexer’s job is not to tell us whether code makes sense, works or contains errors. That comes in a later stage. The lexer should only turn this input into tokens.

> Lmfao, so that's what REPL stands for? Read Eval Print Loop. it is just like the console/interactive mode then.

- [ ] Exercise 1: write support for unicode (and emojis) instead of just ascii.
- [ ] Exercise 2: include support for other special chars for func/var names (`_`).
- [ ] Exercise 3: abstract functionality for reading numbers and identifiers into one function in `lexer.go`.
- [ ] Exercise 4: consider support for not just integers but floats, hext notation, etc.
</details>