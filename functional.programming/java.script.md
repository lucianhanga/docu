#Functional programming is declarative
---

Functional Programming (**FP**) is a **declarative** programming. 

The **declarative** programming is a paradigm that expresses a set of operations without revealing how they are implemented or how the data flows through them. The more popular models used today are **imperative** or **procedural**. 

The **imperative** programming treats a computer programm as a sequence top-to-bottom statements that changes the state of the system to compute a result.

example of **imperative** program:

```js
let array = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
for(let i = 0; i < array.length; i++) {
   array[i] = Math.pow(array[i], 2);
}
array; //-> [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

The **imperative** programming tells in **great** detail **how** to perform certain tasks. It is the most common way of writing code.

The **declarative** programming separates the program description from evaluation. It focuses on the use of ***expreisons** to describe **what** the logic of the programm is wihtout necessarily specifying its control flow or state changes. The perfect example is the SQL statements, the SQL queries are composed of statements that describe **what** the outcome of the query should look like, abstracting the internal mechanism for the data retrieval. 

the example above rewriten shifting towards functional approach:

```js
[0,1,2,3,4,5,6,7,8].map (
    function (num) {
        return Math.pow(num, 2)
    }
)
```

The loop was **removed**. Since the loop artifacts are not abstract constructions by default they cannot be reused that easy. 

**Abstracting loops with functions** lets you take advantage of lambda expressions or arrow functions, introduced in ES6 JavaScript. Lambda expressions provide a succinct alternative to anonymous functions that can be passed in as a function argument:

same example written with **lambda**/**arrow** function: 
```jsx
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9].map(num => Math.pow(num, 2));
//-> [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

A loop is an **imperative** control structure that’s hard to reuse and difficult to plug in to other operations. In addition, it implies code that’s constantly changing or mutating in response to new iterations. Functional programs aim for **statelessness** and **immutability** as much as possible. Stateless code has zero chance of changing or breaking global state. To achieve this, functions that avoid side effects and changes of state should be used: **pure functions**.

### Pure functions

A **pure function** has the following **qualities**:

- It depends only on the **input** provided and **NOT** on any hidden or **external state** that may change during its evaluation or between calls.

- It **doesn’t** inflict changes beyond their scope, such as **modifying a global** object or a **parameter** passed by **reference**.

Side effects of a **pure** function:

- Changing a variable, property, or data structure globally
- Changing the original value of a function’s argument
- Processing user input
- Throwing an exception, unless it’s caught within the same function
- Printing to the screen or logging
- Querying the HTML documents, browser cookies, or databases

Practical functional programming **doesn’t** restrict **all** changes of state; it just provides a framework to help you manage and reduce them, while allowing you to **separate** the **pure** from the **impure**. Impure code produces externally visible side effects.

### OOP vs FP

	

|| Functional |  Object-oriented |
|------------|------------|------------------|
| **Unit of composition** | Functions | Objects (classes) |
| **Programming style** | Declarative | Imperative |
| **Data and behavior** | Loosely coupled into pure, standalone functions | Tightly coupled in classes with methods |
| **State management** | Treats objects as immutable values | Favors mutation of objects via instance methods |
| **Control flow**| Functions and recursion | Loops and conditionals |
| T**hread safety** | Enables concurrent programming | Difficult to achieve |
| **Encapsulation** | Not needed because everything is immutable | Needed to protect data integrity |

Functional solution for searching a list of objects:

```js
const selector = (country) => (person) => (country === person?.address?.country?);
const findPeopleBy = (ppl, selector) => ppl.filter(selector)
let usaPeople = findPeopleBy(people, selector("USA"));
console.log(JSON.stringify(usaPeople, null, 2));
```

### Managing the state of JS Objects

JavaScript objects are highly dynamic which means that is very bad to securing an object **state**.  The user can  modify, add, or delete its properties at any point in time.

An **immutable** object that contains immutable functionality can be considered **pure**. The same level of reasoning that applies to functions translates just as well to simple objects. There are some practices and patterns that can be used to manage **immutability**.

### Treating Objects as values

**Primitive types** are inherently **immutable**. In functional programming, these types are called **values**. 

Although JavaScript primitive types can’t be changed, the state of the variable that refers to a primitive type can. Therefore, you need to be able to provide, or at least emulate, immutable references to data so that your user-defined objects behave as if they were **immutable**.

**ES6** uses the `const` keyword to create **constant references**. Constants can’t be reassigned or re-declared.

JS will **NOT** allow something like this:
```js
    const gravity = 9.8;
    gravity = 10;
```
this will fix the reference of the object but does **NOT** solve the immutability of the object's internal state. The example above is legal:
```js
    const student = new Student("James", "Roman", "111-222-333", "Harvard");
    student.lastname = "Ramon";
```

For simple object structures, a good alternative is to adopt the **Value Object** pattern:

e.g.

```js
function zipCode(code, location) {
   let _code = code;
   let _location = location || '';

   return {
      code: function () {
         return _code;
      },
      location: function () {
         return _location;
      },
      fromString: function (str) {
         let parts = str.split('-');
         return zipCode(parts[0], parts[1]);
      },
      toString: function () {
         return _code + '-' + _location;
      }
   };
}

const princetonZip = zipCode('08544', '3345');
princetonZip.toString(); //-> '08544-3345'
```

In JavaScript, you can use functions and guard access to an object internal state by returning an **object literal interface** that exposes a small set of methods to the caller and treats _code and _location as **pseudo-private variables**. These variables are only accessible in the object literal via **closures**.

Using methods to **return new copies** is another way to implement **immutability**. 

**Value Object** is an **object-oriented design pattern** that was inspired by functional programming. This is another example of how the paradigms elegantly complement each other. This pattern is ideal, but it’s not enough for modeling entire real-world problem domains.

### Deep-freezing moving parts

JavaScript’s new class syntax doesn’t define keywords to mark fields as immutable, but it does support an internal mechanism for doing so by controlling some hidden object metaproperties like `writable`. By setting this property to false, JavaScript’s `Object.freeze()` function can prevent an object’s state from changing.

```js
    const student = Object.freeze(new Student("James", "Roman", "111-222-333", "Harvard"));
    student.lastname = "Ramon";
```
the `student.lastname = "Ramon"` is **not** allowed.

`Object.freeze()` can also immobilize **inherited** attributes. So freezing an instance of Student works exactly the same way and follows the object’s prototype chain protecting every inherited Person attribute. But it can’t be used to freeze nested object attributes.

`Object.freeze()` is a **shallow** operation. To get around this, you need to manually freeze an object’s nested structure, as shown in the following listing.

!!! - IMORTANT - example to be presented

### High-order functions

Because **functions** behave like regular **objects**, you can intuitively expect that they can be passed in as function **arguments** and **returned** from other functions. These are called **higher-order functions**.

JavaScript functions like `sort()` accept other functions as arguments and belong to a category called **higher-order functions**.

```js

function printPeople(people, selector, printer) {
    people.forEach(element => {
        if (selector(element)) 
            printer(element)
    });
}

const printer = person => console.log(JSON.stringify(person))
const selector = country => person => person?.address?.country === country
const selectorUSA = selector("USA")

printPeople(ppl, selector("USA"), printer);
printPeople(ppl, selector("USA"), console.log);
printPeople(ppl, selectorUSA, console.log);

```

A noticeable pattern that occurs in languages like JavaScript is that **function names** can be **passive nouns** like `multiplier`, `comparator`, and `action`. Because they’re first-class, functions can be assigned to variables and executed at a later time.

### Closure & Scopes

A **closure** is a data structure that binds a function to its environment at the moment it’s **declared**. It’s based on the textual location of the function declaration; therefore, a **closure** is also called a **static** or **lexical scope** surrounding the function definition. 

A **scope** groups a set of variable bindings and defines a section of code in which a variable is defined. 

```js
function makeAddFunction(amount) {
    function add (number) {
        return number + amount;
    }
    return add;
}

function makeAddFunctionES6(amount) { return (number) => number+amount; }

const makeAddFunctionES6V2 = amount => number => amount + number

const addTenTo = makeAddFunction(10);
console.log(addTenTo(20));

const addTenToEx = makeAddFunctionES6(10);
console.log(addTenToEx(20));

const addTenToExV2 = makeAddFunctionES6V2(10);
console.log(addTenToExV2(20));

console.log(makeAddFunctionES6V2(10)(20));

```

Name-Resolution in JS:

1.  It checks the variable’s function scope.
2.  If not in the local scope, it moves outward into the surrounding lexical scope, searching for the variable reference until it reaches the global scope.
3.  If the variable can’t be referenced, JavaScript returns undefined.

### Closures Usages

- Emulating private variables
- Making asynchronous server-side calls
- Creating artificial block-scoped variables

#### Emulating private variables

Using **closures**, it’s possible to emulate `private`/encapsulation behaviour also in JS ES6.






