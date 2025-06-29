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
There will be arithmetic, comparison and equality, logical operators, and precedence and grouping (bedmas)

## Statements
Where an expression's main job is to produce a *value*, a statement's job is to produce an *effect*.  To be useful, they have to otherwise change the world in some way -- usually modifying some state, reading input, or producing output. 

For example print statements

## Variables
Variables will be declared with `var`. 

## Control Flow
There will be `if` statements, `while` and `for` loops. 

## Functions
Function call same as in C. We use the `fun` keyword for function definitions. 
- An **argument** is an actual value you pass to a function when you call it. So a function *call* has an *argument* list. 
- A **parameter** is a variable that holds the value of the argument inside the body of the function. Thus, a function *declaration* has a *parameter* list. 

### Closures
Functions are *first class* in Lox, meaning they are real values that you can get a reference to, store in variables, pass around, etc. For example:
```
fun addPair(a, b) {
    return a + b;
}

fun identity(a) {
    return a;
}

print identity(addpair)(1,2); // Prints "3"
```

## Classes
### Why might any langauge want to be object oriented?
For a dynamically typed language, objects are pretty handy. We need *some* way of defining compound data types to bundle blobs of stuff together. 

### Why is Lox object oriented?
Because it's cool.

### Classes or prototypes
When it comes to objects, there are actually two approaches to them, **classes** and **prototypes**. 

In class-based languages, there are 2 core concepts: instances and classes. Instances store the state for each object and have a reference to the instance's class. Classes contain the methods and inheritance chain. To call a method on an instance, there is always a level of indirection. 

![inheritance diagram](assets/class.jpg)

Prototype-based langauges merge these 2 concepts. There are only objects -- no classes -- and each individual object may contain state and methods. Objects can directly inherit from each other:

![objects diagram](assets/objects.jpg)

This means that in some ways prototypal languages are more fundamental than classes. They are really neat to implement because they're so simple. 

However, given this, almost all code written in prototypal languages just end up reinventing classes. Prototypes *are* simpler in the language, but they seem to accomplish that only by pushing the complexity onto the user. 

So, for Lox, we'll just use classes.

### Classes in Lox
We can declare a class and its methods and create instances.

### Instantiation and initialization
