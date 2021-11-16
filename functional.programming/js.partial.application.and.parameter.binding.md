# Partial Application
---

**Partial application** is an operation that **initializes** a subset of a nonvariadic function’s **parameters** to fixed values, creating a function of **smaller arity**.

In simpler terms, if you have a **function** with **five** parameters, and you supply three of the arguments, you end up with a **function** that **expects** the last **two**.

Difference between **currying** and **partial application**:

- **Currying** generates **nested unary functions** at each partial invocation. Internally, the final result is generated from the step-wise composition of these unary functions. Also, variations of curry allow you to partially evaluate a number of arguments; therefore, it gives you complete control over when and how evaluation takes place.

- **Partial application** binds (assigns) a function’s arguments to predefined values and generates a new function of fewer arguments. The resulting function contains the fixed parameters in its closure and is completely evaluated on the subsequent call.

