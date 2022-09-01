# writing an INTERPRETER in go

> Interpreters vs Compilers: they are pretty much the same thing. They both take a bunch of seemingly useless characters (source code) and return something meaningful (that can be executed later on), but the Interpreter does this line by line while the Compiler does it all at once.

> There are a plethora of Compiler/Interpreter architectural styles -- tiny ones that do not bother parsing the code (or offload it to some 3rd party) all the way to more elaborate ones with advanced parsing and evaluation techniques (Think just-in-time (JIT) interpreters). The implementation in this book strikes a solid balance between both extremes by parsing the source code, building an abstract syntax tree out of it and then evaluating the tree. This style is commonly called the tree-walking interpreter.

#### the inspired compiler (with a few tweaks) lives here: [Monkey language go ooh ooh ah ah](https://github.com/dibrinsofor/interpreter)

<details>
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

<details open>
<summary> Chapter 2: Parsing</summary>

tl;dr - parsing is the process by which a compiler turns a sequence of tokens into a tree representation.

A parser collects a bunch of input (or tokens from our lexer) and builds a data structure with it giving a structural representation of the input, while ensuring that syntax is correct.
> it essentially uses this data structure (usually a syntax tree or abstract syntax tree) to internally represent source code.

How do syntax trees and abstract syntax trees differ? with abstract syntax trees, certain details, like newlines, semicolons, braces, etc., are omitted from the tree and are just used as a guide when the parser needs to construct the tree. **While implementations share similarities, there is no universal format for either tree structure.**

Say we have some input like this `"if (5 > 10) {return "magic number go brrr";} else {return "5 is a basic beach";}"`. After it goes through our lexer and into our parser, the generated abstract syntax tree should look something like this:
```
{
    type: "if-statement",
    condition: {
        type: "operator-expression",
        operator: ">",
        left: { type: "integral-literal", value: 5 },
        right: { type: "integer-literal", value: 10 }
        },
    consequence: {
        type: "return-statement",
        returnValue: { type: "string-literal", value: "magic number go brrr" }
        },
    alternative: {
        type: "return-statement",
        returnValue: { type: "string-literal", value: "5 is a basic beach" }
    }
}
```


> Would it still look like this if there were errors? 

> What is a parser generator? how does it all fit in? A parser generator creates a parser e be really a context thing. They provide a lot of functionality but can present drawbacks for certain use cases

> What is CFG? see [this](https://www.youtube.com/watch?v=o64uz2K2S4E) or [this](https://www.youtube.com/watch?v=bxpc9Pp5pZM&list=TLPQMTYwNzIwMjI3yyzpSGAMTw&index=2)

<!-- parser func - variable bindings,  . go interfaces - polymorphism-->

Expressions and Statements
> Debugging, debugging, debugging. Go is changing quickly, some of the things in this book just don't work.

> We're able to Parse Let and Return statements now. on to  expressions, next.

Parsing expressions is not as straight forward as parsing statements (where we just glance through each statement from left to right), we have to consider things like `Operator precedence` and the fact that expressions can appear in any order and as many times as they like.

> Operator precendence: we need to know what order to process operations in. that is, for an expression like `5 * 5 + 10` we would want to somehow represent it in our `AST` as `((5 * 5) + 10)`.

To accomplish this, we adopt Vaughan Pratt's [Top Down Operator Precedence](https://tdop.github.io/), a  BNF grammar alternative. It combines the best properties of [Recursive Descent]() and [Floyd's Operator Precedence]()

> We're able to parse Unary and Binary expressions now 

<!--write post about pratt parsing implementation, explain what it is, why it isnt has not overtaken BNF and it's relation to recursive descent-->

[crockford JS TDOP](http://crockford.com/javascript/tdop/tdop.html)
[crafting interpreters](https://craftinginterpreters.com/parsing-expressions.html)
[Bob Nystrom](https://journal.stuffwithstuff.com/2011/03/19/pratt-parsers-expression-parsing-made-easy/)
[Eli Bendersky's Pratt parser (talks about recursive descent)](https://eli.thegreenplace.net/2010/01/02/top-down-operator-precedence-parsing)
[Pratt Parser](https://abarker.github.io/typped/pratt_parsing_intro.html)
[matklad pp](https://matklad.github.io/2020/04/13/simple-but-powerful-pratt-parsing.html)

</details>

