# Function currying
---

 In JavaScript, a **regular** or **non-curried** function call is permitted to execute with **missing** arguments. In other words, if you define a function `f(a,b,c)` and call it with just `a`, the evaluation proceeds, and the JavaScript runtime sets `b` and `c` to `undefined`.

On the other hand, a **curried function** is one where all **arguments** have been **explicitly defined** so that, when called with a subset of the arguments, it **returns** a new **function** that waits for the **rest of the parameters** to be supplied before running.

skematic for a function defined `f(a,b,c)` 
```
f(a)     ---> f(b,c)
f(a,b)   ---> f(c)
f(a,b,c) ---> Result
```

**Haskell** representation of a **curried** function:
`
curry(f) :: ((a,b,c) -> d) -> a -> b -> c -> d
`

**Currying** is a technique that converts a multivariable function into a stepwise sequence of unary functions by suspending or “procrastinating” its execution until all arguments have been provided, which could happen later.



example of a non-curried function:
```js
// fullname :: (String, String) -> String
const fullname = function (first, last) {
    ...
}
```
example of curried function:
```js
// fullname :: String -> String -> String
const fullname =
   function (first) {
       return function (last)  {
           ...
   }
}
```

### using Ramnda library for currying

```js
// checkType :: (Type, Object) -> Object
// currying ....
// checkType :: Type -> Object -> Object
const checkType = R.curry( (typeDef, obj) => {
    if (!R.is(typeDef, obj)) {
        let type = typeof obj;
        throw new TypeError(`Type mismatch. Expected [${typeDef}] but found [${type}]]`)
    }
    return obj
}
```