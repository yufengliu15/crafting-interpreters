# Crafting Interpreters
## Introduction
### A Map of the Territory
This book is about a language's *implementation*

You can visualize the network of paths an implementation may choose as climbing a mountain. The bottom represents raw source text. Each phase anaylzes the program and traforms it to some higher-level representation. 

Once we reach the peak, this means we can see what their code *means*. Then, we descent down the other side of the mountain, where we transform the higher-level representation down to a lower-level, getting closer to something the CPU may execute. 

![Mountain illustration for programming languages](assets/mountain_languages.jpg)

Let's do an example: `v` `a` `r` `a` `v` `e` `r` `a` `g` `e` `=` `(` `m` `i` `n` `+` `m` `a` `x` `)` `/` `2` `;`
#### Scanning
The first step is **scanning**, also known as **lexing** or **lexical analysis**. It makes sense of the linear stream of characters, and puts them together, called a **token**. Some tokens are `(`, `,`, `123`, `"hi!"` or `min`

Thus, our example after being scanned will look like: `var` `average` `=` `(` `min` `+` `max` `)` `/` `2` `;`

#### Parsing
This is where the syntax gets a **grammar**. Similar to diagramming sentences in English class.

The parser takes the flat sequence of tokens and builds a tree structure that mirrors the nested nature of the grammar. Can be called **parse tree** or **abstract syntax tree**, depending on how close to the  bare syntactic structure of the source language they are. 

![Parser Tree](assets/parser_tree.jpg)

Think of linguistics here. Also note that it is the **parser's job to report syntax errors**

#### Static Analysis
This is where the individual characteristics of each language occurs. 

For example, in an expression like `a + b`, we know that we are adding `a` and `b`, but we don't know what those variables refer to. Local? Global? Where are they defined?

The first bit of analysis that most languages do is called **binding** or **resolution**. For each **identifier**, we find out where that name is defined and wire the two together. This is where **scope** comes into play - the region of source code where a certain name can be used to refer to a certain declaration. 

If the language is statically typed, this is when we type check. 

We are now at the peak of the mountain. All this insight that is visible to us from analysis needs to be stored somwhere:
- Often, it gets stored right back as **attributes** on the syntax tree itself - extra fields in the nodes that aren't initialized during parsing but get filled in later
- Store in a lookup table off to the side, known as a **symbol table**. The key would be the variable and declaration. 
- The most powerful is to transform the tree into a different data structure that suits the semantics of the code. (Next section) 

Everything up to here is considered the **front end** of the implementation. 

Next sections will be the **middle end**.

#### Intermediate Representations
The compiler can be thought of as a pipeline, where each stage's job is to organize the data representing the user's code in a way that makes the next stage simpler to implement. The front end (of the pipeline) is specific to the source language the program is written in. The back end is concerned with the final architecture where the program will run. 

In the middle, the compiler may store the code in some intermediate representation (IR). This simply acts as the middleware between the front and end of the pipeline. 

This allows generability. For example, suppose we want to implement Pascal, C, and Fortran compliers, and we are targeting x86 and ARM. Normally, this would mean we would have to write 6 full compilers (every combination).

A shared intermediate representation reduces dramatcally. Now, we write one front end for each source language that produces the IR, and one back end for each target architecture.

This becomes $O(n*m)$ vs $O(n+m)$ where $n$ represents the number of langauges and $m$ represents the number of architectures.

#### Optimization
Once we understand what the user's program means, we can then further optimize it. 

A simple example is **constant folding**: if some expression always evalutes to the exact same value, we can do the evaluation at **compile time** and replace the code for the expression with its result. For example:
```ocaml
let expression = 3.14158 * (0.75 / 2) * (0.75 / 2);;
```

we could do all of that arithmetic in the compiler and change the code to:
```ocaml
let expression = 0.4417860938;;
```

This book will not cover optimization. Note that many successful languages have few compile-time optimizations. For example, Lua and CPython. 

#### Code generation
