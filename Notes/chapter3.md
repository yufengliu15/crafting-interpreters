# The Lox Language
High level overview of the language we'll be building -- Lox.

## Hello, Lox
```
// Your first Lox program!
print "Hello, world!";
```

Lox's syntax is a member of the C family. 

## A High-Level Language
### Dynamic typing
Lox is dynamically typed. 

Static typing is a ton of work to learn and implement, so we defer our type checking to runtime. 

### Automatic memory management
There are 2 main techniques for managing memory:
1. Reference counting
2. Tracing garbage collection (also called garbage collection)

Ref counters are much simpler to implement, but over time, the limitations become too troublesome. All the languages that used ref counters eventually added a full tracing garbage collector. 

We will be implementing a garbage collector.

## Data Types
Some data types that will be in Lox:
- Booleans
- Numbers (only double-precision floating point)
- Strings
- Nil (Null. If we were doing a statically typed language, it would be worth avoiding this. However in a dynamically typed one, ignoring it is often more annoying than implementing)

## Expressions
