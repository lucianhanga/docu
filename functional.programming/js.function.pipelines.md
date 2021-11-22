# Methos Chains vs. function pipelines
---

The **Haskell** function notation:
```
<function-name> :: <Inputs*> -> <Output>
```
e.g.
```js
// isEmpty :: String -> Boolean
const isEmpty = s => !s || !s.trim();
```

Viewing **functions as mappings of types** is necessary to understand how they can be **chained** and **pipelined**:

- **Chaining** methods together (tightly coupled, limited expressiveness)
- Arranging function **pipelines** (loosely coupled, flexible)


**Chaining** is clearly a syntactical improvement over imperative code and drastically improves its readability. Unfortunately, it’s contrived and tightly coupled to the owning object that confines the number of methods you can apply in the chain, which limits expressiveness of the code. In this case, you’re obliged to use only the set of operations provided by Lodash, and you wouldn’t be able to easily connect functions from different libraries (or your own) into one program.

Functional programming removes the limitations present in method chaining and provides the flexibility to combine any set of functions, no matter where they come from. A **pipeline** is a directional sequence of functions loosely arranged so that **the output of one is input into the next**.

schematic of pipelining (**pipes & filter design pattern**)
```
Input (Type A) --call--> f::A->B --pipe--> (Type B) --pipe--> g::B->C --pipe--> Output(Type C) 
```

#### requirements for compatible functions

Depending on the task at hand, there’s usually quite a gap between a problem definition and a proposed solution; therefore, computations must be carried out in well-defined stages. These stages are represented by functions that execute with the condition that their inputs and outputs be **compatible** in two ways:

- **Type** - The type returned by one function must match the argument type of a receiving function.
- **Arity** - A receiving function must declare at least one parameter in order to handle the value returned from a preceding function call.

Although this is extremely flexible, you often need to know what types of values a function is expecting; having this clearly defined (perhaps **documented** in code using the **Haskell notation**) makes your programs easier to understand.

e.g.
```js
// trim :: String -> String
const trim = str => str.replace(/^\s*|\s*$/g, '');

// normalize :: String -> String
const normalize = str => str.replace(/\-/g, '');

// eg.
// normalize(trim('444-44-4444')); // -> '444444444' 
```

**Arity** can be defined as the** number of arguments** a function accepts; it’s also referred to as the **function’s length**. In **FP**, as a corollary to referential transparency, the **number of arguments** a function declares is often directly **proportional** to its **complexity**.

**Pure functions** that expect a **single argument** are the simplest to use because the implication is that they serve a single purpose—a singular responsibility. The goal is to work with functions with as few arguments as possible, because they’re more flexible and versatile than those that depend on multiple arguments.

#### returning multiple values

take the following example
```js
// isValid :: String -> (Boolean, String)
isValid('444-444-4444'); // -> (false, 'Input is too long.')
```
Functional languages have support for a structure called a `tuple`. It’s a finite, ordered list of elements, usually grouping two or three values at a time, and written `(a, b, c)`. Based on this concept, you can use a `tuple` as a return value from `isValid` that groups a **status** with a possible **error message**, to be returned as a single entity and subsequently passed to another function if need be. `Tuples` are **immutable structures** that pack together items of different types so that they can be passed into other functions.

There are other ways of returning ad hoc data, such as **object literals** or **arrays**:
e.g.
```js
return {
    status: false,
    message: 'Input too long.'
}
```
