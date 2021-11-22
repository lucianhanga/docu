# Function Combinators
---

 **Imperative** code uses procedural control mechanisms like **if-else** and **for** to drive a program’s flow, but **functional programming** doesn’t. As we leave the imperative world behind, we need to find alternatives to fill in that gap; for this, we can use **function combinators**.

**Combinators** are **higher-order functions** that can combine primitive artifacts like other **functions** (or other **combinators**) and behave as **control logic**.

Combinators typically **don’t** declare any variables of their own or contain any business logic; they’re meant to **orchestrate** the flow of a functional program. In addition to `compose` and `pipe`, there’s an infinite number of combinators. The most important ones:

- identity
- tap
- alternation
- sequence
- fork (join)
  
### Identity ( I-Combinator )

The **identity combinator** is used to return the same value which was provided as argument.

```
identity :: (a) -> a
```

### Tap (K-Combinator)

the `tap` is usefull to bridge void functions such as logging functions or functions which write into an HTML object, ... . It manages this by passing itself into a function and returning itself.

```
tap :: (a -> *) -> a -> a
```

In fact, this combinator throws away the result of the function passed into it (if any). 


