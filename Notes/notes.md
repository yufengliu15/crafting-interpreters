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
